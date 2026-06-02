---
lab:
    title: 'Exercise 09 - Configure and deploy a voice agent'
    description: 'Create a Copilot Studio voice agent with generative AI orchestration, configure user consent and DTMF input, enable call recording with consent, and deploy the agent to the Contoso Voice Workstream.'
    duration: '40 minutes'
    level: 300
    islab: true
---

# Exercise 09 - Configure and deploy a voice agent

> [!IMPORTANT]
> This exercise requires the **Contoso Voice Workstream** from Exercise 07. If you were unable to complete Exercise 07, ask your instructor for a pre-configured workstream, or read through this exercise to understand voice agent deployment concepts.

Voice agents handle calls before a human agent is involved. Done well, they resolve issues autonomously or gather enough context that the handoff to a representative feels seamless. In this exercise, you will build a Copilot Studio voice agent for Contoso Coffee using generative AI orchestration, configure it to collect account PINs securely via keypad (DTMF) rather than voice, set up user consent for call recording, and deploy the agent to the voice workstream.

This exercise should take approximately **40** minutes to complete.

## Before you start

You must have completed **Exercise 07** (or have access to a pre-configured voice workstream). You will need access to [Copilot Studio](https://copilotstudio.microsoft.com) at `https://copilotstudio.microsoft.com`.

## Task 1 - Create a voice agent in Copilot Studio

1. Open [**https://copilotstudio.microsoft.com**](https://copilotstudio.microsoft.com) and sign in.

    > [!NOTE]
    > If Copilot Studio does not open, copy the Environment ID from the Power Platform admin center and append it to the URL in this format: `https://copilotstudio.microsoft.com/environments/<Environment ID>`. Make sure to select the one with your contact center resources.

1. In the dialog **Welcome to Microsoft Copilot Studio**, select **Get started** and skip any welcome messages.

1. Confirm you are in the **Contact Center Trial** environment (check the environment selector in the top right).

1. In the **Start building from scratch** section, select **Agent**.

1. For **Name**, enter `Contoso Voice Support Agent` and select **Create**.

1. Your agent may take a few moments to provision.

1. Edit the **Details**, enter the following, and select **Save**:
   - **Description**: `Handles incoming voice calls for Contoso Coffee customer support`

1. In the agent settings, navigate to **Settings** and then to the **Generative AI** tab.

1. Make sure **Use generative AI orchestration for your agent's responses?** is set to **Yes**. If you make any changes, select **Save**.

    > [!NOTE]
    > Generative AI orchestration allows the agent to dynamically determine which topics to trigger based on the customer's spoken intent, rather than relying only on predefined trigger phrases. This produces more natural voice interactions.

1. Navigate to the **Voice** tab.

1. Toggle **Enable voice**.

1. Select **Basic** for **Voice type** (if it is not selected by default), then select **Save**.

    > [!NOTE]
    > **Basic voice** supports DTMF keypad input, text-to-speech, and standard workstream integration - which is what this lab uses. **Real-time voice** is a different, more advanced mode that uses speech-to-speech AI (Azure OpenAI GPT-4o) for ultra-low-latency conversations, but it does not support DTMF topics or the same workstream bot assignment flow.

1. Select **Save** again to confirm voice type.

1. Use the **X** in the upper right corner to exit the Settings.

## Task 2 - Configure the user consent topic

Many jurisdictions require that customers be informed when a call is being recorded. The User Consent topic plays this disclosure at the start of the call. You'll use Copilot Studio's AI authoring feature to generate the topic from a natural language description, then refine it.

1. In the Copilot Studio agent editor, select **Topics**.

1. Select **+ Add a topic** and then select **Add from description with Copilot.**

1. In the **Name your topic** field, enter `User consent`.

1. In the **Create a topic to** field, enter:

   `When a call starts, tell the customer this call may be recorded for quality and training purposes. Ask them to press 1 to consent to recording or press 2 to decline. Save their keypad response in a variable called RecordingConsent.`

1. Select **Create**.

1. Review the generated topic. Verify the following, and correct any differences manually:
   - The opening **Message** node text reads: `This call may be recorded for quality and training purposes.`
   - The **Question** node reads: `Press 1 to consent to recording or press 2 to decline.`
   - The **Question** node uses **Identify**: `Multiple choice options`, has **Assign DTMF keys to options** checked, and **Save user response as**: `RecordingConsent (choice)`.

1. Select **Save**.

1. Select **Topics** > **System**, then select **Conversation Start**.

1. Select the **+** icon between the **On Conversation Start** trigger node and the first **Message** node to insert a new node.

1. Select **Topic management** > **Go to another topic**, then select **User Consent**.

1. Select **Save**.

## Task 3 - Configure DTMF input for PIN collection

Customers who need to authenticate must enter their account PIN using the keypad, not by speaking it aloud. Voice-captured PINs create security risks and appear in transcripts.

1. In the **Topics** list, select **+ Add a topic** → **From blank**.

1. Name the topic by selecting the **Untitled** text box above the designer. Enter `Collect Account PIN`.

    > [!NOTE]
    > You don't need to add trigger phrases to this topic. It will only be called directly from other topics using **Go to another topic**, not triggered by customer speech.

1. Add a **Question** node and configure it as follows:
   - **Question**: `To verify your identity, please enter your 4-digit account PIN on your keypad, followed by the pound sign.`
   - **Identify**: `User's entire response` (with **Accept multi-digit DTMF input** checked)
   - **Number of digits**: `4`
   - **Termination key**: `#`

1. Select the variable placeholder under **Save user response as**. In the **Variable properties** pane, rename the **Variable name** to `AccountPIN` and toggle **Sensitive data** to **On**.

1. Add a **Message** node and enter the message: `Thank you. Verifying your PIN now.`

1. Select **Save**.

    > [!NOTE]
    > By using DTMF multi-digit input rather than speech, the customer's PIN is captured as keypad tones and never transcribed. This is the required approach for PCI DSS-sensitive data such as payment card numbers and account PINs.

## Task 4 - Enable telephony and connect the agent to Dynamics 365 Contact Center

Telephony is enabled at the agent level. You must enable it before connecting the channel, otherwise, the Voice status will show as **Disabled** in the admin center.

1. In Copilot Studio, open the **Contoso Voice Support Agent**.

1. In the top command bar, select **Channels**, then select **Telephony**.

1. Select **Turn on telephony**. You receive a message confirming your agent is connected to telephony features. You can close the **Telephony** pane.

1. Select **Publish** > **Publish** to publish the agent.

## Task 5 - Enable call recording and transcription with consent

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Voice Workstream**.

1. In the voice channel card for **Contoso Voice Channel**, select the **Edit** (pencil) icon.

1. On the **Voice settings** page, select the **Behaviors** tab.

1. In the **Transcription and recording** section, confirm the following are enabled. If they are not enabled, toggle them to **On**:
   - **Transcript and recording**: Select `Transcription and recording`
   - **Start setting**: `Automatic`
   - **Allow customer service representatives to pause and resume**: `Yes`
   - **Request for User Consent**: `Yes`

1. Select **Save**.

    > [!NOTE]
    > When **Request for User Consent** is enabled, the voice agent's User Consent topic controls whether recording proceeds. If the customer declines (presses 2), the platform stops recording immediately and no transcript is generated.

## Task 6 - Add the agent to AI agents in Contact Center

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **AI agents**.

1. Select **+ Add** and select **Connect existing AI agent**. Then select **Next.**

1. Search for and select **Contoso Voice Support Agent**, then select **Connect**.

    > [!NOTE]
    > The agent now appears in the AI agents list. It may take a while for the **Voice status** and **Chat status** to load. Select the **Refresh** button in the top menu to refresh the subgrid. If you need to move on to the next lab, keep checking back.

    You are ready to move on to the next step when **Voice status** and **Chat status** are **Connected**. If you experience a time-out or get an error, republish your agent in Copilot Studio to try again.

## Task 7 - Add the agent to your voice workstream

1. In the left navigation, under **Customer support**, select **Workstreams**, then select **Contoso Voice Workstream**.

1. In the **AI agent** section, select **+ Add AI agent**.

1. Select **Contoso Voice Support Agent**, then select **Connect**.

1. Confirm the agent appears in the **AI agent** section of the workstream.

## Verification

This exercise is complete when:

- **Contoso Voice Support Agent** exists in Copilot Studio with generative AI orchestration enabled
- The **User Consent** topic is connected to the **Conversation Start** system topic and saves the DTMF response to `RecordingConsent`
- The **Collect Account PIN** topic captures the full keypad response in `AccountPIN` using **User's entire response**
- **Contoso Voice Workstream** has transcription and recording enabled with user consent required
- **Contoso Voice Support Agent** is assigned to **Contoso Voice Workstream**
