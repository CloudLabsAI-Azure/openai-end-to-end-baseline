## Lab -01 


### Task 1: Create, test, and deploy a Prompt flow


1. In the **Azure portal**, search for **mlw-<inject key="DeploymentID" enableCopy="false"></inject>** for Machine learning workspace and select **Launch studio**.

2. Click on **Prompt flow** in the left navigation in Machine Learning Studio.

3. Click on the **Connections** tab and click **Create** , Choose **Azure OpenAI** from the dropdown.

4. Fill out the properties:
    - Name: '**gpt35**' Make sure you use this name.
    - Provider: Azure OpenAI
    - Subscription Id: choose from the DropDown
    - Azure OpenAI Account Names: `oai-<inject key="DeploymentID" enableCopy="false"></inject>`
    - API Key: <Choose a key from 'Keys and endpoint' in your Azure OpenAI instance in the Portal>
    - API Base: <Choose the endpoint from 'Keys and endpoint' in your Azure OpenAI instance in the Portal>
    - API type: azure
    - API version:

   >**Note**: Open the openai resource from the portal and copy the key and end point from resource management section.

### Task -2 Clone an existing prompt flow

1. Click on **Prompt flow** in the left navigation in **Machine Learning Studio**.
   
2. Click on the **Flows tab** and click **Create**
 
3. Click **Clone** under **Chat with Wikipedia**.

4. Name it **chat_wiki** and Press **Clone**
   
5. Set the **Connection** and **deployment_name** to **gpt35** and set the **max_tokens property** of the deployment_name to 256, for the following 
    steps:
    - extract_query_from_question
    - augmented_chat
      
8. Click on Save
