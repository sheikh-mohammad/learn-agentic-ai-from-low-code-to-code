# Planning Pattern Example: Research Report Generator

## Overview

This tutorial demonstrates the **Planning Pattern** in agentic AI, where one agent creates a strategic plan and another agent executes it. The Planner Agent breaks down a complex task into actionable steps, and the Executor Agent follows those steps to complete the task.

## Workflow Diagram

```
Start Node ──▶ Planner Agent ──▶ Executor Agent ──▶ End Node
```

## Step-by-Step Tutorial

### Step 1: Create the Planner Agent

The Planner Agent analyzes the user's request and creates a detailed action plan.

1. In OpenAI Agent Builder, click **Add Agent**
2. Name it: `Planner Agent`
3. Add the following System Instructions:

```markdown
You are an expert strategic planner who excels at breaking down complex research tasks into clear, actionable steps.

Your goal is to create a detailed plan for generating a comprehensive research report based on the user's topic.

Instructions:
1. Analyze the research topic provided by the user
2. Identify the key areas that need to be researched
3. Create a structured plan with 3-5 specific research steps
4. Each step should be clear, actionable, and focused on gathering specific information
5. Order the steps logically from foundational research to more specific details

Output format:
Return your plan as a JSON object with the following structure:
- "topic": The research topic (string)
- "steps": An array of research steps, where each step has:
  - "step_number": The step number (integer)
  - "description": What needs to be researched (string)
  - "focus_area": The specific aspect to focus on (string)

Example Output:
{
  "topic": "Artificial Intelligence in Healthcare",
  "steps": [
    {
      "step_number": 1,
      "description": "Research the current state of AI in healthcare",
      "focus_area": "Overview and statistics"
    },
    {
      "step_number": 2,
      "description": "Identify key AI applications in medical diagnosis",
      "focus_area": "Specific use cases and technologies"
    }
  ]
}

Remember:
- Make each step specific and actionable
- Ensure steps build upon each other logically
- Keep the plan focused on the user's topic
```

4. **Configure Structured Output Schema:**
   - In the Planner Agent settings, scroll down to **Output format** field
   - Select **JSON** from the dropdown menu
   - A Structured Output(json) dialog will open
   - Click **Add property** in the dialog
   - Set **Name** field to: `research_plan`
   - Configure the first property:
     - **Name**: `topic`
     - **Type**: `STR` (String)
     - **Description**: `The research topic to be explored`
   - Click **Add property** again for the second property:
     - **Name**: `steps`
     - **Type**: `ARR` (Array)
     - **Array items**: `OBJ` (Object)
     - **Description**: `List of research steps to execute`
   - Configure the object properties within the `steps` array:
     - Click **Add property** under the array item object:
       - **Name**: `step_number`
       - **Type**: `NUM` (Number)
       - **Description**: `Sequential step number`
     - Click **Add property** again:
       - **Name**: `description`
       - **Type**: `STR` (String)
       - **Description**: `What needs to be researched in this step`
     - Click **Add property** again:
       - **Name**: `focus_area`
       - **Type**: `STR` (String)
       - **Description**: `Specific aspect to focus on`

   Final schema structure:
   ```json
   {
     "topic": "string",
     "steps": [
       {
         "step_number": "number",
         "description": "string",
         "focus_area": "string"
       }
     ]
   }
   ```

5. Connect the **Start Node** to the **Planner Agent**

---

### Step 2: Create the Executor Agent

The Executor Agent follows the plan created by the Planner Agent to generate the research report.

1. Click **Add Agent**
2. Name it: `Executor Agent`
3. Add the following System Instructions:

```markdown
You are an expert researcher and writer who executes research plans to create comprehensive, well-structured reports.

Your goal is to follow the research plan provided by the Planner Agent and create a detailed research report.

Instructions:
1. Review the research plan carefully, including the topic and all steps
2. Execute each research step systematically:
   - Use search tools to gather accurate, up-to-date information for each step
   - Focus on the specific areas identified in each step
   - Gather factual data, statistics, examples, and expert insights
3. Synthesize all gathered information into a cohesive research report with the following structure:
   - **Title**: Based on the research topic
   - **Introduction**: Brief overview of the topic and its significance (100-150 words)
   - **Main Body**: Organized sections corresponding to each research step (400-600 words total)
     - Each section should have a clear heading based on the step's focus area
     - Include specific facts, data, and examples
   - **Conclusion**: Summary of key findings and implications (100-150 words)
4. Ensure the report flows logically and maintains an academic, informative tone

Output:
Return the complete research report as formatted text with clear headings and well-structured paragraphs.

Notes:
- Prioritize factual accuracy and cite recent information
- Maintain objectivity and professional writing style
- Stay within 600-900 words total
- Make sure each section addresses the corresponding step from the plan
```

4. **Enable Search Tool:**
   - In the Executor Agent settings, look for the **Tools** section
   - Enable the **Search** tool (or Web Search, depending on your OpenAI Agent Builder version)
   - This allows the agent to search for current information

5. Connect the **Planner Agent** to the **Executor Agent**

---

### Step 3: Configure the End Node

1. Connect the **Executor Agent** to the **End Node**

---

## Step 4: Test Your Workflow

Test the workflow with various research topics:

**Example Test Prompts:**
- "Create a research report on quantum computing applications in cryptography"
- "Research the impact of remote work on corporate culture"
- "Generate a report on sustainable energy solutions for urban areas"
- "Research artificial intelligence ethics in autonomous vehicles"

**What to verify:**
1. The Planner Agent creates a logical, step-by-step research plan
2. The plan includes 3-5 clear steps with specific focus areas
3. The Executor Agent follows the plan systematically
4. The final report addresses all steps from the plan
5. The report is well-structured with introduction, body sections, and conclusion
6. Information is factual and up-to-date

---

## Understanding the Planning Pattern

### Key Characteristics

**Separation of Concerns:**
- **Planner**: Focuses on strategy and breaking down complex tasks
- **Executor**: Focuses on implementation and execution

**Benefits:**
- More organized approach to complex tasks
- Better handling of multi-step processes
- Clearer reasoning and transparency
- Easier to debug (you can see the plan before execution)

**When to Use:**
- Research and analysis tasks
- Multi-step problem solving
- Complex content generation
- Tasks requiring systematic approach
- When transparency of the process is important

---

## Key Takeaways

- **Planning Pattern**: Separates strategic planning from execution, creating a two-phase approach
- **Structured Output**: The Planner Agent uses JSON schema to create a consistent, parseable plan
- **Sequential Execution**: Each agent has a clear role, with the Executor building upon the Planner's output
- **Transparency**: You can see both the plan and the result, making the process more understandable
- **Scalability**: This pattern can be extended with validators, multiple executors, or iterative refinement

---

## Next Steps

Try extending this pattern:
- Add a **Validator Agent** after the Executor to check if all plan steps were addressed
- Implement an **Iterative Executor** that reports back after each step
- Add **conditional branching** based on the plan complexity
- Create a **Plan Refinement** loop where the Executor can request plan clarification

---
