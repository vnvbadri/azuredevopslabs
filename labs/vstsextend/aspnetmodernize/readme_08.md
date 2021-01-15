## Exercise 4: Push the new Docker images from ACR to Azure Container Instances (ACI)

In this exercise, you will create an Azure Container Instance and push the new Docker image from ACR to Azure Container Instance.

You have options as to where the application can be deployed.

* Azure Container Instances
* Azure Container Service
* Service Fabric

You will use a Windows Container on Azure Container Instances (ACI) to bring up Nerd Dinner.

1. You will use Azure CLI to create and push the image to Azure Container Instance. Click on **Cloud Shell** in the Azure portal, choose **Bash**. Click on Show advanced settings enter unique name for Storage account and File share then Create storage. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/bash1.png) 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/bash2.png)

3. Run the following command to Create windows ACI and push the Nerd Dinner image from ACR.

   ```csharp
   az container create --name nerddinnerapp --resource-group nerddinnerapp --os-type windows --image {your acr name}.azurecr.io/nerddinner:{Image Tag} --ip-address public
   ```

   ![deployaci](images/deployaci.png)

   When prompted for **image registry password** paste the password which you had copied in the previous exercise
   > Replace **your acr name** and **Image tag** with your resources details

   It would take approximately 5-10 minutes to deploy ACI.

4. Navigate to the resource group where ACI is being deployed or deployed, and select the **nerddinnerapp** container group.

    ![acistatus](images/acistatus.png)

    Once the **State** of the container is **Running** you can access the deployed **Nerd Dinner** application using **IP address**. Copy the **IP address** and paste in the browser to see the application running.

    ![finaloutput](images/finaloutput.png)

