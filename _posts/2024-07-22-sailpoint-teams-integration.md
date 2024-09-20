---
layout: post
title: Configuring a Private Server for IdentityIQ's Microsoft Teams Service Code
---

## Configuring a Private Server for IdentityIQ's Microsoft Teams Service Code

The sources provide a detailed explanation of how to configure a private server to host IdentityIQ's service code for Microsoft Teams integration. Here's a breakdown of the process and key recommendations:

### Server Selection and Setup:

*   **Dedicated Server:** SailPoint strongly recommends using a separate, private server to run the IdentityIQ service code, distinct from the IdentityIQ application server. This enhances security by preventing direct internet exposure of the IdentityIQ server.
*   **Operating System Support:** The Microsoft Teams bot is compatible with all currently supported Windows and Linux versions. Choose the operating system that best suits your environment and expertise.

### Network Connectivity and Security:

*   **Public IP and DNS Resolution:** Ensure the private server has a public IP address that's publicly resolvable via DNS. This allows Microsoft Teams to establish a connection to the service code.
*   **HTTPS and Valid Certificate:** Enable HTTPS on the private server and install a valid SSL certificate from a Microsoft-trusted Certificate Authority. This establishes a secure communication channel and is essential for Microsoft Teams to trust the service code. Self-signed certificates are not supported.
*   **Firewall Configuration:** Configure your firewall to allow inbound traffic on the designated HTTPS port for the service code. This ensures Microsoft Teams can reach the service code without any blocks.

### Service Code Installation and Configuration:

1.  **Download Platform-Specific Package:** Download the appropriate service code package for your chosen operating system (Windows or Linux) from Compass.
2.  **Extract and Configure Environment File:** Extract the downloaded zip file on the private server. Locate the `env.template` file and create a copy named `.env`. This file contains environment variables that need configuration.
3.  **Configure Essential Parameters:** Edit the `.env` file with the following crucial parameters:
    *   `PUBLIC_HOSTNAME`: Set this to the public DNS hostname of your service code, resolvable to the private server's IP address.
    *   `LOCAL_HOSTNAME`:  Enter the private IP address of the server where the service code runs.
    *   `PUBLIC_PORT` and `PRIVATE_PORT`: Specify the desired public and private ports for hosting the service code. The default values can be modified as needed.
    *   `TENANT_ID`: Input your Azure tenant ID.
    *   `APP_ID`:  Enter the Application (client) ID of your Microsoft Teams app from Azure.
    *   `APP_NAME`: Provide the name of your Microsoft Teams app.
    *   `SSO_CONNECTION_NAME`:  Input the name you assigned to the OAuth connection setting while configuring the Azure bot.
    *   `ENCRYPTION_SECRET`: Set an 8-character secret for encrypting sensitive data.
    *   `IIQ_URL`:  Enter the full URL of your IdentityIQ installation, including the protocol, hostname, port, and context path. Use the load balancer URL if applicable.
4.  **Encrypt and Set App Secret:**  Start the service code and use the provided encryption endpoint (`https://<private IP>:<private port>/util/encrypt`) to encrypt your Microsoft Teams app secret.  Set the encrypted value as `APP_SECRET` in the `.env` file.
5.  **Certificate and Key Configuration:**
    *   Create a dedicated directory (`cert`) within the service code directory to store the SSL certificate and private key.
    *   Obtain the SSL certificate and private key files from your certificate provider.
    *   Place the certificate file (e.g., `certificate.crt`) and private key file (e.g., `private.key`) inside the `cert` directory.
    *   Encrypt the certificate and private key using the encryption endpoint mentioned in the previous step.
    *   Update the `.env` file with the encrypted certificate and key values:
        *   `BOT_CERTIFICATE`: Encrypted certificate value.
        *   `BOT_KEY`: Encrypted private key value.
6.  **Permissions and Ownership:**
    *   Set strict read and write permissions on the `cert` directory, granting access only to the owner of the service code process. This enhances the security of your sensitive key material.
7.  **Start and Verify Service Code:**  Start the IdentityIQ service code. You should see log messages indicating a successful start and connection to Azure services. Verify that the bot responds correctly to commands within Microsoft Teams.

### Additional Considerations:

*   **Microsoft Azure Configuration:**  The sources emphasize that successful integration requires specific configurations within Microsoft Azure, such as creating an API application, a Microsoft Teams application, and an Azure bot. The provided steps outline the required settings and values to ensure seamless communication between IdentityIQ and Microsoft Teams.
*   **Security Best Practices:**  The sources recommend following security best practices throughout the configuration process. This includes using strong encryption for sensitive data, restricting file permissions, and regularly reviewing security settings.

This comprehensive guide to configuring a private server for IdentityIQ's Microsoft Teams service code is based entirely on the information available within the provided sources. Remember to consult the Microsoft Teams documentation and your IT security team for any platform-specific or security-related considerations.


