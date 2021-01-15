## Exercise 2: Deploying to an Azure Web App for containers

In this exercise, we will setup a Release pipeline to deploy the web application to an Azure web app. First,let's create a Web App for Container with MYSQL.

1. Navigate back to your [Azure Portal](https://portal.azure.com).

1. In the Azure Portal, choose **+ Create a resource**, search for **Web App**, select and click *Create*.

1. Provide the following details and click **Next**- 

    * Enter a name for the new web app
    * Choose the Azure subscription 
    * Select existing or create new resource group for the web app. 
    * Leave the App Service plan/Location as it is.

      ![](images/azurewebappcreate1.png)

1. In the Docker tab, select **Azure   Container Registry** as Image source. Select the **Registry, Image and Tag** from the respective drop-downs and click **Review + create** and then **Create**.

    ![](images/azurewebappcreate2.png)

1. Once the provisioning is complete, go to the web app Overview page, and select the URL to browse the web app. You should see the default **Tomcat** page.

1. Append **/myshuttledev** to the web application context path in the URL to get to the MyShuttle login page. For example if your web app URL is `https://myshuttle-azure.azurewebsites.net/` , then your URL to the login page is `https://myshuttle-azure.azurewebsites.net/myshuttledev/`

    ![Login Page](images/loginpage.png)
 
    We could configure *Continuous Deployment* to deploy the web app when a new image is pushed to the registry, within the Azure portal itself. However, setting up an Azure Pipeline will provide more flexibility and additional controls (approvals, release gates, etc.) for application deployment.

1. We need to create Azure Database for MySQL as well. Choose **+ Create a resource**, search for **Azure Database for MySQL**, select and click *Create*. Provide all the required mandatory information and note down **Password** to a notepad. We will use it later in the Deployment pipeline. Click **Review + create** and then **Create**.

    ![Creating MYSQL Server](images/mysqldbcreate.png)

1. Navigate to the Azure Database for MySQL server provisioned.  Save the **Server name** and **Server admin login name** to a notepad.
    
     ![](images/azuredbmysql2.png)

1. Select Connection security. Enable **Allow access to Azure services** toggle and **Save** the changes. This provides access to Azure services for all the databases in your MySQL server.

   ![](images/accesstoazureservices.png)

1. Back in Azure DevOps account, select **Releases** from the **Pipelines** hub. Select the Release definition - **MyShuttleDockerRelease** and click **Edit**.

     ![editrelease](images/editrelease.png)

1. For enabling CD, click on the "lighting icon" and enable **Continuous deployment trigger".

    ![cd](images/cd.png)

1. Click on **MyShuttleDockerBuild** artifact and select **Latest** as Default version.

    ![cd](images/latest.png)

1. Hover the mouse on **Tasks** and select **Azure-Dev**. Configure the environment as below - 

    **Unlink all** and **Confirm**

    ![unlink](images/unlink.png)
1. Select Ubuntu-16.04 in Agent specification 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/dockerjava/images/agentselect.png )

1. Select the **Execute Azure MYSQL:SqlTaskFile** task, choose the Azure subscription, and provide the DB details which were noted down earlier during the creation of the database server. 

    * Link to your Azure Subscription.
    * Select the *Host Name* from the drop down. 
    * *Server Admin Login* - Go to **Variables** section and enter the value for the variable - *$(DBUSER)*. 
    * Enter the *Password*. This is the password provided during the creation of MYSQL database in Azure portal. Go to **Variables** section and enter the value for the variable - *$(DBPASSWORD)*. Click the **lock** icon to decrypt the dummy value and then, enter the password.

    ![Variables](images/variables.png)

    * A *MYSQL script* that is version controlled and provided here which creates the database, tables and populate records.

    ![MySQL DB](images/mysqlcreatetask.png)

1. Select the **Deploy Azure App Service** task and make sure that the following values are provided. Note that the task allows you to specify the Tag that you want to pull. This will allow you to achieve end-to-end traceability from code to deployment by using a build-specific tag for each deployment. For example, with the Docker build tasks you can tag your images with the Build.Number for each deployment.

    - Select your Azure Subscription and previously created App Service.
    - Registry or Namespace - Provide the value of Login server of the created Container Registry. You will find it in the Overview section.
    - Image - Provide the value as web. This is where the container image is stored after build.
    - Tag - Provide the value as $(Build.BuildNumber).

    ![Build Tags](images/vsts-buildtag.png)
 
1. Select **Save** and then click **Create Release**.

1. Check the artifact version you want to use and then select **Create**.

1. Wait for the release is complete and then navigate to the URL `http://{your web app name}.azurewebsites.net/myshuttledev`. You should be able to see the login page.

