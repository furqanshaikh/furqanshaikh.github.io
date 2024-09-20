---
layout: post
title: Prerequisites for Enabling and Integrating SailPoint AI Services with IdentityIQ
---

## Prerequisites for Enabling and Integrating SailPoint AI Services with IdentityIQ

To successfully enable and integrate SailPoint AI Services with your IdentityIQ instance, several prerequisites must be met. These prerequisites can be categorized as:

**1.  IdentityIQ Environment:**

*   **Plugins Enabled:** Ensure that plugins are enabled in your IdentityIQ instance. This is essential for installing the AI Services Recommender Plugin. Verify that the `plugins.enabled=true` setting is present in the `identityiq_home/WEB-INF/classes/iiq.properties` file.
*   **Default hbm.xml Fields:** Refrain from removing any default fields from the various `.hbm.xml` files (like `IdentityExtended.hbm.xml` or `LinkExtended.hbm.xml`), even if you've customized extended and searchable attributes. Removing default fields will prevent AI Services from functioning correctly. You are free to add custom fields as needed.

**2. IdentityNow Tenant:**

*   **Active IdentityNow Tenant:**  You need an active IdentityNow tenant to integrate AI Services with IdentityIQ, as SailPoint's AI Services are part of the IdentityNow platform. This tenant will facilitate data exchange and analysis.
*   **Client Credentials:** Generate OAuth client credentials (Client ID and Client Secret) within your IdentityNow tenant for the AI Services Recommendation API. These credentials are crucial for secure communication between IdentityIQ and AI Services.

**3. Network and Connectivity:**

*   **AI Services Virtual Appliance:** An AI Services Virtual Appliance is deployed for communication between IdentityIQ and AI Services. This appliance requires specific network configurations to facilitate data transfer.
*   **Firewall Configuration:**  Configure your firewall to allow outbound HTTPS traffic from your IdentityIQ instance to the AI Services Virtual Appliance. This ensures uninterrupted communication for data sharing and recommendation retrieval.

**4. IBM JDK and WebSphere Configuration (If Applicable):**

*   **TLS 1.2 Support:** If your IdentityIQ deployment utilizes IBM JDK or WebSphere, ensure that your JVM arguments include `-Dcom.ibm.jsse2.overrideDefaultTLS=true`. This enables TLS version 1.2 support, which is necessary for connecting to AI Services in such environments.

**5.  Additional Considerations:**

*   **Onboarding Process:** Familiarize yourself with the AI Services onboarding process, which outlines the steps for connecting your IdentityIQ instance to AI Services and configuring the necessary settings. This process is essential for seamless integration and data synchronization.
*   **Deployment Steps:** Review and understand the deployment steps outlined in the "Getting Started with AI-Driven Identity Security for IdentityIQ" guide. These steps provide a roadmap for successfully deploying and configuring AI Services within your IdentityIQ environment.
*   **Licensing:** AI Services modules may require separate licensing.  Consult your account manager to confirm your licensing agreement and ensure you have the necessary permissions to access and utilize AI Services.

**Remember:**  These prerequisites assume a standard deployment of IdentityIQ. Your specific configuration, environment, and integration requirements might necessitate additional steps or considerations. Always refer to the official SailPoint documentation and consult with SailPoint support for guidance tailored to your unique setup.


