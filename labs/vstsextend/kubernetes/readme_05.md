## Exercise 2: Trigger a Build and deploy application

In this exercise, let us trigger a build manually and upon completion, an automatic deployment of the application will be triggered. Our application is designed to be deployed in the pod with the **load balancer** in the front-end and **Redis cache** in the back-end.

1. Select **MyHealth.AKS.build** pipeline. Click on **Run pipeline**

    ![manualbuild](images/runpipeline.png)

1. Once the build process starts, select the build job to see the build in progress.
    
    ![clickbuild](images/buildprogress.gif)
    

1. The build will generate and push the docker image to ACR. After the build is completed, you will see the build summary. To view the generated images navigate to the Azure Portal, select the **Azure Container Registry** and navigate to the **Repositories**.

    ![imagesinrepo](images/imagesinrepo.png)

1. Switch back to the Azure DevOps portal. Select the **Releases** tab in the **Pipelines** section and double-click on the latest release. Select **In progress** link to see the live logs and release summary.

    ![releaseinprog](images/releaseinprog.png)

    ![release_summary1](images/release_summary1.png)

1. Once the release is complete, launch the [Azure Cloud Shell](https://docs.microsoft.com/en-in/azure/cloud-shell/overview) and run the below commands to see the pods running in AKS:

    1. Type **`az aks get-credentials --resource-group yourResourceGroup --name yourAKSname`** in the command prompt to get the access credentials for the Kubernetes cluster. Replace the variables `yourResourceGroup` and `yourAKSname` with the actual values.

         ![Kubernetes Service Endpoint](images/getkubeconfig.png)

    1. **`kubectl get pods`**

        ![getpods](images/getpods.png)

        The deployed web application is running in the displayed pods.

1. To access the application, run the below command. If you see that **External-IP** is pending, wait for sometime until an IP is assigned.

    **`kubectl get service mhc-front --watch`**

    ![watchfront](images/watchfront.png)

1. Copy the **External-IP** and paste it in the browser and press the Enter button to launch the application.

    ![finalresult](images/finalresult.png)

### Kubernetes resource view in the Azure portal (preview)

The Azure portal includes a Kubernetes resource viewer (preview) for easy access to the Kubernetes resources in your Azure Kubernetes Service (AKS) cluster. Viewing Kubernetes resources from the Azure portal reduces context switching between the Azure portal and the kubectl command-line tool, streamlining the experience for viewing and editing your Kubernetes resources. The resource viewer currently includes multiple resource types, such as deployments, pods, and replica sets.

The Kubernetes resource view from the Azure portal replaces the AKS dashboard add-on, which is set for deprecation.

![resource review](images/aks-monitor.png)

More information found at: https://docs.microsoft.com/en-us/azure/aks/kubernetes-portal

