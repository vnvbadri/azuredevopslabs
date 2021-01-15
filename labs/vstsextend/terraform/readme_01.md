## Overview

[Terraform](https://www.terraform.io/intro/index.html) is a tool for building, changing and versioning infrastructure safely and efficiently. Terraform can manage existing and popular cloud service providers as well as custom in-house solutions.

Configuration files describe to **Terraform** the components needed to run a single application or your entire datacenter. Terraform generates an execution plan describing what it will do to reach the desired state, and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans which can be applied. 

<div class="bg-slap"><img src="./images/mslearn.png" class="img-icon-cloud" alt="MS teams" style="width: 48px; height: 48px;">Want additional learning? Check out the <a href="https://docs.microsoft.com/en-us/learn/modules/provision-infrastructure-azure-pipelines/" target="_blank"><b><u> Provision infrastructure
in Azure Pipelines</u></b></a> module on Microsoft Learn.</div>

### What’s covered in this lab

In this lab, you will see

1. How open source tools, such as Terraform can be leveraged to implement Infrastructure as Code (**IaC**)
1. How to automate your infrastructure deployments in the Cloud with Terraform and Azure Pipelines

The following image will walk you through all the steps explained in this lab

 ![](images/Terraform-workflow.gif)
## Exercise 1: Adding the Service Principal to the Azure DevOps  

1. Copy the DevOps link from the Lab Environment output page to Navigate to your Parts Unlimited project on Azure DevOps. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/azure-dev-link.png)  

1. After logging into Azure DevOps, click on the Project provided. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-1.png)  

1. Click on Project Settings at the bottom of the page. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-2.png)  

1. In Project setting select Service Connections. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-3.png) 

1. Select New Service Connection. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-4.png)  

1. Now select Azure Resource Manager, Click on Next. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-5.png)  

1. Now select Service Principal (manual) and click on Next. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-6.png) 

1. Fill all the required details which are given in CloudLabs portal and click on Verify and save. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/terraform/images/serv-principal-7.png)

