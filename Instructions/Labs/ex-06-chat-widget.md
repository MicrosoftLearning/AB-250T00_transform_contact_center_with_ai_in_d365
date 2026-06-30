---
lab:
    title: 'Exercise 06 - Configure the live chat widget'
    description: 'Create and configure a live chat channel for Contoso Coffee, including widget appearance, automated messages, pre-chat survey, and proactive chat. Then test and validate the channel end to end.'
    duration: '50 minutes'
    level: 300
    islab: true
---

# Exercise 06 - Configure the live chat widget

Chat is Contoso Coffee's primary digital support channel. Customers visiting the support portal expect a chat widget that greets them, confirms consent, and collects basic information before connecting them with an agent. In this exercise, you will create the Contoso Chat Widget, customize its appearance, add automated messages, configure a pre-chat survey, and enable proactive chat so the widget can initiate conversations with customers who are browsing the support pages.

This exercise should take approximately **30** minutes to complete.

## Before you start

You must have completed **Exercise 04**. The **Contoso Chat Workstream** must exist before you create the chat channel.

## Task 1 - Create the chat channel

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Channels**.

1. Select **Manage** next to **Chat**. The **Chat channels** page appears.

1. Select **+Add chat channel**.

1. On the **Channel details** page, enter:
   - **Name**: `Contoso Chat Widget`
   - **Language**: `English - United States`

1. In **Window size**, select **Custom**. Configure the dimensions as follows:
   - **Width**: `400`
   - **Height**: `600`

    > [!NOTE]
    > As you adjust the width and height values, the preview chat widget on the right side of the page updates in real time - you can watch it resize as you type.

1. Select **Next**.

1. On the **Workstream details** page:
   - Select **Add to existing workstream**
   - Select **Contoso Chat Workstream**

1. Select **Next**.

## Task 2 - Customize the widget appearance

1. On the **Color settings** page, select the **Cobalt** theme.

1. Select **Next**.

1. On the **Header** page, configure the following and select **Next**:
   - **Header message**: `How can we help?`
   - Change the icon to your favorite icon

1. On the **Chat widget** page, configure the following:
   - Review the default widget preview
   - Set the **Proactive chat** toggle to **On**

1. Select **Next**.

    > [!NOTE]
    > Proactive chat allows the system to automatically open the chat widget and present an invitation to customers after a defined period of inactivity on a support page. You will configure the trigger logic in Task 4.

## Task 3 - Add automated messages

Automated messages are sent to customers automatically when specific events occur during a conversation - for example, when an agent is assigned or when the customer is placed in a queue.

> [!NOTE]
> On the **Behaviors** page, you'll see an **Authentication settings** toggle. Authentication is required for persistent chat, where conversations continue across sessions and the system needs to verify the customer's identity. Because the Contoso Chat Workstream uses live chat (not persistent chat), you can leave this toggle off.

1. Under **Custom automated messages**, select **+Add message**.

1. Configure the first automated message:
   - **Message trigger**: `Agent assigned to conversation`
   - **Automated message**: `Hi, you're connected with a Contoso Coffee support representative. How can I help you today?`

1. Select **Confirm**.

1. Select **+Add message** again to add a second message:
   - **Message trigger**: `Customer is next in line`
   - **Automated message**: `You're next in the queue. We will be with you shortly.`

1. Select **Confirm**.

## Task 4 - Configure the pre-chat survey

A pre-chat survey collects information from the customer before the conversation starts. Contoso Coffee requires consent for data collection and collects the customer's first name to personalize the greeting.

1. On the **Behaviors** page, enable the **Pre-conversation survey** toggle.

1. Select **+Add** to add the first survey question and configure it as follows:
   - **Survey question name**: `ContosoConsent`
   - **Question text**: `Contoso Coffee collects demographic data to improve our service. Do you agree to provide basic information?`
   - **Answer type**: `User consent`
   - **Required**: Yes

1. Select **Confirm**.

1. Select **+Add** again to add the second survey question and configure it as follows:
   - **Survey question name**: `FirstName`
   - **Question text**: `What is your first name?`
   - **Answer type**: `Single line`
   - **Required**: Yes

1. Select **Confirm**.

1. Select **Next**.

## Task 5 - Copy the embed snippet

Once saved, the chat widget generates a JavaScript snippet that embeds the widget on any web page.

1. On the **User features** page, review the available features (file attachments, screen sharing). Leave defaults and select **Next**.

1. On the **Notifications** page, leave the default and select **Next**.

1. On the **Review and finish** page, review all configured settings.

1. Select **Create channel**.

1. After the channel is created, locate the **Chat Widget Script** section.

1. Select **Copy** to copy the embed snippet to your clipboard.

    > [!NOTE]
    > In a production deployment, you would paste this snippet into the `<head>` section of your support portal web pages. For this course, you don't need to deploy the widget to a website - you use this snippet in Tasks 7 and 8 to test the channel end to end.

## Task 6 - Open the agent workspace and set your presence

Before testing, you will need two browser windows or tabs:

- **Window 1**: Copilot Service workspace (agent view)
- **Window 2**: The chat widget test page (customer view)

1. Open **Copilot Service workspace** from the application selector.

1. In the top-right corner of the workspace, check your status. Select **Available** from the status options. When your status is Available, you will see a green check mark.

    > [!NOTE]
    > The routing engine only assigns conversations to agents with an available presence status. If you remain offline, conversations will queue but not be assigned.

## Task 7 - Send a test chat conversation

1. Open **Notepad** (or any plain text editor) and paste the embed snippet you copied in Task 5.

1. Select **File** → **Save As**. Set **Save as type** to **All Files**, name the file `test.html`, and save it to your desktop.

1. Open **File Explorer**, navigate to your desktop, and double-click `test.html`, then select the browser to open it. The Contoso chat widget should appear in the corner of the page.

1. The pre-chat survey appears. Complete it:
   - **Consent question**: Accept
   - **First name**: `Alex`
   - Select **Submit**.

1. Type the following message in the chat window: `I need help with my Contoso coffee machine. The LCD screen is blank.`

1. Submit the message.

## Task 8 - Accept the conversation in the agent workspace

1. Switch back to the **Copilot Service workspace** tab.

1. A notification should appear indicating a new incoming conversation. Select **Accept**.

    > [!NOTE]
    > If no notification appears after 30 seconds, verify that your presence is set to **Available** and that your administrator account is a member of **Contoso Support Queue**. Check the queue membership in **Copilot Service admin center** > **Queues** > **Contoso Support Queue**.

1. The conversation opens in a new session. In the communication panel, you can see the customer's message. (If it didn't open automatically, select **My work items (1)** from the left-hand pane, and select the **Visitor 1** work item.)

1. Review the **Conversation details** panel - confirm the customer's name (Alex) is populated from the pre-chat survey response.

1. Type a reply: `Hi Alex, I can help you with that. Let me look into your LCD screen issue.`

1. Send the reply and confirm it appears in the chat window on the test page.

1. Type a closing message to Alex: `I've looked into the LCD screen issue. Try holding the power button for 10 seconds to reset the display. If the problem persists, please contact us again and we'll arrange a replacement.`

1. Send the message and confirm it appears on the test page.

1. On the test page, type a reply as Alex: `That worked, thank you!`

1. Back in the Copilot Service workspace, in the text box, select **Select text from a list of replies** (this appears as a speech bubble with a lightning bolt).

1. From the list of **Quick replies**, select **Have I answered all of your questions today?** and select the **Send** icon.

1. As Alex, in the widget, reply `Yes.`

1. Go back to the **Copilot Service workspace** and end the test conversation by selecting **End** in the communication panel.

1. A conversation summary will appear, generated by Copilot. Ensure the summary matches what you expect.

1. On the **Visitor 1** session tab at the top of the workspace, select the **Close** (X) icon to close the session.

## Verification

This exercise is complete when:

- **Contoso Chat Widget** appears in the chat channels list and is linked to **Contoso Chat Workstream**
- The widget uses the **Cobalt** theme
- Two automated messages are configured (agent assigned and customer next in line)
- The pre-chat survey includes a consent question and a first name question
- Proactive chat is enabled
- A test chat conversation successfully reached the **Copilot Service workspace** as an incoming notification
- The conversation was routed to **Contoso Support Queue**
- You were able to accept, reply, and close the conversation
