---
lab:
    title: 'Exercise 11 - Configure scripts, macros, and productivity tools'
    description: 'Create an agent script with guided steps for Contoso Coffee chat conversations, build a macro that creates a case automatically, and configure rules-based suggested contacts for Teams collaboration.'
    duration: '30 minutes'
    level: 300
    islab: true
---

# Exercise 11 - Configure scripts, macros, and productivity tools

Consistency is a challenge in any contact center. When agents handle dozens of conversations a day, it is easy to skip a step, miss a greeting, or forget to create a case record. Agent scripts solve this by providing a guided checklist agents follow during every conversation. Macros go further - they automate repetitive actions like case creation with a single click. In this exercise, you will build a chat script for Contoso Coffee agents, create a macro that creates a case from the current conversation, and configure rules-based suggested contacts so agents can quickly find the right colleague to consult.

This exercise should take approximately **30** minutes to complete.

## Before you start

You must have completed **Exercise 10**. The **Contoso Support Agent** experience profile must exist with agent scripts enabled.

## Task 1 - Build a case creation macro

Macros automate multi-step actions in the workspace. This macro creates a case record from the current conversation context so agents do not have to manually fill in the customer name, conversation ID, and channel.

> [!NOTE]
> Case creation is relevant when Dynamics 365 Contact Center is deployed alongside Dynamics 365 Customer Service. In a standalone Contact Center deployment, cases aren't used - agents manage conversations directly without creating case records. This task reflects a common hybrid deployment scenario.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Productivity**.

1. On the **Productivity** page, select **Manage** next to **Macros**.

1. Select **+ New** to create a new macro.

1. Enter:
   - **Name**: `Create Case from Conversation`
   - **Description**: `Creates a case record linked to the current conversation`

1. Select **Start macro execution (Productivity automation)** under **Trigger**.

1. Add the following actions in sequence by selecting **+ New step** for each action:

    **Action 1 - Open a new case form**
    - **Connector**: `Productivity automation`
    - **Action**: `Open a new form to create a record`
    - **Entity logical name**: `incident`
    - **Attribute Name**: `title`
    - **Attribute Value**: `${customerName}`

    **Action 2 - Save the record**
    - **Connector**: `Productivity automation`
    - **Action**: `Save the record`

    **Action 3 - Link the case to the conversation**
    - **Connector**: `Omnichannel connector`
    - **Action**: `Link record to the conversation`
    - **Entity record ID**: Select the dynamic value **Entity record ID** from the output of Action 2
    - **Entity primary name**: Select the dynamic value **Entity primary name** from the output of Action 2
    - **Entity logical name**: `incident`

    > [!NOTE]
    > For **Entity record ID** and **Entity primary name**, use the dynamic content picker to select the output values from the **Save the record** action above. These are not values you type - they reference the case record created in Action 2.

1. Select **Save and Close**.

## Task 2 - Create an agent script

Agent scripts appear in the productivity pane during a conversation and guide agents through the required steps in order.

1. On the **Productivity** page, select **Manage** next to **Scripts**.

1. Select **+ New** to create a new script.

1. Enter the following details:
   - **Name**: `Contoso Chat Script`
   - **Unique name**: `msdyn_contoso_chat_script`
   - **Language**: `English (United States)`
   - **Description**: `Guided script for Contoso Coffee chat conversations`

1. Select **Save** (without closing).

1. In the **Script steps** section, add the following steps from the table below in order:

    For each step:

    - Select **+ New script step**
    - Enter the **Name**, **Unique Name**, and **Order**, then set **Action type** to the value shown in the table.
    - If the **Action type** is `Macro`, search for and select the macro name in the **Target macro** field, then enter the description in the **Description** field.
    - If the **Action type** is `Text`, enter the description in the **Text instructions** field.
    - Select **Save and close**.

    | Name | Unique name | Order | Action type | Target macro | Description |
    |------|-------------|-------|-------------|--------------|-------------|
    | `Greet the customer` | `msdyn_greet_customer` | `1` | `Text` | - | `Greet the customer by name and introduce yourself. Use the Contoso Greeting message template if available.` |
    | `Confirm the issue` | `msdyn_confirm_issue` | `2` | `Text` | - | `Ask the customer to describe their issue. Confirm you understand before proceeding.` |
    | `Resolve or create case` | `msdyn_resolve_create_case` | `3` | `Macro` | `Create Case from Conversation` | `Run the macro to create a case record linked to the current conversation.` |
    | `Close and thank customer` | `msdyn_close_thank_customer` | `4` | `Text` | - | `Thank the customer for contacting Contoso Coffee support. Use the Contoso Closing message template. Confirm no further assistance is needed before ending the conversation.` |

    > [!NOTE]
    > If the **Discard suggestions** dialog appears, select **Continue anyway** to discard the suggested changes.


1. Select **Save and Close**.

## Task 3 - Associate the script with the Session Template

1. In the left navigation under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Session Templates**.

1. Select the **Contoso Chat Session** template.

1. On the **Scripts** tab, select **Add Existing Script**.

1. Select **Contoso Chat Script**, and then select **Add**.

1. Select **Save**.

## Task 4 - Configure rules-based suggested contacts for Teams

Rules-based suggested contacts help agents quickly find colleagues to consult during a conversation. When an agent starts a Teams chat from a case record, the system suggests contacts based on defined rules rather than relying only on AI.

1. In the left navigation under **Support experience**, select **Collaboration**.

1. In the **Embedded chat using Teams** section, select **Manage**.

1. Under **Connect Teams chats to Dynamics 365 records**, select **Case**.

1. In the **Suggest contacts** section, confirm that **Rules-based suggested contacts** is toggled **On**. If not, enable it and select **Save**.

1. In the **Update rules for suggesting contacts** section, review the default rules. Reorder them so **Last modified by** appears first (drag it to the top position).

1. Select the **Team Admin** rule (the last rule in the list) and select the **Delete rule** icon to remove it.

    > [!NOTE]
    > A maximum of 10 rules are allowed. The list is already at the limit, so you need to delete one before you can add a new rule.

1. Select **+ Add rule** to add a new rule:

    - **Rule name**: `Queue members`
    - **Rule type**: `Relational`
    - **Select a user or related record**: `Queue Item`
    - **Select a user**: `Owning User`

    > [!NOTE]
    > This rule looks at the Queue Items linked to the case - each Queue Item represents the case being assigned to a queue - and surfaces the **Owning User** of those Queue Items as a suggested contact. In practice, this means the system suggests the agent the case was routed to via queue assignment, making it easy to consult whoever has been handling the same case.

8. Select **Save**.

## Verification

This exercise is complete when:

- **Contoso Chat Script** exists with 4 steps including one macro step
- **Create Case from Conversation** macro exists and creates a case linked to the current conversation
- **Contoso Chat Script** is assigned to the **Contoso Chat Session** session template
- Rules-based suggested contacts are enabled for the **Case** record type with at least one custom rule
