# What Is an Agent (No Code)?

A complete guide to understanding AI agents and building your first agentic workflow using OpenAI's AgentKit.

> **⚠️ Important:** Complete the [Pre-Setup Guide](./pre-setup.md) before class to create your account, add billing, and verify access.

---

## What You Will Learn

By the end of this session, you will:

1. Understand what makes an agent different from a chatbot
2. Know the five main parts of AgentKit and what each does
3. Build your first agent workflow using Agent Builder's visual canvas
4. Add safety controls to protect private information
5. Test your agent and understand what happens at each step

**Time needed:** 90 minutes  
**Prerequisites:** None—this session uses drag-and-drop tools with no coding required

---

## Part 1: Understanding Agents (10 minutes)

### What is an Agent?

[Understand Agents and how they are different from chatbots](./what_is_an_agent.md)

---

## Part 2: The AgentKit Stack (15 minutes)

> **👉 Live Demo:** Open [Agent Builder](https://platform.openai.com/playground/agent-builder) now and follow along as we explore concepts together.

OpenAI's AgentKit includes five tools that work together.

![AgentKit Stack](./public/agentkit-core-components.png)

Here's what each one does:

### 1. Agent Builder (Visual Canvas)

**What it is:** A drag-and-drop workspace where you design workflows  
**What it does:** Lets you connect different steps (called "nodes") to create your agent's behavior  
**Why it matters:** You can see the entire workflow at once and test changes quickly

**Key features:**

- Start from templates or a blank canvas
- Drag nodes onto the canvas
- Connect them with arrows to show the flow
- Preview your agent live before publishing
- Save versions so you can go back if needed

### 2. Connector Registry (Data Manager)

**What it is:** A control center where admins decide what data sources agents can access  
**What it does:** Connects your agent to files, databases, and apps like Google Drive, Dropbox, SharePoint  
**Why it matters:** Keeps data organized and secure—only approved sources get connected

**Key features:**

- Central list of all data connections
- Permission controls (who can connect what)
- Works across ChatGPT and API products
- Supports third-party tools through MCP (Model Context Protocol)

### 3. ChatKit (Chat Interface)

**What it is:** Ready-made chat box you can add to websites or apps  
**What it does:** Displays your agent's conversations with users  
**Why it matters:** Saves weeks of design and coding work—just paste your workflow ID and customize colors

**Key features:**

- Embeds in websites with simple code
- Handles streaming (shows the agent "thinking")
- Manages conversation threads
- Matches your brand style (colors, fonts, logo)

### 4. Evals (Testing & Measurement)

**What it is:** Tools for checking how well your agent performs  
**What it does:** Runs test conversations and scores the results  
**Why it matters:** Finds problems before real users see them

**Key features:**

- **Datasets:** Collections of test questions
- **Trace grading:** Scores entire workflows step-by-step
- **Prompt optimizer:** Suggests better instructions automatically
- **Third-party model support:** Compare OpenAI models with others

**Real result:** Carlyle investment firm cut development time by 50% and increased agent accuracy by 30% using Evals.

### 5. Guardrails (Safety Controls)

**What it is:** Automatic checks that protect users and data  
**What it does:** Blocks or flags dangerous inputs and outputs  
**Why it matters:** Prevents agents from sharing private data or following harmful instructions

**Key features:**

- **PII masking:** Hides phone numbers, addresses, credit cards
- **Jailbreak detection:** Catches attempts to trick the agent
- **Hallucination checks:** Flags made-up information
- **Custom rules:** Add your own safety policies

---

## Part 3: Building Blocks (Nodes) (15 minutes)

> **👉 Live Demo:** In Agent Builder, look at the left sidebar. We'll explore each node type as we discuss it.

In Agent Builder, you create workflows by connecting **nodes**. Each node is a step in the process.

### Core Nodes

**Start Node**

- Every workflow begins here
- Takes the user's input
- Can add it to conversation history
- Passes input to the next step

**Agent Node**

- The "brain" that makes decisions
- Contains instructions (like a job description)
- Chooses which tools to use
- Generates responses
- Can be specialized (one agent for billing, another for technical support)

**Note Node**

- Just a comment or reminder
- Doesn't affect the workflow
- Helps teams understand what's happening

### Tool Nodes

**File Search Node**

- Searches uploaded documents
- Uses vector stores (smart search technology)
- Finds relevant information based on meaning, not just keywords
- Good for FAQs, policies, product manuals

**Guardrails Node**

- Tests inputs or outputs
- Pass or fail decision
- If it fails, you decide what happens next (stop workflow, try again, ask for approval)

**MCP Node (Model Context Protocol)**

- Connects to outside services
- Examples: Gmail, Slack, Zapier, CRM systems
- Lets agents read or write data in other apps

### Logic Nodes

**If/Else Node**

- Makes decisions based on conditions
- Example: "If the question is about billing, send to billing agent. Else, send to general support."
- Uses simple expressions you can write without coding

**While Node**

- Repeats steps while a condition is true
- Example: "Keep searching until you find an answer or reach 3 tries"

**Human Approval Node**

- Pauses the workflow
- Shows a draft to a person
- Waits for approval or rejection
- Records the decision

### Data Nodes

**Transform Node**

- Changes data format
- Example: Turn a list into a table
- Makes sure data fits the shape the next node expects

**Set State Node**

- Creates variables you can use anywhere in the workflow
- Example: Save the customer's name so all agents can use it

---

## Part 4: Hands On Agent Builder - Key Concepts

This section provides a hands-on experience with the core components of Agent Builder. Open Agent Builder and create a new workflow to follow along.

### 1. Agent Node (Chat Only)
- **Objective:** Understand the basic function of the Agent Node from simple chatbot to reasing, tool calling and structured outputs.
- **Activity:** Create a new workflow with only a Start Node and an Agent Node. Configure the Agent Node with a simple persona (e.g., "You are a helpful assistant."). Test it in the preview panel to see how it responds to basic questions.

### 2. Tools (Web Search)
- **Objective:** Learn how to give an agent access to external tools.
- **Activity:** Add a Web Search tool to your agent. Configure the Agent Node to use the search tool when it doesn't know the answer. Test it with a question that requires current information (e.g., "What is the weather in New York today?").

### 3. Output (Structured, Widget)
- **Objective:** Learn how to control the output format of your agent.
- **Activity:** Configure the Agent Node to produce a structured output (e.g., JSON) with specific fields. Use a Widget to display the structured data in a user-friendly way (e.g., a card with a title and description).

### 4. If/Else, WHILE
- **Objective:** Understand how to add logic and loops to your agent's workflow.
- **Activity:**
    - **If/Else:** Add an If/Else node to route the conversation based on user input. For example, if the user asks about a specific topic, use one Agent Node; otherwise, use a different one.
    - **WHILE:** Use a WHILE loop to repeat an action until a condition is met. For example, keep searching for information until a satisfactory answer is found or a certain number of attempts have been made.

### 5. Start Node
- **Objective:** Learn how to configure the initial input and state of your agent.
- **Activity:** Customize the Start Node to include initial variables or context that the agent can use throughout the workflow. For example, set a user's name or location at the beginning of the conversation.

### 6. Prompt Engineering
- **Objective:** Learn how to craft effective prompts for your agent.
- **Activity:** In Agent Node pass state variables, try auto generation option and experiment with different prompt styles and formats to improve the agent's responses. Consider using templates, placeholders, and dynamic content to make the prompts more engaging and informative.

### 7. Discussion about Templates
- **Objective:** Understand how to use and customize pre-built templates.
- **Activity:** Explore the available templates in Agent Builder. Discuss how they can be used as a starting point for new projects and how to customize them to fit specific needs.

---

## Part 5: Lab Project: Automated Grading and Feedback Agent

[View the Class Hands-on Project Details](./class_handson_project.md)

---

## Part 6: Understanding the Results (10 minutes)

### Common Issues and Fixes

| Problem                     | Why it happens                               | How to fix            |
| --------------------------- | -------------------------------------------- | --------------------- |
| Agent ignores instructions  | Instructions too vague                       | Add specific examples |
| Wrong tool called           | Instructions unclear about when to use tools | List exact conditions |
| Guardrail blocks good input | Settings too strict                          | Adjust sensitivity    |
| Slow responses              | Too many file searches                       | Limit search scope    |
| Approval always needed      | No clear decision rules                      | Add if/else logic     |

---

## Part 7: Next Steps and Practice (10 minutes)

### What to practice on your own:

1. **Add file search**

   - Upload a PDF with company policies
   - Create a vector store
   - Connect it with a file search node
   - Test questions about the document

2. **Try branching logic**

   - Add an if/else node
   - Route different question types to different responses
   - Example: Benefits questions → detailed answers, Other → short answers

3. **Connect an MCP**

   - Browse available connectors
   - Pick a simple one (like Google Drive)
   - Set up read-only access
   - Test retrieving a file

4. **Build an eval dataset**
   - Write 10 test questions
   - Run them all at once
   - Compare results
   - Find patterns in failures

### Preparing for Session 2

Session 2 focuses on **connecting knowledge safely**.

Before next class:

1. List 3-5 documents or data sources your agent needs
2. Note any privacy concerns (Does it contain personal data? Trade secrets?)
3. Write down who should approve access
4. Bring one question about data security

### Optional homework:

**Beginner:** Modify your Benefits Assistant to handle a different topic (IT support, office amenities, etc.)

**Intermediate:** Add an if/else node that routes urgent questions differently than casual ones

**Advanced:** Create a simple eval dataset with 5 questions and expected answers, then run trace grading

---

## Part 8: Key Concepts Summary

### Agent vs. Chatbot

- **Chatbot:** One question → one answer
- **Agent:** Goal → multiple steps → result

### The Five AgentKit Tools

1. **Agent Builder:** Visual workflow designer
2. **Connector Registry:** Data source manager
3. **ChatKit:** Ready-made chat interface
4. **Evals:** Testing and measurement
5. **Guardrails:** Safety controls

### Essential Nodes

- **Start:** Takes user input
- **Agent:** Makes decisions
- **Guardrails:** Checks safety
- **Human Approval:** Gets permission
- **File Search:** Finds information
- **If/Else:** Routes based on conditions
- **MCP:** Connects external tools

### Safety Principles

1. Always use guardrails for user input
2. Require approval for sensitive actions
3. Test with fake data first
4. Use structured outputs when possible
5. Review traces to catch problems

### Workflow Lifecycle

1. Design in Agent Builder
2. Test with Preview
3. Publish a version
4. Deploy with ChatKit (or export code)
5. Monitor with Evals
6. Improve based on traces

---

## Frequently Asked Questions

**Q: Do I need to know programming?**  
A: No. Agent Builder is visual. You drag boxes and connect them. Instructions are written in plain English.

**Q: How much does AgentKit cost?**  
A: Agent Builder (beta), ChatKit, and Evals are included with standard OpenAI API pricing. You pay for the AI models you use (like GPT-5).

**Q: Can I use my own data?**  
A: Yes. Upload documents to create vector stores, or connect external sources through MCP connectors.

**Q: What if my agent makes a mistake?**  
A: Use human approval nodes for important actions. Test thoroughly with Evals. Monitor traces to catch issues.

**Q: How do I move from Agent Builder to production?**  
A: Publish your workflow to get an ID. Then either: (1) Use ChatKit to embed it, or (2) Export the SDK code to run it yourself.

**Q: Can I have multiple agents in one workflow?**  
A: Yes. Each agent node can specialize in different tasks. Use if/else nodes to route to the right agent.

**Q: What happens when a guardrail fails?**  
A: You decide. Common options: (1) End the workflow, (2) Send a warning message, (3) Reroute to human approval.

**Q: How do I know my agent is getting better?**  
A: Build eval datasets and run them regularly. Compare scores over time. Use trace grading to find weak spots.

**Q: What's the difference between MCP and file search?**  
A: File search works with documents you upload to OpenAI. MCP connects to external apps like Gmail or Slack.

**Q: Can I roll back to an older version?**  
A: Yes. Agent Builder saves versions. You can revert anytime or deploy different versions in different places.

---

## Resources and References

### Official Documentation

- [Introducing AgentKit](https://openai.com/index/introducing-agentkit/)
- [Agents Guide](https://platform.openai.com/docs/guides/agents)
- [Agent Builder Documentation](https://platform.openai.com/docs/guides/agent-builder)
- [Node Reference](https://platform.openai.com/docs/guides/node-reference)
- [Safety in Building Agents](https://platform.openai.com/docs/guides/agent-builder-safety)

### Templates to Explore

- Customer FAQ assistant (what we used today)
- Research assistant
- Email drafter
- Task classifier
- Multi-agent coordinator

### Community Examples

- **Klarna:** [Support agent handles 2/3 of tickets](https://www.klarna.com/international/press/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month/)
- **Ramp:** Built buyer agent in a few hours (mentioned in [AgentKit launch](https://openai.com/index/introducing-agentkit/))
- **Canva:** [Developer support assistant](https://openai.com/index/introducing-agentkit/) saved 2+ weeks of development time
- **HubSpot:** Customer service agent (featured in [AgentKit announcement](https://openai.com/index/introducing-agentkit/))
- **LY Corporation:** Work assistant built in under 2 hours (featured in [AgentKit launch](https://openai.com/index/introducing-agentkit/))

---

## Glossary

**Agent:** A system that works toward goals through multiple steps, using tools and decision-making

**Workflow:** The complete sequence of steps (nodes) your agent follows

**Node:** A single step in a workflow (like an agent, guardrail, or approval)

**Trace:** A detailed log showing exactly what happened in a workflow run

**Vector store:** A special database that lets agents search documents by meaning, not just keywords

**Guardrails:** Automatic safety checks that protect against data leaks and misuse

**MCP (Model Context Protocol):** A standard way to connect agents to external tools and services

**Eval (Evaluation):** A test that measures how well your agent performs

**Trace grading:** Scoring each step of a workflow to find problems

**Prompt injection:** An attack where someone tries to trick the agent by hiding commands in their input

**PII (Personally Identifiable Information):** Private data like social security numbers, addresses, or phone numbers

**Human approval:** A pause in the workflow where a person reviews and approves before continuing

**Structured output:** Forcing the agent to respond in a specific format (like JSON or a form)

---

Use this guide during the session, for self-study, or as a reference when building your own agents.
