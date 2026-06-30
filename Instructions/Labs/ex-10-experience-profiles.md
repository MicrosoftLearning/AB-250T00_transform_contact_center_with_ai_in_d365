---
lab:
    title: 'Exercise 10 - Configure experience profiles and workspace templates'
    description: 'Create an experience profile for Contoso Coffee customer support representatives, configure session and notification templates, associate templates with the chat workstream, and enable the inbox.'
    duration: '30 minutes'
    level: 300
    islab: true
---

# Exercise 10 - Configure experience profiles and workspace templates

Every Contoso Coffee support agent opens the same Copilot Service workspace - but what they see inside it can be different based on their role. Experience profiles control which tools, templates, and features are available to a given group of agents. In this exercise, you will create the Contoso Support Agent experience profile, configure the session and notification templates that define how conversation sessions appear, associate those templates with the chat workstream, and enable the inbox so agents can manage their work queue from one place.

This exercise should take approximately **30** minutes to complete.

## Before you start

You must have completed **Exercise 04**. The **Contoso Chat Workstream** must exist.

## Task 1 - Remove yourself from the default experience profile

Each user can only belong to one experience profile at a time. Before you can assign yourself to the new Contoso profile you're about to create, you need to remove yourself from the one you're currently in.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Workspaces**.

1. In the **Experience profiles** section, select **Manage**.

1. Select **Search by user**.

1. Search for and select your administrator user account.

1. Select the **Assigned Experience Profile** link to open that experience profile page. (It will most likely be called **Customer Service Trial profile**.)

1. Scroll to the **Users** section. Find your admin account in the list, select **Edit**, select the checkbox next to it, and select **Remove users**.

1. Close the **Edit Users** page and confirm your user account is no longer listed in the **Users** section.

## Task 2 - Create an experience profile

1. In the left navigation under **Support experience**, select **Workspaces**.

1. In the **Experience profiles** section, select **Manage**.

1. Select **+ New** to create a new experience profile.

1. In the **Create a new experience profile** dialog, enter the following:
   - **Name**: `Contoso Support Representative`
   - **Unique name**: `msdyn_contoso_support`
   - **Description**: `Experience profile for Contoso Coffee customer support representatives`

1. Select **Create**.

1. Scroll to the **Users** section and select **+ Add users**.

1. Search for and select your administrator account.

1. Select **Add**.

## Task 3 - Enable productivity tools in the experience profile

1. On the **Contoso Support Representative** experience profile page, scroll to the **Productivity pane** section.

1. Select **Turn on**.

1. Enable the following tools:
   - **Productivity pane:** On
   - **Knowledge search**: On
   - **Agent scripts**: On
   - **Copilot**: On

1. Select **Save and close**.

    > [!NOTE]
    > These tool toggles control what appears in the right-side productivity pane when an agent is handling a conversation. You will configure the actual scripts and knowledge settings in later exercises.

## Task 4 - Create an application tab template

Application tab templates define the pages that open automatically in the workspace when a conversation session starts. Opening the customer's account record gives agents immediate context about the company they're supporting.

1. On the **Workspaces** page, select **Manage** next to **Application tab templates**.

1. Select **+ New** to create a new template.

1. Enter the following on the **General** tab:
   - **Name**: `Contoso Account Record`
   - **Unique name**: `msdyn_contoso_account_record`
   - **Title**: `Account`
   - **Page type**: `Entity Record`
   - **Description**: `Opens the customer account record for the active conversation`
   - **Can Close**: `Yes`

1. Select **Save**. The **Parameters** section appears to the right of the form.

1. In the **Parameters** section, set the following values by selecting the fields from the subgrid, selecting **Edit**, and then filling in the **Value** field:
   - **entityName**: `account`
   - **entityId**: `{anchor._customerid_value}`

    > [!NOTE]
    > If the **Discard suggestions** dialog appears, select **Continue anyway** to discard the suggested changes.

1. After the value is filled in on each record, select **Save and close**.

    > [!NOTE]
    > The `entityName` parameter tells the tab which entity type to open (Account). The `entityId` parameter uses a slug that resolves to the customer account ID from the active conversation at runtime.

1. Select **Save and Close**.

## Task 5 - Create a session template

Session templates define the overall layout and behavior of a conversation session - the title format, the communication panel mode, and which application tabs appear.

1. On the **Workspaces** page, select **Manage** next to **Session templates**.

1. Select **+ New** on the **Active Session Templates** view.

1. Enter the following on the **General** tab:
   - **Name**: `Contoso Chat Session`
   - **Unique name**: `msdyn_contoso_chat_session`
   - **Type**: `Generic`
   - **Communication panel mode**: `Docked`
   - **Title**: `{customerName}`
   - **Description**: `Session template for Contoso Coffee chat conversations`
   - **Anchor tab**: `Customer Summary`

    > [!NOTE]
    > **Generic** type templates are channel-agnostic and appear in the session template picker for messaging workstreams like chat. **Entity** type templates are for entity routing (such as Case routing) and won't appear in a chat workstream's dropdown.

1. Select **Save**.

1. In the **Additional tabs** section, select **Add Existing Application Tab Template**.

1. Search for and select **Contoso Account Record**, then select **Add**.

1. Select the **Scripts** tab and set **Enable build expression** to **Yes**.

    > [!NOTE]
    > Enabling build expressions allows agent scripts to use dynamic values from the conversation context - such as customer name or case number - rather than displaying static text. This makes scripts more relevant and reduces manual copy-paste for agents.

1. Select **Save and Close**.

## Task 6 - Associate the session template with the workstream

1. In the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Chat Workstream**.

1. Navigate to **Show advanced settings**.

1. Select **Edit** in the **Sessions** section.

1. In the **Default template** field, select **Contoso Chat Session**.

1. Select **Save and close**.

## Task 7 - Configure the inbox

The inbox provides agents with a unified view of all assigned and open conversations, organized and filterable by type and status.

1. In the left navigation under **Support experience**, select **Workspaces**.

1. In the **Experience profiles** section, select **Manage**.

1. Select **Contoso Support Representative**.

1. Scroll to the **Channel providers** section and select **Edit**.

1. Turn on **All active channels**.

1. Select **Save and close**.

    > [!NOTE]
    > Enabling **All active channels** makes chat and other messaging channel types available throughout the experience profile - including as record type options in inbox views. Without this setting, the **Chat** record type won't appear when you configure the inbox.

1. Scroll to the **Inbox** section and select **Edit**.

1. Set **Enable Inbox** to **On** (if it is not already enabled).

1. Select **+ Add** to create a new inbox view.

1. Enter the following for the new inbox view:
   - **Name**: `Open Chats`
   - **Representative visibility**: `Show`
   - **Record type**: `Conversation`
   - **Settings type**: `Simple`
   - **Settings**: `Assigned`

1. Set **Custom sort for view (optional)** to **On**.

1. In the **Custom sort for view (optional)** section, set:
   - **Record type**: Conversation
   - **Field**: Last Sent/Received
   - **Sort order**: Newer to Older

1. Select **Save and close** to save your new Inbox view.

1. Select **Save and close** again to save the Inbox settings.

## Verification

This exercise is complete when:

- **Contoso Support Representative** experience profile exists with your admin account assigned
- Knowledge search, agent scripts, and Copilot help pane are enabled in the productivity pane
- **Contoso Account Record** application tab template exists
- **Contoso Chat Session** session template exists and includes the Contoso Account Record tab
- **Contoso Chat Session** is assigned to **Contoso Chat Workstream**
- The inbox is enabled in **Contoso Support Representative** with an **Open Chats** view
