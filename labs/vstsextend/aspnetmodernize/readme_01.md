## Overview

When you decide to modernize your web applications and move them to the cloud, you don’t necessarily have to entirely re-architect your apps. Establishing an environment that emulates your on-premises architecture and putting your application "gets" you there, but doesn't accomplish much more than that.

Re-architecting an application by using an advanced approach like micro-services isn't always an option, because of cost and time restraints. Ripping apart the app and re-writing what sometimes can be years of work and iterations of people and business decisions probably wouldn't be the advised first step.

Depending on the type of application, re-architecting your apps might not be necessary. But adding a Dockerfile, and maybe migrating the database to a service offering like Azure's SQL Database require no code change other than connection strings.

In this Lab, you will use the Nerd Dinner Application. Nerd Dinner is an Open Source ASP.NET MVC Project that helps nerds and computer people plan get-togethers. You can see the site running LIVE at [http://www.nerddinner.com](http://www.nerddinner.com). You will move the application DB to Azure SQL instance and add the Docker support to the application to run the application in Azure Container Instances.

