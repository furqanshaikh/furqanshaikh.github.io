---
layout: post
title: Delta Aggregation Support in SailPoint Web Service Connector
---

## Delta Aggregation Support in SailPoint Web Service Connector

Delta aggregation plays a vital role in optimizing identity management processes by ensuring that only the changes (deltas) since the last aggregation are retrieved, reducing time and resource consumption. In SailPoint IdentityIQ, this feature allows efficient synchronization with external systems by only fetching modified or new records instead of performing a full account aggregation each time.

### Does SailPoint Web Service Connector Support Delta Aggregation?

The Web Service connector, as it stands out-of-the-box, does not natively support delta aggregation. However, through custom configurations and clever rule manipulation, it is possible to enable delta aggregation for Web Service-based integrations.

### Implementing Delta Aggregation with Web Service Connector

To implement delta aggregation in a Web Service connector within SailPoint, you can follow a custom approach that involves using rules and tasks to modify the connector behavior dynamically. Here's an outline of how it can be done:

#### 1. **WebServiceBeforeOperation Rule**

One method for implementing delta aggregation is by using a `WebServiceBeforeOperation` rule. This rule checks the primary account aggregation task and looks for a delta aggregation attribute. If delta aggregation is enabled, the rule manipulates the web service call's `ContextURI` or body payload to include a timestamp. This timestamp represents the last successful aggregation date, retrieved from the application configuration. The web service then returns only the changes since that date.

#### 2. **Standard and Delta Aggregation Tasks**

You will need two separate tasks:

- **Full Account Aggregation Task**: This is the standard task that aggregates all accounts.
- **Delta Account Aggregation Task**: This task runs more frequently and aggregates only the changes since the last aggregation.

Both tasks can be part of a sequential workflow that toggles between full and delta aggregations as needed.

#### 3. **Automating Task Execution**

You can schedule the delta aggregation task to run on an hourly basis, while the full aggregation task could be scheduled less frequently (e.g., weekly). The delta task will focus on identifying newly added or modified accounts, whereas the full task ensures that deleted accounts or any missed changes are captured.

In this scenario:
- **Delta Task**: Runs a rule to set `deltaAggregation = true` and `checkDeleted = false`.
- **Full Task**: Resets `deltaAggregation = false` and `checkDeleted = true`.

By doing this, you ensure that delta aggregation picks up incremental changes, while full aggregation takes care of the rest, including cleanup of deleted accounts.

### Example Configuration

#### BeanShell Rule for Delta Aggregation:

```java
if (deltaAggregationEnabled) {
    task.setAttribute("deltaAggregation", true);
    task.setAttribute("checkDeleted", false);
} else {
    task.setAttribute("deltaAggregation", false);
    task.setAttribute("checkDeleted", true);
}
```

This rule dynamically sets the attributes for each task to determine whether a full or delta aggregation should be performed.

### Dealing with Last Aggregation Timestamp

For delta aggregation to work effectively, you need to keep track of the last successful aggregation timestamp. This timestamp can either be stored in the application configuration or in a custom table in the IdentityIQ database.

Here are two possible methods to retrieve the timestamp:

1. **Application Configuration**: Store the timestamp of the last successful aggregation within the configuration of the connected application and retrieve it during the WebServiceBeforeOperation rule.

2. **Custom Database Table**: Create a custom table in IdentityIQ to store metadata such as the last aggregation timestamp. You can then fetch this timestamp inside the rule and use it to perform the delta aggregation.

### Conclusion

While the Web Service connector in SailPoint IdentityIQ does not inherently support delta aggregation, with custom configurations and rules, you can enable delta aggregation efficiently. This setup can reduce the overhead of full account aggregations and ensure that only the most recent changes are aggregated, making identity management more responsive and scalable.

By scheduling delta aggregation tasks and maintaining full aggregations for cleanup, you can strike a balance between performance and completeness in your integration processes.

