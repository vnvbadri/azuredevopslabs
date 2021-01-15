## Exercise 3: Build your application using Azure CI Pipeline
  In this exercise, you will build your application and publish the required files to an artifact called drop.

  1. Navigate to **Pipelines --> Pipelines**. Select **Terraform-CI** and click **Edit**.

      ![](images/editbuild.png)

  1. Your build pipeline will look like as below. This CI pipeline has tasks to compile .Net Core project. The `dotnet` tasks in the pipeline will restore dependencies, build, test and publish the build output into a zip file (package)  which can be deployed to a web application.
    
      ![](images/ci-pipeline.png)

     For more guidance on how to build .Net Core projects with Azure Pipelines see [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/languages/dotnet-core?view=vsts&tabs=designer#build-your-project).

 1. In addition to the application build, we need to publish terraform files to build artifacts so that it will be available in CD pipeline. So we have added **Copy files** task to copy Terraform file to Artifacts directory.

     ![](images/copyfiles.png)

1. Now click **Queue** to trigger the build. Once the build succeeds, verify that the artifacts have **Terraform** folder and **PartsUnlimitedwebsite.zip** file in the drop.

      ![](images/queuebuild2.gif)

