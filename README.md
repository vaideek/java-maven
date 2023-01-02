# Introduction

MyShuttle is a sample Java/JEE application that provides booking system, admin portal and a control system for the drivers. The application uses entirely open source software including Linux, Java, Apache, and MySQL which creates a web front end, an order service, and an integration service.

![](https://vstsdemodata.visualstudio.com/aa2f337f-2dbf-4700-88e5-bf4f57f49cc6/_api/_versioncontrol/itemContent?repositoryId=14c9c1ce-2de9-4198-a252-3caca0305407&path=%2F1.png&version=GBmaster&contentOnly=true&__v=5)

### Build and deploy Java Application with Azure DevOps


In this Project we are to deploying  an Java application to Azure App Service.
using Azure DevOps pipeline.


### Prerequisites

1. You need an organization before you can create a project. If you haven't created an
   organization yet, create one by following the instructions in Sign up, sign in to 
   Azure DevOps, which also creates a project. Or see Create an organization or project 
   collection.

2. Create a project in organization.
3. Add an Java repository to project.

Set-Up the Infrastructure in Azure Portal for the Project.

4. Create an Azure Web App in Azure Portal.
5. Create Azure database for MySQL.
     
    --- To create Azure Web App. Go to Portal.azure.com

        --- Create a resources group.
        --- Create a App Service in that resources group.
        --- Give the name to App Service.
        --- Select code as publish.
        --- Select runtime stack as Java 8
        --- Select Java web server stack as Apache Tomcat 9.0
        --- Select Windows Operating system.
        --- Select region.
        --- Select App Service Plan.
        --- Review and create.

    --- To create Azure database for MySQL. Go to Portal.azure.com

        --- Create Azure database for MySQL resource.
        --- Select single server database.
        --- Name of the database.
        --- Select the version of MySQL as 5.7
        --- Select the basic configuration server.
        --- Create Username and password.

Once resources are deployed. You need to change some configuration in the resources.

1. Navigate to MySQL database, go to connection security blade in left hand side. And Allow access to azure services.
   it will use Azure Web App to communicate with MySQL.
2. Navigate to properties in MySQL, and copy the server URL and server Username. Use server URL and server Username 
   in the connection string to communicate with App Service.
3. Navigate to Azure Web App, in configuration setting you need to add the connection string.
4. Click on new connection string. Give the name to connectring and pass the value.

Now, The Web App is ready to communicate with MySQL.

#### Create a build pipeline for the Java Application.
   --- you can create CI pipeline using YML (or) classic editor.
   ---Here we will discuss about classisc editor.   
   
   ### First Step
  
   --- Create a build pipeline.
   --- Select the Agent Pool and Agent Specification in the pipeline.
   --- Add the tasks for the Java Application.
    
   ### Tasks for Java Application

   --- Add Maven. 
   --- Add the copy filestask.
   --- Add the publish build artifact task.

   ### Second Step

   Save and Run the build pipeline.
     --- In First task, It wwill build the java application.
     --- In Second task, it will copy the files.
     --- In Third task, it will publish the artifact. Which will he used as a input to the release pipeline.

### Create Release pipeline 

   ### First Step

   This part is to deploy the application into Azure Web App.
   In this stage, you only have one action. 
 
    ### App Service Deploy Task
      --- Create release pipeline.
      --- Select the Azure App Service Deployment template. To perform the release pipeline.
      --- Select the artifact in the artifact location. Add the stage to the release pipeline.
      --- Select the jobs in te stage.
      --- In the stage section select your subscription in which your App Service is created.
      --- Select your App Service type.
      --- Select your App Service name.
      --- Select the file in Package or folder step.

    ### Azure Database for MySQL Deployment 
      --- Select Azure Database for MySQL Deployment task.
      --- Select subscription.
      --- Select Hostname.
      --- Provide username and password.
      --- Select type as MySQL Script File.
      --- Select the file in Package or folder step.
      
      --- In run on agent section select agent pool and agent Specifications.

      --- In Deploy Azure App Service task, select your artifact file in the package section.
      --- Save and create release pipeline...



