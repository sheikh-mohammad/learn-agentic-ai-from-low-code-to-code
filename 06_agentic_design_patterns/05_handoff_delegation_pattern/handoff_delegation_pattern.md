## Agentic Design Pattern - Handoff/Delegation (20 minutes)

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
   - Task: Decide whether to fix the grammar itself or delegate to the Grammar Specialist.  
   - Prompt Example:
     ```
     You are a writing assistant.
     - If grammar issues are simple, fix them directly and return the corrected text.
     - If grammar issues are complex, delegate to the Grammar Specialist.
     - If you are unsure, ask for clarification.

     Output format:
     - { "final_output": "<corrected_text>" }
     - { "delegate_to": "grammar", "text": "<user_text>" }
     - { "escalate": true, "reason": "<why>" }
     ```

2. **Add Delegation Logic:**
   - If the Primary Agent decides delegation is needed → Route to Grammar Specialist.  
   - If not needed → Return the corrected response directly to the user.  

3. **Create Grammar Specialist Agent:**
   - Task: Handle complex grammar, structure, and tone corrections.  
   - Prompt Example:
     ```
     You are a Grammar Specialist.
     Input: { "text": "<user_text>" }
     Task: Correct grammar, punctuation, and sentence structure while keeping meaning unchanged.
     Return JSON:
       { "corrected_text": "<corrected_version>" }
     ```

4. **Add Return Logic:**
   - Grammar Specialist returns the corrected result.  
   - Primary Agent receives it and provides the final output to the user.  
   - If escalation is needed, route to Escalation Agent for clarification.

---

### Summary of Logic
- **If simple issue:** Primary Agent fixes directly  
- **If complex issue:** Delegate to Grammar Specialist  
- **If unclear:** Escalate for clarification

### Example Use Case: Grammar Correction Assistant

**Scenario:** User says, "This sentence have a mistake and need to be fix."

**Primary Agent (Writing Assistant):**  
Analyzes the text and decides:  
- The issue is simple → fixes it directly:  
  ✅ “This sentence has a mistake and needs to be fixed.”

**If the issue is complex (e.g., multiple sentences or tone adjustment):**  
- Delegates to **Grammar Specialist Agent** for detailed correction.

**Grammar Specialist Agent:**  
Improves grammar, punctuation, and flow, then returns the corrected text.

**Primary Agent:**  
Receives the result and provides the final corrected response to the user.

---

### Key Nodes for Handoff/Delegation Pattern

- **Primary Agent node** (decides when to delegate)  
- **If/Else** for delegation decision  
- **Grammar Specialist Agent node** (handles complex grammar fixes)  
- **Set State** to share text between agents  
- **Return logic** to send final corrected text to the user

---
