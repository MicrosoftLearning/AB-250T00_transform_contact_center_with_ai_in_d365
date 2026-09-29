---
lab:
    title: 'Exercise 15 - Configure supervisor controls'
    description: 'Configure screen recording, add context variables, and create a custom analytics security role.'
    duration: '20 minutes'
    level: 300
    islab: true
---

# Exercise 15 - Configure supervisor controls

Supervisors at Contoso Coffee need to ensure conversation quality and enforce compliance with call recording policies. In this exercise, you will enable screen recording for agents, add context variables to the chat workstream, and create a custom security role that grants reporting access without full admin permissions.

This exercise should take approximately **20** minutes to complete.

## Before you start

You must have completed **Exercise 11** (experience profiles must exist) and **Exercise 01** (trial environment provisioned).

## Task 1 - Configure screen recording for representatives

Screen recording allows supervisors to review what an agent's screen looked like during a conversation - useful for quality assurance and training.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Experience profiles**.

1. Select **Contoso Support Representative**.

1. Select **Edit** in the **Productivity pane** section.

1. In the **Screen recording** section, set **Screen recording** to **On**.

1. Select **Save and close**.

    > [!NOTE]
    > Screen recording requires the **Dynamics 365 Contact Center desktop companion application** to be installed on the agent's device. Without the companion app, screen recording cannot capture agent screens even when enabled in the experience profile. This app is available from the admin center or via Microsoft Store deployment.

## Task 2 - Add context variables to the chat workstream

Context variables enrich conversations with customer and conversation data that can then be used in routing rules and productivity tools. You will add two custom variables to the Contoso Support chat workstream.

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Workstreams**.

1. Select the **Contoso Chat Workstream** (or the live chat workstream you created in an earlier exercise).

1. Scroll down to the **Advanced settings** section and expand it.

1. Select **Edit** next to **Context variables**.

1. Select **Add** to add a new context variable.

1. In the **Add context variable** pane, configure the first variable and select **Create**:
   - **Name**: `CustomerTier`
   - **Type**: `Text`

1. Select **Add** again and configure the second variable, then select **Create**:
   - **Name**: `IssueCategory`
   - **Type**: `Text`

1. Select **Close**.

    > [!NOTE]
    > Context variables are available in routing rules, macros, and agent scripts. `CustomerTier` lets you treat premium customers differently - for example, routing them to a priority queue or increasing their escalation priority. `IssueCategory` lets you route specific issue types to specialized queues automatically.
    >
    > In a real implementation, these variables would be populated automatically when a chat conversation starts. There are two common approaches:
    >
    > - **Pre-conversation survey**: If you configure a pre-chat survey with questions like "What type of issue are you experiencing?", the customer's answer is stored as a context variable automatically. The variable name must match the survey question name exactly.
    >
    > - **Live chat SDK (JavaScript)**: Your website can pass variables programmatically when the chat widget loads - for example, reading the signed-in customer's account tier from your CRM and injecting it using the `setContextProvider` API. This means the values arrive silently without the customer needing to answer any questions.
    >
    > In this exercise, the variables are defined but not yet populated. Actual values would flow in at runtime from one of the above sources.

## Task 3 - Create a custom security role for analytics access

Not all users who need to view analytics reports should have full System Administrator access. This task creates a custom role with read-only access to analytics dashboards.

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **User management**.

1. Next to **Security roles**, select **Manage**. This will open your Contact Center trial environment **security roles** page in the Power Platform admin center.

1. Select **+ New role**.

1. Enter:
   - **Role name**: `Contoso Analytics Viewer`
   - **Business unit**: Your org prefix is shown in the dropdown; select it
   - **Description:** `Users who require read-only access to analytics reports.`
   - **Applies To:** `Business teams, supervisors`
   - **Summary of Core Table Privileges**: `Read-only access to analytics`

1. Select **Save**.

1. Expand the **Business Management** tab. Find **User** entity and set **Read** access to **Organization** level if not already set.

1. Use the search function to search for **Omnichannel Realtime analytics** and set **Read** access to **Organization** level.

1. Select **Save + Close**.

1. Assign this role to a test user:
   - On the **Security roles** page, select your new **Contoso Analytics Viewer** role
   - Select **Members** and then select **+ Add people**
   - Search for and select your user name, then select **Add**

## Verification

This exercise is complete when:

- Screen recording is enabled in the **Contoso Support Representative** experience profile
- `CustomerTier` and `IssueCategory` context variables exist on the Contoso Support chat workstream
- **Contoso Analytics Viewer** security role exists and is assigned to a user
