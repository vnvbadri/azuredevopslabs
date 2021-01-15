## Integrating Microsoft Teams with Azure DevOps Services

**Azure DevOps Services** integration with Microsoft Teams provides a comprehensive chat and collaborative experience across the development cycle. Teams can easily stay informed of important activities in your Azure DevOps team projects with notifications and alerts on work items, pull requests, code commits, build and release.

1. Select **Tailwind Traders** team that was created.  Click the ellipsis or **'...'** right side at the top nav of your team channel, and then select **Connectors**.
   
    ![](images/connectors_new.png)

1. Select **Azure DevOps** connector from the list and click **Add**.

   ![](images/azuredevops_connector.png)

1. Click **Add** to add the connector for your team.
   
    ![](images/install_connector_new.png)

1. Select your organization (you may be prompted to sign in first), the project and your team. Choose the type of activity you want to be notified about. Depending on the event, you may be given further fields to filter down the notifications so you can filter out notifications your team does not care about. For example, for work item events, you can filter by area path, work item type, and even particular field changes.

   1. Click on log in.  

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/teams/images/connect-teams-1.png)  

 1. Click on continue.  

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/teams/images/connect-teams-2.png)  

 1. Enter the username, Click on Next. Enter the Password if prompted.  

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/teams/images/connect-teams-3.png)  

 1. Click on Accept.  

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-sathish/labs/vstsextend/teams/images/connect-teams-4.png)

   When you are happy with the configuration, **Save** it.

1. Since Azure DevOps is configured now, activity from your Azure DevOps Services project will start appearing in your Teams channel.
   
   ![](images/azuredevops_activity_new.png)

1. If you want to make a change to an existing connector, navigate to the **Configured** tab on the **Connector** dialog, find the connector and click **Manage**. 

   ![](images/manage_connector.png)

