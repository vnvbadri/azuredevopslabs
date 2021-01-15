## Exercise 1: Configure Build and Release pipeline

Make sure that you have created the AKS project in your Azure DevOps organization through [Azure DevOps Demo Generator](http://azuredevopsdemogenerator.azurewebsites.net/?TemplateId=77372&Name=AKS) (as mentioned in pre-requisites). We will manually map Azure resources such as AKS and Azure Container Registry to the build and release definitions.

1. Navigate to **Pipelines --> Pipelines**. 
   
      ![build](images/pipelines.png)

1. Select **MyHealth.AKS.Build** pipeline and click **Edit**.
   
   ![build](images/editbuild.png)

1. In **Run services** task, select your Azure subscription from **Azure subscription** dropdown. Click **Authorize**.

    ![azureendpoint](images/endpoint.png)

    You will be prompted to authorize this connection with Azure credentials. Disable pop-up blocker in your browser if you see a blank screen after clicking the OK button, and please retry the step.

     This creates an **Azure Resource Manager Service Endpoint**, which defines and secures a connection to a Microsoft Azure subscription, using Service Principal Authentication (SPA). This endpoint will be used to connect **Azure DevOps** and **Azure**.

- Note: If your subscription is not listed or to specify an existing service principal, follow the [Service Principal creation](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/connect-to-azure?view=vsts) instructions.

1. Following the successful authentication, select appropriate values from the dropdown - **Azure subscription** and **Azure Container Registry** as shown. 

   Repeat this for the **Build services, Push services** and **Lock services** tasks in the pipeline. 

    ![updateprocessbd](images/acr.png)

    |Tasks|Usage|
    |-----|-----|
    |**Replace tokens**| replace ACR in **mhc-aks.yaml** and database connection string in **appsettings.json**|
    |![icon](images/icon.png) **Run services**| prepares suitable environment by pulling required image such as aspnetcore-build:1.0-2.0 and restoring packages mentioned in **.csproj**|
    |![icon](images/icon.png) **Build services**| builds the docker images specified in a **docker-compose.yml** file and tags images with **$(Build.BuildId)** and **latest**|
    |![icon](images/icon.png) **Push services**| pushes the docker image **myhealth.web** to Azure Container Registry|
    |![publish-build-artifacts](images/publish-build-artifacts.png) **Publish Build Artifacts**| publishes **mhc-aks.yaml** & **myhealth.dacpac** files to artifact drop location in Azure DevOps so that they can be utilized in Release Definition|

   **applicationsettings.json** file contains details of the database connection string used to connect to Azure database which was created in the beginning of this lab.
    
   **mhc-aks.yaml** manifest file contains configuration details of **deployments**, **services** and **pods** which will be deployed in Azure Kubernetes Service. The manifest file will look like as below

    ![](images/aksmanifest.png)

   For more information on the deployment manifest, see [AKS Deployments and YAML manifests](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#deployments-and-yaml-manifests)

1. Click on the **Variables** tab.
      
    ![](images/variables.png)

     Update **ACR** and **SQLserver** values for **Pipeline Variables** with the details noted earlier while configuring the environment. 
    ![updateprocessbd](images/updatevariablesbd.png)

1. **Save** the changes.

    ![updateprocessbd](images/savebuild.png)

1. Navigate to **Pipelines \| Releases**. Select **MyHealth.AKS.Release** pipeline and click **Edit**.

   ![release](images/release.png)

1. Select Dev stage and click **View stage tasks** to view the pipeline tasks.

   ![releasetasks](images/viewstagetasks.png)

1. In the **Dev** environment, under the **DB deployment** phase, select **Azure Resource Manager** from the drop down for **Azure Service Connection Type**,  update the **Azure Subscription** value from the dropdown for **Execute Azure SQL: DacpacTask** task.

    ![update_CD3](images/dbdeploytask.png)

1. In the **AKS deployment** phase, select **Create Deployments & Services in AKS** task. 
      
    ![](images/aksdeploytask.png)

    Update the **Azure Subscription**, **Resource Group** and **Kubernetes cluster** from the dropdown. Expand the **Secrets** section and update the parameters for **Azure subscription** and **Azure container registry** from the dropdown. 
    
    Repeat similar steps for **Update image in AKS** task.
     
     ![](images/aksdeploytask2.png)

    * **Create Deployments & Services in AKS** will create the deployments and services in AKS as per the configuration specified in **mhc-aks.yaml** file. The Pod, for the first time will pull up the latest docker image.

    * **Update image in AKS** will pull up the appropriate image corresponding to the BuildID from the repository specified, and deploys the docker image to the **mhc-front pod** running in AKS.

    * A secret called **mysecretkey** is created in AKS cluster through Azure DevOps by using command `kubectl create secret` in the background. This secret will be used for authorization while pulling myhealth.web image from the Azure Container Registry.

1. Select the **Variables** section under the release definition, update **ACR** and **SQLserver** values for **Pipeline Variables** with the details noted earlier while configuring the environment. Select the **Save** button.

- Note: The **Database Name** is set to **mhcdb** and the **Server Admin Login** is **sqladmin** and **Password** is **P2ssw0rd1234**. If you have entered different details while creating Azure SQL server, update the values accordingly

   ![releasevariables](images/releasevariables.png)

