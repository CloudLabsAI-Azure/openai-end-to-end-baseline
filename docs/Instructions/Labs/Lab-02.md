## Lab -02 

### Task 1 : Deploy to Azure Machine Learning managed online endpoint.

1. Navigate back to the ML workspace and choose **prompt flow** and select **chat_wiki** flow.
   
2. Create a deployment in the UI, by selecting the **deploy** icon from the tool bar.

3. Choose **Existing** Endpoint and select the one called **ept-<inject key="DeploymentID" enableCopy="false"></inject>**
   
4. Name the deployment **eptdeploy-<inject key="DeploymentID" enableCopy="false"></inject>**.
   
5. Choose a small Virtual Machine size(i.e D series or B series) for testing and set the number of instances to 2.
   
6.Press **Review + Create**

7.Press **Create**

## Task 2 : Publish the Chat front-end web app.

1. Open PowerShell ISE with administrator access from the search bar, Login to the azure

  ```

   az login

  ```

2. Execute the following command to upload the zip file to the storage account.

  - $CLIENT_IP_ADDRESS : Public ip address of the VM
  - $NAME_OF_STORAGE_ACCOUNT[STORAGE-ACC-NAME] :**st1399374**
  - $NAME_OF_WEB_APP:**app-<inject key="DeploymentID" enableCopy="false"></inject>**
  - $RESOURCE_GROUP NAME[RESOURCE-GROUP-NAME]:**ODL-Openai-<inject key="DeploymentID" enableCopy="false"></inject>-02**
  - account-key[ACC-KEY]: Copy the key from the Storage account
  - pip-$BASE_NAME:**pip-<inject key="DeploymentID" enableCopy="false"></inject>**
  - query [IP-ADD]: Public ip address of the VM
    
```

  $CLIENT_IP_ADDRESS=""
  $STORAGE_ACCOUNT_PREFIX="st"
  $WEB_APP_PREFIX="app-"
  $NAME_OF_STORAGE_ACCOUNT=""
  $NAME_OF_WEB_APP=""
  $LOGGED_IN_USER_ID=$(az ad signed-in-user show --query id -o tsv)
  $RESOURCE_GROUP_ID=$(az group show --resource-group [RESOURCE-GROUP-NAME] --query id -o tsv)
  $STORAGE_BLOB_DATA_CONTRIBUTOR="ba92f5b4-2d11-453d-a403-e96b0029c9fe"
  $RESOURCE_GROUP=""
  
  az storage account network-rule add -g $RESOURCE_GROUP --account-name "$NAME_OF_STORAGE_ACCOUNT" --ip-address $CLIENT_IP_ADDRESS
  az role assignment create --assignee-principal-type User --assignee-object-id $LOGGED_IN_USER_ID --role $STORAGE_BLOB_DATA_CONTRIBUTOR --scope $RESOURCE_GROUP_ID
  az storage blob upload --account-name [STORAGE-ACC-NAME] --account-key [ACC-KEY] --container-name deploy --file ./website/chatui.zip --name chatui.zip
  
  # query the Azure Application Gateway Public Ip
  $APPGW_PUBLIC_IP='az network public-ip show --resource-group $RESOURCE_GROUP --name "pip-$BASE_NAME" --query [IP-ADD] --output tsv'
  echo APPGW_PUBLIC_IP: $APPGW_PUBLIC_IP


```
