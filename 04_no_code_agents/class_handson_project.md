# Live Project: Assignments Grading and Feedback Agentic System

This is a lab project that we will build within the class. In your first assignment, you researched real-world agentic AI use cases. You will note that most of them were where human readiness is present.

### How it connects with Real World, Education and Human Readiness?

This isn't just a hypothetical idea; it's a rapidly growing market where well-funded startups are building real products that solve a major pain point for educators.

These companies are proving there is immense value and human readiness for agents that automate the time-consuming tasks of grading and providing feedback, allowing teachers to focus on teaching.

Before we build our own, let's look at the companies you found that are already succeeding in this space. 

| Company | Goal | YC Batch & Funding |
|---|---|---|
| [Gradewiz](https://www.ycombinator.com/companies/gradewiz) | AI Grading for Teachers | W25 - Active |
| [Edexia](https://www.ycombinator.com/companies/edexia) | AI Teacher Assistant for Grading Essays | W25 - Active |
| [Frizzle](https://www.ycombinator.com/companies/frizzle) | AI Grading for Teachers | S25 - Active |
| [Mimir](https://www.ycombinator.com/companies/mimir) | A platform for STEM courses featuring automated grading. It was successfully acquired by HackerRank, proving the viability of this model. | S15 - Acquired |

Note that Mimir is a pre-agentic AI example that was acquired, showing that this has been a valuable problem to solve for a while. The new wave of companies are reimagining this space with more advanced agentic AI capabilities.

Now, let's move from analysis to creation. They've validated the problem, and now we're going to build a solution in our live class.

**Objective:** Build an agent that can extract information from various sources, grade a student's submission, and provide constructive feedback.

## Step-by-step plan we will follow in Agent Builder.

### 1. Domain Knowledge: Decompose the Steps of How Grading Works

Before we touch any tools, we must understand the process. A teacher doesn't just assign a grade. The workflow looks like this:

1. Understand the Material: The teacher first masters the source material (the document, video, etc.).

2. Review the Submission: The teacher reads or watches the student's work.

3. Compare to Rubric: They compare the submission against a predefined grading rubric.

4. Assign a Score: Based on the comparison, they assign points for each criterion.

5. Write Internal Notes: They might jot down notes for themselves about common mistakes or standout points.

6. Formulate Feedback: Using a feedback rubric (Strengths, Weaknesses, Suggestions), they write constructive comments for the student.

### 2. Define What Success Looks Like

For our agent, success means correctly performing the steps above. We will measure it by:

- Accuracy: Does the agent extract the correct facts from the sources?

- Consistency: Does it apply the rubric fairly to different submissions?

- Quality of Feedback: Is the feedback clear, constructive, and personalized?

- Structured Output: Does the agent produce a clean, predictable output (e.g., a JSON object with the grade, remarks, and feedback)?

### 3. How to Build It in Agent Builder: A Workflow Plan

Now, let's map our decomposed steps to the nodes in Agent Builder.

- Input: We'll need to provide the agent with the source materials, the student's submission, and the rubrics.

- Process: A series of agents will perform the tasks of extraction, grading, and feedback generation. The core agentic workflow will be:
  1.  **Extract Data:** The agent needs to process information from a document, a video, and a social media post.
  2.  **Grade and Internal Remarks:** Based on the extracted data and a predefined rubric, the agent will grade the submission and provide internal remarks for the instructor.
  3.  **Feedback for Student:** The agent will generate personalized and constructive feedback for the student based on their submission and the grading results.
  - When building we will omit 1 to focus on proving core value first.

- Output: The final result will be a structured object containing the complete assessment.

## 4. Create the Start Node and State Variables
Every workflow begins with the Start Node. This is where we will define our initial inputs. We will use the Set State Node to create variables that can be used throughout the workflow.

- assignment: An object containing details about assignment.

- student_submission: The text submitted by the student.

- grading_rubric: The criteria and point values for grading.

- feedback_rubric: The structure for the student feedback (Strengths, Areas for Improvement, Actionable Suggestions).

## 5. Plan the Workflow Logic
We need to ensure our agent is robust. We'll use logic nodes to handle potential issues.

- If/Else Node: We will add a check right after the start. If the student_submission variable is empty, the workflow will end. Else, it will proceed. This prevents the agent from running on empty inputs.

- Transform Node: After the final agent generates the grade and feedback, we will use a Transform Node to format the output into a clean, structured JSON object.

- Set State Node: We will use this node again to store the final structured output in a state variable called final_grade_object. This makes the result easily accessible.

## 6. Define the Agent (v0) and Prompt Engineering

We'll start with a single Agent Node. The prompt is the "job description" for our agent. Our v0 prompt will instruct it to perform all the steps:

- "First, carefully review the assignment_sources."
- "Next, analyze the student_submission."
- "Then, using the grading_rubric, evaluate the submission and assign a score for each criterion. Provide brief internal remarks explaining your reasoning."
- "Finally, using the feedback_rubric, write clear and constructive feedback for the student."
- "Return your complete evaluation as a single JSON object."

We will test this initial agent with a sample submission and see how different models handle the complex request.

## 7. Decompose into Multiple Agents (The "Agentic" Approach)
A single agent doing everything can be unreliable. A more advanced, agentic pattern is to use a "team" of specialized agents, each with one clear job. This is how real agentic systems are built. We will structure our workflow with three distinct Agent Nodes:

### Grading Agent:

- Input: The output from the Extraction Agent and the grading_rubric.

- Task: This agent compares the extracted points to the rubric and calculates a score. It also writes the internal remarks for the instructor.

- Output: A structured object containing the scores and internal remarks.

### Feedback Agent:

- Input: The output from the Grading Agent and the feedback_rubric.

- Task: This agent's sole focus is on communication. It takes the grading results and translates them into positive, constructive, and personalized feedback for the student.

- Output: The final, student-facing feedback text.


### AddOn: Extraction Agent (Self Homework for Students):

- Input: assignment_sources and student_submission.

- Task: This agent's only job is to read all the materials and extract the key facts and arguments from both the sources and the student's work.

- Output: A summarized, structured list of key points.

By breaking the problem down this way, each agent has a simpler task, which increases the reliability and quality of the final output. This is a core skill in building effective, production-grade agentic workflows.

## Sample Data

### Assignment: Take Assignment 1 as sample.

### Grading Rubric
- **Data Extraction (40%):**
    - Accuracy of information extracted from the document.
    - Completeness of information extracted from the video.
    - Relevance of information extracted from the social media post.
- **Grading (30%):**
    - Correct application of the grading rubric.
    - Consistency in grading across different submissions.
- **Feedback (30%):**
    - Clarity and constructiveness of the feedback.
    - Personalization of the feedback to the student's submission.

### Feedback Rubric
- **Strengths:** What did the student do well?
- **Areas for Improvement:** What specific areas can the student work on?
- **Actionable Suggestions:** Provide concrete steps the student can take to improve.
