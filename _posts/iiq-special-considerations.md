---
layout: post
title: Special Considerations in IdentityIQ
---

### Special Considerations in IdentityIQ

The sources provide several special considerations related to configuring and managing IdentityIQ:

*   **Database Encryption for Sqlserver JDBC Driver (Installation Guide):** When using Sqlserver JDBC driver versions 10.2 and later, ensure that the Sqlserver database is encrypted. If connecting to an unencrypted database, explicitly add  `encrypt=false` to the JDBC URLs within the `iiq.properties` file.
*   **Java System Properties (Installation Guide):**  You may need to configure specific Java system properties, like proxy settings (`http.proxyHost`, `http.proxyPort`, etc.), for IdentityIQ to interact with external systems or services. Consult the documentation for your specific application server (e.g., Apache Tomcat) to understand how to add Java system properties to the environment. For instance, in Tomcat, you would define the `JAVA_OPTS` environment variable in the  `bin\catalina.bat` or `bin/catalina.sh` file.
*   **Message Broker for Data Extract and Access History (Installation Guide):** Starting with version 8.4, IdentityIQ requires a message broker for the Data Extract and Access History features. While the installation defaults to an Embedded Broker service running an embedded ActiveMQ instance on port 61616, it is recommended to disable this and use an external broker instead. External brokers offer better administration features, message throughput tracking, and statistics.
*   **Database-Specific Column Sizes for Extended Attributes (Installation Guide):** When extending IdentityIQ objects by adding custom attributes, be mindful of database-specific column size limitations. The comments at the beginning of the `IdentityExtended.hbm.xml` file provide guidance on these considerations. Several XML files (`IdentityExtended.hbm.xml`, `LinkExtended.hbm.xml`, etc.) are used to define extended attributes for different object types within IdentityIQ.
*   **Character Considerations for the IdentityIQ Password Policy (Password Management):**  When configuring the password policy specifically for IdentityIQ internal passwords, you have unique settings to define allowable character types (Digits, Uppercase, Lowercase/Non-English, Special Characters). Leaving these fields empty permits all characters. You can also set the password expiration duration for manually set passwords (through the Edit Preferences window) using the "Days until expiration for manually set passwords" option.
*   **Special Characters in Multi-language Descriptions (System Configuration):**  When using multi-language description files, ensure that escaped HTML characters are formatted correctly to display as intended. For instance, to display text in bold, use  `<b>test</b>` instead of just `test`. Similarly, use  `&lt;test&gt;`  to display  `<test>`  correctly. Failure to format escaped characters properly can result in unexpected display issues within descriptions.
*   **Case Sensitivity in Native Change Detection (Release Notes):**  IdentityIQ includes a new option,  `detectNativeIdentityChangeCaseSensitive`, which defaults to  `false`. Enabling this option triggers a `NativeIdentityChangeEvent` even when the native identifier for an Account or Group differs only by case from the value stored in IdentityIQ.  This can impact performance, so consider the implications before enabling it. You can enable this option by adding it to the Attributes Map of the System Configuration.

These considerations highlight specific configuration settings, database interactions, and potential issues related to managing IdentityIQ effectively.

