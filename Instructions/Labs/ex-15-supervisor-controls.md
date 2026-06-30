---
lab:
    title: 'Exercise 15 - Configure supervisor controls and monitor live conversations'
    description: 'Configure screen recording, add context variables, create a conversation orchestration playbook, and create a custom analytics security role.'
    duration: '30 minutes'
    level: 300
    islab: true
---

# Exercise 15 - Configure supervisor controls and monitor live conversations

<!-- DERIK: Tasks 1 and 2 (supervisor permission toggles and real-time analytics dashboard) were removed because the Insights section under Operations is disabled in Contact Center trials. They are documented here for reference but not included as lab steps. In a production environment, these would be configured via Operations > Insights > Ongoing conversation insights > Manage. -->

Supervisors at Contoso Coffee need to ensure conversation quality, intervene when an agent is struggling, and enforce compliance with call recording policies. Without the right configuration, they cannot monitor live conversations, assign overflowed work items, or access quality scores. In this exercise, you will enable screen recording for agents, add context variables to the chat workstream, create a conversation orchestration playbook that handles queue overflow automatically, configure QA Agent scoring thresholds, and create a custom security role that grants reporting access without full admin permissions.

This exercise should take approximately **30** minutes to complete.

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

Context variables enrich conversations with customer and conversation data that can then be used in playbook conditions, routing rules, and productivity tools. You will add two custom variables to the Contoso Support chat workstream so they can be referenced when building the playbook condition in the next task.

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
    > Context variables are available in routing rules, playbook conditions, macros, and agent scripts. `CustomerTier` lets you treat premium customers differently - for example, routing them to a priority queue or increasing their escalation priority. `IssueCategory` lets you route specific issue types to specialized queues automatically.
    >
    > In a real implementation, these variables would be populated automatically when a chat conversation starts. There are two common approaches:
    >
    > - **Pre-conversation survey**: If you configure a pre-chat survey with questions like "What type of issue are you experiencing?", the customer's answer is stored as a context variable automatically. The variable name must match the survey question name exactly.
    >
    > - **Live chat SDK (JavaScript)**: Your website can pass variables programmatically when the chat widget loads - for example, reading the signed-in customer's account tier from your CRM and injecting it using the `setContextProvider` API. This means the values arrive silently without the customer needing to answer any questions.
    >
    > In this exercise, the variables are defined but not yet populated - they exist so you can reference them in routing rules and playbook conditions. Actual values would flow in at runtime from one of the above sources.

## Task 3 - Create a conversation orchestration playbook

Conversation orchestration uses AI-powered playbooks to automatically manage conversations when conditions change - for example, when no representatives are available or a customer has been waiting too long. Instead of fixed routing rules, playbooks respond dynamically throughout the conversation lifecycle.

> [!NOTE]
> Conversation orchestration is a preview feature. Playbooks apply to voice and live chat channels only. Your trial must have at least one queue and workstream configured for messaging or voice (completed in earlier exercises).

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Conversation Orchestration (Preview)**.

1. Select **Prompt gallery** to browse available playbook templates.

1. In the scenarios drop-down, select **Overflow handling**, then select the **Configure overflow based on support representative availability in the queue** card.

1. In the **Playbook name** field, enter: `Contoso Chat Overflow`

1. Under **Queues**, select **Edit** to configure which queues this playbook applies to, and then configure the following:

    - Set **Channel** to **Messaging**.
    - In **Apply to**, select **All messaging queues**.

1. Select **Save**.

1. In the playbook editor, expand **Add variables** and select **+ Add customer attribute**. We will now add the context variables you configured in Task 2.
   - Select **CustomerTier**.
   - Select **IssueCategory**.

    > [!NOTE]
    > After adding each variable, you can optionally provide a **description** that controls how the variable appears in the playbook's natural language condition. This is useful for variables with technical or abbreviated names - for example, `msdyn_cust_tier_cd` would need a description like "Customer tier (Gold, Silver, Bronze)" to be readable in a playbook prompt. `CustomerTier` and `IssueCategory` are already self-explanatory, so no description is needed here.

1. In the **Build playbook** section, you should see the following:

   `For customers where CustomerTier is enter value and IssueCategory is enter value, if no support reps are available immediately, action.`

1. Configure the values so that the new playbook preview reads:

   `For customers where CustomerTier is Premium and IssueCategory is Urgent, if no support reps are available immediately, Offer direct callback.`

    > [!NOTE]
    > This is the high-priority branch of your playbook. When a Premium customer contacts Contoso Coffee about an Urgent issue and no representatives are available, the system immediately offers them a callback rather than making them wait. The `CustomerTier` and `IssueCategory` values you enter here must exactly match what your chat widget or pre-conversation survey will send at runtime - the comparison is case-sensitive.

1. Select the plus sign to add another playbook step.

1. Remove any variables and configure the step as follows:

   `For all customers, if no support reps are available immediately transfer to another queue` with **Default messaging queue** set as the target queue.

    > [!NOTE]
    > This routes overflow conversations to the default messaging queue rather than leaving customers waiting with no path forward. In a production environment, you might transfer to a dedicated overflow queue with extended hours or a lower-priority agent pool.

1. Select **Save** to save the playbook as a **Draft**.

1. Review any validation warnings displayed. If none appear, select **Publish** and select **Publish** again to activate the playbook.

    > [!NOTE]
    > Once published, the playbook actively monitors all voice and messaging queues and triggers its overflow action whenever no representatives are available - without any manual intervention from a supervisor. To stop the playbook, return to this page, select the vertical ellipsis next to the playbook, and select **Edit** > **Deactivate**.

## Task 4 - Create a custom security role for analytics access

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
- The **Contoso Chat Overflow** conversation orchestration playbook is published and active with transfer to **Default messaging queue** on no-rep-availability
- **Contoso Analytics Viewer** security role exists and is assigned to a user
