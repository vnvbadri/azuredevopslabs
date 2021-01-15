## Exercise 1: Migrate the LocalDB to SQL Server in Azure

In this exercise, you will create a SQL Azure instance and migrate the application LocalDB to SQL Server in Azure.

1. Browse to the [Select SQL Deployment option](https://portal.azure.com/#create/Microsoft.AzureSQL) page. 

1. Under **SQL databases**, leave **Resource type** set to **Single database**, and select **Create**. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/select-deployment.png) 

1. On the **Basics** tab of the **Create SQL Database** form, under **Project details**, select the Azure **Subscription** available. 

1. For **Resource group**, select the available Resource group. 

1. For **Database name** enter *mySampleDatabase*. 

1. For **Server**, select **Create new**, and fill out the **New server** form with the following values: 

    - **Server name**: Enter *mysqlserver*, and add some characters for uniqueness. We can't provide an exact server name to use because server names must be globally unique for all servers in Azure, not just unique within a subscription. So enter something like mysqlserver12345, and the portal lets you know if it is available or not. 

    - **Server admin login**: Enter *azureuser*. 

    - **Password**: Enter a password that meets requirements, and enter it again in the **Confirm password** field. 

    Select **OK**. 

1. Leave **Want to use SQL elastic pool** set to **No**. 

1. Under **Compute + storage**, select **Configure database**. 

1. Under the **Compute tier**, select **Serverless**, and then select **Apply**. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/configure-database.png) 

1. Select **Next: Networking** at the bottom of the page. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/new-sql-database-basics.png) 

1. On the **Networking** tab, for **Connectivity method**, select **Public endpoint**. 

1. For **Firewall rules**, set **Add current client IP address** to **Yes**. Leave **Allow Azure services and resources to access this server** set to **No**. 

1. Select **Next: Additional settings** at the bottom of the page. 

    ![Iimage.](https://raw.githubusercontent.com/CloudLabs-MOC/azuredevopslabs/az400-badri/labs/vstsextend/aspnetmodernize/images/networking.png) 

1. On the **Additional settings** tab, in the **Data source** section, for **Use existing data**, select **None** also in the **Azure Defender for SQL** section, for **Enable Azure Defender for SQL**, select **Not now** 

1. Select **Review + create** at the bottom of the page: 

1. On the **Review + create** page, after reviewing, select **Create**.


2. Once the SQL database is provisioned in Azure, open the **SQL Server Object Explorer** in Visual Studio. Click on **Add Server** icon and connect to the Azure SQL server which you have deployed in the previous step.

    ![connecttoazuresql](images/connecttoazuresql.png)
3. To get the schema moved from the LocalDB to the new SQL Azure instance right-click on the LocalDB Instance and select the Schema Compare option.

   ![schemacompare](images/schemacompare.png)

   In the schema compare wizard select target as Azure SQL database and click on compare.

   ![schemacompare2](images/schemacompare2.png)

   Click on **Update** in the next wizard to update the schema to Azure SQL database.

   ![updateschema](images/updateschema.png)
   ![updateschema2](images/updateschema2.png)

4. Similarly to get the data moved from the LocalDB to the SQL Azure instance to right-click on the LocalDB Instance and select the Data Compare tool and walk through the SQL Data Compare wizard.

      ![datacompare](images/datacompare.png)

   In the wizard select target as Azure SQL database and click on compare.

      ![datacompare2](images/datacompare2.png)

   Click on **Update** to move data to Azure SQL database.

      ![datacompare3](images/datacompare3.png)

5. In order to accomplish the **zero code change mantra**, using web.config transforms is the best way to accomplish. Here you will add a new **web.release.config** with a new entry. Open the **web.release.config** in Visual Studio and add the below entry.

   ```csharp
   <connectionStrings>
      <add name="DefaultConnection" connectionString="Data Source=nerddinnerlabsql.database.windows.net;Initial Catalog=nerddinnerlab;Integrated Security=False;User ID=yourUserID;Password=yourdbpassword;Connect Timeout=30;Encrypt=True;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False" providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
   </connectionStrings>
   ```

   >**Note**: Replace the connection string with your Azure SQL database connection string.

  Now you have successfully migrated the application LocalDB to Azure SQL Db and also updated connection string to refer to Azure SQL.

