# Session 6: Visual and Agentic Design Patterns

## Building Intelligent Workflows with Agentic Patterns

**Duration:** 2 hours  
**Level:** Intermediate  
**Prerequisites:** Sessions 4 & 5 (Agent Builder basics, File Search, Connectors, MCP)

---

## What You Will Learn

By the end of this session, you will understand:
- How agents think and act (agentic design patterns)
- How to arrange agentic patterns visually on the canvas
- How to combine multiple patterns for complex systems
- How to build production-ready agentic workflows
- How to version and safely deploy agentic systems

---

## Part 1: Introduction to Agentic Design Patterns (20 minutes)

### What are Agentic Design Patterns?

**Agentic design patterns** are the ways that AI agents think, plan, and act to solve problems. Unlike llm calls that just respond to questions, agents have:

- **Agency:** They can take actions and make decisions
- **Memory:** They remember context across conversations
- **Tools:** They can use external tools and data sources
- **Planning:** They can break down complex tasks
- **Reflection:** They can review and improve their own work

**Why Agent Builder is Agentic-Native:**
Agent Builder is built specifically for creating agentic workflows. It's not just an ai feature builder - it's designed for agents that can think, plan, and act.

### The 5 Core Agentic Patterns We'll Learn

1. **Reflection Pattern** - Agent reviews its own work
2. **Tool Use Pattern** - Agent decides which tools to use
3. **Planning Pattern** - Agent breaks down complex tasks
4. **Multi-Agent Pattern** - Agents collaborate via handoffs
5. **Handoff/Delegation Pattern** - Agents delegate tasks to other agents

---

## Part 2: Agentic Design Pattern #1 - Reflection (20 minutes)

### What is Reflection?

**Reflection** is when an agent generates a response, then reviews it, and improves it if needed. It's like having a quality control step built into your agent.

**The Process:**
1. Agent drafts a response
2. Agent reviews the response: "Is this accurate? Complete? Polite?"
3. If good → Send to user
4. If needs work → Agent improves it

### How to Implement Reflection in Agent Builder

**Visual Structure:**
```
Start → Agent (draft) → Agent (critic) → If good → Response
                              ↓
                        If needs work
                              ↓
                     Agent (improver) → Response
```

**Step-by-Step Implementation:**

1. **Create Draft Agent:**
   - Prompt: "Draft a helpful response to the customer's question"
   - This agent creates the initial response

2. **Create Critic Agent:**
   - Prompt: "Review this response. Check: 1) Is it accurate? 2) Is it complete? 3) Is it polite? Return: 'good' or 'needs_work'"
   - This agent reviews the draft

3. **Add If/Else Logic:**
   - If critic returns "good" → Send response to user
   - If critic returns "needs_work" → Send to improver

4. **Create Improver Agent:**
   - Prompt: "Improve this response. Make it more accurate, complete, and polite"
   - This agent fixes any issues

### Example Use Case: Customer Support

**Scenario:** Customer asks "Why is my order delayed?"

**Draft Agent (Lisa, Customer Service Rep):** "Your order is delayed because of shipping issues."

**Critic Agent (Jennifer, Quality Assurance Manager):** "This is too vague. Needs more specific information about the delay reason, timeline, and what we're doing about it."

**Improver Agent (David, Senior Customer Service Rep):** "Your order is delayed due to weather conditions affecting our shipping partner in Memphis. We expect it to arrive within 2-3 business days. We've sent you a tracking update via email and will provide a $10 credit for the inconvenience."

### Key Nodes for Reflection Pattern

- **Multiple Agent nodes** in sequence
- **If/Else node** for quality check
- **Set State node** to store the draft response
- **Note nodes** to explain each step

---

## Part 3: Agentic Design Pattern #2 - Tool Use (20 minutes)

### What is Tool Use?

**Tool Use** is when an agent intelligently decides which tools to use based on the user's needs. Instead of hardcoding which tool to use, the agent makes smart choices.

**The Process:**
1. User asks a question
2. Agent analyzes: "What do I need to answer this?"
3. Agent chooses appropriate tools
4. Agent uses tools to gather information
5. Agent synthesizes the results

### How to Implement Tool Use in Agent Builder

**Visual Structure:**
```
Start → Agent (router) 
           ↓
      "What do I need?"
           ↓
   ┌───────┼───────┬───────┐
   ↓       ↓       ↓       ↓
File    Web    MCP    Guardrails
Search  Search  Node   Check
   └───────┴───────┴───────┘
           ↓
     Agent (synthesizer)
           ↓
        Response
```

**Step-by-Step Implementation:**

1. **Create Router Agent:**
   - Prompt: "Analyze the user's question. What information do I need? Choose from: knowledge_base, current_data, web_search, or safety_check"
   - This agent decides which tools to use

2. **Add Available Tools:**
   - File Search Node (for knowledge base)
   - Web Search Node (for current information)
   - MCP Node (for real-time data)
   - Guardrails Node (for safety checks)

3. **Create Synthesizer Agent:**
   - Prompt: "Combine the information from the tools to create a comprehensive answer"
   - This agent puts everything together

### Example Use Case: Product Information

**Scenario:** Customer asks "What's the latest price for the iPhone 15?"

**Router Agent (Alex, Product Information Specialist):** "This needs current pricing data" → Chooses MCP Node

**MCP Node:** Gets real-time pricing from Context7

**Synthesizer Agent (Maria, Sales Representative):** "The iPhone 15 starts at $799 for the base model. Here are the current prices for all variants..."

### Key Nodes for Tool Use Pattern

- **Agent node** that chooses tools
- **Multiple tool nodes** available
- **Agent node** that synthesizes results
- **If/Else logic** for tool selection

---

## Part 4: Agentic Design Pattern #3 - Planning (20 minutes)

### What is Planning?

**Planning** is when an agent breaks down a complex task into smaller steps, then executes each step while monitoring progress.

**The Process:**
1. Agent receives complex request
2. Agent creates a plan with steps
3. Agent executes each step
4. Agent checks if step succeeded
5. Agent adjusts plan if needed
6. Agent continues until complete

### How to Implement Planning in Agent Builder

**Visual Structure:**
```
Start → Agent (planner)
     "Break this into steps"
           ↓
     Set State (plan)
           ↓
      While (steps remain)
           ↓
     Agent (executor) → Execute step
           ↓
     Agent (evaluator) → Check progress
           ↓
     Update plan if needed
           ↓
        Response
```

**Step-by-Step Implementation:**

1. **Create Planner Agent:**
   - Prompt: "Break this complex task into 3-5 clear steps. Return the steps as a numbered list"
   - This agent creates the plan

2. **Store Plan in State:**
   - Use Set State node to save the plan
   - This allows other agents to access the plan

3. **Create While Loop:**
   - While there are steps remaining in the plan
   - This creates the execution loop

4. **Create Executor Agent:**
   - Prompt: "Execute the next step in the plan. Use available tools as needed"
   - This agent does the work

5. **Create Evaluator Agent:**
   - Prompt: "Did this step succeed? What's the status? Return: 'success', 'partial', or 'failed'"
   - This agent checks progress

### Example Use Case: Return and Refund Process

**Scenario:** Customer says "I need to return this product and get a refund"

**Planner Agent (Tom, Returns Manager):** 
1. Verify the purchase
2. Check return policy
3. Calculate refund amount
4. Process the refund
5. Send confirmation

**Executor Agent (Sarah, Returns Specialist):** Executes each step using appropriate tools

**Evaluator Agent (Jennifer, Quality Control):** Checks if each step succeeded

### Key Nodes for Planning Pattern

- **Agent node** for planning
- **Set State** to store plan
- **While loop** for execution
- **Agent nodes** for each step
- **If/Else** for success/failure handling

---

## Part 5: Agentic Design Pattern #4 - Multi-Agent (20 minutes)

### What is Multi-Agent?

**Multi-Agent** systems use multiple specialized agents working together. Each agent has specific expertise and they hand off work to each other based on need.

**The Process:**
1. Router agent analyzes the request
2. Router determines which specialist is needed
3. Request is handed off to specialist
4. Specialist uses their expertise and tools
5. If specialist can't solve it, escalate to human

### How to Implement Multi-Agent in Agent Builder

**Visual Structure:**
```
Start → Router Agent
     "What type of issue?"
           ↓
       If/Else
      /   |   \
     /    |    \
Billing Tech General ← Specialist Agents
Agent   Agent Agent
     \    |    /
      \   |   /
    Escalation Agent ← Fallback
           ↓
        Response
```

**Step-by-Step Implementation:**

1. **Create Router Agent:**
   - Prompt: "Analyze the customer's issue. Determine if it's: billing, technical, or general. Return: 'billing', 'technical', or 'general'"
   - This agent decides which specialist to use

2. **Add If/Else Routing:**
   - If "billing" → Billing Agent
   - If "technical" → Technical Agent
   - If "general" → General Agent

3. **Create Specialist Agents:**
   - **Billing Agent:** "You handle billing questions. Use File Search for policies and MCP for current account data"
   - **Technical Agent:** "You solve technical issues. Search documentation and use troubleshooting guides"
   - **General Agent:** "You handle general inquiries. Be helpful and polite"

4. **Add Escalation Path:**
   - If any specialist can't solve the issue
   - Escalate to human with full context

### Example Use Case: Customer Support Triage

**Scenario:** Customer says "My payment was charged twice"

**Router Agent (Lisa, Customer Service Manager):** "This is a billing issue" → Routes to Billing Agent

**Billing Agent (Sarah, Billing Specialist):** 
- Searches billing policies
- Checks account data via MCP
- Provides specific refund process

**If Billing Agent can't resolve:** Escalates to human (Billing Manager) with all context

### Key Nodes for Multi-Agent Pattern

- **Router Agent node**
- **If/Else** for routing
- **Multiple specialist Agent nodes**
- **Human Approval** for escalation
- **Set State** to pass context between agents

---

## Part 6: Agentic Design Pattern #5 - Handoff/Delegation (20 minutes)

### What is Handoff/Delegation?

**Handoff/Delegation** is when one agent delegates a specific task to another agent with specialized expertise, then receives the result back to continue the workflow.

**The Process:**
1. Primary agent receives request
2. Primary agent identifies task that needs specialized expertise
3. Primary agent delegates task to specialist agent
4. Specialist agent completes the task
5. Specialist agent returns result to primary agent
6. Primary agent continues with the complete workflow

### How to Implement Handoff/Delegation in Agent Builder

**Visual Structure:**
```
Start → Primary Agent
     "What do I need to delegate?"
           ↓
     [If/Else] ← Check if delegation needed
           ↓
     [Specialist Agent] ← Delegated task
           ↓
     [Return Result] ← Back to primary
           ↓
     Primary Agent ← Continue workflow
           ↓
     [Response]
```

**Step-by-Step Implementation:**

1. **Create Primary Agent:**
   - Prompt: "Analyze this request. Do I need to delegate any tasks to specialists? Return: 'delegate_to_[specialist]' or 'handle_myself'"
   - This agent decides when to delegate

2. **Add Delegation Logic:**
   - If delegation needed → Route to specialist
   - If not needed → Handle directly

3. **Create Specialist Agents:**
   - **Data Analyst:** "You analyze data and provide insights"
   - **Legal Advisor:** "You review legal implications and provide guidance"
   - **Technical Expert:** "You solve complex technical problems"

4. **Add Return Logic:**
   - Specialist completes task
   - Returns result to primary agent
   - Primary agent incorporates result into final response

### Example Use Case: Business Decision Support

**Scenario:** CEO asks "Should we acquire this startup?"

**Primary Agent (James, Business Strategy Manager):** "This needs financial analysis, legal review, and technical assessment" → Delegates to specialists

**Data Analyst Agent (Carlos, Data Analyst):** Analyzes financials, market data, growth projections
**Legal Advisor Agent (Amanda, Legal Advisor):** Reviews contracts, regulatory issues, IP concerns  
**Technical Expert Agent (Mike, Technical Expert):** Evaluates technology stack, team expertise, integration challenges

**Primary Agent (James, Business Strategy Manager):** Combines all inputs into comprehensive recommendation

### Key Nodes for Handoff/Delegation Pattern

- **Primary Agent node** that decides when to delegate
- **If/Else** for delegation decision
- **Specialist Agent nodes** for specific expertise
- **Set State** to pass context and results
- **Return logic** to bring results back to primary

---

## Part 7: Visual Workflow Patterns (30 minutes)

### How to Arrange Agentic Patterns on Canvas

Now that you understand the agentic patterns, let's learn how to arrange them visually on the Agent Builder canvas.

**Pattern 1: Sequential (for Reflection)**
- **Visual Layout:** Linear arrangement left to right
- **Flow:** Draft → Critic → Improver
- **Best for:** Quality control workflows
- **Canvas tip:** Keep nodes aligned horizontally

**Pattern 2: Parallel (for Tool Use)**
- **Visual Layout:** Tools arranged in parallel branches
- **Flow:** Router → Multiple tools → Synthesizer
- **Best for:** Information gathering
- **Canvas tip:** Group tools vertically, converge to synthesizer

**Pattern 3: Circular (for Planning)**
- **Visual Layout:** Loop structure with While node
- **Flow:** Planner → While loop → Executor → Evaluator
- **Best for:** Multi-step processes
- **Canvas tip:** Use While node to create the loop

**Pattern 4: Branching (for Multi-Agent)**
- **Visual Layout:** Router at top, branches below
- **Flow:** Router → If/Else → Specialists
- **Best for:** Specialized expertise
- **Canvas tip:** Align specialists at same level

### Visual Best Practices

**Layout Guidelines:**
- **Left to right** for time flow
- **Top to bottom** for decisions
- **Group related agents** together
- **Use Note nodes** to explain complex patterns
- **Avoid crossing arrows** when possible

**Readability Tips:**
- Keep nodes aligned on grid
- Use whitespace between sections
- Label all branches clearly
- Add Note nodes for documentation

**Common Visual Mistakes:**
- Spaghetti diagrams (too many crossing lines)
- Nodes too close together
- Unclear branch labels
- Missing fallback paths

---

## Part 7: Comprehensive Hands-On Lab (60 minutes)

### Lab: Customer Support System Using All 5 Agentic Patterns

**System Overview:**
Build one comprehensive agent that uses:
1. **Tool Use** - Decides which knowledge source to use
2. **Multi-Agent** - Routes to specialist agents
3. **Reflection** - Each specialist reviews its answer
4. **Handoff/Delegation** - Specialists delegate complex tasks
5. **Planning** - For complex multi-step issues

**Visual Structure:**
```
        [Start]
           ↓
    [Router Agent] ← Pattern 4: Multi-Agent
    "Analyze issue"
           ↓
       [If/Else]
      /   |   \
     /    |    \
[Billing][Tech][General] ← Specialists
     |     |     |
     ↓     ↓     ↓
[Tool Use] ← Pattern 2
File Search or MCP
     |     |     |
     ↓     ↓     ↓
[Draft Response]
     |     |     |
     ↓     ↓     ↓
[Critic Agent] ← Pattern 1: Reflection
"Is this good?"
     |     |     |
     ↓     ↓     ↓
 [If/Else]
Good? → Response
Bad? → [Improver Agent] → Response
     
[Fallback: Human Approval] ← If all fails
```

### Step-by-Step Lab Instructions

**Step 1: Build Multi-Agent Structure (15 min)**

1. Create Router Agent:
   - Prompt: "Analyze the customer issue. Return: billing, technical, or general"
   - This determines which specialist to use

2. Add If/Else node with 3 branches:
   - Branch 1: billing
   - Branch 2: technical  
   - Branch 3: general

3. Create 3 specialist agents:
   - **Billing Agent:** "You handle billing questions. Be specific about policies and procedures."
   - **Technical Agent:** "You solve technical issues. Use troubleshooting guides and documentation."
   - **General Agent:** "You handle general inquiries. Be helpful and professional."

**Step 2: Add Tool Use Pattern (15 min)**

1. In each specialist, enable File Search tool:
   - Connect to your knowledge base from Session 5
   - Configure to search relevant documents

2. Add MCP Node for real-time data:
   - Connect to Context7 from Session 5
   - Configure for current information

3. Configure each agent to choose tools:
   - Prompt: "Use File Search for policies and procedures. Use MCP for current account data or shipping information."

**Step 3: Add Reflection Pattern (15 min)**

1. After each specialist, add Critic Agent:
   - Prompt: "Review this response. Check: 1) Is it accurate? 2) Is it complete? 3) Is it polite? Return: 'good' or 'needs_work'"

2. Add If/Else after critic:
   - If "good" → Send response to user
   - If "needs_work" → Send to Improver Agent

3. Create Improver Agent:
   - Prompt: "Improve this response. Make it more accurate, complete, and polite while keeping the same information."

**Step 4: Add Human Approval (10 min)**

1. For refunds over $100, add Human Approval node:
   - After Billing Agent, add condition: "If refund_amount > $100"
   - Route to Human Approval node
   - Configure approval message with context

2. Add fallback for complex issues:
   - If any specialist can't solve → Escalate to human
   - Include full conversation context

**Step 5: Test All Patterns (10 min)**

1. **Test Tool Use:**
   - Ask: "What's your return policy?"
   - Should use File Search

2. **Test Multi-Agent:**
   - Ask: "I was charged twice for my order"
   - Should route to Billing Agent

3. **Test Reflection:**
   - Ask a complex question
   - Should see critic and improver in action

4. **Test Human Approval:**
   - Ask: "I want a refund for my $500 order"
   - Should trigger human approval

---

## Part 8: Pattern Reference Guide (15 minutes)

### Quick Reference: When to Use Each Pattern

| Pattern | When to Use | Key Benefit |
|---------|-------------|-------------|
| Reflection | Quality matters, high stakes | Catches errors before user sees |
| Tool Use | Multiple data sources available | Agent chooses right tool intelligently |
| Planning | Multi-step complex tasks | Breaks down into manageable steps |
| Multi-Agent | Different types of expertise needed | Specialists handle their domain |
| Handoff/Delegation | Need specialized expertise for specific tasks | Agents delegate to domain experts |

### Combining Patterns

**Reflection + Tool Use:**
- Agent picks appropriate tool
- Agent uses tool to gather information
- Agent reflects on the result
- Agent improves if needed

**Multi-Agent + Reflection:**
- Router determines specialist
- Specialist uses tools
- Specialist reflects on response
- Specialist improves if needed

**Planning + Tool Use:**
- Agent creates plan
- Each step chooses appropriate tools
- Agent monitors progress
- Agent adjusts plan based on results

**All 5 Patterns:**
- Complex production system
- Router determines specialist
- Specialist delegates complex tasks
- Specialist plans approach
- Specialist uses tools
- Specialist reflects on results
- Human approval for high-stakes decisions

---

## Part 9: Versioning & Safe Launches (10 minutes)

### Versioning Agentic Workflows

**Documentation Strategy:**
- Document which patterns you're using
- Track changes to agent prompts
- Note changes to routing logic
- Version examples:
  - v1.0: Basic multi-agent routing
  - v1.1: Added reflection pattern
  - v2.0: Added planning for complex issues

**Change Log Template:**
```
v1.1 - Added Reflection Pattern
- Added Critic Agent to all specialists
- Added Improver Agent for quality control
- Updated routing logic to include reflection
- Tested with 50 customer scenarios
```

### Safe Launch Strategy

**Testing Approach:**
1. Test each agentic pattern individually first
2. Start with simpler patterns (tool use, multi-agent)
3. Add reflection and planning once stable
4. Monitor agent decision-making in traces

**Launch Checklist:**
- [ ] All patterns tested individually
- [ ] Combined workflow tested end-to-end
- [ ] Human approval paths verified
- [ ] Fallback escalation working
- [ ] Performance monitoring enabled
- [ ] Rollback plan ready

---

## Part 10: Review & Next Steps (10 minutes)

### Key Takeaways

1. **Agent Builder is agentic-native** - Use agentic patterns, not just chatbot patterns
2. **5 core patterns** - Reflection, Tool Use, Planning, Multi-Agent, Handoff/Delegation
3. **Visual patterns** show HOW to arrange agentic patterns on canvas
4. **Production systems** combine multiple patterns for complex workflows
5. **Quality matters** - Use reflection and human approval for important decisions

### Preparation for Session 7

**What's Next:**
- We'll deploy our agentic system
- We'll learn evals to measure agent quality
- We'll add more sophisticated guardrails
- We'll monitor agent decisions and improve

**Think About:**
- Which patterns worked best in your lab?
- What would you add to make it more robust?
- How would you measure success?

---

## Resources

### Official Documentation
- [OpenAI Agent Builder Guide](https://platform.openai.com/docs/guides/agent-builder)
- [Agent Design Patterns](https://platform.openai.com/docs/guides/agent-design-patterns)
- [Multi-Agent Systems](https://platform.openai.com/docs/guides/multi-agent-systems)

### Lab Instructions
- [Comprehensive Lab Guide](lab_agentic_system.md)

---

## Glossary

**Agentic Design Pattern:** A way that AI agents think, plan, and act to solve problems

**Reflection Pattern:** Agent reviews and improves its own work

**Tool Use Pattern:** Agent intelligently chooses which tools to use

**Planning Pattern:** Agent breaks down complex tasks into steps

**Multi-Agent Pattern:** Multiple specialized agents working together

**Visual Workflow Pattern:** How to arrange agentic patterns on the canvas

**Router Agent:** Agent that determines which specialist to use

**Specialist Agent:** Agent with specific domain expertise

**Human-in-the-Loop:** Including human oversight in automated processes

**Escalation:** Passing complex issues to human agents

---

*Use this guide during the session, for self-study, or as a reference when building your own agentic workflows.*
