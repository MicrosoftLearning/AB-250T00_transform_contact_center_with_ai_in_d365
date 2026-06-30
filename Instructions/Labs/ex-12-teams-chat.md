---
lab:
    title: 'Exercise 12 - Enable Teams chat collaboration'
    description: 'Enable embedded Microsoft Teams chat in Dynamics 365, configure chat connections for conversation records, and test linking a Teams conversation to a Dynamics 365 conversation record.'
    duration: '15 minutes'
    level: 300
    islab: true
---

# Exercise 12 - Enable Teams chat collaboration

> [!IMPORTANT]
> **Environment requirement**: This exercise requires a **Microsoft Teams license** and **tenant administrator** permission to grant consent for Enhanced Integration and Confidential Labels. If your trial does not include Teams or you do not have tenant admin access, read through the tasks and proceed to Exercise 14.

Contoso Coffee's customer support representatives often need to consult colleagues from other departments - product engineers, billing specialists, or regional managers - without leaving the conversation they are working on. Embedded Teams chat allows representatives to start a Teams conversation directly from a Dynamics 365 conversation record, and keeps the chat linked to the record so future representatives can see the full consultation history. In this exercise, you will enable Teams chat integration, configure it for conversation records, and test the end-to-end experience.

This exercise should take approximately **15** minutes to complete.

## Before you start

Verify the following:

- Your account has the **Teams Administrator** or **Global Administrator** role in Microsoft Entra ID (required for Enhanced Integration consent)
- A Teams license is assigned to your account in the Microsoft 365 admin center

## Task 1 - Enable Microsoft Teams chat inside Dynamics 365

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Collaboration**.

1. In the **Embedded chat using Teams** section, select **Manage**.

1. On the **Microsoft Teams collaboration and chat** page, set the toggle for **Turn on Microsoft Teams chats inside Dynamics 365** to **Yes** if it is not already enabled.

1. Select **Turn on for all Dynamics 365 apps**.

1. Select **Save**.

## Task 2 - Enable Enhanced Teams Integration

Enhanced Integration enables deeper linking between Teams channels and Dynamics 365 records.

1. On the same **Microsoft Teams collaboration and chat** page, set the toggle for **Turn on the linking of Dynamics 365 records to Microsoft Teams channels** to **Yes**.

1. Set the toggle for **Turn on Enhanced Microsoft Teams Integration** to **Yes**.

1. When prompted, select **Sign in** and complete the admin consent flow.

    > [!NOTE]
    > Enhanced Integration requires tenant admin consent because it grants permissions across your Microsoft 365 tenant.

1. Select **Save**.

## Task 3 - Enable Confidential Labels

Confidential labels allow agents to apply Microsoft Purview sensitivity labels to Teams chats that contain sensitive customer information.

1. On the **Microsoft Teams collaboration and chat** page, set the toggle for **Turn on Confidential Labels** to **Yes**.

1. When prompted, sign in and accept the consent request.

1. Select **Save**.

## Task 4 - Configure chat connections for conversation records

Connecting chats to conversation records ensures that any Teams conversations started from an active conversation are stored and visible within that record.

1. On the **Microsoft Teams collaboration and chat** page, scroll to the **Connect Teams chats to Dynamics 365 records** section.

1. Select **+ Add record types.**

1. Select **Conversation** from the lookup.

1. In the settings pane that appears, review any available settings and accept the defaults.

1. Select **Save**.

## Task 5 - Enable Teams chats for the experience profile

1. On the navigation pane under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Experience profiles**.

1. Select the **Contoso Support Representative** experience profile.

1. In the **Productivity pane** section, select **Edit**.

1. Set the Teams chat toggle to **On**.

1. Select **Save and Close**.

## Task 6 - Test Teams chat from a conversation record

1. Open **Copilot Service workspace** from the application selector.

1. In the left navigation, select **Conversations** and open any existing conversation record. (You may need to change the view to **All conversations** using the view selector if you have no active conversations open. If no conversations exist, use the chat widget from a previous exercise to generate one.)

1. On the conversation record, in the productivity pane on the right side of the workspace, select the **Teams chats** icon.

1. Select **New connected chat**.

1. Add a participant (you can add any available user).

1. Enter a name for the chat: `Consult on customer issue`.

1. Select **Start chat**.

1. On the new chat that opens, enter a message: `Consulting on LCD screen issue - customer reports blank screen after power cycle.`

1. Send the message.

1. Return to the conversation record and verify that the Teams chat appears linked to the record.

## Verification

This exercise is complete when:

- Teams chat is enabled inside Dynamics 365 for all apps
- Enhanced Teams Integration is enabled with admin consent granted
- Conversation records are configured to link Teams chats
- You successfully started a Teams chat from a conversation record and it appears linked to the record
