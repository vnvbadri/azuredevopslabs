## Setting up the environment

The following azure resources need to be configured for this lab:

|Azure resources                      | Description|
|-------------------------------------|------------|
|![Azure Container Registry](images/container_registry.png) Azure Container Registry | Used to store the Docker images privately|
|![AKS](images/aks.png) AKS | Docker images are deployed to Pods running inside AKS|
|![Azure SQL Server](images/sqlserver.png) Azure SQL Server | SQL Server on Azure to host database|

1. Launch the [Azure Cloud Shell](https://docs.microsoft.com/en-in/azure/cloud-shell/overview) from the Azure portal and choose **Bash**. Click on Show advanced settings enter unique name for Storage account and File share then Create storage. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/kubernetes/images/bash1.png) 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/kubernetes/images/bash2.png)

1. **Deploy Kubernetes to Azure, using CLI**:

   i. Get the latest available Kubernetes version in your preferred region into a bash variable. Replace `<region>` with the region of your choosing, for example eastus.

      ```bash
     version=$(az aks get-versions -l <region> --query 'orchestrators[-1].orchestratorVersion' -o tsv)
      ```
   
   ii. Create AKS using the latest version available
    
    ```bash
    az aks create --resource-group akshandsonlab --name <unique-aks-cluster-name> --kubernetes-version $version --generate-ssh-keys --location <region>
    ```
    
- Note: Enter a unique AKS cluster name. AKS name must contain between 3 and 31 characters inclusive. The name can contain only letters, numbers, and hyphens. The name must start with a letter and must end with a letter or a number. The AKS deployment may take 10-15 minutes

1. **Deploy Azure Container Registry(ACR)**: Run the below command to create your own private container registry using Azure Container Registry (ACR).

    ```bash
    az acr create --resource-group akshandsonlab --name <unique-acr-name> --sku Standard --location <region>
    ```
    
- Note: Enter a unique ACR name. ACR name may contain alpha numeric characters only and must be between 5 and 50 characters"
    
1. **Grant ACR access to AKS** : Authorize the AKS cluster to connect to the Azure Container Registry using below command 

    ```bash 

    az aks update -n yourAKSname -g yourResourceGroup --attach-acr yourACRname 

    ```
1. **Create Azure SQL server and Database**: 
    Create an Azure SQL server.
    
    ```bash
    az sql server create -l <region> -g akshandsonlab -n <unique-sqlserver-name> -u sqladmin -p P2ssw0rd1234
    ```

    Create a database

    ```bash
    az sql db create -g akshandsonlab -s <unique-sqlserver-name> -n mhcdb --service-objective S0
    ```
    
- Note: Enter a unique SQL server name. Since the Azure SQL Server name does not support **UPPER** / **Camel** casing naming conventions, use lowercase for the ***SQL Server Name*** field value.
    
1. The following components - **Container Registry**, **Kubernetes Service**, **SQL Server** along with **SQL Database** are deployed. Access each of these components individually and make a note of the details which will be used in Exercise 1.
   
   ![Deploy to Azure](images/azurecomponents.png)
1. Select the **mhcdb** SQL database and make a note of the **Server name**.

   ![Deploy to Azure](images/getdbserverurl.png)

1. Click on "Set server Firewall" and enable "Allow Azure services ..." option.

    ![Allow Services ](images/allow.png)

1. Navigate to the resource group, select the created container registry and make a note of the **Login server** name.

    ![Deploy to Azure](images/getacrserver.png)

Now you have all the required azure components to follow this lab.


