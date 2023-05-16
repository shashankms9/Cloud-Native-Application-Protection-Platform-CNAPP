# Module 3 – Configuring Azure ADO Connector in Defender for DevOps


## Objectives
In this exercise, you will learn how to configure Azure ADO Connector in Defender for DevOps.


### Exercise 1: Configuring Azure ADO Connector

1. Navigate to [Azure DevOps](https://dev.azure.com) and login using the following credentials:

    * Email: <inject key="AzureAdUserEmail"></inject>
    * Password: <inject key="AzureAdUserPassword"></inject>

2. Click on **Organization settings**. 

    ![](images/m3-img6.png)

3. Next, select **Policies (1)** under **Security** and set the toggle button **On** for **Third-party application access via OAuth (2)** and **Allow public projects (3)**. Then click **Save (4)** on **Change policy setting** pop-up.

    ![](images/m3-img46.png)

    ![](images/m3-img47.png)

4. Click on **Azure Devops (1)** to navigate back to the home page. In the **Create a project to get started** pane, enter the **Project name** as **ODL_User_ <inject key="DeploymentID" enableCopy="false" /> (2)** set **Visibility** to **Public (3)** and click **+ Create project (4)**. 

    ![](images/m3-img48.png)

5. Go to **Azure Portal**, navigate to **Microsoft Defender for Cloud**. Click on **Environment Settings (1)** click the **Add environment (2)** button and click **Azure DevOps (preview) (3)** option. 

    ![](images/m3-img1.png)

6. Enter the **Name** for the connector `CNAPP-Devops` **(1)**, select your **Subscription (2)**, select **asclab (3)** resource group, select any **Region (3)**. Select **Next : Select plans > (5)**.

    ![](images/m3-img2.png)

7. In the next page leave the default selection with **DevOps** selected and click **Next: Authorize connection >** button to continue. 

    ![](images/m3-img3.png)

8. Click **Authorize** button. If this is the first time you’re authorizing your DevOps connection, you’ll receive a pop-up screen, that will ask your permission to authorize. Scroll down the popped up window screen and click the **Accept** button as shown in the sample below:

    ![](images/m3-img4.png)

    ![](images/m3-img5.png)

   > **Note**: When you click **Accept** in your Azure DevOps, you’ll notice the proof of Authorization to the **Microsoft Security DevOps** App. You can find this in your Azure ADO organization, under the **Personal Access tokens** / **User Settings** / **Authorizatons**.  

9. After the authorization is complete, select your Azure ADO organization **odluser<inject key="DeploymentID" enableCopy="false" /></inject> (1)** keep the option **Auto discovery of projects (2)** enabled. 	Click **Review and create (3)** button to continue.

      ![](images/m3-img8.png)

10. Click on **Create**.

      ![](images/m3-img9.png)
      
11. After some minutes you will see the Azure DevOps connector in the **Environment settings** page and in about 15 minutes, you will start to seeing the total resources number populating.

      ![](images/m3-img49.png)

### Exercise 2: Configure the Microsoft Security DevOps Azure DevOps Extension

1.	Navigate back to [Azure DevOps](https://dev.azure.com) tab open in your browser. In the right corner, click in the **Shopping bag icon (1)** and click **Browse marketplace (2)** option.

      ![](images/m3-img10.png)

2.	In the marketplace search and select **Microsoft Security DevOps** extension.  

      ![](images/m3-img11.png)

3.	Next click on **Get it free**.

      ![](images/m3-img12.png)

4. Choose your **Organization (1)** from the dropdown menu, select **Install (2)**.

      ![](images/m3-img13.png)

5. Click on **Proceed to Organization**. 

     ![](images/m3-img14.png)

6. From **Organization settings**, click on **Extensions (1)** under **Installed (2)** extensions you can view the **Microsoft Security DevOps (3)** extension that is installed. 

      ![](images/m3-img15.png)

    >**Note** Admin privileges to the Azure DevOps organization are required to install the extension. If you don’t have access to install the extension, you must request access from your Azure DevOps organization’s administrator during the installation process.


### Exercise 3: Install Free extension SARIF SAST Scans Tab

In order to view the scan results (when you execute the pipelines), in an easier and readable format, install this free extension in your Azure DevOps organization.

1. In **Azure DevOps** from the right corner, click in the **Shopping bag icon (1)** and click **Browse marketplace (2)** option.

      ![](images/m3-img10.png)
     
2. In the marketplace search and select **SARIF SANST Scans** extension.

      ![](images/m3-img16.png)

3. Next click on **Get it free**.

      ![](images/m3-img17.png)

4. Choose your **Organization (1)** from the dropdown menu, select **Install (2)**.

     ![](images/m3-img18.png)

5. Click on **Proceed to Organization**. 

     ![](images/m3-img19.png)

6. From **Organization settings**, click on **Extensions (1)** under **Installed (2)** extensions you can view the **SARIF SANST Scans (3)** extension that is installed. 

     ![](images/m3-img20.png)


### Exercise 4: Create a Hosted Build Agent and Pipeline

1. In the **Azure Portal**, click in the search bar, type **vmss** and then click **Virtual machine scale sets**. 

     ![](images/m3-img21.png)

2. Click **Create** button.

     ![](images/m3-img22.png)

3. In the Create a virtual machine scale set page, select your **Subscription (1)**, select **asclab (2)** resource group, provide the **Virtual machine scale set name** as `build-agent` **(3)**, for **Region** select **<inject key="Resource group Location" enableCopy="false" /> (4)**, for **Orchestration mode** select **Uniform (5)** leave all other options as is and change the image to **Windows Server 2022 Datacenter: Azure Edition Core - x64 Gen2 (6)**.

     ![](images/m3-img50.png)

4. In the same page, enter the following username and password for **VMSS** and click **Review + create (4)**.

    - **Username**: demouser
    - **Password**: demo!pass123
    - **Confirm password**: demo!pass123

     ![](images/m3-img24.png)
5. In the next page you should see that all validation has passed and you can click **Create** button. The deployment will take some minutes to finish.

     ![](images/m3-img51.png)

6. Once the deployment is finished, click **Go to resource** button.

     ![](images/m3-img26.png)

7. In the **build-agent** page, click **Instances** option in the left. Confirm the build-agents are **Running**. 

     ![](images/m3-img27.png)

8.  Navigate to [Azure DevOps](https://dev.azure.com), in the main page, click on your **Project**.

     ![](images/m3-img28.png)


9. In the bottom of left navigation page, click **Project settings** option.

     ![](images/m3-img29.png)

10. In the left navigation page, under **Pipelines** section, click **Agent pools (1)** option. In the top corner of the right page, click **Add pool (2)** button.

     ![](images/m3-img30.png)

11. In the **Add agent pool** page, click the drop down list and select **Azure virtual machine scale set**.

     ![](images/m3-img31.png)

12. Select your **subscription (1)** and click **Authorize (2)** button.

     ![](images/m3-img32.png)

13. After the authorization is done, click on the virtual machine scale set drop down list and select **build-agent (1)**. Under the **Name** field, enter **windows-build-agents (2)**.

     ![](images/m3-img33.png)

14. Enter `1` under **Maximum number of virtual machines in the scale set (1)** and **Number of agents to keep on standby (2)** fields then click **Create (3)**.

     ![](images/m3-img34.png)

16. In the **Agent pools** page you can view newly created pool.

     ![](images/m3-img35.png)

### Exercise 5: Configure your pipeline using YAML 

The purpose of this exercise is to allow you to see how the extension used by Defender for DevOps will check your pipeline.

1. Login to the [Azure DevOps](https://dev.azure.com) and open your **Project**.

     ![](images/m3-img28.png)

2. In the left navigation pane, click **Pipelines (1)**. In the right pane, click **Create Pipeline (2)** button.

     ![](images/m3-img36.png)

3. In the **Where is your code?** page, click **Azure Repos Git**.

     ![](images/m3-img37.png)

4. Click on the exisiting **Repository**.

     ![](images/m3-img38.png)

5. In the **Configure your pipeline** page, replace the **YAML code (1)** for the one below and click **Save and run (2)** :

```
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml
trigger: none
pool: windows-build-agents
steps:
- task: UseDotNet@2
  displayName: 'Use dotnet'
  inputs:
    version: 3.1.x
- task: UseDotNet@2
  displayName: 'Use dotnet'
  inputs:
    version: 5.0.x
- task: UseDotNet@2
  displayName: 'Use dotnet'
  inputs:
    version: 6.0.x
- task: MicrosoftSecurityDevOps@1
  displayName: 'Microsoft Security DevOps'
```
     
   ![](images/m3-img39.png)

   > **Note**: Observe that the pool is pointing to windows-build-agents, which is the VMSS that you created.

6. Click **Save and run** button again.

      ![](images/m3-img40.png)

7. Click **View** on **"This pipeline needs permission to access a resource before this run can continue"** pop-up.

      ![](images/m3-img41.png)

8. On **Waiting for review page**, click on **Permit**.

      ![](images/m3-img42.png)

9. Next on **"Permit access?"** pop-up, click **Permit**.

      ![](images/m3-img43.png)


   > **Note**: At this point the job will queue up to run. This step may take some time to spin up a build agent in the VMSS. During this time, if you go back to VMSS dashboard you will see that the instance is getting created

9. In a few more minutes, the job will start to have some activity as shown the example below:

      ![](images/m3-img44.png)

10. After it finishes you can see scan done by Defender for DevOps. To do that click **Microsoft Security DevOps** section in the left and you will see the output of the actions that were done as shown below:

      ![](images/m3-img45.png)



