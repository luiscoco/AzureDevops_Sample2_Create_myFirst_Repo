# Azure DevOps: How to create my first repo and run a pipeline (.NET 8 WebAPI)

## 1. How to create a new repo in my Azure DevOps project




## 2. How to create a .NET 8 WebAPI in VSCode and 


## 3. Initialize, add files, commit changes and push changet to the Azure DevOps repo


## 4. How to create Azure DevOps pipeline


## 5. 

We run Visual Studio 2022 and open the solution

We select the Git changes tab and click on Create Git repo button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/28f3900e-ee92-4a07-83eb-be2aa96fc128)

We select the organization, project and the repo name. We press on the Create and Send changes button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/3b50c285-f753-43c6-8cd6-a1e0b9b43775)

We verify in AzureDevOps the new repo

https://dev.azure.com/organizationName/projectName/_settings/repositories

https://dev.azure.com/luiscocoenriquez/myFirstProject/_settings/repositories

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/5b60218f-8921-4105-a37d-9c2444ae3d17)

## 6. How to create and run a Pipeline

We click on the Repo button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/21928828-ddad-462a-b50a-7d86ba481c48)

We click on the drop-down list and select MyWebApi repo

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/e4068998-80b0-4480-bc4f-79aa3b4000a4)

We click on the **Set up build** button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/9abbb4f8-9974-441d-8918-b7358a97b12c)

We click on the **Starter pipeline** option

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/26fff28d-f475-4c8f-952e-808049cff72f)

We copy the pipeline yaml file content 

```yaml
trigger:
- master

pool:
  vmImage: 'windows-latest'

steps:
- task: UseDotNet@2
  inputs:
    version: '8.x'
    includePreviewVersions: true # Set to true if .NET 8 is still in preview

- script: dotnet restore
  displayName: 'dotnet restore'

- script: dotnet build --configuration Release
  displayName: 'dotnet build'

- script: dotnet test --configuration Release --logger trx
  displayName: 'dotnet test'

- script: dotnet publish --configuration Release --output publishOutput
  displayName: 'dotnet publish'
```

We click on **Save and run** button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/2b885011-b552-427d-9968-7d13119dbd03)

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/3e0c0717-b227-4242-8f66-59dad7b97e2b)

We verify the job is running

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/669a3dbe-899e-4dcc-8a42-5b81f6f10b28)

We get this error message¨:

"##[error]No hosted parallelism has been purchased or granted. 

To request a free parallelism grant, please fill out the following form https://aka.ms/azpipelines-parallelism-request"

If we navigate to this URL: https://aka.ms/azpipelines-parallelism-request

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/46edcf6d-20a1-472b-8588-564d385746f2)

We have to fulfill a form to request Azure DevOps Parallelism Free

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/a5aae297-2bc2-402c-9564-c04feff17e80)


