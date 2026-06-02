---
lab:
    title: 'Exercise 01 - Provision your Dynamics 365 Contact Center trial'
    description: 'Sign up for a Dynamics 365 Contact Center trial, configure initial settings, enable Copilot data movement, and verify that your environment is ready for the course exercises.'
    duration: '10 minutes'
    level: 200
    islab: true
---

# Exercise 01 - Provision your Dynamics 365 Contact Center trial

In this exercise, you will sign up for a Dynamics 365 Contact Center trial, complete the initial environment configuration, and enable the Copilot data movement setting required for AI features used throughout this course. By the end, your trial environment will be fully provisioned and ready for all subsequent exercises.

This exercise should take approximately **10** minutes to complete.

## Course scenario

Throughout this course, you play the role of a system administrator at **Contoso Coffee**, a specialty coffee equipment company that sells and services espresso machines, grinders, and brewing accessories to both consumers and commercial clients. Contoso Coffee's support team handles hundreds of contacts each week - product troubleshooting, warranty claims, order questions, and machine repair scheduling - across chat, voice, and email.

The company is implementing **Dynamics 365 Contact Center** to replace a mix of disconnected tools and manual processes. Your job is to configure the full Contact Center environment: routing work to the right agents, equipping those agents with knowledge and AI assistance, giving supervisors real-time visibility, and setting up proactive outreach for warranty renewals. Each exercise in this course builds on the previous one, so by the end you will have a complete, working Contact Center environment configured for Contoso Coffee.

## Task 1 - Sign up for a Dynamics 365 Contact Center trial

1. Open a browser and go to the [Dynamics 365 free trial page](https://www.microsoft.com/dynamics-365/free-trial) at `https://www.microsoft.com/dynamics-365/free-trial`.

1. Scroll down to find **Dynamics 365 Contact Center** and select **Try for free**.

1. Enter your credentials as provided by your Authorized Lab Host. Select the agreement terms checkbox, then select **Start your free trial**.

    > [!NOTE]
    > If you're redirected to a sign-in page, enter your credentials and sign in.

1. When prompted, select your **Country/Region**, enter a **Job Title**, and enter a phone number for verification (you can use 123456789), then select **Submit**.

1. After provisioning completes, you're directed to the **Copilot Service workspace**. This may take a few minutes.

    > [!NOTE]
    > If prompted to allow microphone access, select **Allow while visiting the site**. This is required for voice channel features used later in the course.

## Task 2 - Verify your environment in Power Platform admin center

1. Open a new browser tab and go to the [**Power Platform admin center**](https://admin.powerplatform.microsoft.com) at `https://admin.powerplatform.microsoft.com`.

1. If prompted, sign in with the credentials you used to create the trial.

1. In the left navigation, select **Manage** and then select **Environments**.

1. Confirm that a **Contact Center Trial** environment is listed. Select it to open the environment details page.

1. Note the **Environment URL**; you will use this throughout the course to access your Dynamics 365 environment. It's a good idea to save it to Notepad or somewhere easily accessible.

## Task 3 - Enable Copilot data movement

Before AI features such as the Customer Assist Agent, Copilot conversation summaries, and knowledge suggestions work, you need to enable cross-region data movement for Copilot in Power Platform admin center.

1. In the [Power Platform admin center](https://admin.powerplatform.microsoft.com), select your **Contact Center Trial** environment to open its detail page.

1. In the **Generative AI features** card, select **Edit**.

1. In the **Generative AI features** pane, review the available options.
   - If you see a **Move data across regions** checkbox, select it, review the terms of use, and select **Save**.
   - If the checkbox is not visible, your environment is in a US region where data movement is not required. Select **Cancel** and continue to Task 4.

    > [!NOTE]
    > The **Move data across regions** checkbox is only shown for non-US regions. For US-based trial environments, Copilot AI models are already hosted in region, and no additional configuration is needed.

## Task 4 - Explore Copilot Service admin center

1. Return to your environment URL tab. If you were redirected away, navigate back using the environment URL from Task 2.

1. From the top application selector (where you see **Copilot Service workspace**), select **Copilot Service workspace** and then select **Copilot Service admin center**.

1. In the left navigation under **Customer support**, select **Channels**.

1. Select **Manage** next to **Manage channels**. Review the channels that are currently enabled by default in the trial. (You should have Voice, Chat, Social, SMS, and Microsoft Teams all enabled.)

1. In the left navigation under **Customer support**, select **User management**.

1. Select **Manage** next to **Enhanced user management**. Confirm that your administrator user is listed in the **Contact center users** view.

1. Select the checkbox next to your administrator user, then select the **Update user attributes** dropdown in the command bar. Note the three available options:
   - **Update skills:** add, activate/deactivate, or remove skills from users
   - **Update queues:** assign or remove users from queues
   - **Update capacity profile:** assign a capacity profile to control workload limits

1. Leave the page without making changes. You will configure these settings in the next exercise.

## Verification

Your environment is correctly provisioned when:

- The **Contact Center Trial** environment appears in Power Platform admin center

- The **Generative AI features** card is visible on the environment detail page (the **Move data across regions** checkbox is only shown for non-US regions)
- You can open **Copilot Service admin center** and navigate to the **Channels** and **User management** sections
