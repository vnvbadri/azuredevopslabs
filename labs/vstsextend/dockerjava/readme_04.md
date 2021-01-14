## Exercise 3: Configuring MySQL connection strings in the Web App

1. Navigate to the Web app that you have created. Click **Configuration** and select **Application Settings**. Scroll down to the **Connection Strings** section.

1. Add a new MySQL connection string with **MyShuttleDb** as the name and the following string - `jdbc:mysql://`**`{MySQL Server Name}`**`.mysql.database.azure.com:3306/alm?useSSL=true&requireSSL=false&autoReconnect=true&user=`**`{your user name}`**`@`**`{MySQL Server Name}`**`&password=`**`{your password}`**. Replace the following with values that you have noted down

    * MYSQL Server Name - **Server Name** in the MYSQL Server *Overview* page
    * Your user name -  **SERVER ADMIN LOGIN NAME** in the MYSQL Server *Overview* page  
    * Your password -**Password** that you provided during the creation of MYSQL server in Azure

    ![MySQL Connection](images/mysqldbconn.png)

1. Click **Save** to save the connection string.

1. You should be able to login to the application now. Return to the web application and try logging in using any of the below *username/password* combination:

    * *fred/fredpassword*
    * *wilma/wilmapassword*
    * *betty/bettypassword*

