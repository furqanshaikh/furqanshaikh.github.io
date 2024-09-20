---
layout: post
title: Activity Data Source in SailPoint IdentityIQ
---

## Discussion on Activity Data Source

In IdentityIQ, an **Activity Data Source** is a source of information about actions taken by users on applications. This activity information is collected, normalized, and stored by IdentityIQ to enable the monitoring and analysis of user behavior.

Here are some key aspects of Activity Data Sources:

*   **Purpose:** Activity Data Sources provide the raw data for IdentityIQ's activity monitoring and reporting capabilities. This data is used to:
    *   **Track User Actions:**  Monitor activities such as logins, file accesses, data modifications, and other application-specific events.
    *   **Detect Anomalies and Risks:** Identify unusual or suspicious activity patterns that might indicate security breaches, policy violations, or insider threats.
    *   **Support Compliance Requirements:** Generate reports and provide audit trails to demonstrate compliance with regulatory frameworks and internal policies.
*   **Types of Activity Data Sources:** IdentityIQ supports various types of Activity Data Sources, catering to different application environments and log formats. Some common types include:
    *   **JDBC Collector:** Collects activity data from relational databases that support JDBC connectivity. This collector requires configuring JDBC connection parameters (connection URL, driver class, username, password) and SQL queries to retrieve relevant activity data.
    *   **Windows Event Log Collector:** Retrieves activity data from Windows event logs. This collector necessitates specifying connection details like the event log server, user credentials, and an MQL query to filter the desired events.
    *   **Log File Collector:**  Gathers activity data from log files stored on various systems. This collector supports different transport mechanisms (local, FTP, SCP) to access log files and requires specifying file names, lines to skip, regular expressions for parsing, and log field definitions.
    *   **RACF Audit Log Collector:** Extracts activity data from RACF (Resource Access Control Facility) audit logs, commonly used in IBM mainframe environments. This collector, similar to the Log File Collector, supports local, FTP, and SCP transports for accessing log files.
    *   **CEF Log File:**  Collects data from log files in the Common Event Format (CEF), a standardized log format used by various security information and event management (SIEM) systems.
*   **Activity Data Source Configuration:** You manage Activity Data Sources through the **Activity Data Source Configuration** page, accessible from the **Application Configuration** page. This page allows you to:
    *   **Add or Edit Data Sources:**  Define a descriptive name, provide a brief explanation of the data source, and select the appropriate **Activity Data Source Type** from the available options.
    *   **Configure Type-Specific Settings:**  Input the necessary connection and query settings for the chosen data source type, as detailed in the previous point about types of Activity Data Sources.
    *   **Define Transformation and Correlation Rules:** Specify rules to transform raw activity data into a format usable by IdentityIQ and correlate it with identities in the system. The **Transformation Rule** converts the collected data, while the **Correlation Rule** establishes links between activities and identities.
*   **Activity Targets:** Within each Activity Data Source, you can define **Activity Targets**. These targets represent specific objects within the data source that are acted upon, such as machine names for logins or file names for file accesses.  Activity Targets are used to:
    *   **Focus Activity Searches:**  Allow administrators to generate searches for activity information on specific targets within a data source.
    *   **Create Activity Target Categories:**  Enable the grouping of targets from multiple applications into categories, simplifying activity monitoring across related systems.
*   **Activity Aggregation Task:**  The actual process of collecting, transforming, correlating, and storing activity data is performed by the **Activity Aggregation** task. This task can be scheduled to run periodically, ensuring that IdentityIQ's activity data is up-to-date.

Activity Data Sources form the backbone of IdentityIQ's ability to monitor and analyze user behavior across diverse applications. By configuring appropriate Activity Data Sources, defining relevant Activity Targets, and scheduling regular Activity Aggregation tasks, organizations can gain valuable insights into user activity, enhance their security posture, and meet their compliance obligations. 


