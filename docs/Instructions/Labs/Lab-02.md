# Lab 02: OpenAI end to end baseline

## Lab scenario
In this lab, you will walk through the process of deploying a machine learning model to an Azure Machine Learning managed online endpoint and publishing a front-end web application to interact with the deployed model. This hands-on experience covers key aspects of the deployment pipeline, including creating and configuring resources on Azure, uploading necessary files, and setting up environment variables.

## Lab objectives
In this lab, you will perform the following:
- Task 1: Deploy to Azure Machine Learning managed online endpoint
- Task 2: Publish the Chat front-end web app

## Estimated timing:

### Task 1: Deploy to Azure Machine Learning managed online endpoint

1. Navigate back to the ML workspace and choose **prompt flow** and select **chat_wiki** flow.

   ![Access Your VM and Lab Guide](/docs/media/openai-main-01.png)
   
3. Create a deployment in the UI, by selecting the **deploy** icon from the tool bar.

    ![Access Your VM and Lab Guide](/docs/media/openai-main-02.png)

5. Choose **Existing** Endpoint and select the one called **ept-<inject key="DeploymentID" enableCopy="false"></inject>**

    ![Access Your VM and Lab Guide](/docs/media/openai-main-03.png)
   
7. Name the deployment **eptdeploy-<inject key="DeploymentID" enableCopy="false"></inject>**.
   
9. Choose a small Virtual Machine size(i.e D series or B series) for testing and set the number of instances to 2.
   
10. Press **Review + Create**

    ![Access Your VM and Lab Guide](/docs/media/openai-main-04.png)
    
12. Press **Create**

    ![Access Your VM and Lab Guide](/docs/media/openai-main-05.png)
    
### Task 2: Publish the Chat front-end web app

1. In the Azure Portal, go to your storage account **st <inject key="DeploymentID" enableCopy="false"></inject>**, navigate to the **Containers** section within **data storage**, and select **Deploy** container. From there, upload the file `chatui.zip` located at `C:\LabFiles\openai-end-to-end-baseline\website\chatui.zip`.

   ![Access Your VM and Lab Guide](/docs/media/openai-main-11.png)
   
2. Click on **chatui.zip** , select **Generate SAS** , Click on **Generate SAS and token URL** then copy sas url.

    ![Access Your VM and Lab Guide](/docs/media/openai-main-10.png)
   
4. Set the environment variable `WEBSITE_RUN_FROM_PACKAGE` in the **app-<inject key="DeploymentID" enableCopy="false"></inject>** with the SAS URL of the zip file.

   ![Access Your VM and Lab Guide](/docs/media/openai-main-08.png)
  
4. Create an A record for DNS .Please edit your hosts file `(C:\Windows\System32\drivers\etc\hosts or /etc/hosts)` and add the following 
   record to the end: **${APPGW_PUBLIC_IP} www.${DOMAIN_NAME_APPSERV_BASELINE}** (e.g. 50.140.130.120  www.contoso.com)

   ![Access Your VM and Lab Guide](/docs/media/openai-main-06.png)

   ![Access Your VM and Lab Guide](/docs/media/openai-main-07.png)
  
5. Browse to the site (e.g. https://app-1399374.azurewebsites.net.com)

   ![Access Your VM and Lab Guide](/docs/media/openai-main-13.png)
   
## Review
In this lab you have completed the following tasks:
- Deployed to Azure Machine Learning managed online endpoint
- Published the Chat front-end web app
