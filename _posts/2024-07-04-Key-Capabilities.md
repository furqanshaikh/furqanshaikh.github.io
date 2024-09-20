---
layout: post
title: Key Capabilities and Functionality Extensions of SailPoint's Plugin Framework
---


## Key Capabilities and Functionality Extensions of SailPoint's Plugin Framework

The SailPoint Plugin Framework offers several key capabilities that allow you to extend the functionality of IdentityIQ. Here's a breakdown:

**Extensibility:**

*   **Class path isolation on the server side:** This allows developers to leverage any third-party libraries or technologies for REST endpoints, background services, or Java classes called from scripts.
*   **JavaScript isolation on the client side:**  Plugin developers can utilize any third-party client-side libraries without conflicts.
*   **Core code protection:** The framework ensures that plugins cannot override or modify the behavior of IdentityIQ's backend code, ensuring security and facilitating smooth upgrades.

**Integration:**

*   **Web service extensions:**  Developers can create custom REST endpoints to exchange data between their plugins and the IdentityIQ data model.
*   **Plugin database access:** Plugins can create and manage their own database tables within IdentityIQ, providing persistent storage for plugin-specific data.

**UI Enhancements:**

*   **Plugin installation and removal:** Plugins can be dynamically installed and removed, offering a user-friendly drag-and-drop experience or requiring installation before IdentityIQ starts.
*   **UI Customization:** Plugins can include user interface elements like:
    *   **Full-page applications:** Create entirely new pages within IdentityIQ.
    *   **Snippets:** Inject small pieces of code to modify existing IdentityIQ user interface pages, such as adding menu options or buttons.
    *   **Widgets:** Develop reusable UI components that users can add to their IdentityIQ home pages.
*   **SailPoint Angular components:** Plugins can leverage the SailPoint Angular library to implement UI elements consistent with the IdentityIQ design, providing a seamless user experience.

**Business Logic Implementation:**

*   **Plugin Java Classes:** Developers can write Java classes to implement custom logic, including:
    *   **REST Classes:**  Extend IdentityIQ's REST API by creating custom endpoints to handle specific actions.
    *   **Plugin Executors:**  Implement background tasks, services, or policies that can be invoked within IdentityIQ.

**Security and Permissions:**

*   **Plugin authorization:** Control access to plugin functionality by defining custom Capabilities and SPRights.  This allows you to restrict access to UI components and secure REST endpoints.

**Examples of Plugin Use Cases:**

*   **Integrating with a third-party service desk system (e.g., BMC Remedyforce) to create and track tickets for provisioning requests.** The sources mention several Service Desk Integration Modules, including ones for BMC Helix Remedyforce, a generic one, and one for Cherwell. This indicates that creating plugins to interact with service desk solutions is a common use case.
*   **Building a custom reporting dashboard to visualize IdentityIQ data in a specific way.** While not explicitly mentioned, the sources provide extensive information on customizing reports in IdentityIQ, suggesting that plugins could be used to extend reporting capabilities even further.
*   **Developing a custom workflow to automate a specific business process related to identity management.** The sources highlight the use of plugins for custom tasks and executors, which can be used to create and manage custom workflows within IdentityIQ.

This response draws exclusively from the provided sources.
