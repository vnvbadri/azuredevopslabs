## Overview

[**Azure Kubernetes Service (AKS)**](https://azure.microsoft.com/en-us/services/kubernetes-service/){:target="_blank"} is the quickest way to use Kubernetes on Azure. **Azure Kubernetes Service (AKS)** manages your hosted Kubernetes environment, making it quick and easy to deploy and manage containerized applications without container orchestration expertise. It also eliminates the burden of ongoing operations and maintenance by provisioning, upgrading, and scaling resources on demand, without taking your applications offline. Azure DevOps helps in creating Docker images for faster deployments and reliability using the continuous build option.

One of the biggest advantage to use AKS is that instead of creating resources in cloud you can create resources and infrastructure inside Azure Kubernetes Cluster through Deployments and Services manifest files.

### Lab Scenario

This lab uses a Dockerized ASP.NET Core web application - **MyHealthClinic** (MHC) and is deployed to a **Kubernetes** cluster running on **Azure Kubernetes Service (AKS)** using **Azure DevOps**.
> There is a  **mhc-aks.yaml** manifest file which consists of definitions to spin up Deployments and Services such as **Load Balancer** in the front and **Redis Cache** in the backend. The MHC application will be running in the mhc-front pod along with the Load Balancer.

The following image will walk you through all the steps explained in this lab

 ![](images/AKS-workflow.gif)


If you are new to Kubernetes, [click here](documentation/readme.md){:target="_blank"} for description of terminology used in this lab.

### What's covered in this lab

The following tasks will be performed:

* Create an Azure Container Registry (ACR), AKS and Azure SQL server

* Provision the Azure DevOps Team Project with a .NET Core application using the Azure DevOps Demo Generator tool.

* Configure application and database deployment, using Continuous Deployment (CD) in the Azure DevOps

* Initiate the build to automatically deploy the application

<div class="bg-slap"><img src="./images/mslearn.png" class="img-icon-cloud" alt="MS teams" style="width: 48px; height: 48px;">Want additional learning? Check out the <a href="https://docs.microsoft.com/en-us/learn/modules/deploy-kubernetes/" target="_blank"><b><u> Automate multi-container Kubernetes deployments</u></b></a> module on Microsoft Learn.</div>

