## Lab -02 OpenAI end to end baseline

### Task 1 : Deploy to Azure Machine Learning managed online endpoint.

1. Navigate back to the ML workspace and choose **prompt flow** and select **chat_wiki** flow.
   
2. Create a deployment in the UI, by selecting the **deploy** icon from the tool bar.

3. Choose **Existing** Endpoint and select the one called **ept-<inject key="DeploymentID" enableCopy="false"></inject>**
   
4. Name the deployment **eptdeploy-<inject key="DeploymentID" enableCopy="false"></inject>**.
   
5. Choose a small Virtual Machine size(i.e D series or B series) for testing and set the number of instances to 2.
   
6. Press **Review + Create**

7. Press **Create**

### Task 2 : Publish the Chat front-end web app.

1. In the Azure Portal, go to your storage account **st <inject key="DeploymentID" enableCopy="false"></inject>**, navigate to the **Containers** section within **data storage**, and select **Deploy** container. From there, upload the file `chatui.zip` located at `C:\LabFiles\openai-end-to-end-baseline\website\chatui.zip`.
  

2. Go to your storage account **st <inject key="DeploymentID" enableCopy="false"></inject>** , Choose containers under data storage , select deploy container , click on chatui.zip , select generate SAS , click on generate sas then copy sas url

3. Set the environment variable WEBSITE_RUN_FROM_PACKAGE in the **app-<inject key="DeploymentID" enableCopy="false"></inject>** with the SAS URL of the zip file.

4. Create an A record for DNS,please edit your hosts file (C:\Windows\System32\drivers\etc\hosts or /etc/hosts) and add the following record to the end: ${APPGW_PUBLIC_IP} www.${DOMAIN_NAME_APPSERV_BASELINE} (e.g. 50.140.130.120  www.contoso.com)

5. Browse to the site (e.g. https://www.contoso.com)
