## Exercise 3: Publish Docker Images to Azure Container Registry (ACR)

 Now that you have validated that the application is running successfully in local Docker, you can publish the image to a new or existing Azure Container Registry using the publishing wizard in Visual Studio.

1. Right-click on the project, select **Publish**

   ![clickpublish](images/clickpublish.png)

2. In the Publish wizard select **Container Registry** and select **Create New Azure Container Registry** and click on **Publish**

   ![publishtarget](images/publishtarget.png)

3. Fill the required details and click on **Create**

   ![acrdetails](images/acrdetails.png)

4. When publishing, the production Docker image is created and pushed to the Azure Container Registry.

   ![pushrefstoacr](images/pushrefstoacr.png)

5. Once the publish is successful, navigate to the deployed ACR in the Azure portal. You will see **nerddinner** repository with image Tag is published.

   ![acrrepositories](images/acrrepositories.png)

6. Select **Access Keys** under settings in ACR and copy the **password**. This password is required in the next exercise.

   ![accesskey](images/accesskey.png)

