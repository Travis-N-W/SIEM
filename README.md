# SIEM Implementation on Microsoft Azure

## 📸 Project Screenshots
Click [here](https://github.com/Travis-N-W/Active-Directory/tree/main/screenshots) to view all screenshots.

## Brief Objective
This project focuses on implementing a **Security Information and Event Management (SIEM) solution** on **Microsoft Azure** by integrating **MISP** (Malware Information Sharing Platform) with **Azure Sentinel** using the **MISP2Sentinel** data connector. The goal was to aggregate threat intelligence feeds, including indicators of compromise (IoCs) and related contextual data from MISP, providing hands-on experience in SIEM implementation and threat intelligence processing.

## Skills Learned
- SIEM Implementation
- Threat Intelligence Integration
- Cloud Security Solutions

## Tools Used
- Microsoft Azure
- Visual Studio Code (VS Code)
- MISP (Malware Information Sharing Platform)
- Docker

## Steps

### 1. **Provisioning an Azure Virtual Machine**
- Created an **Ubuntu Server 24.04 LTS** virtual machine in Azure.
- Configured default settings and deployed the VM in the **East US** region.
- Established an SSH connection to the VM using **Azure CLI**.

### 2. **Installing Docker**
- Followed the official Docker installation guide: [Docker Installation on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).
- Verified the installation by executing `hello-world` in the CLI.

### 3. **Deploying MISP in Docker**
- Cloned the MISP Docker repository from GitHub:
  ```bash
  git clone https://github.com/MISP/misp-docker.git
  ```
- Navigated to the repository folder and followed the README instructions:
  ```bash
  cd misp-docker
  cp template.env .env
  nano .env
  ```
- Configured **BASE_URL** in the `.env` file using the VM’s public IP: `https://52.186.169.243`.
- Opened **port 443** in **Azure Network Security Groups (NSG)** for external access.
- Deployed MISP and accessed the GUI.
- Changed the default admin password for security purposes.

### 4. **Enabling MISP Threat Feeds**
- Imported feed configurations from MISP:
  ```bash
  curl -O https://github.com/MISP/MISP/blob/2.4/app/files/feed-metadata/defaults.json
  ```
- Enabled selected feeds in the **MISP GUI**.

### 5. **Setting Up Microsoft Sentinel**
- Configured **Microsoft Sentinel** in Azure.
- Installed the **MISP2Sentinel** Data Connector from the **Sentinel Content Hub**.
- Followed integration instructions from [MISP2Sentinel GitHub](https://github.com/cudeso/misp2sentinel).

### 6. **Configuring Azure App Registration**
- Created an **App Registration** in the **Azure Portal**.
- Documented:
  - **Client ID**
  - **Object ID**
  - **Tenant ID**
- Generated a **Client Secret** and saved it securely.

### 7. **Granting Permissions in Azure Sentinel**
- Assigned **Microsoft Sentinel Contributor** role to the registered application.
- Configured access in **Log Analytics Workspaces**.

### 8. **Setting Up Azure Key Vault**
- Created a **Key Vault** to store secure values.
- Generated a **MISP API Key** and stored it in the Key Vault.

### 9. **Deploying the Function App**
- Created a **Function App** with:
  - **Python 3.11 runtime**
  - **App Service hosting plan**
  - **East US region**
- Downloaded and deployed the **MISP2Sentinel** function app in **VS Code**.
- Configured **environment variables** in Azure:
  ```bash
  tenant_id, client_id, client_secret, workspace_id, mispurl, AzureFunctionsJobHost_functionTimeout
  ```

### 10. **Verifying Integration**
- Tested function app by manually triggering a run.
- Verified logs for successful API communication.
- Checked **ThreatIntelligenceIndicator** table in Sentinel for incoming data.

### 11. **Final Validation & Cleanup**
- Confirmed data flow from **MISP to Sentinel**.
- Verified **successful IoC ingestion** in Sentinel.
- Deleted all resources after confirming functionality.

## Results
- Successfully integrated **MISP** with **Azure Sentinel**.
- Verified the ingestion of threat intelligence indicators into **Microsoft Sentinel**.
- Created a **functional SIEM** pipeline for threat monitoring and detection.



