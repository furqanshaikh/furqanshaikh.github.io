---
layout: post
title: Integrating SailPoint with CyberArk Using SCIM Server Without AIM Credential Provider
---

### Introduction

Integrating SailPoint with CyberArk allows for streamlined identity governance and privileged access management (PAM). With CyberArk's SCIM (System for Cross-domain Identity Management) server, organizations can manage privileged accounts and users in SailPoint without relying on the AIM Credential Provider. This post will walk you through the steps of setting up a SailPoint-CyberArk integration using the SCIM server, enabling you to query, modify, and manage privileged data without the AIM Credential Provider.

---

### Prerequisites

Before starting the integration, ensure the following components are installed:

#### CyberArk Requirements:
- CyberArk SCIM Server v1.3.5 or above
- CyberArk Vault (with PACLI for querying and managing privileged data)

#### SailPoint Requirements:
- SailPoint IdentityIQ v7.1 patch 2 or above
- SailPoint PAM Module

#### System Requirements:
- **Windows Server 2016 or 2019**
- **Java Version 1.8 (64-bit OpenJDK recommended)**
- **8-core Processor, 32 GB RAM**

---

### Step-by-Step Guide

#### 1. **Download and Set Up SCIM Server**

1. Download the CyberArk SCIM distribution from the CyberArk Marketplace.
2. Extract the contents from the zip file and move the `CyberArk-SCIM` folder to your `C:\` drive.
3. Verify that the folder contains essential files:
    - `CAScimServer-<version>.jar`
    - `PACLI`
    - Configuration files (e.g., `config.yml`, `globalConfig.yml`)

#### 2. **Install Java**

SCIM server requires Java to function. Follow these steps to install and configure Java:

1. Download Java 1.8 (64-bit version) from [here](https://www.oracle.com/java/technologies/javase-downloads.html).
2. After installing Java, set the `%JAVA_HOME%` environment variable:
    - Open **System Properties > Advanced > Environment Variables**.
    - Add `C:\Program Files\Java\bin` to the system's path.

#### 3. **Pre-installation Configuration**

Before proceeding with the SCIM installation, configure the environment variables and ensure system readiness:

1. **Configure PACLI Path**:
    - In the system environment variables, append the PACLI path to the system's `Path` variable: `C:\CyberArk-SCIM\PACLI`.

2. **Enable CyberArk Vault Platform**:
    - Log in to the CyberArk PVWA as an admin.
    - Navigate to **Administration > Platform Management** and activate the CyberArk Vault platform.

#### 4. **Install and Configure SCIM Server**

1. Open a command prompt as an administrator and navigate to the `C:\CyberArk-SCIM` directory.
2. Run the SCIM installation command:
   ```bash
   SCIMInstaller.exe -SailPoint
   ```
   **Note**: The `-SailPoint` flag is case-sensitive.

3. Follow the installation prompts, including entering the necessary Vault and SCIM configuration parameters from your pre-installation checklist.

#### 5. **Configure SailPoint to Communicate with SCIM Server**

1. Create a privileged account in the CyberArk Vault for SailPoint integration.
    - This account will be used by SailPoint to authenticate against the CyberArk SCIM server.

2. Modify the `globalConfig.yml` in the CyberArk-SCIM folder to reflect the SailPoint-specific configurations.

3. In SailPoint, configure a new CyberArk application in **IdentityIQ** using the following information:
    - **SCIM Server URL**: `http://<SCIM_Server_IP>:8080/CyberArk/scim/v2/`
    - **Authentication**: Use basic authentication with the SailPoint-user account created in CyberArk.

#### 6. **Testing the SCIM Server**

Test the SCIM server by accessing the Swagger UI:

1. Open a browser and navigate to:
   ```
   http://<SCIM_Server_IP>:8080/swagger
   ```

2. Test basic SCIM operations, such as querying users and groups, to ensure the server is operational and configured correctly.

3. Alternatively, use the following `curl` command to test connectivity:
   ```bash
   curl -u SailPoint-user:<password> http://<SCIM_SERVER_IP>:8080/CyberArk/scim/v2/ResourceTypes
   ```

#### 7. **Configure OAuth for Secure Authentication (Optional)**

If you want to integrate OAuth for additional security, configure it in the `globalConfig.yml`:

1. In SailPoint, generate the required client ID and secret for OAuth authentication.
2. Update the `globalConfig.yml` with your OAuth provider's details (e.g., Azure AD or Okta):
   ```yaml
   oauth2:
     jwksURI: "https://login.microsoftonline.com/<tenant-id>/discovery/v2.0/keys"
     issuer: "https://login.microsoftonline.com/<tenant-id>/v2.0"
     usernameField: "preferred_username"
   ```

3. Restart the SCIM server to apply the changes.

---

### Conclusion

By following these steps, you can integrate SailPoint IdentityIQ with CyberArk using the SCIM server without relying on the AIM Credential Provider. This setup allows you to manage privileged accounts and users seamlessly through SailPoint's PAM module, ensuring secure and efficient access management.

---

### Additional Resources

- [CyberArk SCIM Server Documentation](https://cyberark.com)
- [SailPoint IdentityIQ PAM Integration Guide](https://sailpoint.com)

