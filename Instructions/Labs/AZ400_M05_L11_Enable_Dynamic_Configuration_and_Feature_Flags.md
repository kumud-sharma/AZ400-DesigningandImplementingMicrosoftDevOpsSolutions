# Lab 11: Enable Dynamic Configuration and Feature Flags

## Lab requirements

- This lab requires **Microsoft Edge** or an [Azure DevOps supported browser.](https://learn.microsoft.com/azure/devops/server/compatibility?view=azure-devops#web-portal-supported-browsers)

- **Set up an Azure DevOps organization:** If you don't already have an Azure DevOps organization that you can use for this lab, create one by following the instructions available at [Create an organization or project collection](https://learn.microsoft.com/azure/devops/organizations/accounts/create-organization?view=azure-devops).

- Identify an existing Azure subscription or create a new one.

- Verify that you have a Microsoft account or an Azure AD account with the Contributor or the Owner role in the Azure subscription. For details, refer to [List Azure role assignments using the Azure portal](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-list-portal) and [View and assign administrator roles in Azure Active Directory](https://learn.microsoft.com/azure/active-directory/roles/manage-roles-portal).

## Lab overview

[Azure App Configuration](https://learn.microsoft.com/azure/azure-app-configuration/overview) provides a service to manage application settings and feature flags centrally. Modern programs, especially those running in a cloud, generally have many distributed components. Spreading configuration settings across these components can lead to hard-to-troubleshoot errors during application deployment. Use App Configuration to store all the settings for your application and secure their accesses in one place.

## Objectives

After you complete this lab, you will be able to:

- Enable dynamic configuration
- Manage feature flags

## Estimated timing: 60 minutes

## Architecture Diagram

  ![Architecture Diagram](images/lab11-architecture-new.png)


## Set up an Azure DevOps organization(Skip if already done)

1. On your lab VM open **Edge Browser** on desktop and navigate to [Azure DevOps](https://go.microsoft.com/fwlink/?LinkId=307137), and if prompted sign with the credentials.

    * Email/Username: <inject key="AzureAdUserEmail"></inject>

    * Password: <inject key="AzureAdUserPassword"></inject>

2. In the pop-up for *Help us protect your account*, select **Skip for now (14 days until this is required)**.

3. On the next page accept defaults and click on continue.
   
   ![](images/1.Organization-1.png)
   
4. On the **Almost Done...** page fill the captcha and click on continue. 

### Exercise 0: Configure the lab prerequisites 

In this exercise, you will set up the prerequisites for the lab, which consist of a new Azure DevOps project with a repository based on the **eShopOnWeb**

**Task 1: (skip if done) Create and configure the team project**

In this task, you will create an **eShopOnWeb** Azure DevOps project to be used by several labs.

   1. On your lab computer, in a browser window open your Azure DevOps organization. Click on **New Project(1)**. Give your project the name **eShopOnWeb(1)** and choose visibility as **Private(2)**. Click on **Create(3)**
      
      ![](images/3.createproject-1.png)
      
 **Task 2: (skip if done) Import eShopOnWeb Git Repository**
 
 In this task you will import the eShopOnWeb Git repository that will be used by several labs.

   1. On your lab computer, in a browser window open your Azure DevOps organization and the previously created eShopOnWeb project. Navigate to **Repos(1)>Files(2)**       and under the Import a repository click on **Import(3)**. 
      
      ![](images/4.Importarepo-1.png)
  
   2. On the **Import a Git Repository** window, Select repository type as **Git(1)** paste the following URL in Clone URL tab                                             **https://github.com/MicrosoftLearning/eShopOnWeb.git(2)** and click on **Import(3)**.
      
      ![](images/5.Importarepo-2.png)
      
   3. The repository is organized the following way:

        O **.ado** folder contains Azure DevOps YAML pipelines
        
        O **.devcontainer** folder container setup to develop using containers (either locally in VS Code or GitHub Codespaces)
        
        O **.github** folder container YAML GitHub workflow definitions.
        
        O **.src** folder contains the .NET 6 website used on the lab scenarios.
        
        ![](images/6.repositoryview.png)
        
   **Task 3: (skip if done) Set main branch as default branch**
   
   1. Go to **Repos(1)>Branches(2)**. Hover on the **main(3)** branch then click the **ellipsis(4)** on the right of the column and Click on **Set as default branch(5)**
      
      ![](images/7.maindefaultbranch.png)
      
### Exercise 1: Import and run CI/CD Pipelines

In this exercise, you will import and run the CI pipeline, configure the service connection with your Azure Subscription and then import and run the CD pipeline.

In this task, you will create an eShopOnWeb Azure DevOps project to be used by several labs.

#### Task 1: Import and run the CI pipeline

Let's start by importing the CI pipeline named **eshoponweb-ci.yml**.

1. From the left navigation pane go to **Pipelines > Pipelines**.Click on **New pipeline** button
   
2. Select **Azure Repos Git (Yaml)**.

   ![](images/9.selectazurereposgityml.png)

3. Select the **eShopOnWeb** repository.

   ![](images/10.selecteshoponwebrepo.png)

4. Select **Existing Azure Pipelines YAML File**.

   ![](images/AZ-400-ss.png)

5. Select the **/.ado/eshoponweb-ci.yml** file then click on **Continue**.

   ![](images/12.ymfilepath.png)

6. Click the **Run** button to run the pipeline.

   ![](images/13.runthepipeline.png)

7. Your pipeline will take a name based on the project name. Let's **rename** it for identifying the pipeline better. Go to **Pipelines>Pipelines** and click on the recently created pipeline. Click on the **ellipsis** and **Rename/move** option. Name it **eshoponweb-ci** and click on **Save**.

   ![](images/14.renamepipeline.png)
   
   ![](images/lab-11-1.png)

**Task 2: Manage the service connection**

You can create a connection from Azure Pipelines to external and remote services for executing tasks in a job.

In this task, you will create a service principal by using the Azure CLI, which will allow Azure DevOps to:

o Deploy resources on your azure subscription
   
o Deploy the eShopOnWeb application
   
> **Note**: If you do already have a service principal, you can proceed directly to the next task.
      
 You will need a **service principal** to deploy Azure resources from Azure Pipelines.
 
 A **service principal** is automatically created by Azure Pipeline when you connect to an Azure subscription from inside a pipeline definition or when you create a new service connection from the project settings page (automatic option). You can also manually create the service principal from the portal or using Azure CLI and re-use it across projects.
 
   1. From the lab computer, start a web browser, navigate to the **portal.azure.com**, and sign in with the user account **email(1)** and **password(2)** that has the Owner role in the Azure subscription you will be using in this lab and has the role of the Global Administrator in the Azure AD tenant associated with this subscription.

      ![](images/16.loginemail.png)
      
      ![](images/17.loginpassword.png)
     
   2. In the Azure portal, click on the **Cloud Shell** icon, located directly to the right of the search textbox at the top of the page.

      ![](images/18.cloudshell.png)
     
   3. If prompted to select either **Bash** or **PowerShell**, select **Bash**.
   
      > **Note**: If this is the first time you are starting **Cloud Shell** and you are presented with the **You have no storage mounted** message, select the subscription you are using in this lab, and select **Create storage** then it will create storage account to store the logs.
         
      ![](images/19.selectbash.png)
      
      ![](images/68.storage.png)
        
   4. From the **Bash** prompt, in the **Cloud Shell** pane, run the following commands to retrieve the values of the Azure subscription ID attribute:
   
       ```
       subscriptionName=$(az account show --query name --output tsv)
       subscriptionId=$(az account show --query id --output tsv)
       echo $subscriptionName
       echo $subscriptionId
       ```
      
      ![](images/20.Bashscript.png)
      
      >  **Note**: Copy both values to a text file. You will need them later in this lab.
     
   5. From the **Bash** prompt, in the **Cloud Shell** pane, run the following command to create a service principal:

      ```
      az ad sp create-for-rbac --name sp-az400-azdo --role contributor --scopes /subscriptions/$subscriptionId
      ```

      > **Note**: The command will generate a JSON output. Copy the output to text file. You will need it later in this lab.

      ![](images/21.serviceprinciplecommand.png)

  6. Next, from the lab computer, start a web browser, navigate to the Azure DevOps **eShopOnWeb** project. Click on **Project Settings>Service Connections(1) (under Pipelines)** and **Create Service Connection(2)**.

      ![](images/22.projectssetting.png)
     
  7. On the **New service connection** blade, select **Azure Resource Manager** and **Next** (may need to scroll down).

      
  8. The choose **Service principal (manual)(1)** and click on **Next(2)**.

     ![](<images/lab-400-border 0.1.png>)

  9. Fill in the empty fields using the information gathered during previous steps:

        o **Subscription Id(1)** and **Subscription Name(2)**.
        
        o **Service Principal Id (or clientId)(3)**, **Service Principal Key (or Password)(4)** and **TenantId(5)** and click **Verify(6)** to check the connection.
        
        o In **Service connection name type azure subs(7)**. This name will be referenced in YAML pipelines when needing an Azure DevOps Service Connection to communicate with your Azure subscription.
        
        o **Enable(8)** Grant access permissions to all pipelines.
        
        o Click on **Verify and Save(9)**
        
        ![](images/27.SPcreation-1.png)
        
        ![](images/lab-400.15.png)
        
        ![](images/lab-400-1.2.1.png)
          
 **Task 3: Import and run the CD pipeline**
 
 Let's import the CD pipeline named **eshoponweb-cd-webapp-code.yml*.
 
   1. Go to **Pipelines(1)>Pipelines(2)** and Click on **New pipeline(3)** button

      ![](images/30.newcdpipeline.png)

   2. Select **Azure Repos Git (Yaml)**

      ![](images/31.newcd-2.png)

   3. Select the **eShopOnWeb** repository

      ![](images/32.newcdreposelect-3.png)

   4. Select **Existing Azure Pipelines YAML File**

      ![](images/33.newpipeline-4.png)

   5. Select the **.ado/eshoponweb-cd-webapp-code.yml(1)** file then click on **Continue(2)**

      ![](images/33.newpipeline-4-1.png)
   
      In the YAML pipeline definition, customize:
      
      - **AZ400-EWebshop-NAME(1)** replace NAME with **<inject key="DeploymentID" enableCopy="false"/>**.
      - **YOUR-SUBSCRIPTION-ID(2)** with your Azure subscription id.
      - **az400-webapp-NAME(3)** replace NAME with **<inject key="DeploymentID" enableCopy="false"/>**.

      ![](images/34.ymlnamereplace-1.png)
         
   6. Click on **Save and Run** and wait for the pipeline to execute successfully.

      > **Note**: The deployment may take a few minutes to complete.When the pipeline is running if you get a prompt  as **Permissions Needed** click on **view** and click on permit 

       ![](images/35.pipelinesave&run.png)
       
       ![](images/36.pipelinesuccess.png)

      The CD definition consists of the following tasks:
       - **Resources**: it is prepared to automatically trigger based on CI pipeline completion. It also downloads the repository for the bicep file.
       - **AzureResourceManagerTemplateDeployment**: Deploys the Azure Web App using bicep template.

  7. Your pipeline will take a name based on the project name. Let's **rename** it for identifying the pipeline better. Go to **Pipelines(1)>Pipelines(2)** and          click on the recently created pipeline. Click on the **ellipsis(3)** and **Rename/move(4)** option. Name it **eshoponweb-cd-webapp-code(5)** and click on          **Save(6)**.

     ![](images/37.rename-1.png)   
     
     ![](images/38.rename-2.png) 

# Exercise 2: Manage Azure App Configuration

In this exercise, you will create the App Configuration resource in Azure, enable the managed identity and then test the full solution.

>Note: This exercise doesn't require any coding skills. The website's code implements already Azure App Configuration functionalities.
If you want to know how to implement this in your application, please take a look at these tutorials: [Use dynamic configuration in an ASP.NET Core app](https://learn.microsoft.com/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core) and [Manage feature flags in Azure App Configuration](https://learn.microsoft.com/azure/azure-app-configuration/manage-feature-flags).

## Task 1: Create the App Configuration resource

1. In the Azure Portal, search for the **App Configuration** service

   ![](images/39.appconfig-1.png)
   
   ![](images/40.createappconfig.png)
   
2. Click **Create app configuration** then select:
    - Your Azure Subscription(1)
    - The Resource Group **(2)** created previously (it should be named **AZ400-EWebShop1-<inject key="DeploymentID" enableCopy="false"/>**)
    - Retain the same region which is in the CD Pipeline previously **(3)**
    - Give a unique name **appcs-<inject key="DeploymentID" enableCopy="false"/>** **(4)**.
    - Select the **Free(5)** pricing tier

    ![](images/41.createappconfig-2.png)
     
3. Click on **Review + create(6)** then **Create**

   ![](images/42.createappconfig-3.png)
   
4. After creating the App Configuration service, go to **Overview(1)** and copy/save the value of the **Endpoint(2)**.

   ![](images/43.endpointurl.png)

## Task 2: Enable Managed Identity

1. Go to the **Web App(1)** deployed using the pipeline (it should be named **az400-webapp-NAME**).

   ![](images/44.webapp-1.png)
   
2. In the **Settings(2)** section, click on **Identity(3)** then switch status to **On(4)** in the **System Assigned** section, click **save(5)>yes(6)** and wait a few seconds for the operation to finish.

   ![](images/45.managedidentity-1.png)
   
   ![](images/46.managedidentity-2.png)
   
3. Go back to the **App Configuration(1)** service and click on **Access control(IAM)(2)** then **+Add(3)->Add role assignment(4)**.

   ![](images/47.roleassignment-1.png)
   
4. In the **Role(1)** section, select **App Configuration Data Reader(2)** and click on **Next(3)**.

   ![](images/48.roleassignment-2.png)
   
5. In the **Members(1)** section, check **Manage Identity(2)** then click on **+ Select members(3)**. In the select manage identities tab select **Managed Identity(4)** as **App Service** of your **Web App(5)** (they should have the same name) and then click on **Select(6)**.

   ![](images/49.roleassinment-3.png)
   
6. Click on **Review and assign**

   ![](images/50.roleassignment-4.png)

## Task 3: Configure the Web App

In order to make sure that your website is accessing App Configuration, you need to update its configuration.
1. Go back to your Web App.
2. In the **Settings(1)** section, click on **Configuration(2)** and select **+ New application setting(3)**.

   ![](images/51.Appsetting-1.png)

3. Add two new application settings:
    - First app setting
        - **Name:** UseAppConfig
        - **Value:** true

         ![](images/52.1stappsetting.png)
      
    - Second app setting
        - **Name:** AppConfigEndpoint
        - **Value:** *the value you saved/copied previously from App Configuration Endpoint. It should look like https://appcs-NAME-REGION.azconfig.io*
      
         ![](images/53.2ndappsetting.png)
      
4. Click **Save** then **Continue** and wait for the settings to be updated.

   ![](images/54.appsetting-2.png)
   
   ![](images/55.appsetting-3.png)
   
5. Go to **Overview(1)** and click on **Browse(2)**

   ![](images/lab-400-border.png)
   
6. At this step, you will see no changes in the website since the App Configuration doesn't contain any data. This is what you will do in the next tasks.

## Task 4: Test the Configuration Management

1. In your website, select **Visual Studio(2)** in the **Brand(1)** drop-down list and click on the arrow button (**>(3)**).

   ![](images/58.brandvisualstudio.png)
2. You will see a message saying **"THERE ARE NO RESULTS THAT MATCH YOUR SEARCH"(4)**.

   ![](images/59.brandvsmsg.png)
   
The goal of this Lab is to be able to update that value without updating the website's code or redeploying it.

3. In order to try this, go back to **App Configuration(1)**. In the **Operations(2)** section, select **Configuration Explorer(3)** and Click on **+ Create(4) > Key-value(5)** then add:
    - **Key(6):** eShopWeb:Settings:NoResultsMessage
    - **Value(7):** *type your custom message*
   Click **Apply(8)** then go back to your website and refresh the webapp browser page.
   
   ![](images/60.appconfigkeyvalue.png)
   
   ![](images/61.appconfigkeyvaluecreate.png)
   
4. You should see your new message instead of the old default value.

   ![](images/62.custommsg.png)
   
Congratulations! In this task, you tested the **Configuration explorer** in Azure App Configuration.

## Task 5: Test the Feature Flag

Let's continue to test the Feature manager.
1. In order to try this, go back to **App Configuration(1)**. In the **Operations(2)** section, select **Feature manager(3)**.

   ![](images/63.featureflag-1.png)
   
2. Click on **+ Create(4)** then add:
    - **Enable feature flag(1):** Checked
    - **Feature flag name(2):** SalesWeekend
   and click **Apply(3)** then go back to your website and refresh the page.
   
   ![](images/64.salesweekend.png)
    
3. You should see an image with text "ALL T-SHIRTS ON SALE THIS WEEKEND".

   ![](images/65.websiteimage.png)
   
4. You can disable this feature in App Configuration and then you would see that the image disappears.

   ![](images/66.disableflag.png)
   
   ![](images/67.dissappearmsg.png)

   **Congratulations!!** In this task, you tested the **Feature manager** in Azure App Configuration.

  **Congratulations** on completing the lab! Now, it's time to validate it. Here are the steps:

  > - Navigate to the Lab Validation tab, from the upper right corner in the lab guide section.
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

## Review

In this lab, you learned how to dynamically enable configuration and manage feature flags.

### You have successfully completed the lab.
