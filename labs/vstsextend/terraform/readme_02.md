## Exercise 2: Examine the Terraform file (IaC) in your Source code
In this lab, you will use PartsUnlimited which is an example eCommerce website developed using .Net Core. You will examine the terraform file which helps you to provision the Azure Resources required to deploy PartsUnlimited website.

1. Navigate to the project in your Azure DevOps account.

1. Select **Repos**. Switch to **terraform** branch.

    ![](images/select-terraform-branch.png)

    Make sure that you are now on the **terraform** branch and **Terraform** folder is there in the repo.

    ![](images/terraformrepo.png)

1. Select the **webapp.tf** file under the Terraform folder. Go through the code.
     
      ![](images/terraformfile.png)

    **webapp.tf** is a terraform configuration file. Terraform uses its own file format, called HCL (Hashicorp Configuration Language). This is very similar to YAML.

    In this example, we want to deploy an Azure Resource group, App service plan and App service required to deploy the website. And we have added Terraform file (Infrastructure as Code) to source control repository in your Azure DevOps project which can deploy the required Azure resources. 
    
    If you would like to learn more about the terraform basics click [here](https://azurecitadel.com/automation/terraform/lab1/)
  
