# Reflection Example: Essay Generator

## Overview

This tutorial demonstrates the **Reflection Pattern** in agentic AI, where one agent generates content and another agent critiques it. Based on the critique, the workflow either accepts the output or routes it for improvement.

## Workflow Diagram

```
Start Node ──▶ Draft Agent ──▶ Reflection Agent ──▶ score ≥ 7?
                                                      │
                                                      ├─ Yes ─▶ End Node
                                                      │
                                                      └─ No ─▶ Improver Agent ──▶ End Node
```

## Step-by-Step Tutorial

### Step 1: Create the Draft Agent

The Draft Agent generates the initial essay based on the user's topic.

1. In OpenAI Agent Builder, click **Add Agent**
2. Name it: `Draft Agent`
3. Add the following System Instructions:

```markdown
Generate an essay based on the topic provided by the user. The essay should be between 200 and 300 words in length and should include factual information relevant to the topic.

You are Sophia, an expert essay writer. You write informative and well-structured essays for students and researchers.

Write a 400–600 word essay on the topic asked by the user. Identify the topic.
Use search to gather recent and factual information on the topic.
Structure the essay into: Introduction, Main Body, and Conclusion.

#### Notes

- Ensure that all information presented is accurate and fact-based.
- Stay within the 200-300 word limit.
- Maintain an informative and objective tone.
```

4. Connect the **Start Node** to the **Draft Agent**

---

### Step 2: Add the Reflection Agent

The Reflection Agent evaluates the draft essay and returns a structured score and feedback.

1. Click **Add Agent**
2. Name it: `Reflection Agent`
3. Add the following System Instructions:

```markdown
Critically review a draft essay as an experienced writing instructor for the following aspects:

- **Accuracy:** Verify all factual information for correctness and if it is up-to-date.
- **Structure:** Ensure the essay employs proper academic structure, clearly having an introduction, body, and conclusion.
- **Grammar and Coherence:** Check for grammatical correctness and logical flow between and within sentences and paragraphs.

Evaluate each of the above criteria before arriving at an overall score.  
Assign an overall score from 1 (very poor) to 10 (excellent) reflecting the quality of the essay and after evaluating the above criteria.  
If the score is less than 7, clearly identify and describe the specific issues and weaknesses in the essay that led to a lower score.  
Your critique should be concise, objective, and actionable.

**Output format:**  
Return your output as a JSON object with the following fields:  
- "score": The overall numeric score (integer, range 1-10).  
- "issues": If the score is less than 7, a list of identified problems; otherwise, return an empty list.

**Example Output:**

{
  "score": [integer],
  "issues": ["[First specific issue]", "[Second issue]", "..."]
}

*(In realistic use, each field should be filled with concise, insightful comments; issue descriptions should be actionable and clear. Example above is for format illustration.)*

---
**Remember:**  
- Evaluate each criterion in detail before scoring.
- Only list issues if score is less than 7.
- Always structure output as specified JSON.
```

4. **Configure Structured Output Schema:**
   - In the Reflection Agent settings, scroll down to **Output format** field
   - Select **JSON** from the dropdown menu
   - A Structured Output(json) dialog will open
   - Click **Add property** in the dialog
   - Set **Name** field to: `critic_evaluation`
   - Configure the first property:
     - **Name**: `score`
     - **Type**: `NUM` (Number)
     - **Description**: `Quantitative overall evaluation score.`
   - Click **Add property** again for the second property:
     - **Name**: `issues`
     - **Type**: `ARR` (Array)
     - **Array items**: `STR` (String)
     - **Description**: `List of specific issues identified in the reading.`
   
   Final schema structure:
   ```json
   {
     "score": "number 1-10",
     "issues": ["string"]
   }
   ```

5. Connect the **Draft Agent** to the **Reflection Agent**

---

### Step 3: Insert an If/Else Node

The If/Else Node creates a branching path based on the critic's score.

1. Click **Add Node** and select **If/Else**
2. Set the condition: `input.output_parsed.score >= 7`
3. Configure the branches:
   - **If condition passes (score ≥ 7)**: The essay is good enough, route directly to the End Node
   - **Else (condition fails, score < 7)**: The essay needs improvement, route to the Improver Agent for revision
4. Connect the **Reflection Agent** to the **If/Else Node**

---

### Step 4: Create the Improver Agent

The Improver Agent revises the essay based on the critic's feedback.

1. Click **Add Agent**
2. Name it: `Improver Agent`
3. Add the following System Instructions:

```markdown
Role:
You are an expert editor who improves essays based on feedback from the Reflection Agent.

Goal: 
Revise the essay using the list of issues identified by the critic. Make sure all problems are fixed while keeping the essay's original intent and meaning.

Instructions:
Review all the issues identified by the Reflection Agent.
For each issue:
Correct factual or accuracy errors.
Improve structure and paragraph flow.
Keep the essay clear, factual, and well-organized.
Do not summarize or mention the issues — just improve the essay text itself.
Return the complete, polished essay as your output.

Output:
Return only the improved essay text, as a single complete piece of writing. Do not include any commentary or reference to the critic's feedback.
```

4. Connect the **Else branch** of the If/Else Node to the **Improver Agent**

---

### Step 5: Configure the End Node

1. Connect the **If branch (Yes)** to the **End Node**
2. Connect the **Improver Agent** to the **End Node**
3. The End Node should display the final essay (either the original draft if score ≥ 7, or the improved version)

---

## Understanding the State Problem

### The Issue

At this point, you might notice a problem: 

- When the Reflection Agent scores the essay **7 or higher**, the workflow skips the Improver Agent and goes directly to the End Node
- However, **the original essay text is no longer accessible** at the End Node because it was only output by the Draft Agent earlier in the workflow
- The If/Else Node only receives the critic's evaluation (score and issues), not the essay itself

### The Solution: Add State Variables

To solve this problem, we need to introduce a **state variable** called `final_essay` that persists throughout the workflow.

---

## Step 6: Add State Variable in Start Node

1. Click on the **Start Node**
2. In the right panel, find the **State variables** section
3. Click **+ Add variable**
4. Configure the state variable:
   - **Name**: `final_essay`
   - **Type**: `String`
5. Click **Save**

This creates a state variable that will be accessible throughout the entire workflow.

---

## Step 7: Add Set State Node (After Draft Agent)

Now we need to capture the Draft Agent's output and save it to the state variable.

1. Click **Add Node** and select **Set global variables**
2. Name it: `Set State - Draft Essay`
3. In the **Set global variables** configuration:
   - **Assign value**: `input.output_text` (this captures the essay text from the Draft Agent)
   - **To variable**: `final_essay` (select from dropdown)
4. Click **+ Add** if you need to add the assignment
5. Reconnect the workflow: **Draft Agent** → **Set State Node** → **Reflection Agent**

This node saves the draft essay into the `final_essay` state variable.

---

## Step 8: Add Set State Node (After Improver Agent)

After the Improver Agent creates the revised essay, we need to update the state variable with the improved version.

1. Click **Add Node** and select **Set global variables**
2. Name it: `Set State - Improved Essay`
3. In the **Set global variables** configuration:
   - **Assign value**: `input.output_text` (this captures the improved essay text from the Improver Agent)
   - **To variable**: `final_essay` (select from dropdown)
4. Click **+ Add** if you need to add the assignment
5. Reconnect the workflow: **Improver Agent** → **Set State Node** → **End Node**

This ensures the `final_essay` state is updated with the improved version before reaching the End Node.

---

## Step 9: Configure End Node Output

Now configure the End Node to display the essay from the state variable.

1. Click on the **End Node**
2. In the **Output** section, select **Structured output (JSON)**
3. Click the **Simple** tab
4. Click **Add property**
5. Configure the property:
   - **Name**: `Essay`
   - **Type**: `STR` (String)
   - **Value**: `final_essay` (select the state variable from dropdown)
6. Click **Update** to save

Now the End Node will output a JSON object containing the essay from the `final_essay` state variable, regardless of which path (high-score or low-score) was taken.

---

## Step 10: Update Workflow Connections

Make sure your connections are correct:

1. **If branch (Yes)**: Connect directly from **If/Else Node** to **End Node**
2. **Else branch (No)**: Connect from **If/Else Node** to **Improver Agent** to **Set State - Improved Essay** to **End Node**

---

## Step 11: Test Your Workflow

Test both paths to ensure state is working correctly:

1. **High-score path**: Provide a topic and verify the original draft appears at the End Node when score ≥ 7
2. **Low-score path**: Provide a topic that generates issues, verify the workflow routes to Improver Agent, and the improved essay appears at the End Node

---

## Key Takeaways

- **Reflection Pattern**: One agent generates content, another critiques it, creating a feedback loop
- **Structured Output**: The Reflection Agent uses JSON schema to return consistent, parseable data
- **Branching Logic**: If/Else nodes enable conditional workflows based on agent outputs
- **State Variables**: Essential for maintaining data across workflow branches
- **State Persistence**: The `final_essay` variable ensures the essay text is accessible at the End Node regardless of which path was taken

---