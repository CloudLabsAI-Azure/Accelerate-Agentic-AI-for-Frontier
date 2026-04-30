# Use case 6 - Build an intelligent banking assistant with MCP tools and Microsoft Agent Framework

**Introduction**

In modern banking, customers expect quick, intuitive, and personalized
services without navigating complex applications. Traditional banking
interfaces often require multiple steps to perform simple tasks like
checking balances, viewing transactions, or making payments.

This use case demonstrates how an **AI-powered Banking Assistant Agent**
simplifies these interactions through a conversational interface. Users
can communicate in natural language, and the system intelligently
interprets their requests and routes them to specialized agents.

The solution is built using a **multi-agent architecture**, where each
agent handles a specific banking function such as account management,
transaction retrieval, and payment processing. An orchestrator
coordinates these agents to deliver accurate, real-time responses,
creating a seamless and efficient digital banking experience.

**Objectives**

By implementing this use case, you will:

- Understand how to design a **multi-agent AI system** for real-world
  applications

- Enable **natural language interaction** for banking operations

- Implement **intelligent request routing** between specialized agents

- Integrate AI agents with **backend banking APIs and services**

- Automate common banking tasks such as:

  - Checking account balances

  - Viewing transaction history

  - Processing payments

- Enhance the system with advanced capabilities like **invoice-based
  payment processing**

- Deliver a **scalable and user-friendly conversational banking
  experience**

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

      ![](./media/image1.png)

3.  **Help** tab holds the Support information. The **ID** value here is
    the **Lab instance ID** which will be used during the lab execution.

     ![](./media/image2.png)

\[!Alert\] **Important:** Make sure you create all your resources under
this Resource group

## Task 1: Register Service provider

1.  Open a browser and login to Azure portal at <https://portal.azure.com/> with your credentials.

    - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

      ![Enter Your Username](./media/gs1.png)

    - **Password:** <inject key="AzureAdUserPassword"></inject>

      ![Enter Your Password](./media/gs2.png)

2.  Click on **Subscriptions** tile.

     ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

3.  Click on the subscription name.

     ![A screenshot of a computer AI-generated content may be
incorrect.](./media/135.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter  **Microsoft.CognitiveServices** and
    select it, and then click **Register**.

     ![](./media/143.png)

     ![](./media/image8.png)

     ![](./media/image9.png)

5.  Repeat the steps \#4 to register the following Resource provider.

    - **Microsoft.AlertsManagement**

## Task 2: Open Github Codespaces environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL: 

    https://github.com/technofocus-pte/Banking-assistant-Agent+

     ![](./media/image13.png)

2.  Click on **fork** to fork the repo. Give unique name to the repo and
    click on **Create repo** button.

    > **Note:** For this task, you are required to use your personal GitHub account.

     ![](./media/image14.png)

     ![](./media/image15.png)

3.  Click on **Code -\> Codespaces -\> Codespaces+**

      ![](./media/image16.png)

4.  Wait for the Codespaces environment to setup .It takes few minutes
    to setup completely

     ![](./media/image17.png)

     ![](./media/image18.png)

## Task 3: Provision Services and deploy application to Azure

1.  Run the following command on the Terminal. It generates the code to
    copy. Copy the code and press Enter.

    ```
    azd auth login
    ```

     ![](./media/image19.png)

     ![](./media/image20.png)

2.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

     ![](./media/image21.png)

3.  Sign in with your Azure credentials.

     ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

     ![A screenshot of a computer error AI-generated content may be
incorrect.](./media/image23.png)

     ![](./media/image24.png)

4.  To create an environment for Azure resources, run the following
    Azure Developer CLI command.It asks you to enter environment name.
    Enter any name of your choice and press enter (eg
    :Bankagent1234)

    ```
    azd env new
    ```

     ![](./media/image25.png)

6.  Run azd up - This will provision Azure resources

    ```
    azd up
    ```

    ![](./media/image27.png)

5.  Select below values.

     - **Select an Azure Subscription to use** : Select your subscription

        ![](./media/image28.png)

     - **azureAiServiceLocation**: France Central or Sweden Central

     - **‘location' infrastructure parameter:** Central US

1. After selecting subscription and location please **Create a New resource group**.

    - Resource Group Name : **newagent-rg**

    - Location : **Central US**
6.  This deployment will take *7-10 minutes* to provision the resources
    in your account and set up the solution with sample data.

     ![](./media/image30.png)

     ![](./media/image31.png)

     ![](./media/image32.png)

     ![](./media/image33.png)

     ![](./media/image34.png)

7.  The service account endpoint has been completed successfully.

     ![](./media/image35.png)

     ![](./media/image36.png)

8.  The service backend has been completed successfully.

     ![](./media/image37.png)

9.  The service payment has been completed successfully.

     ![](./media/image38.png)

10. The service transaction has been completed successfully.

     ![](./media/image39.png)

11. The service web has been completed successfully.

     ![](./media/image40.png)

## Task 4: Verify deployed resources in the Azure portal

1.  Select **Resource groups**

     ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

2.  Click on your assigned Resource group **newagent-rg**.

3.  Make sure all the resources got deployed successfully

     ![](./media/image43.png)

     ![](./media/image44.png)

3.  Make sure the below resource got deployed successfully

     - Foundry

     - Foundry project

     - Account Container App

     - Backend Container App

     - Payment Container App

     - Transaction Container App

     - Web Container App

     - Document Intelligence

     - Container App Environment

     - Azure Cosmos DB account

     - Search service

     - Azure Storage account

       ![](./media/image45.png)

4.  Select **Foundry project**

     ![](./media/image46.png)

6.  Click **Go to Foundry portal** to verify that the model has been
    successfully deployed.

     ![](./media/image47.png)

5.  In Microsoft Foundry, navigate to the **Build** section from the top
    menu to start creating and managing your AI solutions.

     ![](./media/image48.png)

## Task 5: Test the Application

1.  Click on the generated **service web endpoint URL** to open and
    access the deployed application in your browser.

     ![](./media/image49.png)

2.  Click on **Open** button

     ![](./media/image50.png)

3.  Click on **Start banking**

     ![](./media/image51.png)

     ![](./media/image52.png)

4.  On the Banking Assistant home page, select **Transaction Analysis**
    to view and analyze transaction details.

     ![](./media/image53.png)

5.  Select **Start Chat** to initiate a conversation with the Banking
    Assistant.

     ![](./media/image54.png)

6.  Click **Review Card Spend** to analyze and review card transaction
    spending details.

     ![](./media/image55.png)

     ![](./media/image56.png)

     ![](./media/image57.png)

     ![](./media/image58.png)

## Task 6: Delete the resources

1.  From the Azure portal home page, select the assigned Resouce group **newagent-rg**
    Select all the resources under the Resource group and select Delete.

     ![A screenshot of a computer Description automatically
generated](./media/144.png)

2.  Enter **delete** and click on the **Delete** button to confirm
    deletion. Click on **Delete** in the Delete confirmation dialog box.

     ![A screenshot of a computer Description automatically
generated](./media/image60.png)

3.  Confirm the deletion of all the resources with a success message.

     ![A screenshot of a computer screen Description automatically
generated](./media/image61.png)

**Summary**

This use case showcases how an AI-driven, multi-agent system can
modernize traditional banking by transforming it into a **conversational
and intelligent service platform**.

By leveraging specialized agents and orchestration, the solution
efficiently handles diverse banking tasks while maintaining accuracy and
responsiveness. It reduces user effort, improves accessibility, and
enables faster interactions compared to traditional systems.

Overall, the Banking Assistant Agent demonstrates the power of
**Generative AI and multi-agent collaboration** in building scalable,
efficient, and customer-centric financial solutions.
