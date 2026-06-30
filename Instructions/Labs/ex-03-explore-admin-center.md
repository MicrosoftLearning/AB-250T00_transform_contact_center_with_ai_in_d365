---
lab:
    title: 'Exercise 03 - Explore the Copilot Service admin center and agent workspace'
    description: 'Navigate the Copilot Service admin center sections, explore user management settings, and familiarize yourself with the Copilot Service workspace.'
    duration: '10 minutes'
    level: 100
    islab: true
---

# Exercise 03 - Explore the Copilot Service admin center and agent workspace

Before configuring queues, routing, and channels, it helps to understand how the Copilot Service admin center is organized and where key settings live. In this exercise, you will navigate the admin center's main sections, update a user's queue assignments from the user management view, and explore the agent workspace that Contoso Coffee's service representatives use every day.

This exercise should take approximately **10** minutes to complete.

## Before you start

You must have completed **Exercise 02**.

## Task 1 - Navigate the Copilot Service admin center

The admin center is organized into three main groups. Understanding this structure will help you find the right settings quickly throughout the course.

1. In the top header of your Dynamics 365 Contact Center page, select the current app name (the application selector) and choose **Copilot Service admin center**.

1. In the left navigation, review the three main groups and note what each contains:

   | Group | What it contains |
   |-------|------------------|
   | **Customer support** | Channels, workstreams, queues, routing, user management |
   | **Support experience** | Workspaces, productivity tools, knowledge management |
   | **Operations** | Insights, calendar, service terms, service scheduling |

1. Under **Customer support**, select **Routing**. Note the available routing configuration options, including skill-based routing and diagnostics. You will configure these in Exercise 05.

1. Under **Support experience**, select **Workspaces**. Note the **Experience profiles** and **Session templates** sections. You will configure these in Exercise 11.

1. Under **Operations**, select **Calendar**. Note the options for operating hours and holiday schedules. You will configure operating hours in a later exercise.

    > [!NOTE]
    > The **Insights** section (historical and real-time analytics dashboards) is not available in trial environments. Optionally, you will explore analytics in Exercise 18 if your environment has a full license.

## Task 2 - Update user queue assignments

Queue assignments control which queues an agent is a member of, and therefore which conversations they can receive. In this task, you will assign your administrator account to the default messaging queue.

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Enhanced user management**.

1. Select the checkbox next to your administrator account.

1. Select the **Update user attributes** drop-down, then select **Update queues**.

1. In the **Queues** box, select **Default messaging queue**.

1. Select **Add to all**, then select **Save**.

    > [!NOTE]
    > Assigning your account to the default messaging queue means that test conversations you send in later exercises will be routable to you. Without a queue assignment, the routing engine cannot assign work items to your account.

## Task 3 - Explore the Copilot Service workspace

The Copilot Service workspace is the environment where Contoso Coffee's service representatives handle all their customer interactions.

1. In the top header, select **Copilot Service admin center** (the application selector). In the **Apps** picker that opens, select the **Copilot Service workspace** tile.

1. Review the main areas of the workspace:
   - **Inbox** (left navigation) - the agent's primary view of incoming and active conversations
   - **Sessions panel** (left side) - shows open sessions; each conversation opens as a session
   - **Communication panel** (center) - where the agent interacts with the customer
   - **Productivity pane** (right side) - tools such as knowledge search, agent scripts, and Copilot assistance

1. Select **Inbox** from the left navigation. Select the **Filter and sort** icon and review the available filter options (All, Unread, Read) and sort options (by Customer or Date).

## Verification

This exercise is complete when:

- You can identify the three main groups in the Copilot Service admin center and describe what each contains
- Your administrator account is assigned to the **Default messaging queue**
- You can navigate to the Copilot Service workspace and identify the Inbox, sessions panel, communication panel, and productivity pane
