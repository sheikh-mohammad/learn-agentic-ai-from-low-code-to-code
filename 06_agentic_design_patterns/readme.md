# Session 6: Agentic Design Patterns

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
- Lab: Customer Support System Using All 4 Agentic Patterns
  [Customer Support System](lab_agentic_system.md)
---

## Introduction to Agentic Design Patterns  

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

## 1. Agentic Design Pattern #1 - Reflection

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

### Example Use Case: [Essay Generator](./01_reflection_pattern/readme.md)

---

## 2. Agentic Design Pattern #2 - Tool Use

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
Start → Agent
           ↓
      "What do I need?"
           ↓
   ┌───────┼───────┐
   ↓       ↓       ↓
  File    Web     MCP
  Search  Search  Node
   └───────┴───────┘
           ↓
        Response
```

### Example Use Case: [Personal Assistant](./02_tool_use_pattern/readme.md)

### Key Nodes for Tool Use Pattern

- **Agent node** that chooses tools
- **Multiple tool nodes** available
---

## 3. Agentic Design Pattern #3 - Planning

### What is Planning?

**Planning** is when one agent creates a strategic plan by breaking down a complex task into actionable steps, and another agent executes that plan systematically. This pattern separates strategic thinking from execution.

**The Process:**
1. Planner agent receives complex request
2. Planner agent analyzes the task and creates a structured plan with clear steps
3. Executor agent receives the plan
4. Executor agent follows each step systematically
5. Final output reflects completion of all planned steps

### How to Implement Planning in Agent Builder

**Visual Structure:**
```
Start → Agent (planner)
     "Break this into steps"
           ↓
     Agent (executor)
     "Follow the plan"
           ↓
        Response
```


### Example Use Case: [Research Report Generator](./03_planning_pattern/readme.md)

---

## 4. Agentic Design Pattern #4 - Multi-Agent

### What is Multi-Agent?

**Multi-Agent** systems use multiple specialized agents working together. Each agent has specific expertise and they hand off work to each other based on need.

**The Process:**
1. Router agent analyzes the request
2. Router determines which specialist is needed
3. Request is handed off to specialist
4. Specialist uses their expertise and tools
5. If specialist can't solve it, escalate to human

### Example Use Case: [Task Planning Assistant](./04_multi_agent_pattern/multi_agent_pattern.md)

---

## 5. Agentic Design Pattern #5 - Handoff/Delegation

### What is Handoff/Delegation?

**Handoff/Delegation** is when one agent delegates a specific task to another agent with specialized expertise, then receives the result back to continue the workflow.

**The Process:**
1. Primary agent receives request
2. Primary agent identifies task that needs specialized expertise
3. Primary agent delegates task to specialist agent
4. Specialist agent completes the task
5. Specialist agent returns result to primary agent
6. Primary agent continues with the complete workflow

### Example Use Case: [Grammar Correction Assistant](./05_handoff_delegation_pattern/handoff_delegation_pattern.md)

---

## Agentic Pattern Reference Guide  

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

## Review & Next Steps

### Key Takeaways

1. **Agent Builder is agentic-native** - Use agentic patterns, not just chatbot patterns
2. **5 core patterns** - Reflection, Tool Use, Planning, Multi-Agent, Handoff/Delegation
3. **Production systems** combine multiple patterns for complex workflows
4. **Quality matters** - Use reflection and human approval for important decisions

### Lab: Customer Support System Using All 4 Agentic Patterns
- [Customer Support System](lab_agentic_system.md)

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


**Router Agent:** Agent that determines which specialist to use

**Specialist Agent:** Agent with specific domain expertise

**Human-in-the-Loop:** Including human oversight in automated processes

**Escalation:** Passing complex issues to human agents

---

*Use this guide during the session, for self-study, or as a reference when building your own agentic workflows.*
