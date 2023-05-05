# Module 4 – Integrating Defender for DevOps with GitHub Advanced Security

## Objectives
In this exercise, you will learn how to configure GitHub Connector in Defender for DevOps.

### Exercise 1: Connecting your GitHub organization

1.	Login to your Azure Portal and navigate to Defender for Cloud dashboard
2.	In the left navigation pane, click **Environment settings** option
3.	Click the **Add environment** button and click **GitHub (preview)** option. The **Create GitHub connection** page appears as shown the sample below.

![Azure ADO Connector](../Images/Picture1.png?raw=true)

4.	Type the name for the connector, select the subscription, select the Resource Group, which can be the same you used in this lab and the region. 
5.	Click **Next:select plans >** button to continue.
6.	In the next page leave the default selection with **DevOps** selected and click **Next: Authorize connection >** button to continue. The following page appears:

![Azure ADO Connector - Authorize](../Images/Pic2.png?raw=true)


7.	Click **Authorize** button. Now Click **Install** button under Install Defender for DevOps app. If this is the first time you’re authorizing your DevOps connection, you’ll receive a pop-up screen, that will ask you confirmation of which repository you'd like to install the app. 

![Azure ADO Connector - Install](../Images/Pic3.png?raw=true)

![Azure ADO Connector - Choose Repository](../Images/Pic4.png?raw=true)

8. Choose **All repositories** or **only select repositories** as per your choice and click on **Install**

![Azure ADO Connector - Install](../Images/Pic5.png?raw=true)

9. Once you click on install, you’ll receive another pop-up window requesting to enter the password inorder to confirm access   

10. Back to the Azure portal, you’ll notice that the extension is installed > Click on **Review and Create** button to continue.  
11. Navigating to the **Environment Settings** under **Microsoft Defender for Cloud**, you’ll notice the GitHub Connection was successfully created. 

![Azure ADO Connector - Confirming the connector](../Images/Pic6.png?raw=true)

### Exercise 2: Configure the Microsoft Security DevOps GitHub action

To setup GitHub action:
1.	Login to the GitHub repo that you created in Exercise 4.
2.	Select a repository on which you want to configure the GitHub action.
3.	Select **Actions** as shown in the image below 

![Azure GitHub - Actions](../Images/Pic7.png?raw=true)

4.	Select **New Workflow**

![Azure GitHub - New workflow](../Images/Pic8.png?raw=true)

5.	In the text box, enter a name for your workflow file. For example **msdevopssec.yml**

![Azure GitHub - New workflow](../Images/Pic9.png?raw=true)

6.	Copy and paste the following sample action workflow into the **Edit new file** tab. 

~~~~~~
name: MSDO IaC Scan

on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
    
  pull_request:
    branches: [ main ]

  workflow_dispatch:

jobs:
  security:
    runs-on: windows-latest
    continue-on-error: false
    strategy:
      fail-fast: true
      
    steps:
    - uses: actions/checkout@v3
    
    - uses: actions/setup-dotnet@v3
      with:
        dotnet-version: |
          5.0.x
          6.0.x
          
    - name: Run Microsoft Security DevOps
      uses: microsoft/security-devops-action@preview
      continue-on-error: false
      id: msdo
      with:
        categories: 'IaC'

    - name: Upload alerts to Security tab
      uses: github/codeql-action/upload-sarif@v2
      with:
        sarif_file: ${{ steps.msdo.outputs.sarifFile }}
~~~~~~~

7.	Click on **Start Commit** **Commit new file**

![Azure GitHub - Commit](../Images/Pic10.png?raw=true)

![Azure GitHub - Commit](../Images/Pic11.png?raw=true)

The process can take up to one minute to complete. 
A workflow gets created in your repositories github folder with the above copied yml file 

![Azure GitHub - Workflow example](../Images/Picture11.png?raw=true)

8.	Select **Actions** and verify the new action is running/completed running. 

![Azure GitHub - New Action](../Images/Picture12.png?raw=true)

9.	Once this job completes running, navigate to the Security tab > Click on Code scanning 

NOTE: if you don’t see anything is because your code scanning feature is disabled in GitHub. Refer to the prerequisites section of this lab to review the instructions to enable. 

10.	If you see No code scanning alerts here, In the filter of Code scanning tab, choose is:open tool: Notice the available tools Defender for DevOps uses.

![Azure GitHub - Code Scanning](../Images/Picture13.png?raw=true)

11.	Code scanning findings will be filtered by specific MSDO tools in GitHub. These code scanning results are also pulled into Defender for Cloud recommendations.

![Azure GitHub - Code Scanning Findins](../Images/Picture14.png?raw=true)

