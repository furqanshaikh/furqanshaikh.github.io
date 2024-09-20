---
layout: post
title: Initial Operations for a Fresh Production IIQ Deployment
---

## Initial Operations for a Fresh Production IIQ Deployment

SailPoint offer a structured approach to deploying a fresh production instance of IdentityIQ, focusing heavily on the initial setup and configuration process. Here's a consolidated list of initial operations based on the sources:

### System Preparation & Installation

*   **Install & Deploy IdentityIQ:** Follow the detailed instructions in the *IdentityIQ Installation Guide*.
*   **Create Databases:** Create separate databases for IdentityIQ and Access History, even if you don't plan to use the Access History feature initially. Separate instances are recommended for performance reasons.
*   **Secure Database Connection:** Use the `iiq encrypt <password>` command to encrypt the database password for enhanced security.
*   **Import Initial Configuration:** Import essential configuration objects using the IdentityIQ console:
    *   Use `import init.xml` for core IdentityIQ objects.
    *   Use `import init-lcm.xml` to activate Lifecycle Manager features.
    *   Import `init-ai.xml` for AI Services integration.
    *   Import `init-cam.xml` for Cloud Access Management integration.
*   **Start Application Server:** Start your chosen application server (e.g., Tomcat, JBoss, WebLogic) after configuration.

### System Configuration

*   **Access IdentityIQ:** Open a web browser and navigate to your IdentityIQ installation URL (e.g., `http://localhost:8080/identityiq` for a default Tomcat installation).
*   **Log in with Default Credentials:** Use the default user ID `spadmin` and password `admin` for initial access.
*   **Configure Global Settings:** Access Global Settings through the gear icon in the Navigation bar. Key configurations include:
    *   **IdentityIQ Configuration:** Set defaults for notifications, work items, object expiration, UI preferences, and identity history.
    *   **Login Configuration:** Configure authentication settings, including optional integration with an external authentication system.
    *   **Identity and Account Mappings:** Define how IdentityIQ correlates identity data and account attributes from various sources.
    *   **Rapid Setup Configuration:**  Enable and configure global options for Rapid Setup, a streamlined approach to managing joiners, movers, leavers, and identity termination processes.
    *   **AI Services Configuration:** Connect to and configure AI Services for AI-driven identity security functionalities.
    *   **Cloud Access Management Configuration:** Set up connection parameters and synchronize data with Cloud Access Management solutions.
    *   **File Access Manager Configuration:** Configure integration with File Access Manager if this module is installed.
*   **Configure Email Settings:**
    *   Set up email redirection during initial setup for debugging purposes.
    *   Configure email templates for various IdentityIQ events and notifications to match your organization's branding.
*   **Configure Object Expiration:** Define retention policies for identity snapshots, task results, certifications, syslog events, and provisioning transactions.
*   **Configure Auditing:** Review and adjust auditing options to meet your organization's requirements for tracking and reporting.

### Additional Configurations (Optional)

*   **Lifecycle Manager Activation:** If you've purchased Lifecycle Manager, activate it by importing `init-lcm.xml`.
*   **Rapid Setup:** Configure application-specific settings for joiners, movers, and leavers if using Rapid Setup.
*   **Plugins:** Install and configure plugins to extend IdentityIQ's functionality beyond its core capabilities.
*   **Single Sign-On:** Configure single sign-on for seamless access to IdentityIQ from other applications.
*   **Time Synchronization:** Ensure accurate event processing and reporting by synchronizing the IdentityIQ server time.

### Post-Configuration Activities

*   **Verify System Functionality:** Thoroughly test all configured features and integrations to ensure they operate as expected.
*   **User Training:** Provide training to administrators and end-users on using the newly deployed IdentityIQ system.

This detailed breakdown of initial operations for a fresh production IIQ deployment is based on the information provided in the sources. Remember to consult the relevant documentation for your specific environment and requirements.
