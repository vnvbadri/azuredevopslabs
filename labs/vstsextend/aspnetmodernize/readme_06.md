## Exercise 2: Add Docker Support and debug the application locally within the Docker container using Visual Studio

1. Visual Studio has great support for Docker. In order to containerize the application using Docker, all you have to do is right-click on the project, select **Add->Container Orchestrator Support**

   ![adddockersupport](images/adddockersupport.png)

2. Visual Studio then adds the Docker file, compose files and a specific Docker project to the solution. It also inspects the project to determine the proper base image to use for your project.

   ![dockersupportfiles](images/dockersupportfiles.png)

   In the case of Nerd Dinner, it chose to use microsoft/aspnet:4.7.1-windowsservercore-ltsc2016. Here is the complete file.

   ```csharp
   FROM microsoft/aspnet:4.7.1-windowsservercore-ltsc2016
   ARG source
   WORKDIR /inetpub/wwwroot
   COPY ${source:-obj/Docker/publish} .
   ```

3. To run the application locally and debug within the Docker container using Visual Studio and to test the connectivity to the SQL Azure instance, set the **docker-compose** as the startup project and click on **Docker**.

   ![rundocker](images/rundocker.png)

   Visual Studio downloads the base images and subsequently builds your dev images

   ![downloadingimages](images/downloadingimages.png)

   Once the images are downloaded and build is done you will see the application launching in the local browser.

    ![applicationlaunch](images/applicationlaunch.png)

   Now the application is running in local docker. To see the list of docker images you can run the following command.

   ```csharp
    docker images
   ```

     You will see the images similar to this

   ![dockerimages](images/dockerimages.png)

