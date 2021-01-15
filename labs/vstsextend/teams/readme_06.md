## Azure Pipelines with Microsoft Teams

Azure Pipelines app on Microsoft Teams enables you to monitor the events for your pipelines. You can set up and manage subscriptions for releases, pending approvals, completed builds etc. and get notifications right into your Teams channel for these updates. You can also approve releases from within your Teams channel.

### Install Azure Pipelines app to your team

1. Visit the App store in Microsoft Teams and search for the **Azure Pipelines** app. Select **Azure Pipelines** app.
    
     ![](images/add_azurepipelines.png)

1. In the app,click on **Add**.
     
      ![](images/install_azurepipelines_new.png)

1. Once the app is added, click on the drop down and select **Add to a team**
      
      ![](images/add_to_team.png)

1. Select your team and click on **Set up a bot**

      ![](images/set_up_bots.png)

1. Use the `@azure pipelines` handle to start interacting with the app.

1. In Conversations enter `@Azure Pipelines signin`.

    ![](images/azurepipelines_signin.png)

1. The app asks you to **Sign in** and authenticate to Azure Pipelines. Click **Sign in** and complete the authentication.

     ![](images/azurepipelines_signin2.png)
     
     ![](images/azurepipelines_signin3.png)
     
     ![](images/azurepipelines_signin4.png)
    
### Subscribe for the pipelines notifications

To start monitoring a pipeline, use the following command inside a channel:

`@azure pipelines subscribe [pipeline url]`

The pipeline URL can be to any page within your pipeline that has a *definitionId* or *buildId/releaseId* present in the URL.

1. For example, to subscribe for Build pipelines enter
  
   `@azure pipelines subscribe https://dev.azure.com/myorg/Tailwind%20Traders/_build?definitionId=2`
 
   ![](images/azurepipelines_build.png)

   For Build pipelines, the channel is subscribed to the Build completed notification

1. To subscribe for Release pipelines enter

   `@azure pipelines subscribe https://dev.azure.com/myorg/Tailwind%20Traders/_releaseDefinition?definitionId=2`
   
   ![](images/azurepipelines_release.png)

   For Release pipelines, the channel is subscribed to the *Release deployment started*, *Release deployment completed*, and *Release deployment approval pending* notifications.

1. **Managing Subscriptions**: You can add or remove subscriptions by using the following command

     `@azure pipelines subscriptions`
This command lists all of the current subscriptions for the channel and allows you to add/remove subscriptions.
    
    ![](images/azurepipelines_managesub.png)

    ![](images/azurepipelines_managesub2.png)

### Using filters to customize subscriptions
When a user subscribes to any pipeline, a few subscriptions are created by default without any filters being applied. Often, users have the need to customize these subscriptions. For example, users may want to get notified only when builds fail or when deployments are pushed to a production environment. The Azure Pipelines app supports filters to customize what you see on your channel.

Run the `@Azure Pipelines subscriptions` command and select **Add Subscription**.

   ![](images/azurepipelines_managesub.png)

   - **Get notifications only for failed builds**
   
    ![](images/azurepipelines_custombuildsub_new.png)

 - **Get notifications only if the deployments are pushed to prod environment** 
   
    ![](images/azurepipelines_customreleasesub_new.PNG)


