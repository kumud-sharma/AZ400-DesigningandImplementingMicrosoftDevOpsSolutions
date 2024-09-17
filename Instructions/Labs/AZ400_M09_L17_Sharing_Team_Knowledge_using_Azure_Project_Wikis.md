# Lab 17: Sharing Team Knowledge using Azure Project Wikis

## Lab overview

In this lab, you will create and configure wiki in an Azure DevOps, including managing markdown content and creating a Mermaid diagram.

## Objectives

After you complete this lab, you will be able to:

- Create a wiki in an Azure Project
- Add and edit markdown
- Create a Mermaid diagram

## Estimated timing: 60 minutes

## Architecture Diagram
 
  ![Architecture Diagram](images/lab17-architecture-new.png)


## Set up an Azure DevOps organization. 

1. On your lab VM open **Edge Browser** on desktop and navigate to [Azure DevOps](https://go.microsoft.com/fwlink/?LinkId=307137), and if prompted sign with the credentials.

    * Email/Username: <inject key="AzureAdUserEmail"></inject>

    * Password: <inject key="AzureAdUserPassword"></inject>

2. In the pop-up for *Help us protect your account*, select **Skip for now (14 days until this is required)**.

3. On the next page accept defaults and click on continue.

    ![](images/lab1-image1.png)

4. On the **Almost Done...** page fill the captcha and click on continue. 

    ![](images/lab1-image2.png)

# Exercise 0: Configure the lab prerequisites

In this exercise, you will set up the prerequisites for the lab, which consist of the pre-configured **EShopOnWeb** team project based on an Azure DevOps Demo Generator template and a team created in Microsoft Teams.


## Task 1: Configure the EShopOnWeb project

In this task, you will create a new project named **EShopOnWeb** in Azure DevOps Organization.

1.  Click **Sign in** and sign in with the credentials provided in environment details tab.
    
    > **Email/Username**: <inject key="AzureAdUserEmail"></inject>
    
    > **Password**: <inject key="AzureAdUserPassword"></inject>

2.  On the **Create New Project** page, in the **New Project Name** textbox, type **EShopOnWeb (1)**, select visibility as **Private (2)** and then click **Create Project (3)**

     ![](images/AZ400_M09_L17_03.png)
    
# Exercise 1: Publish code as wiki

In this exercise, you will step through publishing an Azure DevOps repository as wiki and managing the published wiki.

> **Note**: Content that you maintain in a Git repository can be published to an Azure DevOps wiki. For example, content written to support a software development kit, product documentation, or README files can be published directly to a wiki. You have the option of publishing multiple wikis within the same Azure DevOps team project.

## Task 1: Publish a branch of an Azure DevOps repo as wiki

In this task, you will create Azure Repository and publish a branch of an Azure DevOps repo as wiki.

> **Note**: If your published wiki corresponds to a product version, you can publish new branches as you release new versions of your product. 

1.  Ensure that you are viewing the **EShopOnWeb** team project on the Azure DevOps portal. 

     > **Note**: You can access the project page directly by navigating to the [https://dev.azure.com/<inject key="DeploymentID" enableCopy="false"/>/EShopOnWeb]URL.

     ![](images/AZ400_M09_L17_04.png)
    
2.  In the vertical menu on the left side of the **EShopOnWeb** pane, click **Repos**.

     ![](images/AZ400_M09_L17_05.png)

3.  Click on the **Files (1)** pane, we can see that **EShopOnWeb is empty. Add some code!**. So click **Initialize (2)** to initialize the repository for the first time.

     ![](images/AZ400_M09_L17_06.png)
    
4.  Click the **Files (1)** pane. In the branch dropdown list , select **main (2)** branch, and review the content of the main branch.

     ![](images/AZ400_M09_L17_07.png)

5.  We will store the Wiki source files in a separate folder within the Repos current folder structure. From within Repos, select **Files**. Notice the **EShopOnWeb (1)** Repo title on top of the folder structure. Select the **ellipsis (2)**. 

     ![](images/AZ400_M09_L17_08.png)

6.  Choose **+New(1) / Folder (2)**, and provide **Documents (3)** as title for the New Folder name. As a repo doesn't allow you to create an empty folder, provide **READ.ME (4)** as New file name. Click to **Create (5)** folder.

     ![](images/AZ400_M09_L17_09.png)

     ![](images/AZ400_M09_L17_10.png)
    
7.  The **READ.ME (1)** file will open in the built-in view mode. Since this is stored **'as code' (2)**, you need to **Commit** the changes by clicking the **Commit (3)** button.

     ![](images/AZ400_M09_L17_11.png)

8.  In the Azure DevOps vertical menu on the left side, click **Overview (1)**, in the Overview section, select **Wiki (2)**, select **Publish code as wiki (3)**.
    
     ![](images/AZ400_M09_L17_12.png)

9.  On the **Publish code as wiki** pane, specify the following **settings** and click **Publish (5)**.
     | Setting | Value |
     | ------- | ----- |
     | Repository | **EShopOnWeb (1)** |
     | Branch | **main (2)** |
     | Folder | **/Documents (3)** |
     | Wiki name | **EShopOnWeb (Documents) (4)** |

     > **Note**: This will automatically open the Wiki section, and publish the editor, where you can provide a Wiki page title, as well as adding the actual content. Notice you are encouraged to use MarkDown format, but make use of the ribbon to help you with some of the MarkDown layout syntax.
    
     ![](images/AZ400_M09_L17_13.png)

10.  In the Wiki Page **Title** field, enter **Welcome to our Online Retail Store!**
    
      ![](images/AZ400_M09_L17_14.png)

11.  In the **body (1)** of the Wiki Page, paste in the following text and **Save (2)** it:
    
      ```
      ##Welcome to Our Online Retail Store!
      At our online retail store, we offer a **wide range of products** to meet the **needs of our customers**. Our selection includes everything       from *clothing and accessories to electronics, home decor, and more*.

      We pride ourselves on providing a seamless shopping experience for our customers. Our website offers the following benefits:
      1. user-friendly,
      2. and easy to navigate, 
      3. allowing you to find what you're looking for,
      4. quickly and easily. 

      We also offer a range of **_payment and shipping options_** to make your shopping experience as convenient as possible.

      ### about the team
      Our team is dedicated to providing exceptional customer service. If you have any questions or concerns, our knowledgeable and friendly           support team is always available to assist you. We also offer a hassle-free return policy, so if you're not completely satisfied with your       purchase, you can easily return it for a refund or exchange.

      ### Physical Stores
      |Location|Area|Hours|
      |--|--|--|
      | New Orleans | Home and DIY  |07.30am-09.30pm  |
      | Seattle | Gardening | 10.00am-08.30pm  |
      | New York | Furniture Specialists  | 10.00am-09.00pm |

      ## Our Store Qualities
      - We're committed to providing high-quality products
      - Our products are offered at affordable prices 
      - We work with reputable suppliers and manufacturers 
      - We ensure that our products meet our strict standards for quality and durability. 
      - Plus, we regularly offer sales and discounts to help you save even more.

      #Summary
      Thank you for choosing our online retail store for your shopping needs. We look forward to serving you!
      ```
     
      ![](images/AZ400_M09_L17_15.png)
      
12.  This sample text gives you an overview of several of the common MarkDown syntax features, ranging from Title and subtitles (##), bold            (**), italic (*), how to create tables, and more.

13.  **Refresh** your browser, or select any other DevOps portal option and return to the **Overview(1)** and **Wiki(2)** section. Notice you are now presented with the **EshopOnWeb (Documents)** Wiki, as well as having the **Welcome to our Online Retail Store(3)** as **HomePage** of the Wiki.
      
     ![](images/AZ400_M09_L17_16.png)
    
     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
     > - Select the **Lab Validation** tab located at the upper right corner of the lab guide section.
     > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
     > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
     > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.


## Task 2: Manage content of a published wiki
In this task, you will manage content of the wiki you published in the previous task.

1. In the vertical menu on the left side, click **Repos (1)**, ensure that the dropdown menu in the upper section of the **Files (2)** pane displays the **EShopOnWeb (3)** repo and **main (4)** branch, in the repo folder hierarchy, select the **Documents (5)** folder, and select the **Welcome-to-our-Online-Retail-Store!.md (6)** file.

    ![](images/AZ400_M09_L17_17.png)

2. Notice how the MarkDown format is visible here as raw text format, allowing you to continue editing the file content from here as well.

   > **Note**: Since the Wiki source files are handled as source code, remember all practices from traditional source control (Clone, Pull Requests, Approvals and more), can now also be applied to Wiki pages.


# Exercise 2: Create and manage a project wiki

In this exercise, you will step through creating and managing a project wiki.

> **Note**: You can create and manage wiki independently of the existing repos. 

## Task 1: Create a project wiki including a Mermaid diagram and an image

In this task, you will create a project wiki and add to it a Mermaid diagram and an image.

1.  On your lab VM, in the Azure DevOps portal displaying the **Overview (1)** and **Wiki (2)** pane of the **EShopOnweb** project, with the content of the **EShopOnWeb (Documents) (3)** wiki selected, at the top of the pane, click the **EShopOnWeb (Documents)** dropdown list header, and, in the drop down list, select **Create new project wiki (4)**. 

     ![](images/AZ400_M09_L17_18.png)

2.  In the Page title text box, type **Project Design**.

     ![](images/AZ400_M09_L17_19.png)

3.  Place the cursor in the body of the page, click the left-most icon in the toolbar representing the header setting and, in the dropdown list, click **Header 1**. This will automatically add the hash character (**#**) at the beginning of the line.

     ![](images/AZ400_M09_L17_20.png)
     ![](images/AZ400_M09_L17_21.png)

4.  Directly after the newly added **#** character, type **Authentication and Authorization** and press the **Enter** key.

     ![](images/AZ400_M09_L17_22.png)

5.  Click the left-most icon in the toolbar representing the header setting and, in the dropdown list, click **Header 2**. This will automatically add the hash character (**##**) at the beginning of the line.

     ![](images/AZ400_M09_L17_23.png)

     ![](images/AZ400_M09_L17_24.png)
6.  Directly after the newly added **##** character, type **Azure DevOps OAuth 2.0 Authorization Flow** and press the **Enter** key.

     ![](images/AZ400_M09_L17_25.png)

7.  **Copy and paste** the following code to insert a mermaid diagram on your wiki.

    ```
    ::: mermaid
     sequenceDiagram
     participant U as User
     participant A as Your app
     participant D as Azure DevOps
     U->>A: Use your app
     A->>D: Request authorization for user
     D-->>U: Request authorization
     U->>D: Grant authorization
     D-->>A: Send authorization code
     A->>D: Get access token
     D-->>A: Send access token
     A->>D: Call REST API with access token
     D-->>A: Respond to REST API
     A-->>U: Relay REST API response
    :::
    ```

    >**Note**: For details regarding the Mermaid syntax, refer to [About Mermaid](https://mermaid-js.github.io/mermaid/#/)

    ![](images/AZ400_M09_L17_26.png)


8.  To the right of the editor pane, in the preview pane, click **Load diagram** and review the outcome. 

     >**Note**: The output should resemble the flowchart that illustrates how to [Authorize access to REST APIs with OAuth 2.0](https://docs.microsoft.com/en-us/azure/devops/integrate/get-started/authentication/oauth?view=azure-devops)

     ![](images/AZ400_M09_L17_27.png)

     ![](images/AZ400_M09_L17_28.png)

9.  In the upper right corner of the editor pane, click the down-facing caret next to the **Save** button and, in the dropdown menu, click **Save with revision message**. 

     ![](images/AZ400_M09_L17_29.png)

10.  In the **Save page** dialog box, type **Authentication and authorization section with the OAuth 2.0 Mermaid diagram** and click **Save**.
     
      ![](images/AZ400_M09_L17_30.png)

11.  On the **Project Design** editor pane, place the cursor at the end of the Mermaid element you added earlier in this task, press the **Enter** key to add an extra line, click the left-most icon in the **toolbar (1)** representing the header setting and, in the dropdown list, click **Header 2 (2)**. This will automatically add the double hash character (**##(3)**) at the beginning of the line.
   
      ![](images/AZ400_M09_L17_31.png)

12.  Directly after the newly added **##** character, type **User Interface** and press the **Enter** key.
    
      ![](images/AZ400_M09_L17_32.png)

13.  Download any image from Google by searching **brand.png (1)** and select the **image** to download.
    
      ![](images/AZ400_M09_L17_33.png)
 
14.  Right click on the image, select **save image as** and save it to the **Desktop (1)** and type File name as **Brand.png (2)** and **Save (3)** it in your lab VM.
    
      ![](images/AZ400_M09_L17_34.png)

15.  On the **Project Design (1)** editor pane, in the toolbar, click the **paper clip icon (2)** representing the **Insert a file** action, in the **Open** dialog box, navigate to the **Desktop (3)** folder, select the **Brand.png (4)** file you downloaded in the previous exercise, and click **Open (5)**.
     
      ![](images/AZ400_M09_L17_35.png)
      ![](images/AZ400_M09_L17_36.png)

16.  Back on the **Project Design** editor pane, review the preview pane and verify that the image is properly displayed.
17.  In the upper right corner of the editor pane, click the down-facing caret next to the **Save** button and, in the dropdown menu, click **Save with revision message**. 
    
      ![](images/AZ400_M09_L17_37.png)

18.  In the **Save page** dialog box, type **User Interface section with the Brand image** and click **Save**.
    
19.  Back on the editor pane, in the upper right corner, click **Close**. 
     
      ![](images/AZ400_M09_L17_39.png)

  **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:

  > - Navigate to the Lab Validation tab, from the upper right corner in the lab guide section.
  > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

## Task 2: Manage a project wiki

In this task, you will manage the newly created project wiki.

>**Note**: You will start by reverting the most recent change to the wiki page.

1.  On you lab VM, in the Azure DevOps portal displaying the **Wiki pane** of the **EShopOnWeb** project, with the content of the **Project Design(1)** wiki selected, in the upper right corner, click the vertical **ellipsis symbol (2)** and, in the dropdown menu, click **View revisions (3)**.

     ![](images/AZ400_M09_L17_40.png)

2.  On the **Revisions** pane, click the entry representing the most recent change. 

     ![](images/AZ400_M09_L17_41.png)
     
3.  On the resulting pane, review the comparison between the previous and the current version of the document, click **Revert**, when prompted for the confirmation, click **Revert** again, and then click **Browse Page**.
    
     ![](images/AZ400_M09_L17_42.png)

     ![](images/AZ400_M09_L17_43.png)

     ![](images/AZ400_M09_L17_44.png)

4.  Back on the **Project Design** pane, verify that the change was successfully reverted.

     >**Note**: Now you will add another page to the project wiki and set it as the wiki home page.

     ![](images/AZ400_M09_L17_45.png)


5.  On the **Project Design** pane, at the bottom left corner, click **+ New page**.

     ![](images/AZ400_M09_L17_46.png)

6.  On the page editor pane, in the **Page title** text box, type **Project Design Overview**, click **Save**, and then click **Close**.

    ![](images/AZ400_M09_L17_47.png)

7.  Back in the pane listing the pages within the **Project Design** project wiki, locate the **Project Design Overview** entry, select it with the mouse pointer, drag and drop it above the **Project Design** page entry. 

     ![](images/AZ400_M09_L17_48.png)
    
     ![](images/AZ400_M09_L17_49.png)

8.  Verify that the **Project Design Overview** entry is listed as the top level page with the home icon designating it as the wiki home page.

    ![](images/AZ400_M09_L17_40.png)

## Review

In this lab, you created and configured Wiki in an Azure DevOps, including managing markdown content and creating a Mermaid diagram.

### You have successfully completed the lab.
