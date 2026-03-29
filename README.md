# DevOps Git Configuration and CI/CD

# Azure Data Engineering: In-Depth CI/CD & DevOps
This repository documents my technical deep-dive into Session 12 of the Azure Data Engineer training, focusing on automating data pipelines using Git and Azure DevOps.

## 🚀 Key Learning Objectives
In this session, I mastered the transition from manual deployments to a professional automated CI/CD lifecycle within **Azure Data Factory (ADF)**.

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

---
*Notes based on Session 12 of the Azurelib Academy Data Engineer Course.*
