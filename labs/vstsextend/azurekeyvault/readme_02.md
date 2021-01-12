### Task 1: Creating a key vault

Next, we will create a key vault in Azure. For this lab scenario, we have a node app that connects to a MySQL database where we will store the password for the MySQL database as a secret in the key vault.

1. If not already logged in, login to the [Azure Portal](https://portal.azure.com).

1. Enter "Key vault" in the search field and press enter. Select **Key Vaults** under services.

1. Select **Add** or the **Create key vault** button to create a new key vault.

    ![](images/addkeyvault.png)

1. Provide a name, subscription, resource group and location for the vault.

     ![](images/kv-create.png)

    Because data in Key Vaults are sensitive and business critical, you need to secure access to your key vaults by allowing only authorized applications and users. To access the data from the vault, you will need to provide read (Get) permissions to the service principal that you will be using for authentication in the pipeline. 

1. Select **Access policy** and then select **+ Add Access Policy** to setup a new policy.

     ![](images/kv_t2_s5.png)

1. You will need specify the permission that you intend to grant the application. This can be permissions to manage the keys and data(secrets). In any case, applications can access the key vault in two ways:

    * User + Application access: Access is granted to specific user who can then be allowed to use any application or can be restricted to use a specific application. 

    * Application-only access: Access is granted to the application which can be run as a daemon service or background job. 

1. Select the **Select principal**  and search for the security principal that you created earlier and select it. You can search by name or ID of the principal.

    ![](images/select-sp.png)

1. Next, we will select the permission to be granted. For now, we will provide **read-only** permissions (Get, List) to secrets only.

    ![](images/kv_t2_s8.png)

1.  Click **Review + create** to close the open blades and select **Create** to create the vault.

1. It should only take a couple of minutes for the service to be created. Once it is provisioned, select the key vault and add a new secret. Let's name it **sqldbpassword**. Provide any value that will be accepted as a password for a MySQL database.

    ![](images/createsecretnew.png)

### Task 3: Check the Azure Pipeline

Now, lets go to the Azure DevOps project that you provisioned using the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/?name=keyvault) and configure the Azure Pipelines to read the secret from the key vault.

1. Navigate to the Azure DevOps project.

    ![](images/project.png)

1. Select **Pipelines \| Pipelines** from the left navigation bar.

1. To trigger a build, choose the **SmartHotel-CouponManagement-CI** definition and then **Run Pipeline** to manually queue it.

    ![](images/kv_t3_s3.png)

1. Go to **Releases** under **Pipelines** and then select and **Edit** the **SmartHotel-CouponManagement-CD** definition.

1. Under **Tasks**, notice the release definition for **Dev** stage has a **Azure Key Vault** task. This task downloads *Secrets* from an Azure Key Vault. You will need to point to the subscription and the Azure Key Vault resource created earlier in the lab.

1. You need to authorize the pipeline to deploy to Azure. Azure pipelines can automatically create a service connection with a new service principal, but we want to use the one we created earlier. Click **Manage**, this will redirect to the Service connections page. 
    
    ![](images/clickmanage.png)

   Click on **New Service connection** -> **Azure Resource Manager** -> **Service Principal (manual)**.
   Fill the information from previously created service principal:

    -  Subscription Id and name: can be found in the keyvault resource overview page.
    -  Service Principal Id = AppId in the copied notes.
    -  Service Principal key = Password in the copied notes.
    -  TenantId , copy from the notes.

    Click on **Verify** to check it works, give the connection a name and click **Verify and Save**.

    ![](images/SC-create.png)
   
1. Select the Service connection you created in previous step for Azure subsciption in Azure Key Vault task.  

1. You can enter the name or select the key vault you created from the drop-down.

1. In the **Secrets filter** field, you can specify an *asterisk* (*) to read all secrets or if you want only specific ones, you can provide the names of the secrets as comma-separated values.

    ![](images/keyvaulttask.png)


    At runtime, Azure Pipelines will fetch the latest values of the secrets and set them as task variables which can be consumed in the following tasks which means the password we stored earlier can be read using **$(sqldbpassword)**.  

1. We pass this value in the next task, **Azure Deployment** where we deploy an ARM template.

    ![](images/armtemplatedeploytask.png)

   Notice the **Override template parameters** field has the database user name as a string but the password value is passed as a variable.

   `-webAppName $(webappName) -mySQLAdminLoginName "azureuser" -mySQLAdminLoginPassword $(sqldbpassword)`

   This will provision the MySQL database defined in the ARM template using the password that you have specified in the key vault. 

   You may want to complete the pipeline definition by specifying the subscription and location for the task. Repeat the same for the last task in the pipeline **Azure App Service Deploy**. Finally, save and create a new release to start the deployment.

{% include note.html content= "You may wonder that we could have passed the value as a secret task variable itself within Azure Pipelines. While that is possible, task variables are specific to a pipeline and can't be used outside the definition it is created. Also, in most cases, secrets such as these are defined by Ops who may not want to set this for every pipeline." %}

### Exercise Challenge

Try creating a new secret to store the user name for the MySQL Database and change the pipeline to fetch and use the secret


### Related Labs
* [Embracing Continuous Delivery with Azure Pipelines](https://azuredevopslabs.com/labs/azuredevops/continuousdeployment/)

* [GitHub integration with Azure Pipelines](https://azuredevopslabs.com/labs/vstsextend/github-azurepipelines/)
