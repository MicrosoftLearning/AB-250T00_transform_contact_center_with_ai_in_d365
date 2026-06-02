---
lab:
    title: 'Exercise 13 - Configure knowledge management'
    description: 'Configure knowledge management settings in Dynamics 365 Contact Center, create article categories, create a knowledge article template, and author a knowledge article.'
    duration: '40 minutes'
    level: 300
    islab: true
---

# Exercise 13 - Configure knowledge management

A knowledge base is only useful if agents can find the right article at the right moment. Contoso Coffee's support team handles hundreds of coffee machine troubleshooting questions each week - without a well-structured knowledge base, every agent reinvents the answer. In this exercise, you will configure knowledge management settings, build a category structure for Contoso Coffee's product range, create a knowledge article template, and author a troubleshooting article.

This exercise should take approximately **40** minutes to complete.

## Before you start

You must have completed **Exercise 01** with Copilot data movement enabled.

## Task 1 - Enable knowledge management for additional record types

By default, knowledge management is enabled for Case and Conversation records. Contoso Coffee also wants agents to see suggested knowledge articles when working with Account records.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Knowledge**.

1. In the **Record types** section, select **Manage**.

1. On the **Record Types** page, select **+ Add**.

1. In the **Add record type** dialog configure the following settings:
   - **Select record type**: `Account`
   - Set the toggle for **Turn on automatic search** to **On**
   - **Provide search results using**: `Account Name`

1. Select **Save and Close**.

## Task 2 - Configure knowledge general settings

1. In the left navigation under **Support experience**, select **Knowledge** again.

1. In the **General Settings** section, select **Manage**.

1. Configure the following:
   - **Search results display count**: `15`
   - **Enable feedback**: **Yes**

1. Select **Save**.

## Task 3 - Create article categories

Categories organize knowledge articles so agents can filter search results by product line or topic.

1. In the left navigation under **Support experience**, select **Knowledge**.

1. In the **Categories** section, select **Manage**.

1. Select **+ New**.

1. Enter the following details:
   - **Title**: `Contoso Products`
   - **Description**: `Top-level category for all Contoso Coffee product knowledge`

1. Select **Save & Close**.

1. Select **+ New** again to create a subcategory with the following details:
   - **Title**: `Coffee Machines`
   - **Description**: `Troubleshooting and maintenance for Contoso Coffee machines`
   - **Parent category**: `Contoso Products`

1. Select **Save & Close**.

1. Create one more subcategory with the following details:
   - **Title**: `Warranty and Service`
   - **Description**: `Warranty coverage, claims, and service procedures`
   - **Parent category**: `Contoso Products`

1. Select **Save & Close**.

## Task 4 - Create a knowledge article template

Knowledge article templates let you standardize the structure of articles so agents always include the same sections. You will create a troubleshooting template, then use it to author the LCD screen article.

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Knowledge**.

1. In the **Article templates** section, select **Manage**.

1. Select **+ New**.

1. In the **Choose language** dialog, select `English - United States` and select **OK**.

1. In the **Name** field, enter `Contoso Troubleshooting Template`

1. In the template body, add the following sections using the formatting toolbar:

    ``` plaintext
    Symptoms
    Describe the issue the customer is experiencing.

    Steps to resolve
    Provide numbered steps to resolve the issue.

    Escalation
    Describe when and how to escalate if the issue is not resolved.
    ```

1. Format the template using the rich text editor toolbar:
   - Select each heading (**Symptoms**, **Steps to resolve**, **Escalation**) and apply **Bold**.
   - Select each description line beneath the headings and apply *Italic*.

1. Select **Save & Close**.

## Task 5 - Author a knowledge article

Now that the template exists, you will use it to create the LCD screen troubleshooting article. This task takes place in **Copilot Service workspace** - the agent-facing app - rather than the admin center.

1. Select the app switcher (the grid icon in the top-left corner) and select **Copilot Service workspace** to switch apps.

1. In the left navigation, select **Knowledge Articles**.

1. Select **+ New from template**.

1. In the **Select Knowledge Article template** dialog, select **Contoso Troubleshooting Template** and then select **OK**.

1. On the **Content** tab, enter:
    - **Title**: `LCD Screen Troubleshooting - Contoso Coffee Machines`
    - **Keywords**: `LCD, screen, blank, display, troubleshoot`
    - **Description**: `Step-by-step guide for resolving blank LCD screen issues on Contoso coffee machines.`

1. In the article body, replace the placeholder text with the following content. Replace each italic placeholder line with the corresponding text below:

   Under **Symptoms**, replace the placeholder with:

    ``` plaintext
    The LCD screen on the Contoso coffee machine is blank or unresponsive.
    ```

   Under **Steps to resolve**, replace the placeholder with:

    ``` plaintext
    1. Check that the machine is plugged in and the power outlet is working.
    2. Press and hold the power button for 10 seconds to perform a hard reset.
    3. Unplug the machine, wait 30 seconds, then plug it back in and power on.
    4. If the screen remains blank after reset, escalate to Tier 2 support.
    ```

   Under **Escalation**, replace the placeholder with:

    ``` plaintext
    If the issue persists after all steps above, create a service request and assign it to the Hardware team.
    ```

1. Use the **Preview** feature to check how your knowledge article will look on different devices.

1. Switch to the **Summary** tab.

1. Select **Save.**

    > [!NOTE]
    > When you save the article, several fields on the **Summary** tab are automatically populated by the system, including **Article Public Number** (a unique reference ID), **Version number**, **Created on**, and **Language**. You don't need to fill these in manually.

1. In the **Related information** section, you will find 5 icons: **Related versions**, **Related translations**, **Related categories**, **Related articles**, and **Related products**. Select **Related categories.**

1. From the ellipses, select **Relate category**.

1. In the **Select Category to Associate with** lookup, select `Coffee Machines`.

1. Select **Associate**.

1. Select **Save** to save the article.

1. Select **Approve And Publish** to publish the article and make it available to agents. (You may need to expand the ellipses in the top menu to see all of the options.)

1. Select **OK** in the **Confirm approval of articles(s)** dialog.

1. In the **Publish** pane, set the Expiration date to a year from today.

1. Set **Publish approved related translations with Article** to **Yes.**

1. Select **Publish.**

    > [!NOTE]
    > Published articles are indexed for knowledge search and will appear in the agent's productivity pane knowledge search results.

## Verification

This exercise is complete when:

- Knowledge management is enabled for **Account** records with automatic search
- Three categories exist: **Contoso Products**, **Coffee Machines**, and **Warranty and Service**
- The **Contoso Troubleshooting Template** exists and contains Symptoms, Steps to resolve, and Escalation sections
- The **LCD Screen Troubleshooting** article is published and assigned to the **Coffee Machines** category
