# Azure DevOps: How to create my first repo and run a pipeline (.NET 8 WebAPI in VSCode and Visual Studio 2022)

## 1. How to create a new repo in my Azure DevOps project

By default when we create a new Project inside one Organization in Azure DevOps a new repo is automatically created.

If we need to create a new repo inside an existing Project we can navigate to **Project->Settings->Repositories** and press on the Create button

**https://dev.azure.com/organizationName/projectName/_settings/repositories**

https://dev.azure.com/luiscocoenriquez/myFirstProject/_settings/repositories

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/66f3b69f-e6ac-4d55-9e12-153d4ddf90de)

We input the repository type, repo name and gitignore file, then we press the create button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/14d6f476-a0d3-4f01-9d61-f02aad3fa9f5)

Pay attention the new repo will be initialized with a **main** branch

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/3b635d55-3706-4ca8-aec9-61da95fc4a70)

## 2. How to create a .NET 8 WebAPI in VSCode and 

Open VSCode and then open a terminal in VSCode.

**Create a new folder for your project and navigate into it**:

```
mkdir MyWebApi
cd MyWebApi
```

**Create a new .NET 8 WebAPI project**:

```
dotnet new webapi -n MyWebApi
```

This command creates a new directory named MyWebApi inside your current folder, and then it generates a basic WebAPI project inside this new directory.

**Open your project in VSCode**:

```
code . -r
```

The **-r** flag tells VSCode to reload the current window with the contents of the current directory.

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/2256bfba-04b9-4cbb-95f1-a8d0ace109a9)

**Test your application (optional)**:

Run your application to ensure everything is working correctly.

```
dotnet run
```

By default, your WebAPI will be accessible at

**https://localhost:5001/swagger/index.html**

or 

**http://localhost:5000/swagger/index.html**

## 3. Initialize a local git repo, add files, commit changes and push changes to the Azure DevOps repo

**Initialize a Git repository**:

```
git init
```

**Add your project files to the repository**:

```
git add .
```

**Commit your changes**:

```
git commit -m "Initial commit"
```

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/28bfff00-9903-4754-9690-4f7781446c83)

**Go to your Azure DevOps project**:

Navigate to your **Azure DevOps portal**. Go to the **Repos** section of your project.

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/fb5ca000-d608-40be-b1d5-36f2a6e96dd4)

Create a **new repository** (if you haven't already)

We navigate to the repo files and we click on the **Clone** button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/bc7305bb-1970-4e32-a69f-652981b963ea)

We copy the **repo URL**:

**https://luiscocoenriquez@dev.azure.com/organizationName/projectName/_git/repoName**

https://luiscocoenriquez@dev.azure.com/luiscocoenriquez/myFirstProject/_git/myfirstrepo

**Git command to push** an existing repository from the command line: 

```
git remote add origin https://luiscocoenriquez@dev.azure.com/luiscocoenriquez/myFirstProject/_git/myfirstrepo
git branch -M main
git push -u origin main
```

**IMPORTANT NOTE**: 

if you've initialized your Azure DevOps repository with some files (like a **README.md** or any other file) that your local repository doesn't have,

you need to first pull the changes from the remote repository, resolve any conflicts if they exist, and then push your changes again.

We pull the changes from the repo in Azure DevOps

```
git pull origin main --allow-unrelated-histories
```

We add the files and commit them

```
git add .
git commit -m "Resolved conflicts between local and remote repositories"
```

Once the conflicts are resolved and the changes from the remote repository are successfully merged into your local repository, we can push your changes:

```
git push -u origin main
```

We verify the new Azure repo with all the pushed changes

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/e5ac0c05-a382-4353-a7e9-1e7cb3b82283)

## 4. How to create a new repo in Visual Studio 2022 Community Edition and push the code to Azure DevOps repo

We run Visual Studio 2022 and open the solution

We select the Git changes tab and click on Create Git repo button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/28f3900e-ee92-4a07-83eb-be2aa96fc128)

We select the organization, project and the repo name. We press on the Create and Send changes button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/3b50c285-f753-43c6-8cd6-a1e0b9b43775)

We verify in AzureDevOps the new repo

https://dev.azure.com/organizationName/projectName/_settings/repositories

https://dev.azure.com/luiscocoenriquez/myFirstProject/_settings/repositories

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/5b60218f-8921-4105-a37d-9c2444ae3d17)

## 5. How to create and run a Pipeline

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

We have to fulfill a form to request **Azure DevOps Parallelism Free**

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/a5aae297-2bc2-402c-9564-c04feff17e80)

See also the information in this URL regarding **Configure and pay for parallel jobs**:

https://learn.microsoft.com/en-us/azure/devops/pipelines/licensing/concurrent-jobs?view=azure-devops&tabs=ms-hosted

Also we can see the **Pricing for Azure DevOps** in the following URL

https://azure.microsoft.com/en-us/pricing/details/devops/azure-devops-services/

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/ca39d007-3524-4946-af12-27bb22ef9b38)

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/38223144-1c9e-4cb2-8efe-166bab08f263)

Another option is navigate to **Organization Settings** and press on the **Set up billing**

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/a5239bff-401b-43bc-b510-5494f3646e7c)

We link Azure DevOps billing to our **Azure Subscription**

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/1b3755f4-f8d4-41a0-9529-dedec8dec239)

After linking our Azure Subscription to Azure DevOps we can set the **MS Host Parallel job** to **1** and press the **Save** button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/5d6c3e3d-d408-42d9-b853-7b013587f7af)

We can verify the MS Host Parallel jobs we updated to 1

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/f5df0884-856e-4c6f-9a45-f3768f4a2ce6)

Now we can navigate to the pipeline and press the **Run pipeline** button

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/a7e144d5-3e29-4a3b-b0fb-208eb14f1ce1)

![image](https://github.com/luiscoco/AzureDevops_Sample2_Create_myFirst_Repo/assets/32194879/57e30578-aaa9-4e39-b525-043242e40c10)





