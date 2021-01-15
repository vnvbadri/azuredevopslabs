## Exercise 1:  Configuring a CI pipeline to build and publish Docker image

In this task, you will configure a CI pipeline that will build and push the image to Azure Container Registry.

1. Open the <a href="https://portal.azure.com" target="_blank">Azure Portal</a>.

1. Select **+ Create a resource** and search for **Container Registry**. Select **Create**. In the *Create Container Registry* dialog, enter a name for the service, select the resource group, location and click **Review + Create**. Once the validation is success click **Create**.

    ![Create Azure Container Registry](images/createacr2.png)

1. Once the resource is provisioned navigate to the resource and Enable Admin user for Container Registry.

    ![Enable Admin User](images/acrenableadminuser.png)

1. Navigate to your Azure DevOps project, select **Pipelines** from **Pipelines**. Select **MyShuttleDockerBuild** and click **Edit**. 

1. Lets look at the tasks used in the build definition.

1. Select the **Maven** task. This task is used to build the pom.xml file. The maven task is updated with the following additional settings

    | Parameter | Value | Notes |
    | --------------- | ---------------------------- | ----------------------------------------------------------- |
    | Options | `-DskipITs --settings ./maven/settings.xml` | Skips integration tests during the build |
    |Code Coverage Tool | JaCoCo | Selects JaCoCo as the coverage tool |
    | Source Files Directory | `src/main` | Sets the source files directory for JaCoCo |

      ![Maven task settings](images/vsts-mavensettings.png)

1. Then there is **Copy** task. We will copy the WAR file from the sources directory to the staging folder.

    | Parameter | Value | Notes |
    | --------------- | ---------------------------- | ----------------------------------------------------------- |
    |Source Folder| $(build.sourcesdirectory)| Copy from the source folder|
    |Contents|target/myshuttledev*.war, *.sql| Copy the MyShuttle WAR file
    |Target Folder|$(build.artifactstagingdirectory)|Copy it to the default staging folder|

1. Next, we have a **Publish** task to publish the build artifacts to Azure Pipelines.

    | Parameter | Value | Notes |
    | --------------- | ---------------------------- | ----------------------------------------------------------- |
    |Path to publish| $(build.artifactstagingdirectory)| Copy contents from the staging folder|
    |Artifact name|drop|Provide a name for the artifact folder.  |
    |Artifact publish location |Azure Pipelines|we will publish it to Azure pipelines|

1. Next, there are two **Docker** tasks to build and publish the images. Select the first **Docker** task and notice that the **Command** is set to **Build**. The other settings of the Docker compose tasks are as follows:

    | Parameter | Value | Notes |
    | --------------- | ---------------------------- | ------------------------------------------- |
    | Azure Subscription | Authorize your Azure subscription | The subscription that contains your registry |
    | Container Registry Type | Azure Container Registry | This is to connect to the Azure Container Registry you created earlier |
    | Azure Container Registry | Your registry | Select the Azure Container registry you created earlier |
    |Command|build|Docker command|
    |Dockerfile|src/Dockerfile|Point to the src folder for the docker file|
    |Use default build context|Uncheck this option|
    |Build context|. (dot representing the root folder)| The build context should be the root folder|
    |Image name| `Web:$(Build.BuildNumber)` | Sets a unique name for each instance of the build |
    |Qualify image name| Check (set to true)|   
    | Include Latest Tag | Check (set to true) | Adds the `latest` tag to the images produced by this build |
   
   While authorizing subscription go to Advanced options and in the pop-up window manually select resource group from drop down 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/dockerjava/images/authorize1.png)

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/dockerjava/images/authorize2.png)

    ![Docker build task](images/dockerbuildtask.png)

1. There is a second **Docker** task with almost the same settings. The only change is the **Command** is set to **Push** and the **Image name** is set to  `Web:$(Build.BuildNumber)`. This action will instruct the task to push the Web image to the container registry.

      ![Maven task settings](images/dockerpublishtask.png)

1. Click the **Save and Queue** button to save and queue this build. Make sure you are using the **Hosted Ubuntu 1604** build agent.

1. Wait for the build to complete. When it is successful, you can go to your Azure portal and verify if the images were pushed successfully. 
    ![images/Azure Container Registry Images](images/portal-acrrepo2.png)

1. If you are following this from the Eclipse lab, you can also verify if the images were pushed correctly from the **Azure Explorer** view. *Sign in* to Azure, refresh Azure Container Registry. Right click and select **Explore Container Registry**. You should see the image - tagged with the build number.

    ![Explore Container Registry](images/exploreacr.png)

