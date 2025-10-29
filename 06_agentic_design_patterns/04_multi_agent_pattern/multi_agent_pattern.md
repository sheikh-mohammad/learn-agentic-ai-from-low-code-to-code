# Example Use Case: Task Planning Assistant

**Scenario:** User says, "Help me plan my day so I can stay focused and not forget my meetings."

**Router Agent:**  
Analyzes the request and decides it’s a **schedule** task → routes to **Schedule Agent**.

**Schedule Agent:**  
Creates a simple daily plan with time blocks.

If the user also needs focus tips or reminders:  
- **Focus Agent** gives short tips (e.g., “Use Pomodoro 50/10”).  
- **Reminder Agent** adds quick reminders (e.g., “08:45 — Prep for meeting”).

If the request is unclear → **Escalation Agent** asks a clarifying question.

---

## How to Implement Multi-Agent in Agent Builder

**Visual Structure:**
```
Start → Router Agent
     "What does the user need help with?"
            ↓
          If/Else
      /      |       \
     /       |        \
Schedule   Focus    Reminder  ← Specialist Agents
 Agent     Agent      Agent
      \       |       /
       \      |      /
     (If unclear, conflict, or missing info)
           ↓
     Escalation Agent ← Fallback
           ↓
        Final Response

```

**Step-by-Step Implementation:**

1. **Create Router Agent (Coordinator):**  
   - **Purpose:** Analyze the user’s request and decide which type of planning help is needed.  
   - **Prompt Example:**  
     ```
     Analyze the user's request and determine the main need.  
     Return one of:  
     - "schedule" → if the user wants help planning their day or tasks  
     - "focus" → if the user wants productivity or focus tips  
     - "reminder" → if the user wants help remembering things  
     - "escalate" → if the intent is unclear
     Output format: { "route": "<one_of_schedule_focus_reminder_escalate>" }
     ```
   - **Example Output:**  
     ```json
     { "route": "schedule" }
     ```

2. **Add If/Else Routing:**  
   - If `"route" == "schedule"` → **Schedule Agent**  
   - Else if `"route" == "focus"` → **Focus Agent**  
   - Else if `"route" == "reminder"` → **Reminder Agent**  
   - Else → **Escalation Agent**  

3. **Create Specialist Agents:**  
   - **Schedule Agent:**  
     "You create a simple daily schedule with realistic time blocks (e.g., 09:00–10:00 — Meeting).    
   - **Focus Agent:**  
     "You give short, practical productivity tips for each major task (e.g., Pomodoro 50/10, silence notifications).  
   - **Reminder Agent:**  
     "You generate short, time-based reminders (e.g., 08:45 — Prep for Meeting).  

4. **Add Escalation Path (Fallback Case):**  
   - Triggered when the Router cannot confidently classify the request or a specialist reports missing info.  
   - **Escalation Agent:**  
     "Ask a simple clarifying question to get missing info (e.g., 'What time does your workday start?') or flag for human review."

## Key Nodes for Multi-Agent Pattern

- **Router Agent**
- **If/Else routing**
- **Specialist Agents** (Schedule, Focus, Reminder)
- **Escalation Agent** (fallback)

---
