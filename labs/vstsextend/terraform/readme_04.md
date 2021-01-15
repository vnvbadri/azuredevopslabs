## Exercise 4: Deploy resources using Terraform (IaC) in Azure CD pipeline

In this exercise, you will create azure resources using Terraform as part of your deployment(CD) pipeline and deploy the PartsUnlimited application to the App service provisioned by Terraform.

1. Navigate to **Pipelines --> Releases**. Select **Terraform-CD** and click **Edit**.
   
    ![](images/editrelease.png)

1. Select **Dev** stage and click **View stage tasks** to view the pipeline tasks.

      ![](images/viewstagetasks.png)

1. You will see the tasks as below.

      ![](images/releasetasks.png)

1. Select the **Azure CLI** task. Select the Azure subscription from the drop-down list and click **Authorize** to configure Azure service connection.
      
    ![](images/azureclitask.png)

   > By default, Terraform stores state locally in a file named terraform.tfstate. When working with Terraform in a team, use of a local file makes Terraform usage complicated. With remote state, Terraform writes the state data to a remote data store. Here we are using Azure CLI task to create **Azure storage account** and **storage container** to store Terraform state. For more information on Terraform remote state click [here](https://www.terraform.io/docs/state/remote.html)

1. Select the **Azure PowerShell** task. Select Azure service connection from the drop-down.
     
     ![](images/azurepowershelltask.png)

   > To configure the Terraform [backend](https://www.terraform.io/docs/backends/) we need Storage account access key. Here we are using Azure PowerShell task to get the Access key of the storage account provisioned in the previous step.

1. Select the **Replace tokens** task.
    
     ![](images/replacetokens.png)

    If you observe the **webapp.tf** file in **Exercise 1, Step 3** you will see there are few values are suffixed and prefixed with **__**. For example **__terraformstorageaccount__**. Using **Replace tokens** task we will replace those values with the variable values defined in the release pipeline.
     
      ![](images/variables.png)

1. Terraform tool installer task is used to install  a specified version of Terraform from the Internet or the tools cache and prepends it to the PATH of the Azure Pipelines Agent (hosted or private).
      
    ![](images/installterraform.png)
1. When running Terraform in automation, the focus is usually on the core plan/apply cycle.

   The main Terraform workflow is shown below:

      ![](images/terraformworkflow.png)

      
    i. Initialize the Terraform working directory.

   ii. Produce a plan for changing resources to match the current configuration.
   
   iii. Apply the changes described by the plan.
    
    The next Terraform tasks in your release pipeline help you to implement this workflow.
1. Select the **Terraform init** task. Select Azure service connection from the drop-down. And make sure to enter the container name  as **terraform**. For the other task parameters information see [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/Extensions/Terraform/Src/Tasks/TerraformTaskV1/README.md)
       
      ![](images/terraform-init2.png)

      ![](images/terraform-init3.png)

    > This task runs `terraform init` command. The `terraform init` command looks through all of the *.tf files in the current working directory and automatically downloads any of the providers required for them. In this example, it will download [Azure provider](https://www.terraform.io/docs/providers/azurerm/) as we are going to deploy Azure resources. For more information about `terraform init` command click [here](https://www.terraform.io/docs/commands/init.html)

1. Select the **Terraform plan** task. Select Azure service connection from the drop-down.
       
      ![](images/terraform-plan.png)
 
    > The `terraform plan` command is used to create an execution plan. Terraform determines what actions are necessary to achieve the desired state specified in the configuration files. This is a dry run and shows which actions will be made.  For more information about `terraform plan` command click [here](https://www.terraform.io/docs/commands/plan.html)

1. Select the **Terraform Apply** task. Select Azure service connection from the drop-down.
  
    ![](images/terraform-approve.png)

    > This task will run the `terraform apply` command to deploy the resources. By default, it will also prompt for confirmation that you want to apply those changes. Since we are automating the deployment we are adding `auto-approve` argument to not prompt for confirmation.

1. Select **Azure App Service Deploy** task. Select Azure service connection from the drop-down.

   ![](images/appservicetask.png)

   > This task will deploy the PartsUnlimited package to Azure app service which is provisioned by Terraform tasks in previous steps.

1. Once you are done **Save** the changes and **Create a release**.
   
   ![](images/releasetrigger.gif)

1. Once the release is success navigate to your Azure portal. Search for **pulterraformweb** in App services. Select **pulterraformweb-xxxx** and browse to view the application deployed.

   ![](images/browseappinportal.png)

   ![](images/webapp.png)

   Do you want to learn more about Terraform? If yes click [here](https://www.terraform.io/) for Terraform documentation.


