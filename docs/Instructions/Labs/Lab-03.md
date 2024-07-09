### Lab -03 Openai end to end baseline

#### Task 1: Deploying the flow to Azure App Service option.

1. Open the Prompt flow UI in Azure Machine Learning Studio

2. Expand the 'Files' tab in the right pane of the UI

3. Click on the download icon to download the flow as a zip file.

4. Perfom the below commands in visual studio code.

   ```
    conda create --name pf python=3.11.4
    conda activate pf
    pip install promptflow promptflow-tools
    
    # You will need to install the following if you build the docker image locally
    pip install keyrings.alt
    pip install bs4
   
    ```

5. Unzip the prompt flow zip file you downloaded

6. In your terminal, change the directory to the root of the unzipped flow

7. Create a folder called 'connections'

8. Create a file for each connection you created in the Prompt flow UI

9. Make sure you name the file to match the name you gave the connection. For example, if you named your connection 'gpt35' in Prompt flow, create a file called 'gpt35.yaml' under the connections folder.

10. Enter the following values in the file:

    ```
      $schema: https://azuremlschemas.azureedge.net/promptflow/latest/AzureOpenAIConnection.schema.json
      name: gpt35
      type: azure_open_ai
      api_key: "${env:OPENAICONNECTION_API_KEY}"
      api_base: "${env:OPENAICONNECTION_API_BASE}"
      api_type: "azure"
      api_version: "2023-07-01-preview"

    ```
>**Note**:The App Service is configured with App Settings that surface as environment variables for OPENAICONNECTION_API_KEY and OPENAICONNECTION_API_BASE.

11. Build the flow
    
 ```
  pf flow build --source ./ --output dist --format docker
  The following code will create a folder named 'dist' with a docker file and all the required flow files.

```

### Task 3: Build and push the image

1. Ensure the requirements.txt in the dist/flow folder has the appropriate requirements. At the time of writing, they were as follows:

  ```
    promptflow[azure]
    promptflow-tools==0.1.0.b5
    python-dotenv
    bs4
  ```
2. Ensure the connections folder with the connection was created in the dist folder. If not, copy the connections folder, along with the connection file to the dist folder.

3. Make sure you have network access to your Azure Container Registry and have an RBAC role such as ACRPush that will allow you to push an image. If you are running on a local workstation, you can set Public network access to All networks or Selected networks and add your machine ip to the allowed ip list.

4. Build and push the container image

5. Run the following commands from the dist folder in your terminal:

  ```
    az login
    
    NAME_OF_ACR="cr$BASE_NAME"
    ACR_CONTAINER_NAME="aoai"
    IMAGE_NAME="wikichatflow"
    IMAGE_TAG="1.1"
    FULL_IMAGE_NAME="$ACR_CONTAINER_NAME/$IMAGE_NAME:$IMAGE_TAG"
    
    az acr build -t $FULL_IMAGE_NAME -r $NAME_OF_ACR .
  
  ```
### Task 3 : Host the chat flow container image in Azure App Service

1. Perform the following steps to deploy the container image to Azure App Service:

2. Set the container image on the pf App Service

    ```
    PF_APP_SERVICE_NAME="app-$BASE_NAME-pf"
    ACR_IMAGE_NAME="$NAME_OF_ACR.azurecr.io/$ACR_CONTAINER_NAME/$IMAGE_NAME:$IMAGE_TAG"
    
    az webapp config container set --name $PF_APP_SERVICE_NAME --resource-group $RESOURCE_GROUP --docker-custom-image-name $ACR_IMAGE_NAME --docker-registry-server-url https://$NAME_OF_ACR.azurecr.io
    az webapp deployment container config --enable-cd true --name $PF_APP_SERVICE_NAME --resource-group $RESOURCE_GROUP
    ```
    
3. Modify the configuration setting in the App Service that has the chat UI and point it to your deployed promptflow endpoint hosted in App Service instead of the managed online endpoint.

    ```
      UI_APP_SERVICE_NAME="app-$BASE_NAME"
      ENDPOINT_URL="https://$PF_APP_SERVICE_NAME.azurewebsites.net/score"
      
      az webapp config appsettings set --name $UI_APP_SERVICE_NAME --resource-group $RESOURCE_GROUP --settings chatApiEndpoint=$ENDPOINT_URL
      az webapp restart --name $UI_APP_SERVICE_NAME --resource-group $RESOURCE_GROUP
    ```
4. Validate the client application that is now pointing at the flow deployed in a container still works
