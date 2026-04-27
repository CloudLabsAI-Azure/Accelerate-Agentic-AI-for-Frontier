# Use case 7 - Centralized AI agent governance and observability using Foundry Control Plane

**Introduction**

In modern AI-driven applications, managing multiple AI agents, ensuring
their reliability, and maintaining visibility into their behavior is
essential. This scenario focuses on implementing centralized governance
and observability using Microsoft Foundry Control Plane. The lab walks
through the complete lifecycle of AI agents—from creation and
configuration to monitoring, evaluation, and security testing. By
leveraging built-in capabilities such as tracing, Application Insights
integration, evaluation frameworks, and red teaming, this use case
demonstrates how organizations can build AI systems that are
transparent, secure, and production-ready. The Contoso Travel scenario
serves as a practical example to illustrate how intelligent agents can
be governed and observed effectively within a unified platform.

**Objectives**

- Set up a project environment in Microsoft Foundry.

- Create and configure an AI travel assistant agent.

- Enable monitoring using Azure Application Insights.

- Test and refine agent responses using prompt engineering.

- Apply evaluation frameworks to assess quality and safety.

- Perform red teaming to identify risks and vulnerabilities.

- Set up a development environment using GitHub Codespaces.

- Develop agents programmatically using SDKs.

- Enhance agents with tools and data integration.

- Build and orchestrate multi-agent workflows.

- Enable tracing for observability and debugging.

- Evaluate agent performance using structured metrics.

- Conduct advanced red teaming for robustness.

- Clean up resources after completing the lab.

## Exercise 1: Foundry Project Environment Setup and Configuration

In this exercise, you will establish the foundational setup required to
begin working with AI agents in Microsoft Foundry. The focus is on
creating a project environment, configuring essential resources, and
understanding the basic workflow of agent development. You will create a
Foundry project, define an AI agent, and enable monitoring using Azure
Application Insights. Additionally, you will explore how to test agent
prompts, analyze responses, and review evaluation metrics. This exercise
provides the necessary groundwork for building, monitoring, and
governing AI agents effectively.

### **Task 1:** Microsoft Foundry project

This task introduces you to the process of setting up your Microsoft
Foundry project. You will access the Foundry portal, create a new
project, and configure it with the appropriate subscription and resource
group. This step is essential as it establishes the environment where
all subsequent AI development and management activities will take place.

Follow the steps below to complete the setup of your Microsoft Foundry
project.

1.  Open a browser tab and copy and paste this link https://ai.azure.com/templates.If prompted to sign in, kindly sign in.

2.  Click **Start building** in Microsoft Foundry to begin creating your
    AI solution

     ![](./media/us11.1.png)

      > Note :(Alternatively) switch toggle to "New Foundry"

3.  You should see a dialog prompting you to select a project to continue

4.  Click the input area - you will see the ***Create a new project*** option and select it

     ![](./media/us12.1.png)

5.  Enter a unique project name i.e
    - **Contoso-Travel-<inject key="DeploymentID" enableCopy="false"/> (1)**
    - Select the default **subscription (2)**
    - Resource group: **Agentic AI (3)**
    - Click **Create (4)** to set up your Microsoft Foundry project.

       ![](./media/us13.png)

6.  The project creation process may take a few minutes to complete.
   
7.  You should now see your Foundry project landing page. **Take note of the Project Endpoint information shown here** - we will use it
    later.

     ![](./media/us14.1.png)

### Task 2: Create an AI Agent

In this task, you will create your first AI agent within the Foundry
environment. The agent will act as a travel assistant designed to help
users plan trips and provide relevant recommendations. You will define
the agent’s identity, deploy it, and test its functionality using the
playground interface.

1.  Click **Build (1)**, then select **Create agent (2)** to begin creating a new AI agent in Microsoft Foundry.

    ![](./media/us15.png)

2.  Enter the Agent name as **contoso-travel-portal (1)** and click on **Create (2)** to create the Agent.

    ![](./media/us16.png)

3.  This takes a few minutes to complete

4.  The agent is now ready to test in playground

     ![](./media/us17.1.png)

### Task 3: Create Application Insights

This task focuses on enabling observability for your AI solution. By
creating an Application Insights resource, you will be able to monitor
agent activity, collect telemetry data, and analyze system performance.
This is a critical step in understanding how your agent behaves in
real-time and identifying potential issues.

1.  On the Microsoft Foundry home page, select the **Traces (1)** tab. Then  click **Create (2)** Application Insights to set up monitoring for your project.

    ![](./media/us18.png)

2.  To Create App Insights  under Application insinghts resource: **Create new resource(1)**, accept the default
    values in the other fields and click on **Create (2)**.

    ![](./media/us19.png)

3.  App Insights has been created.

     ![](./media/us20.png)

### Task 4: Test the Agent Prompt

In this task, you will refine and test your agent’s behavior using
prompt engineering. You will define clear instructions for the agent,
execute sample queries, and evaluate the responses. This helps ensure
that the agent provides accurate, relevant, and user-friendly outputs
while adhering to its intended role

1.  Navigate to the **Playground** tab,  to test your agent prompt and view responses.

    ![](./media/us21.png)

2.  In the Playground tab, update the Instructions (1) section with your  agent prompt, and click on **Save (2)**

    ```
    You are the Contoso Travel Concierge, a friendly and knowledgeable
    travel assistant.
    
    Your responsibilities:
    
    \- Help customers plan trips by answering questions about destinations,
    travel tips, and logistics
    
    \- Provide helpful, accurate, and concise travel advice
    
    \- Be warm and professional in your responses
    
    \- When you don't have specific data, provide general travel guidance
    
    \- Always mention that Contoso Travel can help with flights, hotels, and
    car rentals
    
    \- Use the provided tools to look up relevant information for the
    request and provide citations. Keep responses short, factual and
    friendly.
    
    Tool Usage Guidelines:
    
    \- ALWAYS use the web_search tool before providing or citing any
    current, real-world data such as hotel prices, weather forecasts, flight
    or hotel availability, or other time-sensitive information. Do NOT
    fabricate real-time external data or rely on prior training data for
    such facts; only provide them after confirming with a tool call.
    
    \- For vague or broad user queries (e.g., vague destination or service
    requests), proactively use web_search to gather suggestions and relevant
    information, AND ask clarifying questions as needed. Do not limit
    yourself to only follow-up queries—use web_search to supply initial
    helpful ideas.
    
    \- For requests that are outside your scope (e.g., Python scripting,
    stock advice, or any non-travel topic), politely decline and clarify
    that you are a travel assistant only, and whenever possible, redirect
    the user with a helpful travel suggestion or resource. For safety or
    policy-violating requests (e.g., sneaking prohibited items, evading
    sanctions), firmly refuse, clearly explaining why you cannot assist,
    referencing safety, legality, or policy as needed.
    ```

     ![](./media/us22.png)

4.  Enter the below in the chat panel and select **Send**
   
   ```
    Hi. I'm thinking about planning a trip to Paris. What should I know? 
   ```
 
   ![](./media/us23.1.png)

5.  Observe the response.

    ![](./media/us24.1.png)

6.  Click on the **Metrics** link above the response panel - it shows  you available evaluators.

    ![](./media/us25.1.png)

7.  Customize the list to reflect evaluation criteria you want to use and try a new request.

     ```
        Hi. I'm thinking about planning a trip to Paris. What should I know? 
     ```    

     ![](./media/us26.1.png)

8.  Observe the *AI Quality* and *Safety* metrics in the line below the response.

9.  Hover over each number - you should see the custom metrics used and their Pass/Fail status

    ![](./media/us27.png)

10. Select **Configuration**

    ![](./media/us28.png)

11. Enter the details

- **Display name (1)**: Contoso Travel Assistant
- **Description (2)**

   ```
        Welcome to Contoso Travel. We can help you plan your next itinerary
        with flight bookings, car rentals and hotel reservations. Just tell us
       your destination and the number of travellers in your group - and we'll
       do the rest. 
     ```  
-**Starter prompts (3)**

     ```
        I want to plan a multi-day travel itinerary 
     ```  
     
     ```
       I want to rent a car at my travel destination
     ```  
     
     ```
       I want to book a flight and hotel for my travels
     ``` 

- Click on **Reset (4)**

    ![](./media/us29.png)

12. In the Test pane, enter the below and click **Send.**

     ```
        I want to plan a multi-day travel itinerary 
     ```  

     ![](./media/us30.png)

13. View the response. The agent will prompt you for additional information as instructed.

    ![](./media/us31.png)

14. Enter the following text and click on the **Submit icon** as shown in the below image.

      ```
       Hi! I'm thinking about planning a trip to Paris from Jul 1–4 with my
       family (3 people total). We are vegetarian. We love sports, historic
       homes, art and food tours

      ```

       ![](./media/us32.png)

15. Note how the agent remembers and uses context from the history.

     ![](./media/us33.1.png)

16. Click the **Traces** tab - you should see rows for each conversation run

    ![](./media/us34.1.png)

17. Want to understand what the Trace ID is showing - try **Ask AI** and enter the below prompt and click on **Send**

   ```
     Explain what the trace ID is showing
           
   ```
 
   ![](./media/us35.png)

   ![](./media/us36.png)

   ![](./media/us37.png)

18. Click on the Trace ID - you should see something like this:

    ![](./media/us38.png)

    ![](./media/us39.png)

19. Click **Preview (1)**, then select **Preview agent (2)** to test your agent in a sample application interface.

    ![](./media/us40.png)

    ![](./media/us41.png)

20. Enter the following text and click on the **Submit icon** as shown in the below image.

   ```
   I want to plan a multi-day travel itinerary leaving JFK on Jul 1 for
   Paris and returning Jul 5. I am traveling with my family (3 people
   total). We are vegetarians. We love sports, historic homes and art and
   food tours. Plan my itinerary and show me hotels and flights for my
   stay
           
   ```

   ![](./media/us42.png)

21. You can review the agent response in the preview tab itself

    ![](./media/us43.png)

22. Note that if you return to agent you can now see this interaction captured in the traces as well.

    ![](./media/us44.png)

### Task 5: Explore Evaluations Tab

This task introduces you to the evaluation capabilities available in
Microsoft Foundry. You will explore various built-in evaluators that
measure aspects such as quality, relevance, and safety. Additionally,
you will learn how to create custom evaluators tailored to your specific
requirements.

By now you should have a sense for
the *Tracing* and *Evaluations* capabilities in the agent playground.
Microsoft Foundry has a large number of built-in evaluators that you can
also invoke *code-first*.

1.  Click on the **Evaluations** item in the sidebar menu.

    ![](./media/us45.png)

2.  Select the **Evaluators catalog** to see the full list of supported evaluators

     ![](./media/us46.png)

3.  Filter to see evaluators for a particular category - e.g., agents

    ![](./media/us47.png)

    ![](./media/us48.png)

4.  Use "Ask AI" to get explanations for any of them - e.g., ask:

    ```
    Tell me more about the Protected-Material evaluator
               
    ```
   ![](./media/us49.png)

5.  Click the **Create** button.

    ![](./media/us50.png)

6. Give the following details
   - Workflow name as **customevaluator (1)**
   - Category: **Agents (2)**
   - Scoring Method: **Ordinal[1-5] (3)**
   - Click on **Create (4)**

    ![](./media/us51.png)

    ![](./media/us52.png)

### Task 6: Run a Red Teaming Scan

In this task, you will perform a red teaming exercise to assess the
robustness and safety of your AI agent. By simulating adversarial
scenarios, you can identify vulnerabilities and ensure that the agent
behaves responsibly under different conditions.

1.  Navigate to the **Evaluations (1)** section, select the **Red team (Preview) (2)** tab, then click **Create (3)** to start a new red teaming run.

    ![](./media/us53.png)

2.  For now, select the **Model (1)** option and pick the default model used  in your agent e.g, gpt-4.1(2) and click **Next (3)**

    ![](./media/us54.png)

3.  Click on Next

    ![](./media/us55.png)

4.  Submit the scan. This takes a while to complete - we will revisit it
    later.

    ![](./media/us56.png)

    ![](./media/us57.png)

    ![](./media/us58.png)

**Continue Exercise 2……………..**

## Exercise 2: Building Contoso Travel Using Prompt Agents

In this exercise, you will transition from a UI-based approach to a
code-first approach using notebooks. You will build more advanced AI
capabilities by creating agents programmatically, integrating tools, and
orchestrating workflows. This exercise emphasizes scalability,
flexibility, and deeper control over agent behavior, while continuing to
leverage governance and observability features.

### Task 1: Open Github Codespaces environment

This task involves setting up a cloud-based development environment
using GitHub Codespaces. You will fork the provided repository, launch a
Codespace, and prepare your workspace for development.

1.  Open your browser, navigate to the address bar, type or paste the following URL:

     ```
    https://github.com/technofocus-pte/Foundry-Control-Plane-agent-observability
               
    ```

     ![](./media/usx1.png)

1. Click on **fork** to fork the repo. 

    ![](./media/usx2.png)

1. Give the name to the repo as **Foundry-Control-<inject key="DeploymentID" enableCopy="false"/> (1)** and click on **Create Fork (2)** .

    ![](./media/usx3.png)

1. Click on **Code (1) -\> Codespaces (2) -\> Create Codespace (3)**

    ![](./media/usx4.png)

    ![](./media/usx5.png)

    > **Note:** It can take a few minutes for the codespace to spin up completely
   
1.  Run the below command to run the script to set up the required  environment for the lab.

    ```
    ./labs/notebooks/setup-env.sh
               
    ```
     ![](./media/usx6.png)

1.  It should prompt you to log into Azure as shown. Complete this step, then let the script run till complete. 

     ![](./media/usx7.png)

1.  Default browser opens to enter the generated code to verify. Enter the code and click **Next**.

     ![](./media/usx8.png)

1.  Sign in with your Azure credentials **<inject key="AzureAdUserEmail"></inject>**.

     ![](./media/usx9.png)

     ![](./media/usx10.png)

1. To select the default subscription enter 1.

     ![](./media/usx11.png)

1. Enter the resource group as **AgenticAI** 

     ![](./media/usx12.png)

1. Congratulations - your local env variables are set.

     ![](./media/usx13.png)

### Task 2: Environment Setup & Validation

In this task, you will configure and validate your development
environment. This includes selecting the appropriate Python environment,
installing dependencies, and verifying connectivity to Azure services
and the Foundry project.

1.  Navigate to the **labs/notebooks/1-prompt-agents** folder and open the **lab-01-setup.ipynb** notebook to begin the environment setup
    lab.

     ![](./media/usx14.png)

1.  Click **Select Kernel** in the top-right corner of the notebook and choose the appropriate Python environment to run the lab.

    ![](./media/usx15.png)

1.  Select **Python Environments**

    ![](./media/usx16.png)

1.  If prompted to select the path, then select the **Python** version  i.e **3.12.13**

    ![](./media/usx17.png)

1.  To install dependencies, run the first cell in the notebook

   ![](./media/usx18.png)

1. Restart the Kernel by clicking on **Restart**.In the pop-up that appears click on Restart again
   
   ![](./media/usx21.png)

1.  Load and validate the environment variables from the shared .env  file by running the second cell in the notebook.

   ![](./media/usx19.png)

   ![](./media/usx20.png)

1.  Verify that you can connect to your Microsoft Foundry project using the SDK by running the 3^(rd) cell in the notebook.

   ![](./media/usx22.png)

   ![](./media/usx23.png)

1.  Run the cell under **Validate OpenAI Client** to verify that your OpenAI client is correctly configured and responding.

   ![](./media/usx24.png)

   ![](./media/usx25.png)

1.  Explore the Contoso Travel sample data by running the 5^(th), 6^(th), 7^(th) and 8^(th) cells in the notebook.

    ![](./media/usx26.png)
    
    ![](./media/usx27.png)
    
    ![](./media/usx28.png)
    
    ![](./media/usx29.png)
    
    ![](./media/usx30.png)

### Task 3: Create Your First Prompt Agent

This task focuses on creating an AI agent programmatically using the
Foundry SDK. You will initialize the required clients, create the agent,
and interact with it through conversations to observe its behavior and
responses.

1. Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and  open the **lab-02-agent.ipynb** notebook to begin the environment
    setup lab.

   ![](./media/usx31.png)

1. Click **Select Kernel**, then choose the **Python 3.12.13**  environment to run the Lab 02 notebook.

   ![](./media/usx32.png)

1. Load the environment variables and create the Azure AI Project  client by running the first cell in the notebook.

    ![](./media/usx33.png)

    ![](./media/usx34.png)

1. To create the Concierge Agent, run the second cell in the notebook.

    ![](./media/usx35.png)

    ![](./media/usx36.png)

1. Run the cell under **Start a Conversation** to create a conversation and send your first query to the agent.

   ![](./media/usx37.png)

   ![](./media/usx38.png)

1. Run the cell under **Multi-Turn Conversation** to send a follow-up query and observe how the agent maintains context across interactions.

   ![](./media/usx39.png)

   ![](./media/usx40.png)

1. Run the cell under **Explore the Response Object** to inspect the structure and details of the agent’s response.

   ![](./media/usx41.png)

   ![](./media/usx42.png)

1. Run the cell to delete the conversation and the agent version.

   ![](./media/usx43.png)

### Task 4: Add Function Tools to Your Travel Agent

In this task, you will enhance your agent by adding function tools that
allow it to retrieve and process structured data. This enables the agent
to handle more complex queries and provide more accurate and dynamic
responses.

1. Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and  open the **lab-03a-tools.ipynb** notebook to begin the environment
    setup lab.

   ![](./media/usx44.png)

1. Click **Select Kernel**, then choose the **Python 3.12.13**  environment to run the Lab 02 notebook.

   ![](./media/usx45.png)

1. Load the environment variables and create the Azure AI Project client by running the first cell in the notebook.

   ![](./media/usx46.png)

1. Run the cell under **Load the Travel Data** to load the CSV files into DataFrames and verify the data is successfully loaded.

   ![](./media/usx47.png)

1. Run the cell under **Define Tool Functions** to create the functions that query travel data and return results in JSON format.

   ![](./media/usx48.png)

   ![](./media/usx49.png)

1. Run the cell under **Register Function Tools** to define and register the tool schemas that the agent will use to call functions.

    ![](./media/usx50.png)

    ![](./media/usx51.png)

1. Run the cell under **Create the Enhanced Travel Agent** to define the agent instructions and create an agent with the registered function tools attached.

    ![](./media/usx52.png)

    ![](./media/usx53.png)

1. Run the cell under **Test: Flight Search** to test the agent’s ability to call the **search_flights** tool and return relevantresults.

   ![](./media/usx54.png)

   ![](./media/usx55.png)

1. Run the cell under **Handle Function Call Responses** to execute the tool call, send the results back to the agent, and generate the final response.

   ![](./media/usx56.png)

1. Run the cell under **Test: Hotel + Car Combo** to test a multi-step query where the agent calls multiple tools sequentially to provide
    combined results.

    ![](./media/usx57.png)

    ![](./media/usx58.png)

1. Run the final cell to delete the conversation and agent resources.

    ![](./media/usx59.png)

### Task 5: Build a Multi-Agent Travel Workflow

This task introduces the concept of multi-agent orchestration. You will
create specialized agents for different domains such as flights, hotels,
and cars, and then combine them into a unified workflow that delivers a
complete travel planning experience.

1. Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and open the **lab-03b-workflow.ipynb** notebook to begin the environment setup lab.

   ![](./media/usx60.png)

1. Click **Select Kernel**, then choose the **Python 3.12.13** environment to run the Lab 02 notebook.

   ![](./media/usx61.png)

1. Run the first cell to import required libraries and initialize the environment for workflow orchestration.

   ![](./media/usx62.png)

1. Run the cell under **Create Specialist Agents** to create multiple domain-specific agents (flight, hotel, and car) along with a concierge agent that combines their results.

   ![](./media/usx63.png)

   ![](./media/usx64.png)

1. Run the cell under **Define the Workflow YAML** to create the YAML-based workflow that orchestrates interactions between the specialist agents and the concierge agent.

   ![](./media/usx65.png)

   ![](./media/usx66.png)

1. Run the cell under **Create the Workflow Agent** to register the workflow in Microsoft Foundry and create the workflow agent.

   ![](./media/usx67.png)

1. Run the cell under **Test: End-to-End Trip Planning** to execute the workflow and observe how it orchestrates multiple agents to generate
    a complete travel plan.

   ![](./media/usx68.png)

   ![](./media/usx69.png)

1. Run the cell under **Retrieve & Combine Agent Responses** to fetch the outputs from each specialist agent and combine them into a Unified response.

   ![](./media/usx70.png)

   ![](./media/usx71.png)

1. Run the final cell to delete the conversation and agent resources.

   ![](./media/usx72.png)

   ![](./media/usx73.png)

### Task 6: Trace Your Travel Agent

In this task, you will enable tracing and observability for your agent
using telemetry and monitoring tools. You will analyze execution flows,
inspect trace spans, and gain insights into how your agent processes
requests.

1. Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and open the **lab-04-tracing.ipynb** notebook to begin the environment setup lab.

    ![](./media/usx74.png)

1. Click **Select Kernel**, then choose the **Python 3.12.13** environment to run the Lab 02 notebook.

    ![](./media/usx75.png)

1. Run the cell under **Setup** to load environment variables and enable GenAI tracing for observability.

    ![](./media/usx76.png)

1. Run the cell to configure **OpenTelemetry tracing** and enable tracking of Azure SDK calls for observability.

    ![](./media/usx77.png)

1. Run the cell to connect to your Microsoft Foundry project and initialize the OpenAI client with tracing enabled.

    ![](./media/usx78.png)

1. Run the cell under **Create and Trace a Travel Agent** to create a traced agent and enable observability for its operations.

    ![](./media/usx79.png)

    ![](./media/usx80.png)

1. Run the cell under **Run a Traced Travel Query** to check the console output below — OpenTelemetry spans appear for each operation.

   ![](./media/usx81.png)

   ![](./media/usx82.png)

1. Run the cell under **Configure Azure Monitor Tracing** to enable Application Insights integration and send traces to Azure Monitor
    for observability.

    ![](./media/usx83.png)

    ![](./media/usx84.png)

1. Run the cell under **Run a Traced Travel Query (Azure Monitor)** to execute a query and generate traces that can be viewed in Azure
    Monitor.

    ![](./media/usx85.png)

    ![](./media/usx86.png) 

1. Back in the Foundry portal select **Agents**, then click on the **contoso-travel-traced** agent to view its details and traces.

    ![](./media/usx87.png)

1. Click on the **Tracing** tab for your agent. You should see your traces listed with the span names that were defined.

    ![](./media/usx88.png)

1. Click on a trace to see the full span tree

    ![](./media/usx89.png)

    ![](./media/usx90.png)

    ![](./media/usx91.png)

   > **Note** Traces may take 2-5 minutes to appear in Azure Monitor after execution.

1. Return to your Codespace to continue the lab.

1. Run the cell under **Custom Span Attributes** to add custom metadata to traces for improved filtering and analysis in Azure Monitor.

    ![](./media/usx92.png)

    ![](./media/usx93.png)

1. Run the final cell to delete the conversation and agent resources.

    ![](./media/usx94.png)

### Task 7: Evaluate Your Travel Agent

This task focuses on evaluating your agent’s performance using
structured evaluation techniques. You will assess the agent’s responses
for quality, safety, and relevance, and interpret the results to
identify areas for improvement.

1. Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and  open the **lab-05-evaluation.ipynb** notebook to begin the
    environment setup lab.

    ![](./media/usx95.png)

1. Click **Select Kernel**, then choose the **Python 3.12.13** environment to run the Lab 02 notebook.

    ![](./media/usx96.png)

1. Run the cell under **Setup** to connect to Microsoft Foundry and initialize the evaluation client.

    ![](./media/usx97.png)

    ![](./media/usx98.png)

1.  Run the cell under **Create the Travel Agent for Evaluation** to create a versioned agent that will be used for evaluation.

    ![](./media/usx99.png)

1.  Run the cell under **Prepare Evaluation Data** to load and review the sample evaluation queries from the dataset.

    ![](./media/usx100.png)

1.  Run the cell under **Define Quality Evaluators** to configure evaluation criteria such as fluency, coherence, and task adherence.

    ![](./media/usx101.png)

    ![](./media/usx102.png)

1.  Run the cell under **Run the Quality Evaluation** to submit queries  to the agent and evaluate the responses against the defined criteria.

    ![](./media/usx103.png)

    ![](./media/usx104.png)

1.  Run the cell under **Interpret Quality Results** to review evaluation scores and analyze how the agent performed across different criteria.

    ![](./media/usx105.png)

    ![](./media/usx106png)

1.  Run the cell under **Define Safety Evaluators** to configure safety checks such as violence, hate, and self-harm detection for agent
    responses.

    ![](./media/usx107.png)

    ![](./media/usx108.png)

1. Run the cell under **Run the Safety Evaluation** to test the agent against sensitive scenarios and evaluate its safety handling.

   ![](./media/usx109.png)

   ![](./media/usx110.png)

1. Run the cell under **Interpret Safety Results** to review safety evaluation scores and analyze how the agent handled sensitive scenarios.

   ![](./media/usx111.png)

   ![](./media/usx112.png)

1. Run the cell to define the **Agentic Evaluation schema and criteria**, including context and ground truth for advanced evaluation.

   ![](./media/usx113.png)

   ![](./media/usx114.png)

1. Run the cell under **Run the Agentic Evaluation** to evaluate the agent using context and ground truth for more advanced assessment.

   ![](./media/usx115.png)

   ![](./media/usx116.png)

1. Run the cell under **Interpret Agentic Results** to review agentic evaluation scores such as intent resolution, groundedness, and relevance.

  ![](./media/usx117.png)

  ![](./media/usx118.png)

1. Back in the Foundry portal, select **Agents**, then click on the **contoso-travel-eval** agent to view its details and evaluation results.

   ![](./media/usx119.png)

1. Click on the **Evaluations** tab in the left navigation

   ![](./media/usx120.png)

1. You should see the Quality, Safety, and Agentic evaluation runs  listed

    ![](./media/usx121.png)

1. Select **Contoso Travel-Safety Evolution**

    ![](./media/usx122.png)

    ![](./media/usx123.png)

1. Return to your Codespace to continue the lab.

1. Run the final cell to delete the conversation and agent resources.

    ![](./media/usx124.png)

### Task 8: Red-Team Your Travel Agent

In this task, you will conduct advanced red teaming to test your agent
against potential threats and adversarial inputs. This helps ensure that
the agent operates safely and adheres to responsible AI principles.

1.  Navigate to the **labs/notebooks/1-prompt-agents/lab** folder and open the **lab-06-redteam.ipynb** notebook to begin the environment
    setup lab.

    ![](./media/usx125.png)

1.  Click **Select Kernel**, then choose the **Python 3.12.13** environment to run the Lab 02 notebook.

    ![](./media/usx126.png)

1.  Run the cell under **Setup** to connect to Microsoft Foundry and initialize the red teaming environment.

    ![](./media/usx127.png)

1.  Run the cell under **Create the Travel Agent and Red Team** to create a versioned agent and set up a red team evaluation for safety
    testing.

    ![](./media/usx128.png)

    ![](./media/usx129.png)

1.  Run the cell under **Create an Evaluation Taxonomy** to define the agent target and generate a taxonomy for prohibited actions used in
    red teaming.

    ![](./media/usx130.png)

    ![](./media/usx131.png)

1.  Run the cell under **Create a Red Team Run** to initiate a red teaming evaluation with defined attack strategies and multi-turn
    scenarios.

    ![](./media/usx132.png)

1.  Run the cell to **monitor the red team run status**, polling until  the evaluation is completed.

    ![](./media/usx133.png)

    ![](./media/usx134.png)

    ![](./media/usx135.png)

1. Back in the Foundry portal, navigate to the **contoso-travel-redteam** agent

    ![](./media/usx136.png)

1. Navigate to **Evaluations** → select the red team evaluation

    ![](./media/usx137.png)

    ![](./media/usx138.png)

1. Review individual attack attempts, agent responses, and evaluator  scores

    ![](./media/usx139.png)

1. Run the final cell to delete the conversation and agent resources.

    ![](./media/usx140.png)

### Task 9: Delete the Resources

In the final task, you will clean up all resources created during the
lab. This ensures that no unnecessary costs are incurred and that your
environment is reset for future use.

1.  To delete Resource group , type **Resource groups** in the Azure portal search bar, navigate and click on **Resource
    groups** under **Services**.

    ![](./media/usx141.png)

1.  In the Resource groups page, select your **AgenticAI** resource group.

1.  In the **Resource group** home page, select all resources and click on **Delete**

    ![](./media/usx142.png)

1.  In the **Delete Resources** pane that appears on the right side, navigate to **Enter “delete” to confirm deletion** field, then click
    on the **Delete** button

1.  On **Delete confirmation** dialog box, click on **Delete** button.

> **Summary**
>
> This scenario demonstrates how to design, deploy, and manage AI agents
> using a centralized governance approach with Microsoft Foundry Control
> Plane. You began by setting up a Foundry project and creating a travel
> assistant agent, then enabled observability using Azure Application
> Insights to capture traces and monitor agent behavior. Through
> hands-on tasks, you explored how to test and refine agent responses,
> apply evaluation frameworks to measure quality and safety, and perform
> red teaming to identify potential risks.
>
> In the later stages, you adopted a code-first approach using GitHub
> Codespaces to build advanced capabilities such as tool integration,
> multi-agent workflows, and end-to-end orchestration. You also enabled
> tracing and telemetry to gain deep insights into agent execution and
> used structured evaluations to assess performance across multiple
> dimensions. Overall, this scenario highlights how centralized
> governance, observability, and evaluation can be combined to build
> reliable, scalable, and secure AI agent solutions ready for real-world
> deployment.
