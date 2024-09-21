---
layout: post
title: Implementing a Three-Level Approval Workflow in SailPoint IdentityIQ
---

## Implementing a Three-Level Approval Workflow in SailPoint IdentityIQ

Approval workflows in identity governance are essential to ensure that access requests are validated and approved by the right authorities. In SailPoint IdentityIQ, you can customize workflows to fit your organization's approval requirements, including multi-level approval processes. This post explores how to implement a **three-level approval** system, where access requests go through:

1. **Level 1**: Manager of the requester
2. **Level 2**: General Manager of the department
3. **Level 3**: Any additional approver (for example, security officers or specific identities)

### Understanding SailPoint Approval Workflow

SailPoint's provisioning workflows allow for flexible approval configurations using the `approvalScheme` and `approvingIdentities` variables. By leveraging these variables, you can create sequential or parallel approval flows that involve multiple identities, managers, or workgroups.

In this case, we will create a sequential three-level approval process using a custom workflow.

### Steps to Implement the Three-Level Approval Process

#### 1. **Define Workflow Variables**

Start by defining the variables that will store the identities of the approvers at each level:

```xml
<Variable editable="true" name="manager"/>
<Variable editable="true" name="generalManager"/>
<Variable editable="true" name="identityApprover"/>
```

These variables will store the identities of the manager, general manager, and any other specific identity (e.g., security officer or external approver) that need to approve the request.

#### 2. **Configure Approval Scheme**

In SailPoint, the `approvalScheme` variable determines how approval items are generated and processed. To create a three-level approval flow, you can use the following setup:

```xml
<Variable initializer="manager,generalManager,identityApprover" name="approvalScheme">
    <Description>
        A comma-separated string that defines how approval items are generated.
        The approval process will include the requester's manager, the department's
        general manager, and an additional identity approver.
    </Description>
</Variable>
```

#### 3. **Setting Approving Identities**

The `approvingIdentities` variable will contain the identities or workgroups that need to approve the request. You can concatenate the identities as follows:

```xml
<Variable input="true" name="approvingIdentities">
    <Description>
        List of identities and/or workgroups names/ids involved in the approval process.
    </Description>
</Variable>
```

For this three-level approval process, the identities of the manager, general manager, and identity approver can be dynamically set in the workflow:

```xml
<Variable initializer="manager,generalManager,identityApprover" input="true" name="approvingIdentities"/>
```

#### 4. **Parallel vs. Sequential Approvals**

You can configure the approval flow to be either **parallel** or **sequential** depending on your organization's requirements.

For **sequential approval** (one approver after the other):

```xml
<Variable initializer="sequential" name="approvalMode"/>
```

For **parallel approval** (all approvers receive the request simultaneously):

```xml
<Variable initializer="parallel" name="approvalMode"/>
```

In our case, since the approvals need to be processed in sequence (starting with the manager, then the general manager, and finally the identity approver), we use the **sequential** mode.

#### 5. **Building the Approval Workflow**

With the variables and configuration in place, you can now define the actual workflow steps. Here's a simplified example:

```xml
<Workflow name="ThreeLevelApprovalWorkflow">
    <Start>
        <!-- Initial step: Search for the requester and prepare the request -->
    </Start>

    <ApprovalSet>
        <!-- Step to build the approval set based on the defined scheme -->
    </ApprovalSet>

    <Approval>
        <!-- Step to execute the approval process -->
        <ApprovalStage stage="1" actor="${manager}" />
        <ApprovalStage stage="2" actor="${generalManager}" />
        <ApprovalStage stage="3" actor="${identityApprover}" />
    </Approval>

    <Provision>
        <!-- If all approvals are successful, proceed with provisioning -->
    </Provision>

    <Notify>
        <!-- Notify security officers or relevant teams -->
    </Notify>

    <Audit>
        <!-- Log the workflow for auditing purposes -->
    </Audit>

    <Stop>
        <!-- End of workflow -->
    </Stop>
</Workflow>
```

### Scheduling and Customization

Once you have the workflow configured, it can be scheduled to run based on specific triggers or events (e.g., an access request or entitlement modification). The flexibility of SailPoint allows for further customizations, such as:
- Setting timeouts for each approval level
- Escalating requests if approval is not received in time
- Adding additional approval steps if required

### Conclusion

By leveraging SailPoint IdentityIQ’s flexible workflow engine, you can implement complex, multi-level approval processes that ensure proper oversight over access requests. The three-level approval process described here ensures that each access request is validated by the requester's manager, the department's general manager, and an additional identity approver, adding layers of security and compliance to your provisioning workflows.

Whether you're handling role assignments, entitlement modifications, or identity provisioning, this customizable approval process helps streamline governance while adhering to organizational policies.
