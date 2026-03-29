# DevOps Git Configuration and CI/CD

# Azure Data Engineering: In-Depth CI/CD & DevOps
This repository documents my technical deep-dive into automating data pipelines using Git and Azure DevOps.

## 🚀 Key Learning Objectives
I Understand the transition from manual deployments to a professional automated CI/CD lifecycle within **Azure Data Factory (ADF)**.

### 1. Git Integration & Version Control
*   **Source Control:** Configured ADF to sync with Azure DevOps Git/GitHub.
*   **Collaboration Branch:** Learned to use the `main` branch for syncing changes from multiple developers.
*   **Feature Branching:** Implemented a branching strategy to develop features in isolation before merging via Pull Requests (PRs).

### 2. The Publishing Mechanism (`adf_publish`)
*   Understood the unique role of the `adf_publish` branch.
*   Learned how ADF generates **ARM (Azure Resource Manager) Templates** automatically when clicking the 'Publish' button.
*   Explored how these templates act as the "source of truth" for deployments.

### 3. Automated Release Pipelines
*   **Continuous Integration (CI):** Automating the validation of code during the PR process.
*   **Continuous Delivery (CD):** Setting up Release Pipelines in Azure DevOps to move code across environments:
    *   `Development` -> `UAT/Test` -> `Production`
*   **Triggers:** Configuring automatic deployments whenever the `adf_publish` branch is updated.

### 4. Environment Parameterization
*   Mastered the use of **Pipeline Parameters** and **Global Parameters**.
*   Learned how to dynamically swap Connection Strings and Linked Service configurations so the same pipeline works across different environments (Dev vs. Prod) without manual edits.

## 🛠 Tech Stack
*   **Service:** Azure Data Factory (V2)
*   **Platform:** Azure DevOps
*   **Version Control:** Git
*   **Infrastructure:** ARM Templates

###  Step 1: Feature Development & Local Testing
The process begins with an individual developer working in a dedicated environment.

*  Action: Create a new Feature Branch (e.g., feature/login-pipeline) from the collaboration branch (usually main).
*  Task: Develop your pipelines, datasets, and linked services.
*  Validation: Use the Debug button in ADF to test the pipeline logic without affecting the production data.
###  Step 2: Pull Request (PR) & Code Review
Once development is complete, the code must be merged into the shared repository.

*  Action: Create a Pull Request in Azure DevOps from your feature branch to the main branch.
*  Review: A lead developer or peer reviews the JSON code changes for best practices and naming conventions.
*  Merge: Once approved, the feature branch is merged into main.
###  Step 3: Generating ARM Templates (The "Publish" Phase)
This is a unique step specific to Azure Data Factory that bridges the gap between Git and Deployment.

*  Action: Switch to the main branch in the ADF portal and click the Publish button.
*  Result: ADF internally validates the code and generates ARM (Azure Resource Manager) Templates.
*  Storage: These templates (JSON files) are automatically saved into a hidden system branch called adf_publish.
### Step 4: Configuring the Release Pipeline
In Azure DevOps, you set up the automation "engine" that moves the code.

*  Artifact Source: Point the Release Pipeline to the adf_publish branch of your repository.
*  Trigger: Enable Continuous Deployment Trigger so the pipeline starts automatically whenever a new "Publish" occurs.
*  Stages: Define your environments (e.g., Dev, UAT, Production).
### Step 5: Environment Parameterization & Deployment
The final step ensures the pipeline connects to the right data sources in each environment.

*  Action: Use the ARM Template Deployment task in the Release Pipeline.
*  Override Parameters: This is the most critical part. You must provide the specific Connection Strings, Secret Keys, or Folder Paths for the target environment (e.g., swapping a dev-blob-storage link for prod-blob-storage).
*  Execution: Run the release. The pipeline will deploy the exact logic from your Dev environment into the Production ADF instance.
