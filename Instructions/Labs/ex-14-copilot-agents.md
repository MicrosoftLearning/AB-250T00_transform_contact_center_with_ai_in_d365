---
lab:
    title: 'Exercise 14 - Configure Copilot features'
    description: 'Verify Copilot prerequisites and connect knowledge sources.'
    duration: '20 minutes'
    level: 300
    islab: true
---

# Exercise 14 - Configure Copilot features

Contoso Coffee's agents handle complex troubleshooting questions across dozens of coffee machine models. Without AI assistance, they spend significant time searching for the right answer. In this exercise, you will verify the Copilot prerequisites, connect the Dynamics 365 knowledge base, and enable Copilot features for support representatives.

This exercise should take approximately **20** minutes to complete.

## Before you start

You must have completed **Exercises 01 and 13**. Copilot data movement must be enabled, and at least one published knowledge article must exist (the LCD Screen Troubleshooting article from Exercise 13).

## Task 1 - Verify Copilot prerequisites

1. In **Copilot Service admin center**, in the left navigation under **Support experience**, select **Productivity**.

1. Next to **Copilot settings**, select **Manage**.

1. On the **Copilot settings** page, confirm that the **Copilot help pane: Ask a question - let service team members chat with AI** checkbox is selected. If it is not, select it and then select **Save**.

1. Verify that **Cross-region data movement** is enabled for the environment. If it is not, open **Power Platform admin center**, select the **Contact Center Trial** environment, select **Settings** > **Features**, and enable it.

    > [!NOTE]
    > The **Cross-region data movement** option is only shown for non-US regions. For US-based trial environments, Copilot AI models are already hosted in region and no additional configuration is needed.

## Task 2 - Connect knowledge sources to Copilot

Copilot can only suggest relevant articles if it knows where to look. You will enable the Dynamics 365 knowledge base as a Copilot knowledge source through the Customer Support agent settings.

1. On the **Copilot settings** page, scroll to the **Agents within Copilot** section.

1. Next to **Customer Support**, select **Settings**.

1. On the **Customer Support** page, select the **Overview** tab.

1. In the **Instructions** field, enter the following custom prompt instructions:

    ``` plaintext
    You are assisting Contoso Coffee support representatives. Respond in a professional and friendly tone. Provide clear, concise guidance based on the knowledge base. Use bullet points or numbered steps when explaining troubleshooting procedures. If the knowledge base does not contain a clear answer, advise the agent to escalate the issue to Tier 2 support.
    ```

    > [!NOTE]
    > Custom instructions tell Copilot how to behave when responding to users. By specifying the tone, format, and escalation guidance here, you ensure that every Copilot response is consistent with Contoso Coffee's support standards - without agents needing to craft detailed prompts themselves. Instructions are applied to all **Ask a question** responses generated from the Dynamics 365 knowledge base.

1. In the **Knowledge sources** section, select the **Use your organization's knowledge base as knowledge source** checkbox.

1. Select **Save**.

    > [!NOTE]
    > This enables Copilot to use your published Dynamics 365 knowledge articles to answer agent questions and draft responses. The number of articles currently indexed is displayed next to the option.

## Task 3 - Configure Copilot features for agents

Copilot features are enabled per experience profile, so agents only see the capabilities relevant to their role.

1. In the left navigation under **Support experience**, select **Workspaces**.

1. Select **Manage** next to **Experience profiles**.

1. Select **Contoso Support Representative**.

1. In the **Copilot AI features** section, select **Edit.**

1. Enable the following features:

   | Feature | Setting |
   |---------|---------|
   | Ask a question | **On** |
   | Intent-based suggestions | **On** |
   | Write an email - help pane | **On** |
   | Live conversation summary | **On** |
   | Suggested actions view | **On** |
   | Case-based knowledge creation | **On** |

   Uncheck to disable the remaining features.

1. Select **Save and close**.

    > [!NOTE]
    > Features not enabled here will not appear in the agent's workspace, even if they are configured globally. Enabling only the features your agents need keeps the workspace focused and reduces distraction.

## Verification

This exercise is complete when:

- Copilot is enabled with cross-region data movement confirmed
- The Dynamics 365 knowledge base is enabled as a Copilot knowledge source in the Customer Support agent settings
- Copilot help pane, conversation summary, and draft email are enabled on the **Contoso Support Representative** experience profile
