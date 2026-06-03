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
- Task 3: Migrate to Azure Database for PostgreSQL Flexible Server using Predefined Tasks
- Task 4: Migrate to Azure Blob Storage using Predefined Tasks
- Task 5: Migrate to Azure Service Bus using Predefined Tasks
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

### Task 3: Migrate to Azure Database for PostgreSQL Flexible Server using Predefined Tasks

In this task, you will migrate the application's database layer from the local PostgreSQL instance to Azure Database for PostgreSQL Flexible Server using a predefined migration task. Copilot will generate a migration plan, update configuration files, provision Azure resources, and apply the required code changes.

1. For this workshop, click the **Run Task** in the Assessment Report, on the right of the row **Secure Azure Database for PostgreSQL with Managed Identity**.

   ![Confirm Solution](images/new/a1.png)

1. After clicking the **Run Task** button in the Assessment Report, the Copilot Chat panel will open with Agent Mode.

1. The Copilot Agent will first analyze the project and generate a migration plan.

1. After the plan is generated, Copilot Chat will stop with two generated files: **plan.md** and **progress.md**. 

1. If prompted, enter "Continue" or "Proceed" in the chat to confirm and execute the plan.

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

   ![Confirm Solution](images/35.png)

1. Review the proposed code changes and click **Keep** to apply them.

   ![Confirm Solution](images/new/a4.png)

   >**Note:** When prompted, click **Continue**/**Allow** in chat notifications or type **y**/**yes** in terminal as Copilot Agent follows the plan and leverages agent tools to create and run provisioning and deployment scripts, fix potential errors, and finish the deployment. **DO NOT interrupt** when provisioning/**Todos** or deployment scripts are running.

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.
   
In this task, you have migrated the application’s database from a local PostgreSQL instance to Azure Database for PostgreSQL Flexible Server by generating and executing an automated migration plan.

### Task 4: Migrate to Azure Blob Storage using Predefined Tasks

In this task, you will replace the application's dependency on AWS S3 with Azure Blob Storage. Using predefined tasks, Copilot will update the storage configuration, generate necessary migration scripts, provision blob storage resources, and apply all required code modifications.

1. Click the **Run Task** in the Assessment Report, on the right of the row `Storage Migration (AWS S3)` - `Migrate from AWS S3 to Azure Blob Storage`.
 
   ![](images/23.png)

1. When prompted, click **Continue**/**Allow/Enable more AI features** in chat notifications or type **y**/**yes** in terminal as Copilot Agent follows the plan and leverages agent tools to create and run provisioning and deployment scripts, fix potential errors, and finish the deployment.

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

1. The following steps are the same as the above PostgreSQL server migration.

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.
   
In this task, you have replaced AWS S3 with Azure Blob Storage by updating storage configurations, provisioning cloud resources, and applying the required application code changes.

### Task 5: Migrate to Azure Service Bus using Predefined Tasks

In this task, you will migrate the application's messaging component from RabbitMQ to Azure Service Bus. Copilot will generate a migration plan, update messaging libraries and configurations, provision Service Bus resources, and refactor the project to use Azure-native messaging services.

1. Click the **Run Task** in the Assessment Report, on the right of the row `Messaging Service Migration (Spring AMQP RabbitMQ)` - `Migrate from RabbitMQ(AMQP) to Azure Service Bus`.

   ![](images/21.png)
   
1. When prompted, click **Continue**/**Allow** in chat notifications or type **y**/**yes** in terminal as Copilot Agent follows the plan and leverages agent tools to create and run provisioning and deployment scripts, fix potential errors, and finish the deployment. 

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

1. The following steps are the same as the above PostgreSQL server migration.

   ![](images/22.png)

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.
   
In this task, you have migrated the messaging layer from RabbitMQ to Azure Service Bus by refactoring application messaging, updating configurations, and provisioning Azure messaging resources.   
   
### Task 6: Expose health endpoints using Custom Tasks

In this task, you will create a custom Copilot task to expose health endpoints using Spring Boot Actuator. You will define a task prompt, attach external documentation as reference, let Copilot generate the required changes, and apply the modifications to enable application health monitoring.

1. Open the sidebar of `GITHUB COPILOT MODERNIZATION`. Click the `+` button in the **Tasks** view to create a Custom Skill.

   ![Create Formula From Source Control](images/create-formula-from-source-control.png)

1. A **Create a Skill** form opens with the following fields. Fill them in as shown below:

     - **Skill Name:** `expose-health-endpoint` **(1)**
     - **Skill Description:** This skill helps add Spring Boot Actuator health endpoints for Azure Container Apps deployment readiness. **(2)** 
     - **Skill Content:**  You are a Spring Boot developer assistant. Follow the **Spring Boot Actuator documentation** to add basic health endpoints required for Azure Container Apps deployment. **(3)**

   ![](images/new/b1.png)
                     
1. Click **Save** to create the task.

   ![](images/new/b2.png)

1. Click the **Run Task** button to trigger the custom task.

   ![](images/new/b3.png)
   
   >**Note** : If you see **Run Skill** instead, click **Run Skill** to trigger it.

   ![](images/new/c6.png)

1. Wait for the predefined deployment prompt to appear in the Copilot Chat panel with Agent Mode enabled. Click inside the prompt text in Copilot Chat. Edit and add the following sentence to the prompt.

   ```
   Resource link : https://docs.spring.io/spring-boot/reference/actuator/endpoints.html
   ```
   ![](images/gc35.png)
   
1. Review the proposed code changes and click **Keep** to apply them.

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.
   
In this task, you have created and executed a custom Copilot task to enable Spring Boot Actuator health endpoints for application monitoring and Azure readiness probes.

### Task 7: Containerize Applications

In this task, you will containerize the web and worker modules of the application using Containerization Tasks. Copilot will generate Dockerfiles, build container images, resolve build issues, and prepare the application for cloud deployment inside containers.

1. Open the sidebar of `GITHUB COPILOT MODERNIZATION`. In **Tasks** view, click the **Run Task** button of **Common Tasks** -> **Containerize Tasks** -> **Containerize Application**.
  
    ![Run Containerize Application task](images/containerization-run-task.png)

1. When prompted, click **Continue** or **Allow** in chat notifications, or type **y** / **yes** in the terminal as Copilot Agent follows the plan and leverages agent tools to create and run provisioning and deployment scripts, fix potential errors, and complete the deployment.  

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

2. A predefined prompt will be populated in the **Copilot Chat panel** with **Agent Mode** enabled.  
   Copilot Agent will analyze the workspace and create a file named **containerization-plan.copilotmd** containing the containerization plan.

   ![Containerization prompt and plan](images/containerization-plan.png)

1. View the plan and collaborate with Copilot Agent as it follows the **Execution Steps** in the plan by clicking **Continue**/**Allow** in pop-up chat notifications to run commands. Some of the execution steps leverage agentic tools of **Container Assist**.
    
1. Copilot Agent will help generate Dockerfile, build Docker images and fix build errors if there are any. Click **Keep** to apply the generated code.

   >**Note** : Please wait while Copilot completes the task, which may take approximately 20–30 minutes.

1. Navigate to the **worker (1)** folder in VS Code and verify that the **Dockerfile (2)** is created.

    ![](images/new/b4.png)

In this task, the application was containerized using the GitHub Copilot App Modernization Containerization Task, where Copilot generated the containerization-plan.copilotmd, created Dockerfiles for the application modules, and successfully built Docker images with all changes accepted via “Keep”. These Docker artifacts (Dockerfiles and images) are then used as deployment inputs in Task 8, where the application is provisioned and deployed to Azure Kubernetes Service.

### Task 8: Deploy to Azure

In this task, you will deploy the fully modernized and containerized application to Azure using a predefined deployment task. Copilot will generate a deployment plan, provision all required Azure resources, create deployment scripts, execute the deployment, and verify successful provisioning in the Azure portal.

1. Open the sidebar of `GITHUB COPILOT APP MODERNIZATION`. In **Tasks** view, click the **Run Task** button of **Common Tasks** -> **Deployment Tasks** -> **Provision Infrastructure and Deploy to Azure**.

    ![Run Deployment task](images/deployment-run-task.png)

1. Wait for the predefined deployment prompt to appear in the Copilot Chat panel with Agent Mode enabled. Click inside the prompt text in Copilot Chat. **Edit** the last sentence of the prompt to **Hosting service: AKS**.

   ![Deployment progress](images/image.png)

   > **Note:** If you are prompted to select **az login**, follow the steps below:

1. Select **Work or school account (1)** from the prompt and click **Continue (2)**.

      ![](images/new/b9.png)

1. You will see the **Sign into Microsoft Azure** page. Enter the following credentials:

      - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

1. Enter the password:

      - **Password:** <inject key="AzureAdUserPassword"></inject>

1. When prompted, select **No, sign in to this app only** and continue.

      ![](images/new/b5.png)

1. Return to the **Visual Studio Code** terminal. You will be prompted to select a subscription from a list. Enter **1** and press **Enter**.

      ![](images/new/b6.png)

      > **Note:** If the **az login** prompt does **not appear in the browser**:
      >
      > 1. Open a **terminal in VS Code**.
      > 2. Ensure the terminal is opened under the **asset-manager** folder.
      > 3. Run the `az login --use-device-code` command and complete the sign-in process:

1. Click **Continue**/**Allow** if pop-up notifications to let Copilot Agent analyze the project and create a deployment plan in **plan.copilotmd** with Azure resources architecture, recommended Azure resources for project and security configurations, and execution steps for deployment.

1. View the architecture diagram, resource configurations, and execution steps in the plan. Click **Keep** to save the plan and type in **Execute the plan** to start the deployment.

1. When prompted, click **Continue**/**Allow** in chat notifications or type **y**/**yes** in terminal as Copilot Agent follows the plan and leverages agent tools to create and run provisioning and deployment scripts, fix potential errors, and finish the deployment. You can also check the deployment status in **progress.copilotmd**. 

   >**Note** : **Do not interrupt** while the provisioning or deployment scripts are running.

   >**Note** : Please wait while Copilot completes the task, which may take approximately 30–45 minutes.

1. Once deployment completed you can view the deployment status as below: 

   ![Deployment progress](images/image2.png)

    > **Note:** The response generated by the above prompt may vary. If your prompt returns an error, press **Ctrl + C** to copy the error and **Ctrl + V** to paste it in the Copilot chat and run. GitHub Copilot should automatically resolve the errors.

    >**Note:** If you face error: **Hmmm… can't reach this page**, terminate the chat and add the below given prompt.

    ```
    Migrate the PostgreSQL database to Azure Database for PostgreSQL Flexible Server, and deploy only the web application to Azure Kubernetes Service (AKS).
    ```
 
1. Navigate to Pods and check if they are in running state and try to access the External IP.

   >**Note:** If you encounter any errors copy those errors and paste in Copilot chat. GitHub Copilot should automatically resolve the errors.

1. In the Edge browser, navigate to the **Azure portal** and select **Resource Groups**.

   ![Deployment progress](images/15.png)

1. On the **Resource Groups** page, select the newly created resource group.

   ![Deployment progress](images/14.png)

1. You will now see that all the resources have been successfully deployed in the Azure portal.

   ![Deployment progress](images/image1.png)

1. To access the web application, Navigate to the **AKS resource** in the Azure portal.

   ![Deployment progress](images/new/c1.png)

1. From the left navigation pane, expand **Kubernetes resources (1)**, click on **Services and Ingresses (2)** and click the **IP address (3)** of the service.

   ![Deployment progress](images/new/c2.png)

1. You will be redirected to a new tab where your web application is displayed.

   ![Deployment progress](images/gc31.png)
   
In this task, you have deployed the fully modernized and containerized application to Azure Kubernetes Service (AKS) by provisioning infrastructure, executing deployment scripts, and validating resources in the Azure portal.

## Summary

In this lab, you have completed the following:

- Assessed Your Java Application
- Upgraded Runtime and Frameworks
- Migrated to Azure Database for PostgreSQL Flexible Server using Predefined Tasks
- Migrated to Azure Blob Storage using Predefined Tasks
- Migrated to Azure Service Bus using Predefined Tasks
- Exposed health endpoints using Custom Tasks
- Containerized Applications
- Deployed to Azure

### You have successfully completed the lab!

In this lab, you used the **GitHub Copilot App Modernization** extension to assess, modernize, containerize, and deploy a Java application to Azure through a complete end-to-end modernization workflow. You evaluated the existing application, upgraded the Java runtime and frameworks, migrated the database to **Azure Database for PostgreSQL Flexible Server**, moved storage to **Azure Blob Storage**, transitioned messaging to **Azure Service Bus**, enabled **health monitoring with Spring Boot Actuator**, containerized the application using **Docker**, and successfully deployed it to **Azure Kubernetes Service (AKS)**. This lab demonstrated how GitHub Copilot accelerates Java application modernization and cloud migration with automation, intelligence, and minimal manual effort.
