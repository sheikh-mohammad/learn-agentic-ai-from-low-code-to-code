# Lab: Customer Support System Using All 4 Agentic Patterns

**Duration:** 60 minutes  
**Level:** Intermediate  
**Prerequisites:** Sessions 4 & 5 (Agent Builder, File Search, Connectors, MCP)

---

## Lab Overview

Build a comprehensive customer support system that demonstrates all 5 agentic design patterns:
1. **Multi-Agent Pattern** - Route to specialist agents
2. **Tool Use Pattern** - Choose appropriate tools
3. **Reflection Pattern** - Review and improve responses
4. **Planning Pattern** - Handle complex multi-step issues
5. **Handoff/Delegation Pattern** - Delegate tasks between agents

---

## System Architecture

**Visual Structure:**
```
        [Start]
           ↓
    [Router Agent] ← Multi-Agent Pattern
    "Analyze issue"
           ↓
       [If/Else]
      /   |   \
     /    |    \
[Billing][Tech][General] ← Specialist Agents
     |     |     |
     ↓     ↓     ↓
[Tool Use] ← Tool Use Pattern
File Search or MCP
     |     |     |
     ↓     ↓     ↓
[Draft Response]
     |     |     |
     ↓     ↓     ↓
[Critic Agent] ← Reflection Pattern
"Is this good?"
     |     |     |
     ↓     ↓     ↓
 [If/Else]
Good? → Response
Bad? → [Improver Agent] → Response
     
[Fallback: Human Approval] ← For complex issues
```

---

## Step 1: Build Multi-Agent Structure (15 minutes)

### 1.1 Create Router Agent

**Purpose:** Determine which specialist agent should handle the customer's issue.

**Configuration:**
- **Node Type:** Agent
- **Name:** "Router Agent"
- **Prompt:** 
```
Analyze the customer's issue and determine which specialist should handle it.

Return exactly one of these values:
- "billing" - for payment, refund, pricing, account issues
- "technical" - for product problems, troubleshooting, technical support
- "general" - for general questions, information, basic support

Customer issue: {{user_input}}

Return only: billing, technical, or general
```

**Test the Router:**
- "I was charged twice for my order" → Should return "billing"
- "My app keeps crashing" → Should return "technical"
- "What are your business hours?" → Should return "general"

### 1.2 Add If/Else Routing

**Purpose:** Route to the appropriate specialist based on router's decision.

**Configuration:**
- **Node Type:** If/Else
- **Condition:** `{{router_agent_output}} == "billing"`
- **True Branch:** Route to Billing Agent
- **False Branch:** Add another If/Else for technical vs general

**Second If/Else:**
- **Condition:** `{{router_agent_output}} == "technical"`
- **True Branch:** Route to Technical Agent
- **False Branch:** Route to General Agent

### 1.3 Create Specialist Agents

**Billing Agent:**
- **Node Type:** Agent
- **Name:** "Billing Agent"
- **Prompt:**
```
You are Sarah, a Billing Specialist with 5 years experience. Handle payment, refund, pricing, and account issues.

Be specific about:
- Policy details and procedures
- Exact amounts and timelines
- Required documentation
- Next steps for the customer

Customer issue: {{user_input}}
```

**Technical Agent:**
- **Node Type:** Agent
- **Name:** "Technical Agent"
- **Prompt:**
```
You are Mike, a Technical Support Specialist with 8 years experience. Solve product problems and provide troubleshooting.

Be specific about:
- Step-by-step solutions
- Technical requirements
- Known issues and workarounds
- When to escalate to engineering

Customer issue: {{user_input}}
```

**General Agent:**
- **Node Type:** Agent
- **Name:** "General Agent"
- **Prompt:**
```
You are Lisa, a Customer Service Representative with 3 years experience. Handle general questions and provide information.

Be helpful about:
- Company information
- Basic product questions
- General policies
- Directing to appropriate specialists

Customer issue: {{user_input}}
```

---

## Step 2: Add Tool Use Pattern (15 minutes)

### 2.1 Enable File Search in Each Specialist

**Purpose:** Give each specialist access to relevant knowledge base documents.

**Configuration for Billing Agent:**
- **Node Type:** File Search
- **Name:** "Billing Knowledge Base"
- **Vector Store:** Connect to your billing policies vector store from Session 5
- **Search Query:** `{{user_input}}`

**Configuration for Technical Agent:**
- **Node Type:** File Search
- **Name:** "Technical Documentation"
- **Vector Store:** Connect to your technical docs vector store from Session 5
- **Search Query:** `{{user_input}}`

**Configuration for General Agent:**
- **Node Type:** File Search
- **Name:** "General Knowledge Base"
- **Vector Store:** Connect to your general knowledge vector store from Session 5
- **Search Query:** `{{user_input}}`

### 2.2 Add MCP Node for Real-Time Data

**Purpose:** Provide access to current account and shipping information.

**Configuration:**
- **Node Type:** MCP Node
- **Name:** "Real-Time Data"
- **MCP Server:** Connect to Context7 from Session 5
- **Features:** Enable account data and shipping information
- **Query:** `{{user_input}}`

### 2.3 Update Specialist Prompts for Tool Use

**Updated Billing Agent Prompt:**
```
You are Sarah, a Billing Specialist. Use the available tools to get accurate information.

Available tools:
- File Search: For policies and procedures
- MCP Node: For current account data and shipping info

Use File Search for policy questions.
Use MCP Node for current account status or shipping information.

Customer issue: {{user_input}}
```

**Updated Technical Agent Prompt:**
```
You are Mike, a Technical Support Specialist. Use the available tools to solve problems.

Available tools:
- File Search: For documentation and troubleshooting guides
- MCP Node: For current system status and known issues

Use File Search for documentation and guides.
Use MCP Node for current system status.

Customer issue: {{user_input}}
```

**Updated General Agent Prompt:**
```
You are Lisa, a Customer Service Representative. Use the available tools to provide information.

Available tools:
- File Search: For general company information
- MCP Node: For current business hours and contact info

Use File Search for company information.
Use MCP Node for current business hours and contact details.

Customer issue: {{user_input}}
```

---

## Step 3: Add Reflection Pattern (15 minutes)

### 3.1 Create Critic Agent

**Purpose:** Review each specialist's response for quality.

**Configuration:**
- **Node Type:** Agent
- **Name:** "Critic Agent"
- **Prompt:**
```
You are Jennifer, a Quality Assurance Manager. Review this customer service response for quality.

Check these criteria:
1. Is it accurate? (factually correct)
2. Is it complete? (answers the customer's question fully)
3. Is it polite? (professional and helpful tone)
4. Is it actionable? (gives clear next steps)

Response to review: {{specialist_agent_output}}

Return exactly: "good" or "needs_work"
```

### 3.2 Add Quality Check Logic

**Purpose:** Route responses based on quality assessment.

**Configuration:**
- **Node Type:** If/Else
- **Condition:** `{{critic_agent_output}} == "good"`
- **True Branch:** Send response to user
- **False Branch:** Send to Improver Agent

### 3.3 Create Improver Agent

**Purpose:** Improve responses that need work.

**Configuration:**
- **Node Type:** Agent
- **Name:** "Improver Agent"
- **Prompt:**
```
You are David, a Senior Customer Service Representative. Improve this customer service response. Make it more accurate, complete, polite, and actionable.

Original response: {{specialist_agent_output}}
Customer issue: {{user_input}}

Improve the response while keeping the same core information.
```

### 3.4 Connect Reflection to All Specialists

**For each specialist (Billing, Technical, General):**
1. Add Critic Agent after the specialist
2. Add If/Else for quality check
3. Add Improver Agent for the "needs_work" branch
4. Connect "good" branch to final response

---

## Step 4: Add Handoff/Delegation Pattern (15 minutes)

### 4.1 Create Delegation Logic

**Purpose:** Allow specialists to delegate complex tasks to other specialists.

**Configuration:**
- **Node Type:** If/Else
- **Condition:** After each specialist, check if task needs delegation
- **True Branch:** Route to appropriate specialist
- **False Branch:** Continue with reflection

### 4.2 Add Delegation Specialists

**Legal Specialist:**
- **Node Type:** Agent
- **Name:** "Legal Specialist"
- **Prompt:**
```
You are Amanda, a Legal Advisor with 10 years experience. Handle legal questions, policy interpretation, and compliance issues.

Be specific about:
- Legal requirements and regulations
- Policy implications
- Compliance considerations
- When to escalate to legal team

Delegated task: {{delegated_task}}
```

**Data Analyst:**
- **Node Type:** Agent
- **Name:** "Data Analyst"
- **Prompt:**
```
You are Carlos, a Data Analyst with 6 years experience. Analyze data, create reports, and provide insights.

Be specific about:
- Data analysis and trends
- Statistical insights
- Report generation
- Data visualization recommendations

Delegated task: {{delegated_task}}
```

### 4.3 Update Specialist Prompts for Delegation

**Updated Billing Agent Prompt:**
```
You are Sarah, a Billing Specialist. Use the available tools to get accurate information.

Available tools:
- File Search: For policies and procedures
- MCP Node: For current account data and shipping info

If you encounter legal questions about billing policies, delegate to Legal Specialist.
If you need data analysis of billing trends, delegate to Data Analyst.

Customer issue: {{user_input}}
```

**Updated Technical Agent Prompt:**
```
You are Mike, a Technical Support Specialist. Use the available tools to solve problems.

Available tools:
- File Search: For documentation and troubleshooting guides
- MCP Node: For current system status and known issues

If you encounter legal questions about data privacy or compliance, delegate to Legal Specialist.
If you need analysis of technical performance data, delegate to Data Analyst.

Customer issue: {{user_input}}
```

### 4.4 Add Return Logic

**Purpose:** Return delegated results back to original specialist.

**Configuration:**
- **Node Type:** Set State
- **Action:** Store delegated result
- **Return to:** Original specialist for final response

---

## Step 5: Add Human Approval (10 minutes)

### 5.1 Add Human Approval for High-Value Refunds

**Purpose:** Require human approval for refunds over $100.

**Configuration:**
- **Node Type:** Human Approval
- **Name:** "High-Value Refund Approval"
- **Condition:** After Billing Agent, check if refund amount > $100
- **Approval Message:** 
```
High-value refund request requires approval.

Customer: {{user_input}}
Proposed refund: {{refund_amount}}
Context: {{billing_agent_output}}

Please review and approve or modify the refund amount.
```

### 5.2 Add Escalation for Complex Issues

**Purpose:** Escalate issues that specialists can't resolve.

**Configuration:**
- **Node Type:** Human Approval
- **Name:** "Complex Issue Escalation"
- **Condition:** If any specialist indicates they can't resolve
- **Escalation Message:**
```
Complex issue requires human intervention.

Customer: {{user_input}}
Specialist: {{specialist_name}}
Attempted solution: {{specialist_output}}
Reason for escalation: {{escalation_reason}}

Please take over this case.
```

---

## Step 6: Test All Patterns (10 minutes)

### 6.1 Test Tool Use Pattern

**Test Case 1: Policy Question**
- **Input:** "What's your return policy for electronics?"
- **Expected:** Should use File Search for policy information
- **Verify:** Response includes specific policy details

**Test Case 2: Current Account Status**
- **Input:** "What's the status of my order #12345?"
- **Expected:** Should use MCP Node for real-time data
- **Verify:** Response includes current order status

### 6.2 Test Multi-Agent Pattern

**Test Case 1: Billing Issue**
- **Input:** "I was charged twice for my order"
- **Expected:** Should route to Billing Agent
- **Verify:** Response is billing-focused

**Test Case 2: Technical Issue**
- **Input:** "My app keeps crashing on startup"
- **Expected:** Should route to Technical Agent
- **Verify:** Response includes troubleshooting steps

**Test Case 3: General Question**
- **Input:** "What are your business hours?"
- **Expected:** Should route to General Agent
- **Verify:** Response includes business hours

### 6.3 Test Reflection Pattern

**Test Case 1: Good Response**
- **Input:** "What's your return policy?"
- **Expected:** Critic should return "good"
- **Verify:** Response goes directly to user

**Test Case 2: Needs Improvement**
- **Input:** "I want a refund" (vague request)
- **Expected:** Critic should return "needs_work"
- **Verify:** Improver Agent enhances the response

### 6.4 Test Handoff/Delegation Pattern

**Test Case 1: Legal Question**
- **Input:** "Is it legal to charge a restocking fee for electronics?"
- **Expected:** Should delegate to Legal Specialist
- **Verify:** Response includes legal analysis

**Test Case 2: Data Analysis Request**
- **Input:** "Can you analyze my billing history for the past year?"
- **Expected:** Should delegate to Data Analyst
- **Verify:** Response includes data insights

### 6.5 Test Human Approval

**Test Case 1: High-Value Refund**
- **Input:** "I want a refund for my $500 order"
- **Expected:** Should trigger human approval
- **Verify:** Human approval node is activated

**Test Case 2: Complex Issue**
- **Input:** "I have a unique problem that doesn't fit any category"
- **Expected:** Should escalate to human
- **Verify:** Escalation message is sent

---

## Lab Completion Checklist

- [ ] Router Agent correctly identifies issue types
- [ ] If/Else routing works for all three specialists
- [ ] Each specialist has access to File Search and MCP Node
- [ ] Specialists use tools appropriately
- [ ] Critic Agent reviews responses accurately
- [ ] Improver Agent enhances poor responses
- [ ] Human approval triggers for high-value refunds
- [ ] Escalation works for complex issues
- [ ] All patterns work together seamlessly
- [ ] System handles edge cases gracefully

---

## Troubleshooting

### Common Issues

**Router not working:**
- Check prompt format and expected output values
- Ensure If/Else conditions match router output exactly

**Tools not being used:**
- Verify File Search and MCP Node connections
- Check specialist prompts mention available tools

**Reflection not working:**
- Ensure Critic Agent output format matches If/Else condition
- Check that all specialists connect to reflection flow

**Human approval not triggering:**
- Verify approval conditions are correctly set
- Check that approval messages include necessary context

### Debug Tips

1. **Use Note nodes** to document each section
2. **Test each pattern individually** before combining
3. **Check agent outputs** in the trace view
4. **Verify tool connections** are working
5. **Test with simple cases first** before complex scenarios

---

## Next Steps

After completing this lab, you should be able to:
- Build multi-agent systems with specialized roles
- Implement intelligent tool selection
- Add quality control through reflection
- Include human oversight where needed
- Combine all patterns for complex workflows

**Ready for Session 7:** Deploy and monitor your agentic system!
