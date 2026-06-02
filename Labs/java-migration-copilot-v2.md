# GitHub Copilot Java App Modernization

### Estimated Duration: 4 Hours 

## 📖 Overview

In this lab, you will modernize **Contoso Ltd.'s** Asset Manager application using **GitHub Copilot App Modernization**. The application currently runs on legacy Java technologies and depends on multiple infrastructure components that are not optimized for modern cloud environments.

Using GitHub Copilot App Modernization, you will perform a **complete end-to-end modernization journey**. You will begin by assessing the application to understand its current architecture, dependencies, and migration readiness. Based on the assessment recommendations, you will upgrade application frameworks, migrate supporting services to Azure-native alternatives, and implement operational improvements required for cloud deployment.

Throughout the lab, **GitHub Copilot** will assist with planning, code generation, infrastructure provisioning, configuration updates, and deployment activities. The modernization process includes migrating the PostgreSQL database to Azure Database for PostgreSQL Flexible Server, replacing AWS S3 with Azure Blob Storage, replacing RabbitMQ with Azure Service Bus, enabling application health monitoring through Spring Boot Actuator, containerizing application components, and deploying the final solution to Azure Kubernetes Service (AKS).

By the end of the lab, the Asset Manager application will be transformed into a modern, containerized, cloud-native solution running on Azure infrastructure.

## 🎯 Objectives

You will be able to complete the following tasks:
- Task 1: Assess Your Java Application
- Task 2: Upgrade Runtime and Frameworks
- Task 3: Generate and Review the Modernization Plan
- Task 6: Expose health endpoints using Custom Tasks
- Task 7: Containerize Applications
- Task 8: Deploy to Azure

### Task 1: Assess Your Java Application

In this task, you will run and explore the sample Java application and use the GitHub Copilot App Modernization extension to assess the project. The assessment will identify code issues, framework versions, migration blockers, and recommendations to determine the application's readiness for modernization and migration to Azure.

1. On the **LabVM**, click **Start (1)** at the bottom of the screen, search for **Docker Desktop (2)**, and select **Docker Desktop (3)** from the menu.

   ![](images/11.png)
   
1. Click **Accept** to agree to the **Docker Subscription Service Agreement**.

   ![](images/gc22.png)

1. On the **Welcome to Docker** page, click **Skip**.

   ![](images/T1S3-0106.png)
   
1. On the **Welcome Survey** page, click **Skip**.

   ![](images/gc28.png)
   
1. On the **Sign in** page, click **Skip**.

   ![](images/gc29.png)
   
1. If an error indicates that **WSL needs updating**, follow the steps below:

   ![](images/new/b7.png)
   
   - From Windows Search, type **PowerShell (1)** and select **Windows PowerShell (2)**.

      ![](images/new/c4.png)

   - Run the following command.

      ```
      wsl --update
      ```

      ![](images/new/c5.png)

   - From the system tray, click the **arrow icon (1)**, right-click **Docker Desktop (2)**, and select **Quit Docker Desktop (3)** to stop the service.

      ![](images/new/b8.png)

   - Click **Start (1)** at the bottom of the screen, search for **Docker Desktop (2)**, and open the **Docker Desktop (3)** again.

      ![](images/11.png)

2. On the **LabVM**, click **Start (1)** at the bottom of the screen and select **File Explorer (2)** from the menu.

   ![](images/T1S7-0106.png)

1. In **File Explorer**, navigate to: `C:\LabFiles\java-migration-copilot-samples\asset-manager`

   ![](images/25.png)

1. In the File Explorer address bar, replace the path `C:\LabFiles\java-migration-copilot-samples\asset-manager` with **cmd**, then press **Enter**.

   ![](images/26.png)

1. This will open a Command Prompt window. In the Command Prompt window, type the following command and press **Enter**:

   ```
   scripts\startapp.cmd
   ```

   ![](images/27.png)

1. This will **use the local file system instead of S3 to store images** and **launch RabbitMQ and PostgreSQL using Docker**. 

1. Copy the **web application URL**, **RabbitMQ Management URL**, along with the **username** and **password**, and note them down.

   ![](images/29.png)

   > **Note:** If two Windows prompts appear, minimize them and let them run in the background. **Do NOT interrupt** the process.

   > ![](images/30.png)

   > **Note:** If you encounter any errors in the terminal, repeat steps to run the application again.

   > ![](images/new/c3.png)

1. In the Edge browser, open a new tab and enter **[http://localhost:8080](http://localhost:8080)**. You will be navigated to the **AWS S3 Asset Manager** web page.

   ![](images/31.png)

1. In a new browser tab, enter the following **URL (1)** and sign in using the credentials:

   ```
   http://localhost:15672
   ```

   - **Username:** guest **(2)**
   - **Password:** guest **(3)**
   - Click on **Login (4)**.

      ![](images/32.png)

1. You will be navigated to the **RabbitMQ Management** web page.

   ![](images/33.png)

1. From the **Lab VM** desktop, double-click on the **Visual Studio Code** shortcut on the desktop of your virtual environment.

   ![](images/5.png)

1. On the **Welcome to VS Code** page, click on **Continue with GitHub**. 

   ![](images/T1S17-0106.png)

1. Enter the following details to sign in:

   - Username: **odl-user-<inject key="DeploymentID" enableCopy="false"/>_clabs (1)**
   - Click on **Sign in with your identity provider (2)**.

      ![](images/T1S18-0106.png)

1. On the Single sign-on to CLoudLabs Organizations select **Continue**.

   ![](images/T1S19-0106.png)

1. On the Permissions requested window, click on **Accept**.

   ![](images/T1S20-0106.png)

1. On the Authorize Visual Studio Code page, click on **Continue** to select the account to authorize.

   ![](images/T1S21-0106.png)

1. Click on Authorize Visual Studio Code.

   ![](images/T1S22-0106.png)

1. When prompted, click **Open** to allow vscode.dev to launch the project in **Visual Studio Code**.

   ![](images/new/4.png)

1. On VS Code, close the Make it yours page by clicking on the **X** icon.

   ![](images/T1S24-0106.png)

1. Click on **Explorer (1)** and select **Open Folder (2)** from the options.

   ![](images/7.png)

1. From File Explorer, navigate to `C:\LabFiles\java-migration-copilot-samples` **(1)**, select the **asset-manager (2)** folder from the Quick Access section, and click on **Select Folder (3)**.

   ![](images/4.png)

1. On the pop-up window for **Do you trust the authors of the files in this folder?**, select **Yes, I trust the authors**.

    ![](images/8.png)

1. Click on the **Extensions (1)** button on the left-hand banner, search for **GitHub Copilot modernization (2)** and **Install (3)** the extension.

    ![](images/gc23.png)

1. In **GitHub Copilot Chat**, click the **model selector (1)** located below the prompt text box and select **Claude Sonnet 4.6 (2)** from the dropdown menu.

   ![](images/T1S29-0106.png)

1. Open the **GitHub Copilot modernization (1)** extension from the left panel. In the **QUICKSTART** view, click the **Start Assessment (2)** button to start the app assessment.

   ![](images/T1S30-0106.png)

1. On the Assessment Reports screen, select **Recommended Assessment** to proceed with the default evaluation setup.

   ![](images/new/7.png)

1. In the Recommended Assessment dialog, select the required domains and click **OK** to continue.

   ![](images/new/8.png)

1. Please wait until the assessment is completed and the report is generated. Once generated, it will automatically open in a new tab.
   
   > **Note:** The report generation may take about 5 minutes.

1. Review the **Assessment Report**. Select the **Issues** tab to view the proposed solutions for the issues identified in the report.

   ![](images/T1S34-0106.png)

In this task, you have successfully analyzed the existing Java application using GitHub Copilot App Modernization to identify framework versions, code issues, migration blockers, and readiness for modernization and cloud migration.   

### Task 2: Upgrade Runtime and Frameworks (Optional)

In this task, you will use predefined Copilot tasks to automatically upgrade the project’s Java runtime version and frameworks such as Spring/Spring Boot. Copilot will analyze the application, apply necessary version updates, recommend fixes, and commit changes in a new branch.

   >**Note** : This lab uses **Java 25**, which is already up to date. In real-world scenarios, applications may run on older Java versions (e.g., Java 8/11), and upgrading to the latest version is recommended for better security, performance, and compatibility.

1. From the **Github Copilot modernization (1)** from the left side, select **Upgrade Java Runtime & Frameworks (2)**. This will open the Copilot Chat panel with a predefined prompt to upgrade the Java runtime and frameworks **(3)**.

    ![Java Upgrade](images/new/T2S1-0106.png)

    ![Java Upgrade](images/new/T2S1a-0106.png)

1. If prompted to choose the Java or Springboot versions to upgrade to, select the latest versions available.

   ![](images/new/T2S2-0106.png)

1. The agent will check out a new branch and start upgrading the JDK version and Spring/Spring Boot framework. Click **Allow** for any requests from the agent whenever they appear.

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

   ![](images/new/c8.png)

1. If prompted, click **Allow** to grant the required permissions.

1. In the Visual Studio Code prompt, click **Allow** to sign in with GitHub.

   ![Confirm Solution](images/new/a2.png)

1. In the account selection prompt, choose **odl-user-<inject key="DeploymentID" enableCopy="false"/>_clabs** to proceed with authentication.

   ![Confirm Solution](images/new/a3.png)

   >**Note** : Do not select the **Fix CVE** or **Generate Unit Tests** options during this step, as they are not required for the current lab objectives.

   > ![](images/new/c9.png)

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.
   
In this task, you have successfully upgraded the Java runtime and Spring/Spring Boot frameworks using predefined Copilot tasks to ensure the application is secure, modern, and cloud-ready.   

### Task 3: Generate and Review the Modernization Plan

In this task, you will use GitHub Copilot to generate a comprehensive modernization plan based on the assessment report. The plan will outline the necessary steps, code changes, and infrastructure updates required to modernize the application and migrate it to Azure. You will review the generated plan, understand the proposed changes, and prepare for the subsequent migration tasks.

1. On the Assessment Report, select the following:

    - Target Service: **Azure Kubernetes Service (AKS) (1)**
    - Click on **Create Plan (2)**

        ![](images/new/T3S1-0106.png)

1. The Copilot Chat panel will open with a predefined prompt to generate a modernization plan based on the assessment report. 

    ![](images/T3S2-0106.png)

1. When prompted, click on **Allow** to run the agent that will analyze the application and generate a detailed modernization plan.

1. At the end, it will ask you **The plan is ready, what would you like to do?**, select **Review the plan first**.     

    ![](images/T3S3-0106.png)

In this task, you have successfully generated a comprehensive modernization plan using GitHub Copilot based on the assessment report. You have reviewed the proposed changes and are now prepared to execute the modernization tasks in the subsequent task.

### Task 4: Execute the Modernized Plan    

In this task, you will execute the modernization plan generated by GitHub Copilot App Modernization. The plan includes framework upgrades, Azure service migrations, security improvements, and containerization activities. GitHub Copilot Agent will analyze the project, apply code changes, generate configuration updates, provision required resources, and implement the modernization tasks defined in the plan. 

1. In the Copilot Chat panel, enter the following prompt to execute the modernization plan:

    ```
    Execute the modernization plan.

    Implement:
    - RabbitMQ to Azure Service Bus migration
    - AWS S3 to Azure Blob Storage migration
    - PostgreSQL Managed Identity integration
    - Azure Key Vault integration
    - Azure Storage File Share migration
    - Containerization
    Do not provision infrastructure or deploy the application yet.
    ```

    ![](images/new/T4S1-0106.png)

    > **Note:** When prompted click on **Allow** to let the agent run and implement the modernization tasks. This process may take approximately 30–40 minutes to complete.

    > **Note:** Do not interrupt while provisioning scripts, migration scripts, or code transformation tasks are running.

1. Note in the above prompt we have specifically asked the agent to **not provision infrastructure or deploy the application yet**, as we want to focus on code changes and framework upgrades in this step, and the infrastructure provisioning and deployment will be covered in the next tasks.    

1. During execution, GitHub Copilot **may** generate or update the following files:

   * progress.md
   * tasks.md
   * Additional migration and configuration files

    Review these files to monitor the modernization progress.

1. After the agent has completed executing the modernization plan, review the code changes, configuration updates, and migration scripts generated by the agent to understand the modifications made to modernize the application.

In this task, you have successfully executed the modernization plan using GitHub Copilot Agent to implement service migrations and code transformations required to modernize the application. You have reviewed the changes made to ensure the application is now modernized and ready for the next steps of infrastructure provisioning and deployment.