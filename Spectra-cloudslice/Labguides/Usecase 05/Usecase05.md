## Use case 5 - Extracting Customer Insights from Conversations using Foundry IQ and AI agents

**Introduction**

This usecase focuses on building an end-to-end AI-powered solution to
extract meaningful customer insights from unstructured conversations and
documents using Azure AI services and intelligent agents. Participants
will deploy a complete cloud-based application using Azure Developer
CLI, provision services such as Azure OpenAI, Cognitive Services, and
Kubernetes, and integrate them into a scalable architecture.

The solution demonstrates how organizations can analyze housing reports,
contracts, and conversational data to uncover trends, compare insights,
and support data-driven decision-making. It also introduces the use of
Foundry AI agents for advanced document analysis, summarization, and
contextual querying.

**Scenario**

In this usecase, you step into the role of a data analyst or AI engineer
working for an organization dealing with large volumes of **customer
conversations, housing reports, and contract documents**. The
organization faces a common challenge: valuable insights are buried
inside unstructured data such as PDFs, reports, and handwritten
contracts, making manual analysis slow, error-prone, and inefficient.

To solve this, the organization adopts an **AI-driven solution using
Azure Foundry and AI agents**. Your task is to design, deploy, and test
this intelligent system that can automatically process documents,
understand context, and generate meaningful insights.

**Objectives**

- Understand and configure Azure resources including resource groups,
  subscriptions, and service providers.

- Deploy an AI-driven application using Azure Developer CLI (azd) and
  GitHub Codespaces.

- Provision and integrate services such as Azure OpenAI, Azure Cognitive
  Services, AKS, and Cosmos DB.

- Upload and process large volumes of documents for analysis (e.g.,
  housing reports, contracts).

- Use AI agents to:

  - Extract insights from documents

  - Compare reports and identify trends

  - Analyze structured and unstructured data

- Perform intelligent queries to generate summaries, tables, and
  comparative analysis.

- Validate deployment and test real-world use cases such as housing
  affordability analysis and contract evaluation.

- Clean up resources after completion to optimize cost and resource
  usage.

## Task 0: Understand the VM and the credentials

In this task, we will identify and understand the credentials that we
will be using throughout the lab.

1.  **Instructions** tab hold the lab guide with the instructions to be
    followed throughout the lab.

2.  **Resources** tab has got the credentials that will be needed for
    executing the lab.

    - **URL** – URL to the Azure portal

    - **Subscription** – This is the ID of the subscription assigned to
      you

    - **Username** – The user id with which you need to login to the
      Azure services.

    - **Password** – Password to the Azure login. Let us call this
      Username and password as Azure login credentials. We will use
      these creds wherever we mention Azure login credentials.

    - **Resource Group** – The **Resource group** assigned to you.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)

3.  **Help** tab holds the Support information. The **ID** value here is
    the **Lab instance ID** which will be used during the lab execution.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)

\[!Alert\] **Important:** Make sure you create all your resources under
this Resource group

## Task 1: Register Service provider

1.  Open a browser go to +++https://portal.azure.com+++ and sign in with
    your cloud slice account below.

Username: <+++@lab.CloudPortalCredential>(User1).Username+++

Password: <+++@lab.CloudPortalCredential>(User1). *TAP*+++

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

![A login box with a red box and blue box with text AI-generated content
may be incorrect.](./media/image4.png)

2.  Click on **Subscriptions** tile.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

3.  Click on the subscription name.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter **+++** **Microsoft.CognitiveServices+++** and
    select i,t, and then click **Register**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image9.png)

5.  Repeat the steps \#4 to register the following Resource provider.

- +++**Microsoft.AlertsManagement**+++

## Task 2: Retrieve resource group name and location

1.  Type in +++**Resource group+++** in the search bar and
    select **Resource groups**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image10.png)

2.  Click on your assigned **Resource group**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image11.png)

3.  In **Resource group** page, copy **resource group name and
    location** and paste them in a notepad, then **Save** the notepad to
    use the information in the upcoming tasks.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image12.png)

## Task 3: Open Github Codespaces environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL: 

> +++https://github.com/technofocus-pte/KnowledgeSolutionAccelerator.git+++

2.  Click on **fork** to fork the repo. Give unique name to the repo and
    click on **Create repo** button.

![](./media/image13.png)

3.  Click on **Create fork**

4.  Click on **Code -\> Codespaces -\> Codespaces+**

![](./media/image14.png)

![](./media/image15.png)

4.  Wait for the Codespaces environment to setup .It takes few minutes
    to setup completely

![](./media/image16.png)

5.  Run the following command to install the Azure Developer CLI
    (**azd**) on your codespace.

+++curl -fsSL https://aka.ms/install-azd.sh | bash+++

![](./media/image17.png)

## Task 4: Provision Services and deploy application to Azure

1.  Run the following command on the Terminal. It generates the code to
    copy. Copy the code and press Enter.

+++azd auth login+++

![](./media/image18.png)

2.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

![](./media/image19.png)

3.  Sign in with your Azure credentials.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image21.png)

![](./media/image22.png)

4.  To create an environment for Azure resources, run the following
    Azure Developer CLI command.It asks you to enter environment name
    .Enter any name of your choice and press enter (eg :+++agentXXXX+++)

**Note:** When creating an environment, ensure that the name consists of
lowercase letters.

+++azd env new+++

![](./media/image23.png)

5.  Run below command to provision the services to Azure, build your
    container.

+++azd env set AZURE_RESOURCE_GROUP {Name of existing resource group}+++

![](./media/image24.png)

6.  Run azd up - This will provision Azure resources

+++azd up+++

![](./media/image25.png)

7.  Select below values.

- **Select an Azure Subscription to use** : Select your subscription

- **azureAiServiceLocation**: Central US

![](./media/image26.png)

![](./media/image27.png)

6.  This deployment will take *20-25 minutes* to provision the resources
    in your account and set up the solution with sample data.

![](./media/image28.png)

![](./media/image29.png)

7.  Now the deployment is complete

![](./media/image30.png)

8.  Run the following command to install PowerShell in Codespaces

sudo apt-get update

sudo apt-get install -y powershell

![](./media/image31.png)

![](./media/image32.png)

9.  Run the following command to install PowerShell in Codespaces to
    enable execution of PowerShell scripts within your development
    environment.

+++ curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash+++

![](./media/image33.png)

4.  Run the following command to log in to your Azure account and
    authenticate your session.

![](./media/image34.png)

![](./media/image35.png)

10. Enter your email address for certificate management, then open the
    provided URL and enter the displayed code to complete Azure login
    authentication.

![](./media/image36.png)

![](./media/image37.png)

11. Select your subscription

![](./media/image38.png)

12. After successfully logging in to Azure, review the deployed resource
    details and proceed with configuring the Kubernetes infrastructure.

![](./media/image39.png)

13. AKS cluster updated successfully

![](./media/image40.png)

14. Verify that the application routing add-on is enabled, note the
    external IP address assigned to NGINX, and proceed with assigning a
    DNS name to the public IP.

![](./media/image41.png)

15. Assign the required role to the AKS system-assigned managed
    identity, then monitor the node pool upgrade process until it
    completes successfully.

![](./media/image42.png)

16. Update the Kubernetes YAML files with the container image path and
    email address, then configure AKS by deploying Cert Manager and
    application images to the cluster.

![](./media/image43.png)

![](./media/image44.png)

![](./media/image45.png)

![](./media/image46.png)

17. Once the deployment is successful, review the provided details,
    access the frontend application using the given URL, and proceed
    with the data import process using the specified command.

![](./media/image47.png)

18. Click on **Open** button

![](./media/image48.png)

![](./media/image49.png)

## Task 5: Verify deployed resources in the Azure portal

1.  Select **Resource groups**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image50.png)

2.  Click on your assigned **Resource group**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image51.png)

3.  Make sure the below resource got deployed successfully

- Kubernetes service

- Container App

- Container registry

- Container App Environment

- Azure Cosmos DB account

- Search service

- Azure Storage account

- Azure OpenAI

![](./media/image52.png)

6.  Click on **Azure OpenAI.**

![](./media/image53.png)

7.  Click **Go to Foundry portal** to verify that the model has been
    successfully deployed.

![](./media/image54.png)

![](./media/image55.png)

## Task 6: Test the Application – Housing Affordability & Report Analysis

1.  Return to the application to continue testing the Housing
    Affordability and Report Analysis features.

> ![](./media/image49.png)

2.  Click on **Upload documents**

![](./media/image56.png)

3.  Click on **Browse files**

![](./media/image57.png)

4.  Browse to **C:\LabFiles\LabFiles\Data** on your VM, then select 
    ** all files** and click on **Open** button.

![](./media/image58.png)

5.  Uploading the documents may take approximately 10–13 minutes to
    complete.

![](./media/image59.png)

![](./media/image60.png)

![](./media/image61.png)

6.  Enter +++ **What are the main factors contributing to the current
    housing affordability issues?**+++ and select **Send**.

![](./media/image62.png)

![](./media/image63.png)

![](./media/image64.png)

## Task 7: Housing Report Search & Comparison

1.  Search for: **"Housing Report"** to filter the document list

2.  Select **Annual Housing Report 2022** and **Annual Housing Report
    2023**

    - Confirm the top panel shows **"2 Selected"**

![](./media/image65.png)

3.  Enter +++ **Analyze the two annual reports and compare the positive
    and negative outcomes YoY. Show the results in a table.**+++ and
    select **Send**.

> ![](./media/image66.png)
>
> ![](./media/image67.png)

4.  Click **DETAILS** on **Annual Housing Report 2023**

![](./media/image68.png)

![](./media/image69.png)

3.  Scroll to **pages 10 & 11**

![](./media/image70.png)

4.  Click on **Chat** tab in the pop-up viewer

![](./media/image71.png)

5.  Enter +++ **Can you summarize and compare the tables on page 10 and
    11?**+++ and select **Send**.

![](./media/image72.png)

5.  Review the summarized comparison

![](./media/image73.png)

6.  Close the pop-up viewer

## Task 8: Contracts Search & Analysis

1.  Search for: **"Contracts"** to filter the document list

2.  Select **6 handwritten contract documents**

![](./media/image74.png)

3.  Enter +++ **Analyze these forms and create a table with all buyers,
    sellers, and corresponding purchase prices.**+++ and
    select **Send**.

![](./media/image75.png)

4.  Review the table for correct buyer/seller names and purchase prices

![](./media/image76.png)

5.  Click **DETAILS** on one of the handwritten contracts

![](./media/image77.png)

![](./media/image78.png)

6.  Click on **Chat** tab in the pop-up viewer

![](./media/image79.png)

7.  Enter +++**What liabilities is the buyer responsible for within the
    contract**+++ and select **Send**.

![](./media/image80.png)

8.  Review the response for specific obligations (e.g., fees, taxes,
    maintenance, contingencies)

![](./media/image81.png)

## Task 9: Delete the resources

1.  From the Azure portal home page, select the assigned Resource group.
    Select all the resources under the Resource group and select Delete.

![](./media/image82.png)

![](./media/image83.png)

2.  Enter +++**delete**+++ and click on the **Delete** button to confirm
    deletion. Click on **Delete** in the Delete confirmation dialog box.

![](./media/image84.png)

3.  Confirm the deletion of all the resources with a success message.

## Summary

In this lab, you successfully deployed a full-stack AI solution that
leverages Azure services and AI agents to analyze and extract insights
from customer-related data. You learned how to provision infrastructure,
deploy applications, and integrate multiple Azure services into a
cohesive system.

Through hands-on tasks, you explored how AI can process complex
documents such as housing reports and contracts, generate summaries,
perform comparisons, and extract key information like buyer/seller
details and financial insights. This demonstrates the practical value of
AI in transforming unstructured data into actionable intelligence.

Overall, the lab highlights how organizations can use AI-powered agents
and cloud-native tools to enhance decision-making, automate analysis,
and gain deeper insights from customer conversations and documents at
scale
