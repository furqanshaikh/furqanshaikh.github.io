---
layout: post
title: Two Main Tasks in Configuring a PAM Application
---

## Two Main Tasks in Configuring a PAM Application

The two main tasks for configuring a Privileged Account Management (PAM) application in IdentityIQ are:

1.  **Configuring a PAM Application:** This task involves setting up a connection between IdentityIQ and your PAM vendor's system to aggregate data on PAM accounts, groups, vaults, and permissions.

    *   This process utilizes a PAM-specific application (connector) type called "Privileged Account Management".
    *   You need to configure the application to include both a **connector** and a **target collector**:
        *   The **connector** is responsible for aggregating users, groups, and containers into IdentityIQ.
        *   The **target collector** reads in permissions users have on containers, and can write permissions back to the target system.
    *   The PAM connector, based on IdentityIQ's SCIM 2.0 connector, requires configuration details like Base URL and authentication methods (OAuth2.0, API Token, or Basic Authentication).
2.  **Configuring PAM Global Settings:** This task focuses on setting up global options for the PAM module within IdentityIQ.

    *   These settings control aspects like how PAM containers can be modified within IdentityIQ.
    *   You can define whether to allow adding/removing identities and privileged items in PAM containers, and whether to enable owners to modify PAM containers.
    *   Global settings also dictate the business process used for provisioning PAM identities. You can either utilize the standard LCMManage Passwords business process or define a custom workflow of type LCMProvisioning.

These two tasks are essential for setting up the PAM module in IdentityIQ. While these tasks establish the foundation for PAM integration, the sources also highlight additional configurations related to credential cycling, Rapid Setup processes, and task management for aggregation, indexing, and refreshing PAM data.


