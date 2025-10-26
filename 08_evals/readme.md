# Session 8: Evals You’ll Actually Use (No‑Code)

## Why
Quality loops make agents reliable. In AgentKit’s no‑code Agent Builder, you’ll use built‑in evaluations (datasets, trace grading, automated prompt optimization, third‑party model support) to design–run–improve without writing code.

## Objectives
- Design a simple eval dataset from real tickets/prompts (≈20 cases)
- Use trace grading to grade whole runs and spot brittle steps
- Apply prompt optimization from grader + human annotations; re‑run to compare
- Compare third‑party models (what/why/when) to inform model selection

## Lab
1. Build a 20‑case dataset in Agent Builder: label intents, expected behaviors, acceptance notes
2. Run the initial eval; bookmark failing traces using trace grading
3. Use grader suggestions + your annotations to refine system instructions/prompts
4. Re‑run; capture deltas (pass rate, tokens, latency) and note trade‑offs

## Deliverable
- Eval report with before/after metrics and 2 documented prompt changes

## Skill focus (post‑Step 6)
- Architect evaluation loops: derive datasets from real work, grade traces, iterate prompts
- Make evidence‑based decisions about model choice using third‑party comparisons

## Resources
- AgentKit overview (Agent Builder, datasets, trace grading, prompt optimization, third‑party models): `https://openai.com/index/introducing-agentkit/`
- Evaluation best practices (design datasets, trace grading, prompt tuning, comparisons): `https://platform.openai.com/docs/guides/evaluation-best-practices?api-mode=responses`

## How to use in AgentKit (No‑Code)
1. Open Agent Builder → Create or select your agent workflow.
2. Add a Dataset → import or author ~20 real prompts/tickets; add expected behavior and acceptance notes.
3. Run Evaluation → enable Trace Grading; run and bookmark failing traces.
4. Optimize → apply grader suggestions + your own annotations to refine instructions/prompts.
5. Compare Models → (optional) run on third‑party models; record accuracy, tokens, and latency.
6. Re‑run → collect before/after metrics and write a short eval report.