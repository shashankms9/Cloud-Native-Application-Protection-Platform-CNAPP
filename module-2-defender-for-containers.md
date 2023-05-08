# Module 2 - Defender for Containers

## Objectives
This exercise guides you on how to validate and use Defender for Containers.

### Exercise 1: Install Docker Desktop

First you need to install Docker Desktop so that we can oush a vulnerable image to our existing Azure Container registry registy.

1. Navigate to the below URL to download the Docker and click on **Download Docker Desktop for Windows**.

   ```
   https://www.docker.com/products/docker-desktop
   ```
    
   ![Download Docker](Images/download-docker.png)
    
2. Once downloading is completed, open **File Explorer** from the LabVM and click on **Downloads** **(1)**. Then double-click on **Docker Desktop Installer** **(2)** to install Docker.

   ![Install Docker](Images/install-docker.png)

3. In the Configuration tab to add shortcut to desktop, click on **Ok**.

4. Installation will take around 5 mins to complete. Once the installtion succeeded, click on **Close and restart**. Your LabVM will be restarting to complete docker installation.

   ![Install Docker](Images/docker-close-restart.png)

5. Once the LabVM is restarted. Search for PowerShell in Search bar and select **Windows PowerShell**.

   ![Open Powershell](Images/open-powershell.png)

6. Verify your docker version by executing in PowerShell 

   ```
   docker version
   ```

   You may see an output like the one below:

   ![Docker Version in Powershell](Images/docker-version.png)


### Exercise 2: Download vulnerable image from Docker Hub into the Container Registry

Now you will use Docker to download a vulnerable image from it and push it into the Container Registry you created using the ARM template in Lab 1.

1. Navigate to the Azure Portal, search for **container** **(1)** in the search box and select **Container registries** **(2)**.

   ![Container registry in Azure](Images/search-cr.png)

2. Open the Container Registry named **<inject key="Container registry" enableCopy="true"/>**.

   ![Container registry open](Images/select-cr.png)

3. In the Overview of it, verify the Login server name only. 

   ![ACR server name](Images/copy-crname.png)

4.	Switch back to PowerShell, you will also need to login to your Azure subscription via **az login**. Enter the following **Email/Username** and **Password** in the browser and click on **Sign in**:

   * Email/Username: **<inject key="AzureAdUserEmail" enableCopy="true"/>** 

   * Password: **<inject key="AzureAdUserPassword" enableCopy="true"/>**

5. Make sure to update **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command.
   
   ```
   az acr login --name NameOfServer
   ```
 
   ![ACR login](Images/acr-login.png)

6. Download vulnerable image from docker hub, by running the command below in Powershell:

   ```
   docker pull vulnerables/web-dvwa
   ```

   ![ACR login](Images/docker-pull.png)

7. Check the image on your local repository by running the command below:

   ```
   docker pull vulnerables/web-dvwa
   ```

   ![Docker images](../Images/5dockerimages.png?raw=true)

8. Create an alias of the image by runnig the following command (replace *secteach365* in following instructions with the name of your server that you copied above): 

   ```
   docker tag vulnerables/web-dvwa secteach365.azurecr.io/vulnerables/web-dvwa
   ```

9. Check again the image on your local repository by running the command below: 

   ```
   docker images secteach365.azurecr.io/vulnerables/web-dvwa
   ```

   ![Docker local repository](Images/6dockerlocalrepo.png)


10. Run docker push to upload the new image to the azure repository and generate image scan (it can take some time), using the command below:

    ```
    docker push secteach365.azurecr.io/vulnerables/web-dvwa
    ```

    ![Docker push](Images/7dockerpush.png)

11. Then go to the Azure portal and find the Container registry you created.

12. Go to Repositories in the Container Registry. Notice the vulnerable image is found in the ACR repository.

    ![Image in ACR](Images/8imageinacr.png)

### Exercise 3: Investigate the recommendation for vulnerabilities in ACR

Once a vulnerable image has been pushed to the Azure Container Registry registry, then Microsoft Defender for Containers will start scanning the image for vulnerabilities, by using Qualys. You will now look into the recommendation in Microsoft Defender for Cloud for this. 
 
 1. Go to **Microsoft Defender for Cloud** in the **Azure Portal**.
 2. Go to the **Recommendations** tab in Defender for Cloud.
 3. In the **Resource type** filter, have it equal **Container registries**. <br />

 ![Recommendation for vulnerabilities in ACR](../Images/9recommendation.png?raw=true)
 4. Click on the recommendation **Container registry images should have vulnerability findings resolved** to get more details about it. <br />
 ![Recommendation for vulnerabilities in ACR More details](../Images/10recommendationmoreinfo.png?raw=true)
 <br />
 5. Look around at what's available in the recommendation. Take note of the Remediation Steps.
<br />
  ![Remediation Steps](../Images/remsteps.png?raw=true)
  <br />
 6. Select the vulnerability **Container registry images should have vulnerability findings resolved** to get more details about the patch available for it and how to remediate it.
 <br />
 ![Debian](../Images/11debian.png?raw=true)
 

