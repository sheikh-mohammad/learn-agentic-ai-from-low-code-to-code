# Session 9: Observability & Cost Control
## Monitoring Production Agents and Optimizing for Efficiency (No-Code)

---

## 📋 Prerequisites Checklist

Before we start, make sure you have:

- [ ] **Completed Session 8** - Understanding of traces and evaluations
- [ ] **Agent in production** - Grading agent or similar with real usage
- [ ] **Real conversation data** - At least 10 real user interactions
- [ ] **Agent Builder access** at [platform.openai.com/agent-builder](https://platform.openai.com/agent-builder)

**That's it!** All cost analysis and metrics are tracked in Agent Builder traces.

---

## 🎯 Learning Objectives

By the end of this 2-hour session, you will be able to:

### Understand & Apply:
- Explain the difference between pre-production evals and production observability
- Read production traces to identify real user issues
- Spot tool-call loops, dead ends, and inefficiencies
- Calculate token costs and identify waste

### Analyze & Optimize:
- Identify the top 3 cost drivers in your agent
- Create lightweight A/B tests for optimization
- Measure before/after impact on tokens, latency, and quality
- Make data-driven decisions about agent improvements

### Create Production Systems:
- Build continuous monitoring practices
- Set up cost alerts and thresholds
- Create self-improving agent workflows
- Balance cost, speed, and quality trade-offs

---

## 📚 What You Will Learn

By the end of this session, you will master:
- ✅ **Production trace analysis** - Reading real user conversations for insights
- ✅ **Issue identification** - Spotting loops, dead ends, and token waste
- ✅ **Cost optimization** - Reducing tokens and latency without sacrificing quality
- ✅ **A/B testing** - Comparing variants to make evidence-based decisions
- ✅ **Continuous monitoring** - Building self-improving production systems

---

## 🧠 Session Structure

### Timeline

- **Part 1:** From Evals to Production Observability (15 min)
- **Part 2:** Reading Production Traces (25 min)
- **Part 3:** Identifying Issues - Loops, Dead Ends, Waste (30 min)
- **Part 4:** Cost Optimization Strategies (20 min)
- **Part 5:** Lightweight A/B Testing (15 min)
- **Part 6:** Complete Observability Lab (20 min)
- **Part 7:** Consolidation & Next Steps (5 min)

---

## Part 1: From Evals to Production Observability (15 min)

### Building on Session 8

**What we learned in Session 8:**
- Built evaluation datasets (10-20 test cases)
- Used traces to debug issues during development
- Created graders for quality checks
- Optimized prompts based on eval results

**What changes when you go to production:**

| Session 8: Pre-Production Evals | Session 9: Production Observability |
|----------------------------------|-------------------------------------|
| 10-20 test cases | 100s-1000s of real conversations |
| Controlled testing | Real user behavior (unexpected!) |
| One-time optimization | Continuous improvement |
| "Does it work correctly?" | "Is it efficient and cost-effective?" |
| Perfect test data | Messy, real-world data |
| Focus: Quality | Focus: Quality + Cost + Speed |

---

### The Self-Improving System Mindset

**❌ Traditional Approach:**
```
Launch → Hope it works → Fix when users complain → Update occasionally
```

**✅ Self-Improving Approach:**
```
Launch → Monitor continuously → Learn from usage → Optimize automatically → Improve over time
```

**Real Example:**

Your grading agent from Sessions 4 & 8:
- **Pre-production (Session 8):** Tested with 20 student submissions, found issues, optimized
- **Production (Session 9):** Now grading 100 submissions/week
  - Week 1: 450 tokens/submission average, 4.2s latency
  - Week 4: After monitoring & optimization: 280 tokens/submission, 2.8s latency
  - **Result:** 38% cost reduction, 33% faster, same quality

**This is what observability enables.**

---

### What to Monitor in Production

**Performance Metrics:**
- **Response Time:** How quickly does each submission get graded?
- **Token Usage:** How many tokens per submission? (This is your cost!)
- **Error Rate:** What % of submissions fail to grade?
- **Success Rate:** What % complete successfully?

**Quality Metrics:**
- **Grading Accuracy:** Are grades consistent and fair?
- **Feedback Quality:** Is feedback helpful and specific?
- **User Satisfaction:** Are teachers happy with results?
- **Edge Case Handling:** How does it handle unusual submissions?

**Business Metrics:**
- **Cost per Submission:** Total tokens × price per token
- **Time Saved:** Hours saved vs. manual grading
- **ROI:** Value provided vs. cost to run
- **Usage Patterns:** When do teachers use it most?

---

### The Key Insight

> **In Session 8, traces helped us debug during development.**
> **In Session 9, traces help us optimize during production.**

**Same tool (traces), different purpose.**

---

## Part 2: Reading Production Traces (25 min)

### From Test Data to Real Usage

**Scenario:** Your grading agent has been running for 2 weeks. You have 200 real grading sessions.

**Time to analyze what's actually happening.**

---

### SHOW: Instructor Analyzes a Production Trace (10 min)

**Real Grading Agent Trace:**

**Submission:** Student wrote 150 words about "AI use case in healthcare"

**The Trace:**

```
Span 1: Start Node [0.1s]
  Input: {assignment_details, student_submission, grading_criteria}
  ✓ State initialized

Span 2: If/Else - Check Submission [0.05s]
  Condition: Is submission empty?
  Result: FALSE → Proceed to grading
  ✓ Validation passed

Span 3: Grading Agent [3.2s] [380 tokens]
  Input: Full submission + criteria
  Task: Grade and provide feedback
  Output: {grade: 85, remarks: "...", feedback: "..."}
  ✓ Grading completed

Span 4: Transform Node [0.1s]
  Input: Agent output
  Task: Format to JSON
  Output: Clean structured object
  ✓ Transform successful

Span 5: Set State [0.05s]
  final_grade_object = {...}
  ✓ Result stored

Total Time: 3.5s
Total Tokens: 380
Status: ✓ Success
Cost: 380 × $0.000002 = $0.00076 (~0.08¢)
```

**Analysis:**

✅ **What's working:**
- Fast validation (If/Else)
- Successful completion
- Clean output format

⚠️ **Potential issues:**
- 380 tokens seems high for 150-word submission
- 3.2s is slow (most time in Grading Agent)
- Where are those 380 tokens going?

**Instructor Think-Aloud:**
> "Looking at this trace, I see the agent took 3.2 seconds and used 380 tokens. For a 150-word submission, that feels expensive. In Session 8, we tested quality. Now we need to optimize cost and speed without hurting quality. Let's dig deeper."

---

### GUIDE: Analyzing Traces Together (10 min)

**Instructor leads class through a trace:**

**Scenario:** Another real submission

```
Span 1: Start Node [0.1s]
Span 2: If/Else Check [0.05s]
Span 3: Grading Agent [5.8s] [620 tokens] ⚠️
  Problem: Why so slow? Why so many tokens?
Span 4: Transform [0.15s]
Span 5: Set State [0.05s]

Total: 6.1s, 620 tokens
```

**Class Discussion:**

**Instructor asks:**
1. "What's different between this trace and the first one?"
   - (Answer: Much slower, way more tokens)

2. "Where should we investigate first?"
   - (Answer: Span 3 - Grading Agent - that's where the time and tokens go)

3. "What might cause 620 tokens for grading one submission?"
   - (Possible answers: Prompt too long, repeating instructions, verbose feedback)

**Key Learning:**
> **Production traces show you where the real problems are - not where you think they are.**

---

### PRACTICE: Analyze Your Production Traces (5 min)

**Task:** Open 3-5 real traces from your agent

**What to look for:**

```
For each trace, note:

1. Total time: _____s
2. Total tokens: _____
3. Which span took longest: _____
4. Which span used most tokens: _____
5. Any failed spans: Yes/No
6. Overall status: Success/Failure
```

**Quick Self-Assessment:**

- [ ] I found my slowest trace
- [ ] I identified which span is the bottleneck
- [ ] I know how many tokens my average grading costs
- [ ] I spotted at least one inefficiency

---

## Part 3: Identifying Issues - Loops, Dead Ends, Waste (30 min)

### The Three Production Problems

Based on analyzing 1000s of production traces across AgentKit users, these are the most common issues:

1. **Tool-Call Loops** - Agent gets stuck calling the same tool repeatedly
2. **Dead Ends** - Workflow stops unexpectedly without completing
3. **Token Waste** - Using way more tokens than necessary

Let's learn to spot each one.

---

### Problem 1: Tool-Call Loops (10 min)

**What it is:** Agent calls the same tool over and over, never moving forward

**Example Trace:**

```
Span 1: Start
Span 2: Grading Agent [2.1s] [300 tokens]
  Tool call: file_search("grading criteria")
  Result: {...}
Span 3: Grading Agent [2.1s] [300 tokens]
  Tool call: file_search("grading criteria")  ← Same tool again!
  Result: {...}
Span 4: Grading Agent [2.1s] [300 tokens]
  Tool call: file_search("grading criteria")  ← Still searching!
  Result: {...}
Span 5: Timeout Error [0s]
  Workflow stopped: Maximum iterations reached

Total: 6.3s, 900 tokens, FAILED
```

**Why it happens:**
- Agent instructions unclear about when to stop searching
- Tool returns incomplete results
- No guard rails on iteration count
- Agent doesn't realize it already has the information

**How to spot it:**
- Look for **repeated tool calls** to same tool
- Check for **escalating token usage** across spans
- See if workflow **times out** or hits max iterations

**How to fix:**
- Add iteration limits: "Search once, then proceed"
- Improve tool instructions: "If you find X, move to grading"
- Add If/Else node: Check if data found before calling tool again

---

### Problem 2: Dead Ends (10 min)

**What it is:** Workflow stops unexpectedly without completing the task

**Example Trace:**

```
Span 1: Start [0.1s]
Span 2: If/Else Check [0.05s]
  Condition: submission.length > 100
  Result: FALSE  ← Student wrote 95 words
  Workflow ends here (no else branch!)

Total: 0.15s, 5 tokens, INCOMPLETE
Status: Success (but didn't grade!)
```

**Why it happens:**
- Missing else branch in If/Else logic
- Guard rails too strict (rejected valid input)
- Agent decides not to continue (needs clearer instructions)
- State variable missing or malformed

**How to spot it:**
- Workflow shows **Success** but didn't produce output
- Trace **ends abruptly** without final output span
- Tokens used are **unusually low** (workflow barely ran)
- User reports "agent did nothing"

**How to fix:**
- Add else branches: Cover all paths
- Review guard conditions: Are they too strict?
- Add default behavior: "If uncertain, continue with warning"
- Test edge cases: Empty, short, long, malformed inputs

---

### Problem 3: Token Waste (10 min)

**What it is:** Using way more tokens than necessary for the task

**Example Trace:**

```
Span 1: Start
Span 2: Grading Agent [4.5s] [850 tokens] ⚠️
  Input: 200-word submission
  Prompt includes:
    - Full assignment instructions (500 words)
    - All grading criteria (300 words)
    - Feedback examples (400 words)
    - Student submission (200 words)
  Total input: 1400 words → ~1850 tokens

  Output:
    - Grade + feedback (150 words) → 200 tokens

  Total tokens: 1850 input + 200 output = 2050 tokens processed
  Billed tokens: 850 (compressed but still high)

Status: Success, but expensive!
```

**Why it happens:**
- **Prompt bloat:** Including unnecessary context
- **Repetitive instructions:** Saying same thing multiple ways
- **Verbose examples:** Long examples when short ones work
- **Full document retrieval:** Loading entire docs when excerpts suffice

**How to spot it:**
- Compare **tokens used** vs. **task complexity**
  - Simple task, high tokens = waste
- Check **input token count** - is prompt too long?
- Look for **similar traces** with different token counts
- Calculate **cost per task** - is it higher than expected?

**Token Usage Benchmarks:**

| Task | Expected Tokens | High (Wasteful) |
|------|----------------|-----------------|
| Grade 200-word essay | 300-400 | > 600 |
| Simple classification | 50-100 | > 200 |
| Multi-agent routing | 100-150 | > 250 |
| Generate feedback | 200-300 | > 500 |

**How to fix:**
- **Trim prompts:** Remove unnecessary context
- **Use summaries:** Don't include full documents
- **Simplify instructions:** One clear statement vs. three repetitive ones
- **Optimize retrieval:** Only fetch relevant sections
## Part 4: Cost Optimization Strategies (20 min)

### Understanding Your Costs

**OpenAI Pricing (as of 2025):**

| Model | Input Tokens | Output Tokens |
|-------|--------------|---------------|
| GPT-4 | $0.01 / 1K | $0.03 / 1K |
| GPT-4 Turbo | $0.002 / 1K | $0.006 / 1K |
| GPT-3.5 | $0.0005 / 1K | $0.0015 / 1K |

**Example Calculation:**

Your grading agent processes 100 submissions/week:
- Average: 400 tokens/submission (300 input + 100 output)
- Model: GPT-4 Turbo

**Weekly Cost:**
```
Input:  100 × 300 tokens × $0.002/1K = $0.06
Output: 100 × 100 tokens × $0.006/1K = $0.06
Total: $0.12/week = $6.24/year
```

**Seems cheap? Let's scale:**

If you're a university with 50 teachers, each grading 100 submissions/week:
```
5,000 submissions/week × $0.0012 = $6/week = $312/year
```

**Now multiply by inefficiencies:**
- If you're using 800 tokens instead of 400: **$624/year** (2x)
- If you're using wrong model (GPT-4 vs Turbo): **$3,120/year** (10x)

**Optimization matters at scale.**

---

### Strategy 1: Prompt Compression (5 min)

**Before Optimization:**

```
You are an assignment grading assistant for educators. Your task is to carefully review student submissions and provide comprehensive feedback based on predefined criteria.

When grading, please consider the following:
- First, read the entire submission thoroughly
- Then, review each grading criterion individually
- For each criterion, assign points based on the rubric
- Write internal remarks for the instructor explaining your scoring decisions
- Finally, create student-facing feedback

The feedback should follow this structure:
- Start with what the student did well (strengths)
- Then mention areas that need improvement
- End with specific, actionable suggestions for how to improve

Remember to be fair, constructive, and encouraging in your feedback.
```

**Token count:** ~140 tokens

**After Optimization:**

```
You are a grading assistant. For each submission:

1. Apply grading criteria and assign points
2. Write instructor remarks (reasoning)
3. Write student feedback:
   - Strengths (what worked)
   - Gaps (what's missing)
   - Actions (how to improve)

Be fair and constructive.
```

**Token count:** ~60 tokens

**Savings:** 80 tokens/submission × 100 submissions = 8,000 tokens/week = 57% reduction

---

### Strategy 2: Right-Sizing Your Model (5 min)

**Model Selection Decision Tree:**

**Simple tasks** (classification, routing, short answers):
→ Use GPT-3.5 or GPT-4 Turbo
→ **10x cheaper** than GPT-4

**Complex tasks** (analysis, nuanced grading, creative feedback):
→ Use GPT-4 or GPT-4 Turbo
→ Better quality, worth the cost

**Example:**

Your grading agent has two parts:
1. **Triage/Validation** (simple): Is submission valid? → Use GPT-3.5
2. **Detailed Grading** (complex): Apply rubric, write feedback → Use GPT-4 Turbo

**Cost comparison:**

All GPT-4:
```
100 validations × 100 tokens × $0.01/1K = $0.10
100 gradings × 400 tokens × $0.01/1K = $0.40
Total: $0.50/week
```

Optimized:
```
100 validations × 100 tokens × $0.0005/1K = $0.005
100 gradings × 400 tokens × $0.002/1K = $0.08
Total: $0.085/week
```

**Savings:** 83% reduction by right-sizing!

---

### Strategy 3: Reduce Redundant Tool Calls (5 min)

**Common Pattern:**

```
Agent calls file_search("grading criteria")
→ Gets results
→ Forgets results
→ Calls file_search("grading criteria") again ❌
```

**Why it happens:**
- Agent instructions unclear: "Use file search to find criteria"
- No instruction to "remember what you found"
- No state management

**Fix: Add State Management**

```
1. Set State: Store criteria at workflow start
2. Agent instructions: "Use the criteria from state.grading_criteria"
3. No more repeated searches ✓
```

**Impact:**
- Before: 2-3 file searches per submission (600 tokens)
- After: 0 file searches per submission (0 tokens)
- **Savings:** 600 tokens/submission

---

### Strategy 4: Batch Operations (5 min)

**Inefficient Pattern:**

```
For each of 20 submissions:
  - Load grading criteria
  - Grade submission
  - Clear context
```

**Efficient Pattern:**

```
Load grading criteria once
For each of 20 submissions:
  - Grade using cached criteria
```

**Implementation in Agent Builder:**
- Use Set State at workflow start
- All agents reference state.grading_criteria
- Criteria loaded once, reused 20 times

**Savings at Scale:**
- Before: 20 × 200 tokens (criteria) = 4,000 tokens
- After: 1 × 200 tokens (criteria) = 200 tokens
- **Savings:** 3,800 tokens (95% reduction on criteria loading)

---

## Part 5: Lightweight A/B Testing (15 min)

### The A/B Testing Mindset

**You have a hypothesis:** "If I shorten my prompt, costs will drop without hurting quality."

**But how do you know for sure?**

**Answer: A/B Test**

---

### Setting Up an A/B Test in Agent Builder

**Variant A (Current):**
```
Your current grading agent with long, detailed prompts
Average: 400 tokens, 3.5s, 90% accuracy
```

**Variant B (Optimized):**
```
Same grading agent with compressed prompts
Hypothesis: 250 tokens, 2.5s, 90% accuracy (same quality, lower cost)
```

**How to Test:**

1. **Duplicate your workflow** in Agent Builder
   - Version A: Keep original
   - Version B: Make optimizations

2. **Run both on same test set**
   - Use your 20-case eval dataset from Session 8
   - Run A on all 20
   - Run B on all 20

3. **Compare results**

---

### Comparing A vs. B

**Metrics to Track:**

| Metric | Version A | Version B | Change |
|--------|-----------|-----------|--------|
| Avg tokens | 400 | 280 | -30% ✅ |
| Avg latency | 3.5s | 2.6s | -26% ✅ |
| Pass rate (graders) | 18/20 (90%) | 17/20 (85%) | -5% ⚠️ |
| Human rating | 4.2/5 | 4.0/5 | -5% ⚠️ |
| Cost per submission | $0.0012 | $0.00084 | -30% ✅ |

**Analysis:**

✅ **Good:** 30% cost reduction, 26% faster
⚠️ **Trade-off:** Slight quality drop (90% → 85%)

**Decision:**
- If cost is critical: Choose B
- If quality is critical: Stick with A
- If both matter: Find middle ground (Version C)

---

### PRACTICE: Design Your A/B Test (10 min)

**Task:** Plan an A/B test for one optimization

**Template:**

```
Hypothesis: If I [change X], then [metric Y] will improve by [Z%]

Variant A (Control):
  Description: Current setup
  Expected:
    - Tokens: _____
    - Latency: _____s
    - Quality: _____%

Variant B (Test):
  Change: [What you'll modify]
  Expected:
    - Tokens: _____
    - Latency: _____s
    - Quality: _____%

Success Criteria:
  - [ ] Token reduction > 20%
  - [ ] Quality drop < 5%
  - [ ] Latency improvement or neutral

Test Plan:
  1. Run both on 20-case dataset
  2. Compare all metrics
  3. Decide: Deploy B, Keep A, or Create C
```

**Example Optimizations to Test:**

1. **Prompt compression** - Shorter instructions
2. **Model change** - GPT-4 → GPT-4 Turbo for simple tasks
3. **Caching** - Load criteria once vs. per submission
4. **Guard rails** - Tighter validation to skip bad inputs early

---

## Part 6: Complete Observability Lab (20 min)

### Putting It All Together

**Objective:** Complete a full production analysis and optimization cycle

---

### Task: Production Optimization Report

**Using your grading agent (or provided example), complete this analysis:**

---

#### Step 1: Collect Production Data (5 min)

```
Agent: _______________________________
Time Period: Last ____ days/weeks
Total Submissions Processed: _____

Collect 10 real conversation traces and document:

Trace #1:
  - Tokens: _____
  - Latency: _____s
  - Status: Success/Failure
  - Issues spotted: _________________

Trace #2:
  - Tokens: _____
  - Latency: _____s
  - Status: Success/Failure
  - Issues spotted: _________________

[Continue for all 10]

Calculate Averages:
  - Avg tokens: _____
  - Avg latency: _____s
  - Success rate: _____%
```

---

#### Step 2: Identify Top 3 Issues (5 min)

```
Issue #1: [Tool-call loop / Dead end / Token waste]
  Where: Span ____ in traces #___
  Impact:
    - Extra tokens: _____
    - Extra time: _____s
    - Failed submissions: _____
  Evidence: [Screenshot or trace excerpt]

Issue #2: [Tool-call loop / Dead end / Token waste]
  Where: Span ____ in traces #___
  Impact:
    - Extra tokens: _____
    - Extra time: _____s
    - Failed submissions: _____
  Evidence: [Screenshot or trace excerpt]

Issue #3: [Tool-call loop / Dead end / Token waste]
  Where: Span ____ in traces #___
  Impact:
    - Extra tokens: _____
    - Extra time: _____s
    - Failed submissions: _____
  Evidence: [Screenshot or trace excerpt]
```

---

#### Step 3: Propose Fixes (5 min)

```
Fix for Issue #1:
  Change: [What you'll modify]
  Expected Impact:
    - Token reduction: _____ (___%)
    - Latency reduction: _____s (___%)
    - Quality impact: None / Slight drop / Improvement
  Implementation: [Specific steps in Agent Builder]

Fix for Issue #2:
  Change: [What you'll modify]
  Expected Impact:
    - Token reduction: _____ (___%)
    - Latency reduction: _____s (___%)
    - Quality impact: None / Slight drop / Improvement
  Implementation: [Specific steps in Agent Builder]

Fix for Issue #3:
  Change: [What you'll modify]
  Expected Impact:
    - Token reduction: _____ (___%)
    - Latency reduction: _____s (___%)
    - Quality impact: None / Slight drop / Improvement
  Implementation: [Specific steps in Agent Builder]
```

---

#### Step 4: Calculate ROI (5 min)

```
Current State (Before Optimization):
  - Submissions per week: _____
  - Tokens per submission: _____
  - Cost per submission: $_____
  - Weekly cost: $_____
  - Annual cost: $_____

Projected State (After Optimization):
  - Submissions per week: _____ (same)
  - Tokens per submission: _____ (reduced by ___%)
  - Cost per submission: $_____
  - Weekly cost: $_____
  - Annual cost: $_____

Savings:
  - Weekly: $_____
  - Annual: $_____
  - Percentage reduction: ____%

Time Savings:
  - Latency reduction: _____s per submission
  - Total time saved per week: _____ minutes
  - Total time saved per year: _____ hours
```

---

### Deliverable: Observability Report

**Create a 1-paragraph summary:**

```
Production Analysis Summary

After analyzing [#] production traces from our [agent name], we identified three main optimization opportunities: [Issue 1], [Issue 2], and [Issue 3]. These issues are causing [X% higher costs / Y seconds extra latency / Z% failures]. By implementing [specific fixes], we project a [X%] reduction in token usage (from [N] to [M] tokens/submission), [Y%] faster responses (from [N]s to [M]s), and [Z%] cost savings (from $[N] to $[M] annually). Quality is expected to [remain stable / improve slightly / drop by <5%]. We recommend implementing these changes in phases and monitoring impact through A/B testing.

**Before/After Trace Screenshots:**
[Attach 2-3 screenshots showing the issues and proposed fixes]
```

---

## Part 7: Consolidation & Next Steps (5 min)

### Key Takeaways

**What You Learned Today:**

✅ **Production ≠ Testing**
- Session 8 taught pre-production evaluation
- Session 9 taught production monitoring
- Different goals, same tools (traces)

✅ **The Three Production Problems**
1. Tool-call loops (stuck repeating)
2. Dead ends (workflow stops early)
3. Token waste (using too many tokens)

✅ **Optimization Strategies**
1. Compress prompts (50-60% token reduction)
2. Right-size models (83% cost savings)
3. Eliminate redundant calls (95% on repeated ops)
4. Batch operations (load once, use many times)

✅ **A/B Testing Framework**
- Create hypothesis
- Test variant against control
- Measure tokens, latency, quality
- Make data-driven decision

✅ **Continuous Monitoring**
- Collect production traces regularly
- Identify patterns and issues
- Optimize based on evidence
- Re-measure and iterate

---

### The Self-Improving Agent Mindset

**Week 1:** Launch agent, collect traces
**Week 2:** Analyze traces, identify issues
**Week 3:** Implement fixes, A/B test
**Week 4:** Deploy winner, repeat

**This is how production AI systems improve over time.**

---

### Connection to Session 10: Guardrails

**Today:** We optimized for cost and speed
**Next Session:** We'll add safety controls (guardrails) to protect:
- User privacy (PII masking)
- Agent behavior (jailbreak prevention)
- Output quality (hallucination detection)

**The goal:** Fast, cheap, safe, and high-quality agents.

---

### Homework (Optional)

**Beginner:**
- Collect 10 production traces
- Calculate average tokens and latency
- Identify 1 optimization opportunity

**Intermediate:**
- Complete the full observability lab
- Implement 1 optimization
- Run before/after comparison

**Advanced:**
- Set up weekly monitoring process
- Create dashboard tracking tokens, latency, errors
- Implement 3 optimizations and measure ROI

---

## 📖 Resources & References

### Official OpenAI Documentation
- [Agent Builder Documentation](https://platform.openai.com/docs/guides/agent-builder)
- [Traces and Observability](https://platform.openai.com/docs/guides/traces)
- [OpenAI Pricing](https://openai.com/api/pricing/)

### Real-World Examples
- **RAMP:** Used observability to optimize procurement agent (70% faster builds)
- **HubSpot:** Monitored ChatKit deployment to improve response times
- **Carlyle:** Tracked costs to justify investment in AI agents

### Tools Mentioned
- Agent Builder Traces View (shows token counts, timing, costs)
- Datasets UI (from Session 8)

---

## 💡 Tips & Best Practices

### Monitoring Production Agents

**✅ Do:**
- Check traces weekly (at minimum)
- Set cost budgets and alerts
- Track trends over time (not just snapshots)
- Prioritize optimizations by ROI
- Test changes with A/B before full rollout

**❌ Don't:**
- Ignore production after launch
- Optimize without measuring impact
- Sacrifice quality for cost savings
- Make multiple changes at once (can't isolate impact)
- Forget to document what you changed

---

### Cost Optimization

**✅ Do:**
- Start with biggest token users
- Compress prompts without losing clarity
- Use appropriate models for each task
- Cache/reuse data when possible
- Measure before and after

**❌ Don't:**
- Use GPT-4 for simple tasks
- Include unnecessary context
- Load same data repeatedly
- Over-optimize at expense of quality
- Forget about user experience

---

### A/B Testing

**✅ Do:**
- Test one change at a time
- Use same dataset for A and B
- Measure all metrics (cost, speed, quality)
- Run enough tests for confidence
- Document decisions and reasoning

**❌ Don't:**
- Change multiple things at once
- Use different test cases for A vs B
- Focus only on cost (ignore quality)
- Deploy without testing
- Forget to monitor after deployment

---

## 🎯 Common Pitfalls & Solutions

### Pitfall 1: "My agent costs too much!"

**Diagnosis:** Check token usage per task

**Solutions:**
1. Compress prompts (biggest impact usually)
2. Switch to GPT-4 Turbo or GPT-3.5 where appropriate
3. Eliminate repeated tool calls
4. Reduce context window size

---

### Pitfall 2: "Users complain it's too slow"

**Diagnosis:** Check trace latency breakdown

**Solutions:**
1. Find slowest span (usually agent or tool call)
2. Optimize that specific span
3. Consider parallel operations if possible
4. Reduce agent processing time with shorter prompts

---

### Pitfall 3: "Optimization broke quality"

**Diagnosis:** Compare quality metrics before/after

**Solutions:**
1. Roll back the change
2. Find middle ground (Version C)
3. Optimize different dimension (cost vs speed vs quality)
4. Use A/B testing to validate before full rollout

---

### Pitfall 4: "Can't find the issue in traces"

**Diagnosis:** Not looking at enough traces

**Solutions:**
1. Analyze 10-20 traces, not just 1-2
2. Look for patterns across multiple traces
3. Filter by failed vs. successful
4. Compare fast vs. slow submissions
5. Ask: "What's different about the problem cases?"

---

## 🔧 Troubleshooting Guide

### Issue: "I can't find traces for my agent"

**Solutions:**
- Make sure agent has been used in production
- Check that you're looking at the right workflow version
- Verify traces are enabled in settings
- Try using Preview mode to generate test traces

---

### Issue: "Token counts seem wrong"

**Solutions:**
- Remember: Tokens ≠ Words (1 token ≈ 0.75 words)
- Check both input and output tokens in the trace details
- Verify which model is being used (affects tokenization)
- Agent Builder traces show exact token counts for each span

---

### Issue: "A/B test results are inconclusive"

**Solutions:**
- Use larger test set (20+ cases minimum)
- Ensure test cases are diverse
- Check if differences are statistically meaningful
- Run test multiple times to verify consistency

---

### Issue: "Optimizations didn't reduce costs as expected"

**Solutions:**
- Verify changes were actually deployed
- Check if you're measuring the right metrics
- Look for other sources of token usage
- Calculate costs correctly (input + output tokens)

---

## 🎊 Congratulations!

**You've completed Observability & Cost Control for AgentKit.**

You now have the skills to:
- ✅ Monitor production agents systematically
- ✅ Identify cost drivers and inefficiencies
- ✅ Optimize for tokens, latency, and quality
- ✅ Run A/B tests to validate improvements
- ✅ Build self-improving agent systems

**These skills separate casual builders from production experts.**
