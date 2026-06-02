---
lab:
    title: 'Exercise 04 - Configure queues and workstreams'
    description: 'Create a messaging workstream and an advanced queue for Contoso Coffee, configure operating hours, overflow handling, and the assignment method.'
    duration: '25 minutes'
    level: 300
    islab: true
---

# Exercise 04 - Configure queues and workstreams

Every customer interaction in Dynamics 365 Contact Center enters the system through a **workstream** and waits in a **queue** until it is assigned to an agent. Workstreams define the channel and distribution behavior; queues define the pool of agents and the rules for prioritizing and assigning work. In this exercise, you will build the queue and workstream infrastructure that Contoso Coffee's chat channel will use throughout the rest of the course.

This exercise should take approximately **25** minutes to complete.

## Before you start

You must have completed **Exercise 02**. The **Contoso Support Representatives** capacity profile and your administrator account's queue assignment must exist before you begin.

## Task 1 - Create a messaging workstream

A workstream is the entry point for a channel. It defines how incoming conversations are received, distributed to agents, and linked to a queue.

1. Open **Copilot Service admin center** from the **Apps** selector.

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Workstreams**.

1. Select **+ New workstream**.

1. Select **Inbound** and then select **Next**.

1. Enter the following details:
   - **Name**: `Contoso Chat Workstream`
   - **Type**: `Messaging`
   - **Channel**: `Chat`
   - Do not check the **Persistent chat** checkbox.
   - **Work distribution mode**: `Push`
   - **Fallback queue**: Select **Choose existing**, then select **Default messaging queue (All users)**

1. Select **Create**.

    > [!NOTE]
    > **Push** distribution means the system automatically assigns conversations to available agents based on capacity. **Persistent chat** allows customers to continue a previous conversation if they return within the session timeout window.

1. Confirm the workstream is created and displayed with the option to configure the chat channel. You will configure the chat channel widget in Exercise 06.

## Task 2 - Create an advanced queue

Advanced queues work with unified routing to apply prioritization and assignment rules. Contoso Coffee's support team handles chat conversations from a dedicated queue with defined working hours.

1. In the left navigation under **Customer support**, select **Queues**.

1. Select **Manage** next to **Advanced queues**.

1. Select **+ New queue** to create a new queue.

1. Enter the following details:
   - **Name**: `Contoso Support Queue`
   - **Type**: `Messaging`
   - **Queue priority**: `1`

1. Select **Create**.

    > [!NOTE]
    > **Queue priority** determines the order in which queues are considered when the routing engine assigns work items. Lower numbers indicate higher priority - a queue with priority `1` is evaluated before queues with priority `2` or higher.

1. On the **Contoso Support Queue** page, select **Add users**. Search for and add your administrator account.

1. In the **Operating hours** section, select **+Set operating hours**.

1. In the **Set operation hours** pane, select the **Name** drop-down and select **+Create new.**

1. Enter `Contoso Business Hours` for **Name** and select **Save**.

1. Select the **Working Hours** tab.

1. Select **+New** and select **Working hours** from the drop-down.

1. Create a schedule named `Contoso Business Hours` with the following settings:
   - Keep **today's date** as the date selected
   - **Repeat**: Select Mo, Tu, We, Th, Fr (you can either do this by selecting **Every day** and deselecting Su and Sa)
   - **Start time:** 8:00 AM
   - **End time:** 5:00 PM
   - **Time zone**: Select your local time zone

1. Select **Save**.

1. The calendar will update.

1. Select **Save and Close** to save the operating hours schedule and return to the queue.

## Task 3 - Configure overflow handling

Overflow handling ensures that conversations are redirected when the queue cannot handle them - for example, when wait times are too long or the queue is outside operating hours.

1. On the **Contoso Support Queue** page, scroll to the **Overflow handling** section and select **Add condition-action pair**. Under **When work items are queued**, select **Add condition-action pair**.

1. Configure the following overflow condition:
   - **Condition**: Waiting time in queue exceeds `5` minutes
   - **Action**: Transfer to another queue
   - **Select a queue**: Default messaging queue (1 user)**

1. Select **Save and close**.

    > [!NOTE]
    > This overflow condition ensures that customers are not left waiting indefinitely if all Contoso agents are at capacity. In a production deployment, you might route to a fallback team or trigger a callback.

## Task 4 - Configure the assignment method

The assignment method controls how conversations in the queue are distributed to available agents. Contoso Coffee uses Advanced Round Robin to distribute work evenly across the team.

1. On the **Contoso Support Queue** page, scroll to the **Assignment method** section.

1. Select **See more**.

1. Select **Advanced round robin**.

1. Select **Save & close**.

    > [!NOTE]
    > **Advanced round robin** distributes work items evenly across available agents in sequence, while still respecting agent capacity and skills. In a production deployment, you can also create a custom assignment method with prioritization rules to route conversations based on attributes such as escalation count or language.

<!-- 
## FUTURE TASK: Create a custom prioritization ruleset (UI broken in trials as of May 2026 - restore when fixed)

Prioritization rulesets control the order in which work items in a queue are assigned to agents. Contoso Coffee wants high-priority issues assigned before standard requests.

1. On the **Contoso Support Queue** page, scroll to the **Assignment method** section and select **See more**.

1. On the **Assignment method** page, select **Create New**.

1. In the **Create work assignment** dialog, enter:
   - **Name**: `Contoso Work Assignment`
   - **Description**: `Prioritizes high-priority issues for Contoso Support Queue`

1. Select **Create**.

1. In the **Prioritization ruleset** area, select **+ Create ruleset**.

1. Enter:
   - **Name**: `Contoso Prioritization Ruleset`
   - **Description**: `Routes high-priority cases first`

1. Select **Create**.

1. On the **Contoso Prioritization Ruleset** page, select **+ Create rule**.

1. In the **Create Prioritization Rule** dialog, enter:
   - **Rule Name**: `High priority first`

1. Under **Conditions**, select **+ Add**, then select **Add related entity**. Add the **Issue (Case)** entity.

1. Set the condition: **Priority** **Equals** `High`.

1. In the **Order by** area, select **First in, first out**.

1. Select **Create**.
-->

## Task 5 - Link the queue to the workstream

Now that the queue and workstream are configured, connect them so that conversations arriving through the Contoso Chat Workstream are routed to the Contoso Support Queue.

1. In the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Chat Workstream**.

1. Scroll to the **Routing rules** section. Next to **Route to queues**, select **+Create ruleset**.

1. On the **Create ruleset** dialog, enter:
   - **Name:** `Default routing`
   - **Description:** `Default rule to route all chats to Contoso Support Queue`
   - Select **Create**

1. On the **Decision list** page, select **+Create rule**.

1. In the **Create route to queue rule** dialog, enter:
   - **Rule Name**: `Route to Contoso Support Queue`

1. Leave the **Conditions** area empty so that all conversations are routed to this queue.

1. In the **Route to queues** section, select **Contoso Support Queue**.

1. Select **Create**.

1. Select the rule **Route to Contoso Support Queue**.

1. Select **Save and close**.

    > [!NOTE]
    > Because no conditions are defined, all incoming conversations on this workstream are routed to the Contoso Support Queue. In a production deployment, you would define conditions - for example, routing by language or customer type - to direct conversations to different queues.

## Verification

This exercise is complete when:

- **Contoso Chat Workstream** exists as a push-mode messaging workstream with live chat enabled
- **Contoso Support Queue** exists as an advanced messaging queue with operating hours and overflow handling configured
- The **Contoso Support Queue** assignment method is set to **Advanced round robin**
- The workstream is linked to **Contoso Support Queue**
