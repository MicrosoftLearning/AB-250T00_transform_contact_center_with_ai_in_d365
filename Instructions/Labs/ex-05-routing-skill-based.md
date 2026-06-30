---
lab:
    title: 'Exercise 05 - Configure routing rules and skill-based routing'
    description: 'Enable skill-based routing, create a work classification ruleset that categorizes incoming conversations by customer, configure a route-to-queue ruleset, and attach both to the Contoso Chat Workstream.'
    duration: '45 minutes'
    level: 300
    islab: true
---

# Exercise 05 - Configure routing rules and skill-based routing

Routing is the brain of the contact center. Without it, every conversation lands in the same queue regardless of urgency, customer value, or required expertise. In this exercise, you will configure the routing pipeline for Contoso Coffee's chat channel. You will enable skill-based routing so Spanish-language conversations go to qualified agents, create a work classification rule that tags high-value customer conversations, and build a route-to-queue rule that sends those tagged conversations to the right queue automatically.

This exercise should take approximately **45** minutes to complete.

## Before you start

You must have completed **Exercise 04**. The **Contoso Chat Workstream**, **Contoso Support Queue**, and **Spanish** skill must all exist before you begin.

## Task 1 - Create a rating model

Skill-based routing requires a rating model that defines the scale used to measure agent proficiency. You will create a **Language** rating model for Contoso Coffee's multilingual support team.

1. In **Copilot Service admin center**, in the left navigation under **Customer support**, select **Routing**.

1. Next to **Skill-based routing**, select **Manage.**

1. In the **Rating Models** subgrid, select **+New Rating Model**.

1. Enter the following:
   - **Name**: `Language Rating Model`
   - **Min Rating Value**: `1`
   - **Max Rating Value**: `10`

1. Select **Save**.

1. In the **Rating Values** section, select the ellipses in the corner of the subgrid and then select **+ New Rating Value**.

1. Create the following entries. After each entry, select **Save and close.**

   | Name | Value |
   |------|-------|
   | `Basic` | `1` |
   | `Conversational` | `5` |
   | `Business` | `8` |
   | `Fluent` | `10` |

    > [!NOTE]
    > If the **Discard suggestions?** dialog appears at any point during this process, select **Continue anyway** to continue without applying AI-generated suggestions.

1. Select the **Value** column header in the **Rating Values** subgrid. Select **Smaller to larger** to sort the values.

1. Confirm that all four rating values - **Basic**, **Conversational**, **Business**, and **Fluent** - appear in the **Rating Values** subgrid, in that order.

## Task 2 - Enable skill-based routing on the workstream

Skill-based routing is enabled at the workstream level by setting the default skill-matching algorithm. This tells the routing engine to match incoming conversations to agents based on their skills and proficiency.

1. In the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Chat Workstream**.

1. Select **See more** in the **Work distribution** settings.

    > [!NOTE]
    > This panel exposes several additional workstream settings worth exploring:
    >   
    > - **Auto-close after inactivity** - automatically closes a conversation after a defined period of agent inactivity, preventing stale conversations from blocking capacity.
    > - **Work distribution mode** - locked to **Push** for this workstream, meaning the system assigns conversations automatically rather than requiring agents to pick them up.
    > - **Capacity** - sets the capacity unit cost of each conversation assigned through this workstream; used in conjunction with capacity profiles.
    > - **Block capacity for wrap up** - when enabled, the agent's capacity remains occupied during the post-conversation wrap-up period so they aren't assigned a new conversation immediately.
    > - **Allowed presences** - defines which agent presence statuses (for example, Available, Busy) are eligible to receive work from this workstream.
    > - **Keep the same representative for the entire conversation** - ensures that a returning customer is reconnected to the same agent if they rejoin within the session window.

1. For **Block capacity for wrap up**, select **Custom time**. Set the custom time to `3` minutes `0` seconds.

1. Under **Default skill matching algorithm**, select **Exact match**.

    > [!NOTE]
    > **Exact match** requires the assigned agent to have all required skills at or above the minimum proficiency threshold. If no agent meets the criteria, the conversation remains unassigned in the queue. Use **Closest match** if you want the system to assign conversations even when no agent has an exact skill match.

1. Select **Save and close.**

## Task 3 - Create a skill attachment ruleset

Skill attachment rules are a type of work classification ruleset. They attach skills to incoming conversations so the routing engine can match conversations to agents who have the required skill and proficiency. You will create a rule that attaches the **Spanish** skill to any conversation where the customer's language is Spanish.

1. In the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Chat Workstream**.

1. In the **Routing rules** section, scroll to **Work classification (optional)** and select **+ Create ruleset**.

1. Select **Create new**.

1. In the **Create work classification ruleset** dialog configure the following:
   - **Rule type**: `Logical rules`
   - **Name**: `Contoso Skill Attachment Rules`
   - **Description**: `Attaches the Spanish skill to conversations from Spanish-speaking customers`

1. Select **Create**.

    > [!NOTE]
    > There are two rule type options:
    >
    > - **Logical rules** - you manually define conditions and outputs using the decision list builder. Best for straightforward, deterministic routing logic where the criteria are well-known and stable.
    > - **Machine learning model** - uses an AI model trained on historical conversation data to predict and attach attributes automatically. Best for complex or high-volume environments, but requires model training and setup.

1. On the **Decision list** page, select **+Create rule**.

1. In the **Create work classification rule** dialog, enter:
   - **Rule Name**: `Attach Spanish skill - Mexico`

1. In the **Conditions** area, select **+ Add row**. Set the condition:
   - **Attribute**: `Customer Language`
   - **Operator**: `Equals`
   - **Value**: `Spanish - Mexico`

1. Set the **Output** as **Skills**.

1. Select the **Set to** lookup. In the **Select skills** pane that appears, select:
   - **Skill**: `Spanish`
   - **Proficiency**: `Conversational`

1. Select **Save and close.**

1. Select **Create.**

1. Repeat the previous steps to create three more rules with the same output, one for each remaining Spanish variant:

    | Rule Name | Condition Value |
    |-----------|----------------|
    | `Attach Spanish skill - Puerto Rico` | `Spanish - Puerto Rico` |
    | `Attach Spanish skill - Spain` | `Spanish - Spain` |
    | `Attach Spanish skill - United States` | `Spanish - United States` |

    > [!NOTE]
    > Because the condition toggle is fixed to **And** and can't be changed to **Or**, creating one rule per language variant is the correct approach. Each rule is evaluated independently in the decision list, so any matching variant will attach the Spanish skill.

1. Confirm that all four rules appear in the decision list.

    > [!NOTE]
    > These rules attach the **Spanish** skill at **Conversational** proficiency to any incoming conversation where the customer language is Spanish. The routing engine then uses the exact match algorithm (set in Task 2) to find an agent with at least Conversational proficiency in Spanish.

## Task 4 - Create a work classification ruleset

Work classification rules run before a conversation is assigned to a queue. They inspect the conversation's properties and set output values - such as a service level or category - that route-to-queue rules can then act on.

Contoso Coffee wants conversations from **Trey Research** (a key commercial account) to be tagged as **Gold** service level and routed to the Contoso Support Queue immediately.

1. In the left navigation under **Customer support**, select **Workstreams**.

1. Select **Contoso Chat Workstream**.

1. In the **Routing rules** section, select **See more** next to **Work classification (optional)**.

1. On the **Work classification** page, select **Create new**.

1. In the **Create work classification ruleset** dialog configure the following:
   - **Rule type**: `Logical rules`
   - **Start new or use a template:** New ruleset
   - **Name**: `Contoso Classification Rules`
   - **Description**: `Classifies Trey Research conversations as Gold service level`

1. Select **Create**.

1. In the **Decision list**, select **+Create Rule**.

1. Configure the rule:
   - **Rule Name**: `Set Gold service level`
   - Select **+Add**, then **Add related entity**, and add the **Issue (Case)** entity
   - **Condition**: **Customer** **Equals** `Trey Research`

1. In the **Output** section, scroll to **Related entities** in the dropdown and select **Issue (Case)**. (Do not select **Issue**; it will appear before **Issue (Case)** in the dropdown, but keep scrolling. We want to select the field that exists on the related entity.)

1. In **Select attribute or related entity**, select **Service Level**.

1. In **set to**, select **Gold.**

1. Select **Create**.

1. Confirm that **Set Gold service level** appears in the decision list.

## Task 5 - Create a route-to-queue ruleset

Route-to-queue rules use the output values set by the work classification ruleset to direct conversations to the correct queue. You will create a rule that routes Gold service level conversations to the Contoso Support Queue.

1. On the **Contoso Chat Workstream** page, in the **Routing rules** section, select the **Default routing** ruleset.

1. In the **Decision list**, select **+ Create Rule**.

1. Configure the rule:
   - **Rule Name**: `Route Gold to Contoso Support Queue`
   - Select **Add related entity** and select **Issue (Case)**
   - **Condition**: **Service Level** **Equals** `Gold`
   - **Queue**: `Contoso Support Queue`

1. Select **Create**.

1. Confirm that **Route Gold to Contoso Support Queue** appears in the decision list.

1. Click the **up** arrow to move it to the 1st position in the decision list.

## Task 6 - Verify the routing configuration

With both rulesets attached to the workstream, review the complete routing pipeline to confirm everything is connected correctly.

1. On the **Contoso Chat Workstream** page, review the **Routing rules** section. Confirm the following are all present:
   - **Work classification**: Contains **Contoso Skill Attachment Rules** and **Contoso Classification Rules**
   - **Route to queues**: Specifies **Default messaging queue** as the fallback queue and specifies the Ruleset as **Default routing**

1. Confirm that all sections show the expected values. Changes made in each pane were saved when you selected **Save and close** in earlier tasks.

    > [!NOTE]
    > When a chat conversation arrives through this workstream, the routing engine will: (1) apply skill requirements to match the conversation to a qualified agent, (2) run the classification rules to check for Trey Research and set the service level, and (3) run the route-to-queue rules to direct the conversation to the correct queue. You will test this end-to-end in Exercise 08.

## Verification

This exercise is complete when:

- **Skill-based routing** is enabled and the **Language Rating Model** exists with four rating values
- **Contoso Chat Workstream** has a Spanish skill requirement with minimum proficiency of 4
- **Contoso Classification Rules** workstream ruleset exists with the **Set Gold service level** rule
- **Contoso Route-to-Queue Rules** exists with the **Route Gold to Contoso Support Queue** rule
- All rulesets are attached to **Contoso Chat Workstream**
