---
layout: post
title: CyberArk SCIM Server Authentication Using Credential Files
---

### CyberArk SCIM Server Authentication Using Credential Files

The CyberArk SCIM server can authenticate to the CyberArk Vault using credential files, which is CyberArk's recommended method for enhanced security. This method avoids storing passwords directly and instead uses dynamically rotated credentials retrieved on demand.

Here's how the process works:

1. **Credential File Creation:**
   *   First, you need to identify the username associated with the SCIM-account object in the SCIM Config safe. This information is stored in the "UserName" file category property of the SCIM-account object.
   *   Next, create a credential file using the CyberArk `CreateCredFile` utility. The file name should be the same as the username identified in the previous step, with a ".cred" extension. For example, if the username is "SCIM-user", the credential file should be named "SCIM-user.cred".
   *   The `CreateCredFile` utility takes several parameters, including the username, password, hostname, and entropy file. The specific command to create the credential file is provided in the sources.
2. **Credential File Placement:** Once the credential file is created, it needs to be placed in the `c:\CyberArk-SCIM` folder along with its associated entropy file.
3. **SCIM Server Authentication:** When the SCIM server needs to authenticate to the Vault, it first checks for a credential file with the name "SCIM-user.cred" in the `c:\CyberArk-SCIM` directory. If this file is found, the SCIM server uses the username from the credential file and the credential itself to authenticate to the Vault. The AIM Credential Provider is not used in this scenario.
4. **Automatic Password Change:** When using credential files, the automatic password change feature is enabled. This means that every time the SCIM server logs into the Vault, a new randomized password is generated and updated in both the authentication file and the Vault.

**Fallback Mechanism:**

If a credential file named "SCIM-user.cred" is not found, the SCIM server will attempt to authenticate using the AIM Credential Provider.

**Log Verification:**

The sources provide examples of debug and trace logs that can be used to verify whether the SCIM server is using a credential file or the AIM Credential Provider for authentication.

**Additional Notes:**

*   The sources highlight that using the default authentication method (user-password credentials stored in the vault) can expose the password in Windows Audits if this feature is enabled at the OS level.
*   For existing SCIM server installations (version 1.3.4 and earlier), CyberArk recommends upgrading to version 1.3.5 or later to take advantage of the credential file authentication method.

By using credential files, the CyberArk SCIM server benefits from a more secure authentication method, reducing the risks associated with storing and managing passwords directly.


### What are the two internal authentication methods available for the CyberArk SCIM server?

The two internal authentication methods available for the CyberArk SCIM server are:

*   **CyberArk Credential Files (Recommended):** This method, introduced in SCIM version 1.3.5, enhances security by using dynamically rotated credentials instead of a stored password. CyberArk recommends this method.

    To implement this method, a credential file containing the username from the SCIM-account object must be created and stored in the `c:\CyberArk-SCIM` folder. When the SCIM server needs to authenticate to the Vault, it will prioritize using this credential file over the AIM Credential Provider.
*   **Username-password credentials stored in the vault (default):** This method uses the AIM Credential Provider to retrieve the username and password for the SCIM server from the CyberArk Vault. This method is the default but is less secure than using credential files because it requires storing the password in the Vault. The sources note that this method can expose the password in the Windows audit logs if Windows Audits is enabled at the OS level.

The sources recommend using credential files over the AIM Credential Provider and suggest upgrading to SCIM Server version 1.3.5 or later to utilize this authentication method. 
