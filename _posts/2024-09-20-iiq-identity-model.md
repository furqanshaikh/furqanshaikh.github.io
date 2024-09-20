---
layout: post
title: Identity Model in IdentityIQ
---


## Discussion on Identity Model

The sources offer a detailed look at the **Identity Model** within IdentityIQ, a pre-built structure that simplifies how workflows interact with identity data, particularly in forms. Let's explore its significance, structure, and usage.

**Why is the Identity Model important?**

Workflows in IdentityIQ often revolve around making changes to identities. Before the Identity Model, managing identity data within workflows, especially when using forms, was cumbersome. Each attribute required separate handling:

*   Defining individual business process variables for each attribute.
*   Passing each variable to and from the approval workflow.
*   Defining each variable as a form argument.

This approach led to complexity and increased the potential for errors.

The Identity Model solves these problems by representing the entire Identity as a single, manageable unit within a workflow. It acts as a container holding all relevant identity data, streamlining how workflows interact with this data, particularly in forms.

**How does the Identity Model work?**

The Identity Model is essentially a map (a collection of key-value pairs) populated with various identity attributes and related information. You can access this model within workflows through a dedicated library method called `getIdentityModel`.

**What are the key components of the Identity Model?**

The Identity Model includes a comprehensive set of entries representing various facets of an identity:

*   **Standard and Extended Identity Attributes:**  This includes all basic identity attributes like first name, last name, email, manager, etc., along with any custom extended attributes defined in your IdentityIQ installation. Most are stored as strings, with multi-valued attributes represented as lists.
*   **Role Information:** Includes lists for both `detectedRoles` and `assignedRoles`, providing insights into the roles associated with the identity.
*   **Manager Details:** Stores the manager's name as a string and provides a separate `info map` with additional manager information, including their ID, name, and display name.
*   **Time-Related Data:** Includes dates for `lastRefresh`, `lastLogin`, and `passwordExpiration`, offering temporal context to the identity's activity.
*   **Flags and Status Information:** Contains boolean flags like `isWorkgroup`, `managerStatus`, `correlated`, and `correlatedOverriden`, along with information about assigned scopes and transformer options.
*   **Object Class Information:** Stores the class of the object (`sailpoint.object.Identity`) and the transformer class (`sailpoint.transformer.IdentityTransformer`) used for data manipulation.

**How do I use the Identity Model in my workflows?**

Here's a step-by-step guide on utilizing the Identity Model:

1.  **Define Process Variable:** Create a process variable within your workflow (e.g., `identityModel`) to store the Identity Model.
2.  **Initialize and Populate:** In an early workflow step, call the `getIdentityModel` method from the `IdentityLibrary` to initialize and populate the `identityModel` variable. You can pass an identity name or ID as an argument to pre-populate the model with existing identity data.
3.  **Link to Form:** In the approval step containing your form, create an argument (e.g., `workItemFormBasePath`) and set its value to the `identityModel` variable. This creates a bridge between the form and the Identity Model, allowing data exchange.
4.  **Reference Attributes:** Within the form, directly reference attributes from the `identityModel` as if they were individual variables (e.g., use "firstname" instead of "identityModel.firstname").
5.  **Process Changes:** After form submission, utilize the `buildPlanFromIdentityModel()` method to compare the initial and modified versions of the `identityModel`, identifying differences and automatically generating a provisioning plan to implement changes.

**Example:**

Consider a scenario where a workflow form needs to display and allow editing of ten identity attributes. Without the Identity Model, you would manage ten separate variables. The Identity Model simplifies this by storing all attributes within a single `identityModel` variable. When the form loads, it accesses and displays these attributes. After the user edits and submits the form, the workflow compares the updated `identityModel` with its original state and provisions any necessary changes to the identity object. This streamlined process reduces complexity and potential errors.

**Additional Notes:**

*   While the sources focus on the Identity Model's role in workflows and forms, its utility may extend to other areas where streamlined identity data management is beneficial.

*   The sources provide a basic outline and usage pattern for the Identity Model. Further customization and advanced implementations might require deeper exploration of IdentityIQ's API documentation and potentially involve custom coding.

By incorporating the Identity Model, IdentityIQ empowers organizations to handle identity data within workflows more efficiently, especially when forms are involved. It reduces the complexity of managing individual attributes, simplifies form interactions, and ultimately leads to a more robust and maintainable identity management system. 


