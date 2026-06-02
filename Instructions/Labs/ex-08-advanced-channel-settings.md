---
lab:
    title: 'Exercise 08 - Configure advanced channel settings'
    description: 'Configure conversation lifecycle settings, consult and transfer limits, message templates, custom presence statuses, and automatic customer identification for Contoso Coffee.'
    duration: '20 minutes'
    level: 300
    islab: true
---

# Exercise 08 - Configure advanced channel settings

Beyond basic channel setup, Dynamics 365 Contact Center provides a layer of advanced settings that control how conversations behave throughout their lifecycle. In this exercise, you will configure consult and transfer settings, reusable message templates, a custom presence status for Contoso Coffee's training periods, and notification behavior for missed and rejected conversations.

This exercise should take approximately **20** minutes to complete.

## Before you start

You must have completed **Exercise 06**. The **Contoso Chat Workstream** and **Contoso Chat Widget** must exist.

## Task 1 - Configure consult and transfer settings

Consult and transfer settings control how agents can involve other agents in a conversation - either for advice (consult) or to hand the conversation off entirely (transfer).

1. In the left navigation under **Customer support**, select **Channels**.

1. Select **Manage** next to **Consult and transfer**.

1. Enable the **Consult to queue** toggle.

1. Set the countdown values:
   - **Voice**: `30` seconds
   - **Messaging**: `30` seconds

1. Enable the **Transfer to representatives** toggle under **Transfer settings**.

1. Select **Save**.

## Task 2 - Create a message template

Automated message templates are sent to customers automatically when specific events occur during a conversation. You can create global templates here and reuse them across channels.

1. In the left navigation under **Support experience**, select **Productivity**.

1. Select **Manage** next to **Message templates**.

1. Select **+New**.

1. Enter and select the following:
   - **Channel**: `Live chat`
   - **Name**: `Contoso Greeting`
   - **Message trigger**: `Agent assigned to conversation`
   - **Automated message**: `Hi, you're connected with a Contoso Coffee support agent. How can I help you today?`
   - **Default language**: `English - United States`

1. Select **Save & Close**.

1. Select **+ New** again to create a second template:
   - **Channel**: `Live chat`
   - **Name**: `Contoso Closing`
   - **Message trigger**: `Agent ended conversation`
   - **Automated message**: `Thank you for contacting Contoso Coffee support. Please reach out if you need further assistance.`
   - **Default language**: `English - United States`

1. Select **Save & Close**.

## Task 3 - Create a custom presence status

Custom presence statuses allow you to add organization-specific availability states beyond the default options. Contoso Coffee holds regular training sessions during which agents are unavailable for customer conversations.

1. In the left navigation under **Support experience**, select **Productivity**.

1. Select **Manage** next to **Custom presence**.

1. Select **+New**.

1. Enter and select the following:
   - **Name**: `Contoso Employee Training`
   - **Presence text**: `In Training`
   - **Base status**: `Busy`
   - **Description**: `Agent is attending a training session and is unavailable for conversations.`

1. Select **Save and Close**.

    > [!NOTE]
    > Setting the base status to **Busy** means agents with this presence will not receive new conversations. Supervisors can still see them as distinctly "In Training" rather than generically busy.

## Task 4 - Review notification behavior and configure sound settings

When an agent misses or rejects an incoming conversation notification, the system automatically changes their presence so they aren't assigned new work until they're ready. These settings are enabled by default - in this task you'll confirm they're active and then configure the live chat notification sound.

1. In the left navigation under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Notifications**.

1. Select the **Missed Notifications** tab. Confirm that **Change agent status to inactive after a missed notification** is set to **Yes**.

    > [!NOTE]
    > When an agent misses a notification, their presence is automatically set to **Inactive**, preventing new conversations from being assigned until they manually reset it. This avoids conversations being routed to an agent who isn't at their desk.

1. Select the **Agent Reject** tab. Confirm that **Change agent status to "Do not disturb" after a notification is rejected** is set to **Yes**.

    > [!NOTE]
    > When an agent rejects a notification, their presence is set to **Do not disturb**. This signals intentional unavailability, as distinct from simply missing a notification.

1. Select the **Sound Notification settings** tab.

1. Set the **Enable sound notifications** toggle to **Yes**.

1. Under **Live chat**, configure the following:
   - **Play sound**: `Yes`
   - **Repeat until answered**: `Yes`
   - **Sound**: Remove **Wood bounce** and select **Wood frog.**

1. Select **Save & Close**.

## Verification

This exercise is complete when:

- Two message templates exist: **Contoso Greeting** and **Contoso Closing**
- A custom presence status named **In Training** exists with a base status of Busy
- Missed and rejected notification settings are confirmed active; live chat sound notifications are enabled with **Repeat until answered**
