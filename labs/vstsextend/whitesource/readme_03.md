## Exercise 2: Trigger a build

You have a **Java code** provisioned by the Azure DevOps demo generator. You will use **WhiteSource Bolt** extension to check the vulnerable components present in this code.

1. Go to **Pipelines** section under **Pipelines** tab, select the build definition **WhiteSourceBolt** and click on **Run pipeline** to trigger a build. Click **Run** (leave defaults).

   ![build-def](images/run.png)

1. To view the build in progress status, click on job named **Phase 1**.

   ![inprogress_build](images/phase.png)

   ![queue-build](images/progress.png)

1. While the build is in progress, let's explore the build definition. The tasks that are used in the build definition are listed in the table below.

    |Tasks|Usage|
    |----|------|
    |![npm](images/npm.png) **npm**| Installs and publishes npm packages required for the build|
    |![maven](images/maven.png) **Maven**| builds Java code with the provided pom xml file|
    |![whitesourcebolt](images/whitesourcebolt.png) **WhiteSource Bolt**| scans the code in the provided working directory/root directory to detect security vulnerabilities, problematic open source licenses|
    |![copy-files](images/copy-files.png) **Copy Files**| copies the resulting JAR files from the source to the destination folder using match patterns|
    |![publish-build-artifacts](images/publish-build-artifacts.png) **Publish Build Artifacts**| publishes the artifacts produced by the build
    
1. Once the build is completed, click back navigation to  see the summary which shows **Test results, Build artifacts** etc. as shown below. 

   ![go back](images/back.png)
   ![build_summary](images/build_summarynew.png)

1. Navigate to **WhiteSource Bolt Build Report** tab  and wait for the report generation of the completed build to see the vulnerability report.

   ![](images/selectwhitesourcetab.png)
   ![report](images/WhiteSourceBolt13.png)

