# Usecase 01 - Create a Knowledge Assistant agent for HR in Copilot Studio  that leverages Azure AI Search

## Overview

A large enterprise wants to reduce the time employees spend searching
for HR-related information (policies, benefits, leave guidelines, etc.)
spread across SharePoint, PDFs, internal wikis, and documents.

To overcome this issue, in this lab, you will build a **Knowledge
assistant** **agent** in **Copilot Studio** that uses **Azure AI
Search**, to index and semantically search across enterprise HR
documents.

## Lab Objective

- Exercise 1: Create an Azure AI Search resource
- Exercise 2: Create a Storage account
- Exercise 3: Create an Azure OpenAI Service and deploy a model
- Exercise 4: Create a vector index
- Exercise 5: Create a knowledge assistant agent
- Exercise 6: Add the Azure AI Search as a knowledge source

## Exercise 1: Create an Azure AI Search resource

In this exercise, you will create an Azure AI Search resource from the
Azure portal. This will be used to search the documents using AI
capability.

**Azure AI Search** is a cloud-based service for searching within your
privately curated data. It uses a combination of Microsoft’s AI and
JSON-based indexes to provide fast, relevant search results.

1. In the Azure portal, go to the **top search bar**, enter **Microsoft Foundry (1)**, and from the results, choose **Microsoft Foundry (2)** under the **Services**.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-0.png)

1. In the **Microsoft Foundry** page, expand **Use with Foundry (1)**, select **AI Search (2)**, and then click **+ Create (3)** to begin creating a new AI Search resource.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-1.png)

1. On the **Create a search service** page under the **Basics** tab, provide the following details:

     - Select the **Resource group** as **AgenticAI (1)** from the dropdown.
     - Enter **Service name**  as **searchleaves-<inject key="DeploymentID" enableCopy="false"/> (2)**.
     - Choose the appropriate **Location (3)** based on your region or lab requirement.
     - Verify that the **Pricing tier (4)** is set to **Standard** (default selection).
     - Click on **Review + create (5)** to validate the configuration and proceed with deployment.

       ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-2.png) 

1. On the **Review + create** tab, verify all the configured settings and then click **Create** to deploy the AI Search service.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-3.png) 

1. Once the deployment is complete, click on **Go to resource** to navigate to the newly created AI Search service.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-4.png) 

1. On the AI Search service **Overview** page, locate the **URL** under the **Essentials** section and click the **copy icon** next to it to copy the service endpoint for later use.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-5.png) 

1. In the AI Search service, navigate to **Settings**, select **Keys**, and under **Manage admin keys**, click the **copy icon** next to the **Primary admin key** to copy it for later use.

   ![image](./media/uc1-6.png)

1. In the AI Search service, go to **Identity**, switch the **Status** to **On** to enable the system-assigned managed identity, and then click **Save** to apply the changes.

   ![image](./media/uc1-7.png)

1. In the confirmation dialog to enable the system-assigned managed identity, click **Yes** to proceed and register the identity with Microsoft Entra ID.

   ![image](./media/uc1-8.png)

## Exercise 2: Create a Storage account

1. In the Azure portal, go to the **top search bar**, enter **Storage accounts (1)**, and from the results, choose **Storage accounts (2)** under the **Services**.

   ![image](./media/uc1-9.png)

1. On the **Storage accounts** page, click **+ Create** to begin creating a new storage account.

   ![image](./media/uc1-10.png)

1. On the **Create a storage account** page under the **Basics** tab, configure the required settings as follows:

    - Select **Resource group**: **AgenticAI**
    - Enter **Storage account name** as **leavepolicystg<inject key="DeploymentID" enableCopy="false"/>**
    - Choose **Region**
    - Set **Preferred storage type**: **Azure Blob Storage or ADLS Gen2**
    - Keep **Performance**: **Standard**
    - Set **Redundancy**: **LRS**
    - Click **Review + create**

      ![image](./media/uc1-11.png)

1. On the **Review + create** tab, verify all the configured storage account settings and click **Create** to deploy the storage account.

   ![image](./media/uc1-12.png)

1. Once the deployment is complete, click **Go to resource** to open the newly created storage account.

   ![image](./media/uc1-13.png)

1. In the storage account, navigate to **Data storage**, select **Containers**, and then click **+ Add container** to create a new container.

   ![image](./media/uc1-14.png)

1. In the **New container** pane, enter **document** as the **Name**, keep the access level as **Private**, and click **Create** to create the container.

   ![image](./media/uc1-15.png)

1. After the container is created, locate and select the **document** container from the list to open it.

   ![image](./media/uc1-16.png)

1. In the **document** container, click **Upload**, then in the upload pane select **Browse for files**, choose the file you want to upload, and proceed with the upload.

   ![image](./media/uc1-17.png)

1. Select the **LeavePolicy.docx** from **C:\Labfiles\LabFiles** and then click on **Upload**.

1. In the storage account, navigate to **Access Control (IAM)**, click **+ Add**, and select **Add role assignment** to begin assigning permissions.

   ![image](./media/uc1-18.png)

1. In the **Add role assignment** pane, search for **Storage Blob Data Reader**, select the role from the list, and click **Next** to proceed.

   ![image](./media/uc1-19.png)

1. In the **Members** tab, keep **Assign access to** as **User, group, or service principal**, click **Select members**, search and choose the ODL user **<inject key="AzureAdUserEmail"></inject>**, click **Select**, and then proceed by clicking **Next**.

   ![image](./media/uc1-20.png)

1. In the **Members** tab, select **Managed identity**, click **Select members**, choose **Search service** from the managed identity dropdown, select your AI Search service instance, and proceed to assign it.

   ![image](./media/uc1-22.png)

1. In the **Select managed identities** pane, choose the **Search service** managed identity, select your AI Search service instance, and click **Select** to add it.

   ![image](./media/uc1-23.png)

1. In the **Add role assignment** pane, verify that both the required user and the **Search service managed identity** are listed under **Members**, then click **Review + assign** twice to complete the role assignment.

   ![image](./media/uc1-24.png)

In this exercise, we have created a Storage account and added the
document and required Role permissions to it.

## Exercise 3: Create an Azure OpenAI Service and deploy a model

1. In the Azure portal search bar, type **Azure OpenAI** (1), then select **Azure OpenAI** from the **Services** list (2) to open it.

   ![image](./media/uc1-25.png)

1. In the **Azure OpenAI** page, click **+ Create** (1) and then select **Azure OpenAI** (2) from the dropdown to begin creating a new resource.

   ![image](./media/uc1-26.png)

1. In the **Create Azure OpenAI** page, select **Resource group** as **AgenticAI** (1), choose the **Region** (2), enter **Name** as **openaiservice-<inject key="DeploymentID" enableCopy="false"/>** (3), keep the **Pricing tier** as **Standard S0** (4), and click **Next** (5) to proceed.

   ![image](./media/uc1-27.png)

1. On the **Review + submit** tab, verify all the configured details and click **Create** to deploy the Azure OpenAI resource.

   ![image](./media/uc1-28.png)

1. Once the deployment is complete, click **Go to resource** to open the Azure OpenAI resource.

   ![image](./media/uc1-29.png)

1. In the Azure OpenAI resource, navigate to **Access control (IAM)** (1), click **+ Add** (2), and select **Add role assignment** (3) to assign permissions.

   ![image](./media/uc1-30.png)

1. In the **Add role assignment** pane, search for **Cognitive Services OpenAI User** (1), select the role from the list (2), and click **Next** (3) to continue.

   ![image](./media/uc1-31.png)

1. In the **Members** tab, keep **Assign access to** as **User, group, or service principal** (1), click **Select members** (2), search and choose the ODL user **<inject key="AzureAdUserEmail"></inject>**, then click **Select** (5) and proceed.

   ![image](./media/uc1-32.png)

1. In the **Members** tab, select **Managed identity** (1), click **Select members** (2), choose **Search service** from the managed identity dropdown (3), select your AI Search service instance (4), and proceed.

   ![image](./media/uc1-33.png)

1. In the **Select managed identities** pane, confirm the selected **Search service** managed identity and click **Select** to add it.

   ![image](./media/uc1-34.png)

1. In the **Add role assignment** pane, verify that both the required user and the **Search service managed identity** are listed under **Members** (1), then click **Review + assign** (2) twice to complete the role assignment.

   ![image](./media/uc1-35.png)

1. On the Azure OpenAI resource page, click **Go to Foundry portal** to open the service in Microsoft Foundry.

   ![image](./media/uc1-36.png)

1. In the **Microsoft Foundry** portal, navigate to **Deployments** (1), click **+ Deploy model** (2), and select **Deploy base model** (3) to start deploying a model.

   ![image](./media/uc1-37.png)

1. In the **Select a model** pane, search for **text-embedding-3-large** (1), select the model from the list (2), and click **Confirm** (3) to proceed.

   ![image](./media/uc1-38.png)

1. In the **Deploy text-embedding-3-large** pane, keep the **Deployment type** as **Standard** (1) and click **Deploy** (2) to create the model deployment.

   ![image](./media/uc1-39.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="84aae3c9-71f4-401e-a136-f446d2da1749" />

## Exercise 4: Create a vector index

1. Back in the Azure portal, open the **searchleaves-<inject key="DeploymentID" enableCopy="false"/>** AI Search service resource.

1. On the AI Search service page, click **Import data** to start importing data into the search index.

   ![image](./media/uc1-40.png)

1. In the **Import data** pane, select **Azure Blob Storage** as the data source to proceed with importing data.

   ![image](./media/uc1-41.png)

1. In the **Import data** workflow, select **RAG** as the scenario to enable AI-powered search over your data.

   ![image](./media/uc1-42.png)

1. In the **Configure your Azure Blob Storage** step, select the **Storage account** **leavepolicystg<inject key="DeploymentID" enableCopy="false"/>** (1), choose the **Blob container** as **document** (2), and click **Next** (3) to proceed.

   ![image](./media/uc1-43.png)

1. In the **Vectorize your text** step, configure the following:

    - Set **Kind** to **Azure OpenAI** (1)
    - Select your **Subscription** (2)
    - Choose the **Azure OpenAI service** **openaiservice-<inject key="DeploymentID" enableCopy="false"/>** (3)
    - Set **Model deployment** to **text-embedding-3-large** (4)
    - Select **System assigned identity** for authentication (5)
    - Click **Next** (6) to proceed

      ![image](./media/uc1-44.png)

1. In the **Vectorize and enrich your images** step, leave the default options unchanged (no selection) and click **Next** to proceed.

   ![image](./media/uc1-45.png)

1. In the **Vectorize and enrich your images** step, leave the default options unchanged (no selection) and click **Next** to proceed.

   ![image](./media/uc1-46.png)

1. In the **Review and create** step, verify the configuration details and click **Create** to complete the RAG setup.

   ![image](./media/uc1-47.png)

1. Once the setup is complete, click **Close** to view and test your indexed data.

   ![image](./media/uc1-48.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="77d3c91e-95a7-41d5-a2dc-5ee605b4ef21" />

## Exercise 5: Create a knowledge assistant agent

1. In a new tab, enter the following URL to open **Microsoft Copilot Studio** using your login credentials.

    ```
    https://copilotstudio.microsoft.com
    ```

1. Select **Get Started** in the Welcome to Microsoft Copilot Studio.

   ![image](./media/image58.png)

1. Enter the following agent description prompt in the prompt box to define your agent’s purpose and click Send.

   ```
   You are a Knowledge assistant agent for HR who will answer questions related to leaves and leave policies to the employees.
   ```

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/cs2.png)

1. Once the agent is created, in the Test pane, enter **How many days
    of Maternity leaves can I avail?** and click **Send.**

1. Click on **Test** from the top-right corner, then enter following prompt to validate your agent’s response.

   ```
   How many days of Maternity leaves can I avail?
   ```

   ![image](./media/cs4.png)

1. It gives a generalized response as shown in the screenshot below.

   ![image](./media/cs5.png)

## Exercise 6: Add the Azure AI Search as a knowledge source

1. From the **Overview** page of the agent, select **Add knowledge**.

   ![A screenshot of a computer AI-generated content may be incorrect.](./media/cs1.png)

1. Select Azure AI Search from the list of knowledge sources available.

   ![A screenshot of a computer AI-generated content may be incorrect.](./media/image64.png)

1. Click on the **drop down** next to **Not connected** in the next screen and select **Create new connection**.

   ![A screenshot of a search engine AI-generated content may be incorrect.](./media/image65.png)

1. Enter the **Endpoint url** and the **Admin key** values which we saved to a notepad in a previous exercise and then click on **Create** to create the connection.

   ![A screenshot of a computer AI-generated content may be incorrect.](./media/image66.png)

1. Once the connection is established, the available index is listed and already selected. Click on **Add to agent**.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/image67.png)

1. The AI Search service is added as a knowledge source to the agent and is in **Ready** state now. Ensure that the **Web search** option is **disabled** in the Knowledge section.

   ![A screenshot of a computer AI-generated content may be incorrect.](./media/cs3.png)

1. Now, let us test the agent with the same question we tried before.

1. Click **New test session**, enter your query, and review the generated response to verify the agent’s accuracy.

   ```
   How many days of Maternity leaves can I avail?
   ```

1. You can see that the response from the agent now is from the document uploaded in the AI Search service.

   ![A screenshot of a computer AI-generated content may be
incorrect.](./media/uc1-51.png)

## Summary

In this lab, we have learnt to connect the agent to a Azure AI Search
service as a knowledge source and test the agent based on the source.

