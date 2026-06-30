---
lab:
    title: 'Exercise 02 - Configure users, security roles, and capacity profiles'
    description: 'Configure role persona mappings, create a capacity profile, assign it to a user, and create a skill in preparation for routing exercises.'
    duration: '10 minutes'
    level: 200
    islab: true
---

# Exercise 02 - Configure users, security roles, and capacity profiles

Contoso Coffee's contact center supports three distinct roles: customer support representatives who handle customer conversations, supervisors who monitor and intervene in live interactions, and administrators who manage the platform. Before any routing or channel configuration can work correctly, these roles need the right security permissions and capacity settings. In this exercise, you will configure role persona mappings, create a capacity profile that limits how many simultaneous conversations a customer support representative can handle, and create a skill that will be used in the skill-based routing exercise.

This exercise should take approximately **10** minutes to complete.

## Before you start

You must have completed **Exercise 01** and have access to your Dynamics 365 Contact Center trial environment.

## Task 1 - Review and configure role persona mappings

Role persona mappings control which security roles are associated with the Agent, Supervisor, and Admin personas. Assigning the correct roles ensures that users see the right workspace features and have the right permissions.

1. Open your Dynamics 365 Contact Center trial environment and navigate to **Copilot Service admin center**.

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Role persona mapping**.

1. Select the **Agent** persona. In the **Edit roles** pane, review the security roles currently assigned.

1. Select the **Supervisor** persona and review its assigned roles.

1. Select the **Admin** persona and review its assigned roles. Note that the Admin persona has access to the full admin center.

    > [!NOTE]
    > Contoso Coffee uses the default persona-to-role assignments for this course. You're reviewing them here to understand the permission model before configuring users. Changes to role mappings affect all users in the environment.

1. Select **Save and Close** without making changes.

## Task 2 - Create a capacity profile

A capacity profile defines how many work items can be assigned to a customer support representative at the same time. Contoso Coffee's customer support representatives handle up to three simultaneous chat conversations.

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Capacity profile**.

1. On the **Capacity profiles** page, select **Create new**.

1. On the **Details** tab, enter the following:
   - **Profile name**: `Contoso Support Representatives`
   - **Work item limit**: `3`
   - **Reset frequency**: `Immediate`
   - **Assignment blocking**: Set to **Yes**

    > [!NOTE]
    > Setting **Assignment blocking** to **Yes** means that when a customer support representative reaches their work item limit, the system will not automatically assign them additional conversations. This prevents representatives from being overloaded.

1. Select **Save and Close**.

1. Confirm that **Contoso Support Representatives** appears in the capacity profile list.

## Task 3 - Assign the capacity profile to a user

1. On the **Capacity profiles** page, select the **Contoso Support Representatives** profile to open it.

1. Select the **Users** tab.

1. Select **+ Add user**.

1. Search for and select your administrator account, then select **Add user**.

1. Select **Save and Close**.

    > [!NOTE]
    > In a production deployment, you would assign the capacity profile to all customer support representatives who will handle chat conversations. For this course, assigning it to your admin account is sufficient to validate routing behavior.

## Task 4 - Create a skill for routing

Skills allow the routing engine to match incoming conversations to customer support representatives with the required expertise. Contoso Coffee supports customers in multiple languages, so a **Spanish** language skill is needed for the skill-based routing exercise.

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Skills**.

1. Select **+ New** to create a new skill.

1. Enter the following on the **New Characteristic** page:
   - **Name**: `Spanish`
   - **Type**: `Skill`
   - **Description**: `Used to route Spanish-language conversations to qualified customer support representatives`

1. Select **Save & Close**.

    > [!NOTE]
    > If the Discard suggestions? dialog appears, select **Continue anyway**.

1. Confirm that **Spanish** appears in the skills list.

## Task 5 - Assign the skill to your user

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Enhanced user management**.

1. Select the checkbox next to your administrator account.

1. Select the **Update user attributes** drop-down, then select **Update skills**.

1. In the **Skills** box, select **Spanish**. Under **Default Rating Model**, set the **Proficiency** to `Proficient`.

1. Select **Add to all**, then select **Save**.

    > [!NOTE]
    > The Default Rating Model offers three levels: Familiar, Proficient, and Good. Selecting **Proficient** indicates a solid working knowledge of Spanish. You will use this skill in the routing configuration in Exercise 05.

## Verification

This exercise is complete when:

- The **Contoso Support Representatives** capacity profile exists with a work item limit of 3 and immediate reset
- Your administrator account is assigned to the **Contoso Support Representatives** capacity profile
- The **Spanish** skill exists and is assigned to your administrator account with a proficiency rating
