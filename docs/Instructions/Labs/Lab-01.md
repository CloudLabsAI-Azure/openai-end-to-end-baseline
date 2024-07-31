# Lab 01: Managing and Enhancing Prompt Flows

## Lab Scenario

In this lab, you will engage in a series of steps aimed at creating, testing, and deploying a prompt flow using Azure Machine Learning Studio. This process begins with establishing a connection to Azure OpenAI, followed by the cloning of an existing prompt flow. Subsequently, you will configure this cloned flow to meet specific requirements or objectives. Finally, the flow will undergo testing to ensure its functionality and effectiveness before being deployed for practical use.

## Lab Objectives

In this lab, you will perform the following tasks:

- **Task 1:** Create, test, and deploy a Prompt flow
- **Task 2:** Clone an existing prompt flow
- **Task 3:** Add runtime & Test the flow

## Estimated Timing: 80 Minutes

### Task 1: Create, Test, and Deploy a Prompt Flow

1.  In the **Azure portal** page, in the **Search resources, services, and docs** search for and select **mlw-<inject key="DeploymentID" enableCopy="false"></inject>** for machine learning workspace and select **Launch studio**.

     ![Access Your VM and Lab Guide](../media/mlw.png)

1.  On the **Azure AI | Machine Learning Studio**, under **mlw-<inject key="DeploymentID" enableCopy="false"></inject>** workspace, from the left navigation pane select **Prompt flow**.

    ![Access Your VM and Lab Guide](../media/openai_3_1.png)

1.  Select the **Connections** tab and click on **Create (1)**. Moving on, choose **Azure OpenAI (2)** from the dropdown.

    ![Access Your VM and Lab Guide](../media/openai_6-1.png)

1. Navigate back to the Azure Portal. In the **Search resources, services, and docs** space, search for and select **oai-<inject key="DeploymentID" enableCopy="false"></inject>**. 

1. On the **oai-<inject key="DeploymentID" enableCopy="false"></inject>** tab, from the left navigation pane under **Resource Management**, select **Keys and Endpoints**.

1. Copy the value of **KEY 1** and **Endpoint**, and paste these values into the notepad. You will use these values in the next step.

1. Navigate back to the **Connections** tab and follow these instructions to fill out the properties for creating connections:
    
   - Name: **gpt35**
   - Provider: **Azure OpenAI**
   - Subscription ID: Select the default.
   - Azure OpenAI Account Names: **oai-<inject key="DeploymentID" enableCopy="false"></inject>**
   - API Key: Paste the KEY 1 value here that you had copied in the previous step.
   - API Base: Paste the Endpoint value here that you had copied in the previous step.
   - API type: **Azure**
   - API version: Keep it as default.
   - Select **Save**

### Task 2: Clone an Existing Prompt Flow
   
1.  Now select the **Flows (1)** tab and click on **+ Create (2)**.

    ![Access Your VM and Lab Guide](../media/flow.png)
 
1.  On the **Create a new flow** page, under **Explore gallery**, in **Chat with Wikipedia (1)** box, select **Clone (2)**.

    ![Access Your VM and Lab Guide](../media/chatwithclone.png)
   
1. On the **Clone flow**, name the folder name as **chat_wiki** and click on **Clone.**
   
1. Set the **Connection (1)** and **deployment_name (2)** to **gpt35** and set the **max_tokens** property of the deployment_name to **256** for the following steps:
   - extract_query_from_question
   - augmented_chat
  
    ![Access Your VM and Lab Guide](../media/openai_08_9.png)

    ![Access Your VM and Lab Guide](../media/openai_11-1.png)
   
6. Click on **Save (1)** and select **Start compute session (2)**.

   ![Access Your VM and Lab Guide](../media/save.png)

     >**Note**: Wait for the compute session to complete. It takes 1-3 minutes.

### Task 3: Add Runtime & Test the Flow

1. Select **Run** to execute all the nodes after the present node has completed its run.

   ![Access Your VM and Lab Guide](../media/openai_12.png)
   
     >**Note**: Use the scrollbar or down arrow button to navigate downwards of the page, ensuring the graph flow remains unchanged.

4. After executing all the nodes, select the **Chat (1)** button.

   ![Access Your VM and Lab Guide](../media/chat.png)
   
6. Enter a question: `What is the difference between this model and previous neural network?`  Wait for the output to be generated, then check the answer and the number of tokens used.

   ![Access Your VM and Lab Guide](../media/trace.png)

> **Congratulations** on completing the task! Now, it is time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at **labs-support@spektrasystems.com**. We are available 24/7 to help you out.
<validation step="a191a267-12d7-4c02-a757-1bff8a5daa07" />

## Review

In this lab, you have completed the following tasks:

- Created, tested, and deployed a prompt flow.
- Cloned an existing prompt flow.
- Added runtime & tested the flow.


