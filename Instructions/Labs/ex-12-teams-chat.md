---
lab:
    title: 'Exercise 12 - Enable Teams chat collaboration'
    description: 'Configure Microsoft Teams integration and chat connections for conversation records, and test linking a Teams chat to a Dynamics 365 conversation record.'
    duration: '15 minutes'
    level: 300
    islab: true
---

# Exercise 12 - Enable Teams chat collaboration

> [!IMPORTANT]
> **Environment requirement**: This exercise requires a **Microsoft Teams license** and might require **tenant administrator** permission to grant consent for enhanced integration. If your trial does not include Teams or you do not have tenant admin access, read through the tasks and proceed to Exercise 14.

Contoso Coffee's customer support representatives often need to consult colleagues from other departments - product engineers, billing specialists, or regional managers - without leaving the conversation they are working on. Embedded Teams chat allows representatives to start a Teams conversation directly from a Dynamics 365 conversation record, and keeps the chat linked to the record so future representatives can see the full consultation history. In this exercise, you will configure Teams chat integration for conversation records and test the end-to-end experience.

This exercise should take approximately **15** minutes to complete.

## Before you start

Verify the following:

- Your account has the **Teams Administrator** or **Global Administrator** role in Microsoft Entra ID (required for Enhanced Integration consent)
- A Teams license is assigned to your account in the Microsoft 365 admin center

## Task 1 - Configure enhanced Teams integration

Enhanced Integration enables deeper linking between Teams channels and Dynamics 365 records.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Collaboration**.

1. In the **Embedded chat using Teams** section, select **Manage**.

1. On the **Microsoft Teams collaboration and chat** page, set the toggle for **Turn on the linking of Dynamics 365 records to Microsoft Teams channels** to **Yes**.

1. Locate the option for enhanced Microsoft Teams integration and set it to **Yes**.

    > [!NOTE]
    > The option name varies by tenant. In UK trials, it is named **Turn on Enhanced Microsoft Teams Integration**. US trial environments might display a different name. If your trial does not display an enhanced integration option, continue to the next task.

1. If prompted, select **Sign in** and complete the admin consent flow.

    > [!NOTE]
    > Enhanced Integration requires tenant admin consent because it grants permissions across your Microsoft 365 tenant.

1. Select **Save**.

## Task 2 - Enable confidential labels where available

Confidential labels allow agents to apply Microsoft Purview sensitivity labels to Teams chats that contain sensitive customer information.

> [!NOTE]
> **Turn on Confidential Labels** is available in UK trial environments but might not appear in US trial environments. If the option is not displayed, skip this task and continue to Task 3.

1. On the **Microsoft Teams collaboration and chat** page, if the **Turn on Confidential Labels** option is available, set it to **Yes**.

1. If prompted, sign in and accept the consent request.

1. Select **Save**.

## Task 3 - Configure chat connections for conversation records

Connecting chats to conversation records ensures that any Teams conversations started from an active conversation are stored and visible within that record.

1. On the **Microsoft Teams collaboration and chat** page, scroll to the **Connect Teams chats to Dynamics 365 records** section.

1. Select **+ Add record types**.

1. Select **Conversation Record** from the lookup.

1. In the settings pane that appears, review any available settings and accept the defaults.

1. Select **Save**.

## Task 4 - Enable Teams chats for the experience profile

1. On the navigation pane under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Experience profiles**.

1. Select the **Contoso Support Representative** experience profile.

1. In the **Productivity pane** section, select **Edit**.

1. Set the **Teams chats** toggle to **On**.

1. Select **Save and Close**.

## Task 5 - Test Teams chat from a conversation record

1. Open **Copilot Service workspace** from the application selector.

1. In the left navigation, select **Conversations** and open any existing conversation record. (You may need to change the view to **All conversations** using the view selector if you have no active conversations open. If no conversations exist, use the chat widget from a previous exercise to generate one.)

1. On the conversation record, in the productivity pane (the vertical toolbar on the right side of the workspace), select the **Teams chats** icon, located below the Copilot icon.

   > [!NOTE]
   > If the **Teams chats** icon doesn't appear on the productivity pane, configuration changes from earlier tasks might still be processing. Wait a few minutes, then refresh your browser or reopen **Copilot Service workspace**, and check again.

1. Select **New connected chat**.

1. Add a participant (you can add any available user).

1. Enter a name for the chat: `Consult on customer issue`.

1. Select **Start chat**.

1. On the new chat that opens, enter a message: `Consulting on LCD screen issue - customer reports blank screen after power cycle.`

1. Send the message.

1. Return to the conversation record and verify that the Teams chat appears linked to the record.

## Verification

This exercise is complete when:

- Enhanced Teams Integration is enabled where the option is available, with admin consent granted if prompted
- Confidential Labels are enabled where the option is available
- Conversation records are configured to link Teams chats
- You successfully started a Teams chat from a conversation record and it appears linked to the record
