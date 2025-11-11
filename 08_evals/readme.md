# Session 8: Evaluation Mastery for AgentKit
## Building Quality Loops with Evidence-Based Testing (No-Code)

**The Evaluation Mindset:**

> "Every agent launch should be backed by evaluation data. If you can't measure it, you can't improve it. If you can't prove it works, don't launch it."

---

## 📋 Prerequisites Checklist

Before we start, make sure you have:

- [ ] **Agent built** from Part 2 (Grading Agent with working nodes)
- [ ] **Agent Builder access** at [platform.openai.com/agent-builder](https://platform.openai.com/agent-builder)
- [ ] **Ran your agent at least once** in preview mode (generates traces)

**That's it!** Everything else (datasets, graders, results tracking) is built into Agent Builder.

---

## 🎯 Learning Objectives

By the end of this 4-hour session, you will be able to:

### Remember & Understand (Knowledge):
- Explain what evaluations are in AgentKit and why they matter for production agents
- Describe the five evaluation features available in Agent Builder
- List the three best practices from OpenAI for effective evaluations

### Apply (Skills):
- Create an evaluation dataset with 10-20 high-quality test cases
- Add human feedback columns and rate agent outputs systematically
- Build automated graders for quality criteria
- Read and interpret traces to find execution issues

### Analyze (Critical Thinking):
- Identify failure patterns in evaluation results
- Diagnose problems using trace analysis
- Compare before/after optimization results and understand trade-offs

### Evaluate & Create (Mastery):
- Use the Optimize button to improve agent prompts based on evidence
- Build complete quality loops: evaluate → optimize → re-evaluate
- Make evidence-based decisions about agent production readiness

---

## 📚 What You Will Learn

By the end of this session, you will master:
- ✅ **Datasets UI** - Create systematic test cases in a spreadsheet-like interface
- ✅ **Human feedback collection** - Add manual ratings and annotations for quality judgment
- ✅ **Automated graders** - Create criteria-based quality checks that scale
- ✅ **Automated prompt optimization** - Let AI improve your prompts based on eval results
- ✅ **End-to-end trace analysis** - Debug entire multi-agent workflows step-by-step
- ✅ **Eval best practices** - Start small, use real data, iterate quickly
- ✅ **Production-ready eval workflows** - Build quality loops that scale

---

## 🧠 Session Structure

- **Part 1:** Foundation - Why Evals Matter (20 min)
- **Part 2:** From v0 to Component-Level Evaluation (30 min)
- **Part 3:** Building Graders - Define "Good" (30 min)
- **Part 4:** Datasets UI - Systematic Testing (25 min)
- **☕ Break** (10 min)
- **Part 5:** Human Feedback - Adding Judgment (20 min)
- **Part 6:** Optimize Button - Automated Improvement (25 min)
- **☕ Break** (10 min)
- **Part 7:** Full Workflow Traces - Multi-Agent Debugging (25 min)
- **Part 8:** Complete Quality Loop (30 min)
- **Part 9:** Consolidation & Transfer (5 min)

---

## Part 1: Foundation - Why Evals Matter (20 min)

### 🚨 The Production Disaster Story

**Scenario:**
> Your customer support agent works great in testing. You deploy it to production. Within 2 hours:
> - 30% of users get wrong answers
> - Support tickets triple instead of decreasing
> - Your boss asks: "What went wrong?"
> - You realize: You never tested systematically

**Question to reflect on:** *"Have you ever launched something that worked in testing but failed when real users tried it?"*

### The Solution: Quality Loops

**❌ Old Way:**
```
Build → Hope → Deploy → React to Problems
```

**✅ New Way:**
```
Build → Evaluate → Optimize → Deploy → Monitor → Improve
```

### 🏢 Real-World Impact

Companies using AgentKit evaluations systematically:

| Company | Use Case | Result with Evals |
|---------|----------|-------------------|
| **RAMP** | Procurement agent | **70% faster** to build vs. previous methods |
| **HubSpot** | AI assistant with ChatKit | **Saved weeks** of build time using ChatKit |
| **Carlyle** | Investment analysis agent | **50% faster** build, **30% better** accuracy |

**The pattern:** Teams that evaluate systematically launch faster and with higher quality.

---

## 📊 The 5 Evaluation Features in AgentKit

AgentKit provides exactly **five evaluation capabilities**. Here's what each does:

### 1. Datasets UI

**What it is:** A spreadsheet-like interface for creating test cases
**When to use:** Testing agent responses systematically
**Example:** 10 customer questions → check if answers are good

**Visual:**
```
┌─────────────────────────────────────────────────┐
│ Input            │ Expected Output │ Criteria   │
├─────────────────────────────────────────────────┤
│ "What's weather?"│ Current weather │ Has temp   │
│ "Forecast?"      │ 7-day forecast  │ Multi-day  │
│ "Is it raining?" │ Yes/No + detail │ Direct ans │
└─────────────────────────────────────────────────┘
```

---

### 2. Human Feedback

**What it is:** Rating columns you add manually (👍👎, stars, comments)
**When to use:** When quality needs human judgment (tone, helpfulness, UX)
**Example:** Is the response polite? Is it actually helpful?

**Why it matters:** Automated tests can't catch everything. Human judgment captures nuance.

---

### 3. Automated Graders

**What it is:** AI that checks agent outputs against specific criteria
**When to use:** Scaling quality checks to 100s of test cases
**Example:** "Financial analysis must contain both upside and downside arguments"

**How it works:**
- You define criteria in plain English
- LLM evaluates each agent response against that criteria
- Returns pass/fail + explanation

---

### 4. Optimize Button

**What it is:** AI automatically rewrites your prompts based on eval results
**When to use:** After finding patterns in failures
**Example:** Agent too verbose → Click Optimize → Get shorter, clearer responses

**The magic:** System analyzes failures + grader feedback + human annotations → suggests improved prompts

---

### 5. Traces

**What it is:** Step-by-step execution log showing every span (node) the agent executed
**When to use:** Debugging multi-agent routing issues, finding bottlenecks
**Example:** "Why did triage agent send query to wrong specialist?"

**Visual:**
```
Span 1: Start Node [0.1s]
  ↓
Span 2: Triage Agent [1.2s] → Routed to Weather Agent
  ↓
Span 3: Weather Agent [2.1s] → Called weather API
  ↓
Span 4: Output [0.1s]
Total: 3.5s, 450 tokens
```

---

## 🎯 The Three Best Practices from OpenAI

Throughout this session, we'll apply these three critical principles:

### 1. Start Simple and Early
- Begin with **10-20 test cases** (not 1000s)
- Create evals from day 1 (don't wait for "perfect")
- Grow your dataset as you discover issues

### 2. Use Real Data
- Use actual user queries (not synthetic test cases)
- Capture the "messiness of the real world"
- Include typos, ambiguous questions, edge cases

### 3. Align Your LLM Graders
- Test grader outputs against human judgment
- Refine criteria based on disagreements
- Document your quality standards

**Remember:** Quality matters more than quantity in evaluation datasets.

---

## Part 2: From v0 to Component-Level Evaluation (30 min)

### The Agent Builder-Native Evaluation Flow

**You've already built your v0** (from Session 4 or Part 2). Now let's evaluate it using **only Agent Builder's built-in tools**.

**Today's Running Example: Assignment Grading Agent**

---

### Step 1: Run Your Agent in Preview Mode (5 min)

**SHOW: Instructor demonstrates**

1. **Open your Grading Agent** in Agent Builder
2. **Click "Preview"** (bottom right)
3. **Test with a sample submission:**
   ```
   Student submission: "AI can help healthcare by analyzing medical
   images faster. For example, detecting cancer in X-rays. This saves
   doctors time and catches diseases early."
   ```
4. **Watch it run** - Agent processes, generates grade and feedback
5. **Look at what happened** - Output appears

**You just generated your first trace!**

---

### Step 2: Examine the Trace (5 min)

**Click "View Trace"** (in preview results)

**What you'll see:**

```
Span 1: Start Node [0.1s]
  ↓
Span 2: Set State [0.05s]
  ↓
Span 3: If/Else Check [0.02s]
  ↓
Span 4: Grading Agent [3.2s] [420 tokens]
  Input: Full submission + criteria
  Output: {grade: 78, remarks: "...", feedback: "..."}
  ↓
Span 5: Transform [0.1s]
  ↓
Total: 3.5s, 420 tokens
```

**What you notice:**
- ✅ It worked
- ⚠️ But is 78/100 the right grade?
- ⚠️ Is the feedback helpful?
- ⚠️ Did it apply all criteria?

**You don't know yet - you need to test more systematically.**

---

### Step 3: Component-Level Evaluation (Start Small!) (10 min)

**Key Insight from OpenAI:**
> **Don't evaluate the whole workflow first. Start with ONE component.**

**Why?**
- Easier to debug (one node at a time)
- Faster feedback
- Build confidence incrementally
- Isolate which node has issues

**Component-level = Node-level**

**Let's evaluate just the "Grading Agent" node:**

1. **In Agent Builder, click on your "Grading Agent" node**
2. **Click "Evaluate" button** (right panel)
3. **Datasets UI opens** - this is where you'll test this ONE node

**You're now in evaluation mode for this specific component.**

---

### Step 4: Run Quick Component Test (5 cases) (10 min)

**PRACTICE: Test your Grading Agent node with 5 submissions**

**In Datasets UI, add 5 test cases:**

| Submission Type | Input (Summary) | What to Check |
|----------------|-----------------|---------------|
| Excellent | Full analysis, sources, clear | Grade 90-100? Specific feedback? |
| Good | Solid but missing details | Grade 75-85? Constructive notes? |
| Needs Work | Vague, no sources | Grade 50-65? Helpful guidance? |
| Edge: Very Short | Only 2 sentences | Handles gracefully? |
| Edge: Empty | Empty string | Returns error message? |

**Click "Run Evaluation"** - Agent Builder tests all 5 cases

**Results appear immediately:**

```
Test 1: ✓ Grade: 95, Feedback provided
Test 2: ✓ Grade: 82, Feedback provided
Test 3: ✓ Grade: 58, Feedback provided
Test 4: ⚠️ Grade: 45 (too harsh for short but valid)
Test 5: ✓ Error handled gracefully
```

**What you learned:**
- ✅ Basic functionality works
- ✅ Empty input handled
- ⚠️ Issue: Too harsh on short submissions
- **Next: Build graders to automate this checking**

---

### The Bridge to Automated Testing

**What you've done so far:**

✅ Ran agent in preview (generated traces)
✅ Examined what happened (trace view)
✅ Evaluated ONE component (Grading Agent node)
✅ Found an issue (too harsh on short inputs)

**What's next:**

Instead of manually checking "is this grade right?", you'll:
1. **Build graders** - Define what "good" looks like automatically
2. **Create larger dataset** - Test 20 cases systematically
3. **Optimize** - Fix issues based on evidence
4. **Test full workflow** - Only after components work

**Now you're ready to define "good" with graders.**

---

## Part 3: Building Graders - Define "Good" (30 min)

### Why Graders Come BEFORE Large Datasets

**From Part 2, you tested 5 cases manually and had to eyeball each result:**
- "Is 78/100 the right grade?"
- "Is this feedback helpful?"
- "Did it cover all criteria?"

**This doesn't scale to 20, 50, or 100 cases.**

**Solution: Build graders that automatically check quality.**

---

### What Are Graders?

**Graders are automated quality checks** that run on every eval case.

**Example:**
```
WITHOUT grader:
  Output: {grade: 78, feedback: "Good work"}
  You: "Hmm, is that good enough?" 🤷

WITH grader:
  Grader checks: "Does feedback follow structure (Strengths, Gaps, Actions)?"
  Result: ❌ FAIL - Missing "Strengths" section
  You: "Aha! I know exactly what's wrong!" ✅
```

**Graders turn subjective checking into objective, automated testing.**

---

### SHOW: Instructor Creates First Grader (10 min)

**In Datasets UI (still in your Grading Agent node eval):**

1. **Click "Add Grader"** (top right)
2. **Name it:** "Feedback Structure Check"
3. **Define criteria in plain English:**

```
The agent's student_feedback must follow this structure:
1. Strengths: What the student did well
2. Areas for Improvement: Specific gaps
3. Actionable Suggestions: How to improve

All three sections must be present and non-empty.
```

4. **Choose type:** LLM-based grader
5. **Save**

**Test it on your 5 cases:**

```
Test 1: ✓ PASS - All sections present
Test 2: ✓ PASS - All sections present
Test 3: ❌ FAIL - Missing "Strengths" section
Test 4: ✓ PASS - All sections present
Test 5: N/A - Empty input (different error)
```

**Now you know:** Test 3 has an issue automatically!

---

### Create 3 Essential Graders for Grading Agent (15 min)

**Grader 1: Output Completeness**

```
Criteria: Output must be valid JSON containing:
- grade (number 0-100)
- internal_remarks (string, non-empty)
- student_feedback (string, non-empty)

All three fields must exist and be the correct type.
```

**Why:** Catches format errors

---

**Grader 2: Feedback Quality**

```
Criteria: The student_feedback must:
1. Be at least 50 words long
2. Include specific examples from the submission
3. Follow the structure: Strengths, Gaps, Actions
4. Avoid generic phrases like "good job" without specifics

Grade as PASS only if all 4 conditions met.
```

**Why:** Ensures helpful, personalized feedback

---

**Grader 3: Grading Criteria Application**

```
Criteria: The internal_remarks must reference ALL items
from the grading criteria list. Check that each criterion
is mentioned and addressed.

Example: If criteria are [Analysis Depth, Sources, Clarity],
then remarks must mention how the student performed on all three.
```

**Why:** Ensures consistent, complete grading

---

### PRACTICE: Build Your 3 Graders (5 min)

**Task:** Add these 3 graders to your Grading Agent eval

1. Click "Add Grader" for each
2. Copy the criteria above (or customize for your use case)
3. Choose "LLM-based grader"
4. Save each one

**Re-run your 5 test cases with graders enabled**

**Results now show:**

```
Test 1: ✓✓✓ (all 3 graders pass)
Test 2: ✓✓❌ (fails Grader 3 - didn't mention all criteria)
Test 3: ✓❌❌ (fails Graders 2 & 3)
Test 4: ✓✓✓
Test 5: ❌❌❌ (empty input fails all)
```

**Now you can see exactly what's working and what's not!**

---

### The Power of Graders

**Before graders:**
- Manual checking
- Inconsistent standards
- Can't scale

**After graders:**
- Automatic checking
- Consistent standards every time
- Run on 100s of cases instantly

**Now you're ready to create a larger dataset knowing graders will catch issues.**

---

## Part 4: Datasets UI - Systematic Testing (25 min)

### Where We Are Now

**You've accomplished:**
- ✅ Ran agent in preview mode (Part 2)
- ✅ Examined traces (Part 2)
- ✅ Did 5-case component test (Part 2)
- ✅ Built 3 graders that automatically check quality (Part 3)

**Next step:** Scale to 20 cases with automated checking

---

### Why 20 Cases? Quality Over Quantity

**From OpenAI Best Practices:**
> Start with 10-20 high-quality test cases, not 100 random ones.

**Why this works:**
- Forces you to think about edge cases
- Each case teaches you something
- Graders catch issues instantly
- You can iterate quickly

**We're targeting 20 because:**
- 10 typical cases (common submissions)
- 5 edge cases (tricky situations)
- 5 error cases (graceful failures)

---

### SHOW: Expanding Dataset in Agent Builder (10 min)

**Instructor demonstrates:**

#### Step 1: Open Datasets UI

1. **Click on your "Grading Agent" node**
2. **Click "Evaluate"** (opens Datasets UI)
3. **You already have 5 cases from Part 2** ✓
4. **Your 3 graders are active** ✓

#### Step 2: Add More Test Cases

**Click "Add Row"** and fill in:

| Case | Submission Type | Input Summary | What Graders Should Catch |
|------|----------------|---------------|--------------------------|
| 6 | Typical | Strong thesis, good sources | ✓✓✓ All pass |
| 7 | Typical | Decent work, minor gaps | ✓✓❌ Grader 3 catches incomplete criteria |
| 8 | Typical | Good content, weak structure | ✓❌✓ Grader 2 catches feedback structure |
| 9 | Typical | Meeting minimum requirements | ✓✓✓ All pass |
| 10 | Typical | Above average with creativity | ✓✓✓ All pass |
| 11 | Edge | Excellent but 10% over word limit | Should grade high but note limit |
| 12 | Edge | Multiple submissions for same assignment | Should handle latest or flag confusion |
| 13 | Edge | Submission in different language | Should handle gracefully |
| 14 | Edge | Image-only submission (no text) | Should request text version |
| 15 | Edge | Collaborative work (2 students) | Should flag policy question |
| 16 | Error | Empty submission | ❌❌❌ All fail (expected) |
| 17 | Error | Submission for wrong assignment | Should detect misalignment |
| 18 | Error | Only title, no content | Should require actual submission |
| 19 | Error | Spam/nonsense text | Should detect invalid input |
| 20 | Error | Very short (20 words) | Should flag insufficient work |

#### Step 3: Run Evaluation with Graders

**Click "Run Evaluation"**

**Agent Builder automatically:**
1. Runs your agent on all 20 cases
2. Applies all 3 graders to each result
3. Shows pass/fail for each grader
4. Generates summary statistics

**Results appear instantly:**

```
Overall: 15/20 cases passed all graders (75%)

Grader 1 (Output Completeness):   18/20 pass (90%)
Grader 2 (Feedback Quality):       16/20 pass (80%)
Grader 3 (Criteria Application):   14/20 pass (70%)

⚠️ Grader 3 is catching the most issues -
   agent often misses grading criteria
```

#### Step 4: Drill Into Failures

**Click on failed cases:**

```
Case 7: ✓✓❌
- Grader 3 failed: "internal_remarks missing Analysis Depth"
- Agent output: Mentioned sources and clarity, but skipped analysis depth
- FIX NEEDED: Agent prompt should emphasize checking ALL criteria

Case 8: ✓❌✓
- Grader 2 failed: "Feedback too generic, lacks specific examples"
- Agent output: "Good job overall, needs improvement"
- FIX NEEDED: Prompt should require specific examples from submission
```

---

### The Power of Automated Grading

**Before graders (Part 2):**
- Manually checked 5 cases: "Hmm, is this good?"
- Can't scale beyond 10 cases
- Inconsistent standards
- Takes hours

**With graders (Now):**
- Automatically checked 20 cases in 2 minutes
- Instant pass/fail for each quality dimension
- Consistent standards every time
- Clear patterns emerge (Grader 3 catches most issues)

**This is the breakthrough: Scale + Speed + Consistency**

---

### PRACTICE: Expand Your Dataset to 20 Cases (15 min)

**Task:** Add 15 more cases to your 5-case dataset

**Structure your additions:**
- **5 more typical cases** (cases 6-10)
- **5 edge cases** (cases 11-15)
- **5 error cases** (cases 16-20)

**Use this quick-add format in Datasets UI:**

For each new case, add:
1. **Input:** The submission scenario
2. **What to expect:** Approximate grade range
3. **What graders should catch:** Which graders should pass/fail

**Work in Datasets UI:**
1. Click "Add Row"
2. Fill in submission details
3. Add case
4. Repeat for all 15 cases
5. **Click "Run Evaluation"** when all 20 are ready

**Your graders will check all 20 automatically.**

---

### Interpreting Results

**After your evaluation runs, look for:**

#### 1. Overall Pass Rate
```
16/20 cases pass all graders = 80%
```
**Is this good enough?** Depends on your use case:
- Teaching assistant: 90%+ needed
- Internal tool: 80%+ acceptable
- High-stakes decisions: 95%+ required

#### 2. Per-Grader Performance
```
Grader 1: 18/20 (90%) - Good!
Grader 2: 17/20 (85%) - Good!
Grader 3: 14/20 (70%) - Problem area ⚠️
```

**Action:** Focus fixes on what Grader 3 checks (criteria application)

#### 3. Failure Patterns

**Do failures cluster?**
- All edge cases failing → Agent needs better instruction for unusual inputs
- All error cases passing → Graders too lenient, tighten criteria
- Random failures → Agent inconsistent, need more examples in prompt

**OpenAI Best Practice:**
> Don't aim for 100% immediately. Identify patterns, fix root causes, re-run.

---

### Quick Wins: Common Fixes

**If Grader 1 (Completeness) fails often:**
```
Add to agent prompt:
"Always return: grade, student_feedback, and internal_remarks.
Never skip any field."
```

**If Grader 2 (Feedback Quality) fails often:**
```
Add to agent prompt:
"In student_feedback, include:
1. Specific examples from their submission
2. At least 3 actionable suggestions
3. Encouraging tone"
```

**If Grader 3 (Criteria) fails often:**
```
Add to agent prompt:
"In internal_remarks, explicitly mention each grading criterion:
- Analysis Depth: [your assessment]
- Sources: [your assessment]
- Clarity: [your assessment]"
```

---

### Key Takeaway

**The Evaluation Loop:**
1. **Test** 20 cases with graders → 2. **Find patterns** in failures → 3. **Fix** agent prompt → 4. **Re-run** evaluation → 5. **Repeat** until pass rate acceptable

**This is systematic quality improvement. No guessing.**

---

## Part 5: Human Feedback - Adding Human Judgment (20 min)

### The Automation Gap

**Present these 3 agent responses - which is best?**

**Scenario:** User asked "What's the weather in Karachi?"

**Response A:**
> "The temperature in Karachi is 28°C, humidity 65%, partly cloudy."

**Response B:**
> "It's a pleasant 28 degrees in Karachi today with some clouds. You might want a light jacket for the evening!"

**Response C:**
> "WEATHER DATA: KARACHI = 28C | HUMID = 65% | CONDITION = PARTLY_CLOUDY"

**Discussion Questions:**
- Which is most helpful?
- Which is most accurate?
- Which follows the expected format?
- Can automated graders catch the difference in tone and helpfulness?

**The Insight:**

All three contain the same information, but human judgment captures:
- **Tone** (conversational vs. robotic)
- **Helpfulness** (actionable advice vs. raw data)
- **User experience quality** (friendly vs. technical)

**This is why we need human feedback alongside automated tests.**

---

### Adding Human Feedback Columns

#### SHOW: Instructor Demo (10 min)

**In the Datasets UI:**

1. **Click "Add Column"**
2. **Add "Rating" column** - Choose type: 1-5 stars or thumbs up/down
3. **Add "Feedback" column** - Choose type: Free text
4. **Add "Issues" column** - Choose type: Tags (tone, accuracy, format, completeness, other)

**Run evaluation → Rate results manually**

**Example of completed human feedback:**

| Input | Agent Output | Rating | Feedback | Issues |
|-------|-------------|--------|----------|--------|
| "Weather?" | "28°C in Karachi..." | ⭐⭐⭐⭐ | Good info, but could be friendlier | Tone |
| "Forecast?" | Widget with 7-day data | ⭐⭐⭐⭐⭐ | Perfect! Clear and visual | None |
| "Is it raining?" | "No, it's partly cloudy..." | ⭐⭐⭐⭐⭐ | Direct answer, helpful | None |
| "Weather in Mars" | "I can only provide Earth weather..." | ⭐⭐⭐ | Correct handling, but robotic | Tone |

---

### PRACTICE: Rate Your Results (10 min)

#### Task: Run Evaluation and Add Human Feedback

1. **Your 20-case dataset from Part 4** is already evaluated with automated graders
2. **Now add human judgment - click "Add Column":**
   - Star rating (1-5)
   - Feedback (text)
   - Issues (tags)
3. **Manually rate each response:**
   - Read the agent's output carefully
   - Rate it honestly
   - Write specific feedback (not just "good" or "bad")
   - Tag specific issues

**Rating Guidelines:**

| Stars | Meaning |
|-------|---------|
| ⭐⭐⭐⭐⭐ | Perfect - exactly what user needs |
| ⭐⭐⭐⭐ | Good - mostly correct, minor issues |
| ⭐⭐⭐ | Okay - correct but not ideal |
| ⭐⭐ | Poor - incorrect or unhelpful |
| ⭐ | Failure - completely wrong or broken |

**Feedback Examples:**

- ❌ Vague: "Good"
- ✅ Specific: "Accurate data, but too technical for average users"

- ❌ Vague: "Bad response"
- ✅ Specific: "Didn't answer the question directly - buried answer in paragraph 3"

---

### Reflection (5 min)

**Think about:**
- "Did you find any surprises? Cases you thought would pass but failed?"
- "Cases that passed automated criteria but felt wrong to you?"
- "What patterns do you see in your ratings?"

**Key Learning:**
> Human feedback captures nuance that automated tests miss. Always combine both for complete quality assessment.

---

## ☕ Break (10 min)

---

## Part 6: Optimize Button - Automated Improvement (25 min)

### The Magic "Optimize" Button

**What it does:**
> Analyzes your evaluation results (failures, grader feedback, human annotations) and automatically generates an improved version of your agent's prompt.

**Why it's powerful:**
- Saves hours of manual prompt engineering
- Finds patterns you might miss
- Based on evidence, not guessing
- Learns from your specific quality standards

**But remember:** Always review suggestions critically. Don't blindly accept.

---

### SHOW: The Optimization Process (10 min)

#### Instructor Demonstration

**Step 1: Review Eval Results**

**Scenario:** Weather agent eval results
- 6/10 cases passed
- 4 failures all showed same pattern: responses too technical

**Example failures:**
- Input: "What's the weather?"
- Output: "Meteorological conditions: 28°C, relative humidity 65%, barometric pressure 1013 hPa..."
- Human feedback: ⭐⭐ "Too technical for average users"

**Pattern identified:** Agent uses jargon, not conversational language

**Step 2: Click "Optimize" Button**

- System analyzes all failures
- Reviews grader feedback
- Checks human annotations
- Generates improved prompt

**Step 3: Review Suggested Changes**

**Original prompt:**
```
You are a weather information agent.
Provide accurate meteorological data including temperature,
humidity, and atmospheric conditions.
```

**Optimized prompt:**
```
You are a friendly weather assistant.
Provide weather information in simple, conversational language
that anyone can understand. Include temperature and conditions,
but avoid technical jargon like "barometric pressure" or
"relative humidity" unless specifically asked.
```

**Changes made:**
- ✅ Added "friendly" to set tone
- ✅ Specified "simple, conversational language"
- ✅ Explicitly said "avoid technical jargon"
- ✅ Gave examples of what to avoid

**Instructor Think-Aloud:**
> "The Optimize button suggested changing 'accurate meteorological data' to 'simple, conversational language'. Looking at my failures, all 4 cases had feedback about being too technical. This makes sense. I'll accept this change."

---

### When to Accept vs. Reject Suggestions (10 min)

#### Decision Framework

**✅ Accept When:**
- Change directly addresses identified failure pattern
- Doesn't contradict your business requirements
- Makes prompt clearer and more specific
- You understand WHY it helps
- Improves quality without sacrificing important features

**❌ Reject When:**
- Changes conflict with business requirements
  - Example: Removes "be polite" when that's mandatory
- Makes prompt confusing or contradictory
- Doesn't actually address the root cause of failures
- You don't understand what it's doing
- Hurts performance on edge cases

**⚠️ Modify When:**
- Suggestion is partially good
- Needs to preserve some original intent
- Can be combined with manual improvements
- Addresses one issue but creates another

#### Real Examples

**Example 1: Accept**
- **Issue:** Responses too long
- **Suggestion:** Add "Keep responses under 150 words"
- **Decision:** ✅ Accept - directly addresses the issue

**Example 2: Reject**
- **Issue:** Tone too formal
- **Suggestion:** Remove "always be professional"
- **Decision:** ❌ Reject - professionalism is required for customer support

**Example 3: Modify**
- **Issue:** Missing context
- **Suggestion:** "Always ask for user's location before providing weather"
- **Decision:** ⚠️ Modify to: "If location isn't clear from context, politely ask for clarification"
- **Reason:** Don't always need to ask - user might have said "weather in NYC"

---

### PRACTICE: Run Optimization (15 min)

#### Task: Optimize Your Agent Based on Eval Results

**Instructions:**

1. **Review your eval results from Part 4**
   - Which cases failed?
   - What patterns do you see in failures?
   - What did graders flag?
   - What did your human ratings show?

2. **Click "Optimize" button in Agent Builder**
   - Wait for system to analyze
   - Review suggested prompt changes
   - Compare original vs. optimized

3. **Make your decision:**
   - Accept the suggestion?
   - Reject it?
   - Modify it?
   - Document your reasoning

4. **Apply changes and re-run evaluation**

**Worksheet to guide your decision:**

```
Original Prompt:
_______________________________________
_______________________________________

Failure Patterns Identified:
1. _______________________________________
2. _______________________________________
3. _______________________________________

Optimized Prompt (from Optimize button):
_______________________________________
_______________________________________

Changes Made:
1. _______________________________________
2. _______________________________________
3. _______________________________________

My Decision:
[ ] Accept as-is
[ ] Reject completely
[ ] Modify (explain below)

If modifying, my version:
_______________________________________
_______________________________________

Why this decision:
_______________________________________
_______________________________________
```

---

### ANALYZE: Compare Before/After (10 min)

#### Create Comparison Table

**Run evaluation again with your optimized prompt**

**Document results:**

| Metric | Before Optimization | After Optimization | Change |
|--------|-------------------|-------------------|--------|
| Cases passing all graders | __/10 | __/10 | +/- __ |
| Average star rating | __/5 | __/5 | +/- __ |
| Responses with tone issues | __ | __ | +/- __ |
| Responses with completeness issues | __ | __ | +/- __ |
| Responses with accuracy issues | __ | __ | +/- __ |

**Reflection Questions:**
- "What improved most significantly?"
- "Did anything get worse?"
- "What would you change in the next iteration?"
- "Is this agent ready for production?"

**Key Learning:**
> **Always measure.** Optimization isn't magic - it's informed iteration based on evidence. Sometimes suggestions help, sometimes they don't. Always validate with your eval dataset.

---

## ☕ Break (10 min)

---

## Part 7: Traces - Debugging Multi-Agent Systems (25 min)

### What Are Traces?

**Simple Definition:**
> A trace is like a replay of everything your agent did, step by step, with timing and token usage for each step.

**Why They Matter:**
- 🔍 See where routing decisions went wrong
- 🐛 Find where agents get stuck in loops
- 💰 Identify wasteful token usage
- ⏱️ Understand timing and latency issues
- 🔧 Debug complex multi-agent workflows

---

### SHOW: Reading Your First Trace (15 min)

#### Instructor Demonstrates with Real Trace

**Example Scenario:**
> User asks: "What's the weather in Karachi?"

**Trace Visualization:**

```
┌─────────────────────────────────────────────────┐
│ Span 1: Start Node                   [0.1s]    │
│   Input: "What's the weather in Karachi?"       │
│   ✓ Added to conversation history              │
│   Passed to next node                           │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│ Span 2: Triage Agent (Router)        [1.2s]    │
│   Received input                                │
│   Analyzed intent: weather query                │
│   Decision: Route to Weather Agent              │
│   Tokens used: 150                              │
│   ✓ Successful routing                          │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│ Span 3: Weather Agent                [2.1s]    │
│   Received: "What's the weather in Karachi?"    │
│   Tool call: get_weather(location="Karachi")    │
│   API response: {temp: 28, conditions: "..."}   │
│   Generated widget with weather data            │
│   Tokens used: 300                              │
│   ✓ Widget created successfully                │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│ Span 4: Output                        [0.1s]    │
│   Returned widget to user                       │
│   Total time: 3.5s                              │
│   Total tokens: 450                             │
│   ✓ Success                                     │
└─────────────────────────────────────────────────┘
```

**What to notice:**
- ✅ Each span = one step in the workflow
- ⏱️ Timing for each step (helps find bottlenecks)
- 💰 Token usage tracking (helps optimize costs)
- ✓/✗ Success/failure indicators
- 🔀 Routing decisions clearly shown

---

### Common Trace Patterns (10 min)

#### Pattern 1: ✅ Perfect Execution

```
Start → Router → Correct Specialist → Tool Use → Output
        [0.1s]   [1.2s]               [2.0s]     [0.1s]
```

**Characteristics:**
- Direct path, no retries
- Reasonable timing
- Moderate token usage
- Clear decision making

---

#### Pattern 2: ❌ Wrong Routing

```
Start → Router → Wrong Agent → Error → Retry → Router → Correct Agent
        [1.2s]   [2.0s]        [0.1s]  [1.0s]  [1.2s]   [2.0s]
                 ❌                              ✓
```

**Characteristics:**
- Wasted time and tokens on wrong agent
- User experiences delay
- Router needs better instructions

**Fix:** Improve routing criteria in Triage Agent prompt

---

#### Pattern 3: ❌ Tool Call Loop (Infinite Loop)

```
Start → Agent → Tool → Agent → Same Tool → Agent → Same Tool → Timeout
        [1.0s]  [2.0s] [1.0s]  [2.0s]      [1.0s]  [2.0s]     [ERROR]
```

**Characteristics:**
- Agent keeps calling same tool repeatedly
- Never reaches conclusion
- Hits timeout or max iterations
- Users see error or very long wait

**Fix:** Add loop detection, limit iterations, improve agent's decision logic

---

#### Pattern 4: ❌ Token Waste

```
Start → Agent [2500 tokens] → Simple Output
        [5.0s]
```

**Characteristics:**
- Excessive tokens for simple task
- Slow response time
- High cost
- Over-engineered prompt

**Fix:** Simplify prompt, reduce context window, remove unnecessary instructions

---

### PRACTICE: Debug Using Traces (15 min)

#### Task: Find and Document One Issue Using Traces

**Instructions:**

1. **Run your full multi-agent workflow**
   - Use 3-5 test cases
   - Ensure they hit different agents in your system
   - Include at least one that you expect might fail

2. **Review traces for each case:**
   - Open trace view in Agent Builder
   - Expand all spans
   - Note timing and token usage
   - Look for the patterns shown above

3. **Identify one issue:**
   - Find a case that failed or performed poorly
   - Use the trace to pinpoint exactly where it went wrong
   - Document the problem with evidence from the trace

4. **Propose a fix:**
   - Based on the trace, what would you change?
   - Instructions? Tool settings? Routing logic?

**Template for Documentation:**

```
Issue Found: _______________________________

Test Case:
  Input: _______________________________
  Expected: _______________________________
  Actual: _______________________________

Trace Evidence:
  Problem occurred at: Span __ [Agent/Node name]

  What the trace shows:
  _______________________________
  _______________________________

  Timing: _____ seconds
  Tokens used: _____

  Specific problem:
  [ ] Wrong routing
  [ ] Tool call loop
  [ ] Token waste
  [ ] Other: _______________________________

Impact:
  User experience: _______________________________
  Cost impact: _______________________________

Proposed Fix:
  What to change: _______________________________
  Expected improvement: _______________________________

  Specific changes to make:
  _______________________________
  _______________________________
```

**Example - Completed Template:**

```
Issue Found: Router sending weather queries to Web Search Agent

Test Case:
  Input: "What's the weather in Karachi?"
  Expected: Route to Weather Agent
  Actual: Routed to Web Search Agent first, then re-routed

Trace Evidence:
  Problem occurred at: Span 2 [Triage Agent]

  What the trace shows:
  - Triage Agent analyzed query
  - Decided to route to Web Search Agent (wrong choice)
  - Web Search Agent returned web results about Karachi weather
  - User said "I want current conditions"
  - Triage Agent re-routed to Weather Agent

  Timing: 8.5 seconds total (should be ~3s)
  Tokens used: 850 (should be ~450)

  Specific problem:
  [x] Wrong routing
  [ ] Tool call loop
  [ ] Token waste
  [ ] Other

Impact:
  User experience: Slow response, had to clarify intent
  Cost impact: Nearly 2x token usage

Proposed Fix:
  What to change: Improve Triage Agent routing instructions
  Expected improvement: Direct routing to Weather Agent for weather queries

  Specific changes to make:
  - Add to Triage Agent prompt: "Weather queries (current conditions,
    forecasts, temperature) should ALWAYS route to Weather Agent.
    Only use Web Search for weather NEWS or historical weather data."
  - Add examples in prompt of weather vs. web search queries
```

---

## Part 8: Complete Quality Loop (30 min)

### The Full Quality Loop

**Review the complete cycle:**

```
1. Component Test (5 cases on one node)
   ↓
2. Create Automated Graders (define quality standards)
   ↓
3. Expand Dataset (20 cases with grader checks)
   ↓
4. Run Evaluation with Graders
   ↓
5. Add Human Feedback (capture nuance)
   ↓
6. Analyze Traces (for multi-agent systems)
   ↓
7. Use Optimize Button (or make manual improvements)
   ↓
8. Re-evaluate with improved agent
   ↓
9. Compare Results & Document
   ↓
10. Decide: Deploy or Iterate Again
```

**You've learned each step. Now you'll execute the complete cycle independently.**

---

### PRACTICE: Independent Application (45 min)

#### Task: Complete a Full Evaluation Cycle

**This is your capstone exercise for this session.**

---

#### Phase 1: Baseline Evaluation (15 min)

**Objective:** Establish your starting point with comprehensive data

**Checklist:**

- [ ] **You should already have 20 cases from Part 4** ✓
  - If you need to add more edge cases, do so now
  - Ensure all agent capabilities are covered

- [ ] **Run full evaluation with all features enabled:**
  - All graders active
  - Human rating columns ready
  - Traces recorded

- [ ] **Collect ALL baseline data:**

**Baseline Metrics Template:**

```
Agent: _______________________________
Date: _______________________________
Dataset size: _____ cases

PASS/FAIL METRICS:
- Cases passing all graders: _____/20 (____%)
- Cases with 4+ star rating: _____/20 (____%)

GRADER BREAKDOWN:
- [Grader 1 name]: _____/20 passed
- [Grader 2 name]: _____/20 passed
- [Grader 3 name]: _____/20 passed

HUMAN FEEDBACK:
- Average star rating: _____/5
- Most common issues: _______________________________

TRACES (if multi-agent):
- Average response time: _____ seconds
- Average tokens per case: _____
- Wrong routing incidents: _____
- Tool call loops: _____

TOP 3 FAILURE PATTERNS:
1. _______________________________
2. _______________________________
3. _______________________________
```

---

#### Phase 2: Optimize (15 min)

**Objective:** Make evidence-based improvements

**Checklist:**

- [ ] **Review all evaluation data:**
  - Which cases failed most consistently?
  - What do graders flag repeatedly?
  - What does human feedback say?
  - What do traces reveal?

- [ ] **Identify top 3 issues to fix:**

```
Issue 1: _______________________________
  Evidence: _______________________________
  Proposed fix: _______________________________

Issue 2: _______________________________
  Evidence: _______________________________
  Proposed fix: _______________________________

Issue 3: _______________________________
  Evidence: _______________________________
  Proposed fix: _______________________________
```

- [ ] **Make improvements:**
  - Use Optimize button, OR
  - Manually refine prompts, OR
  - Combination of both

- [ ] **Document exactly what you changed:**

```
Changes Made:

Change 1:
  What: _______________________________
  Why: _______________________________
  Expected impact: _______________________________

Change 2:
  What: _______________________________
  Why: _______________________________
  Expected impact: _______________________________

Change 3:
  What: _______________________________
  Why: _______________________________
  Expected impact: _______________________________
```

---

#### Phase 3: Re-Evaluation (10 min)

**Objective:** Measure the impact of your changes

**Checklist:**

- [ ] **Re-run evaluation with improved agent**
  - Use same 20-case dataset
  - Use same graders (don't change criteria)
  - Use same rating approach

- [ ] **Collect after metrics:**

```
AFTER OPTIMIZATION METRICS:

PASS/FAIL METRICS:
- Cases passing all graders: _____/20 (____%)
- Cases with 4+ star rating: _____/20 (____%)

GRADER BREAKDOWN:
- [Grader 1 name]: _____/20 passed
- [Grader 2 name]: _____/20 passed
- [Grader 3 name]: _____/20 passed

HUMAN FEEDBACK:
- Average star rating: _____/5
- Most common issues: _______________________________

TRACES (if multi-agent):
- Average response time: _____ seconds
- Average tokens per case: _____
- Wrong routing incidents: _____
- Tool call loops: _____
```

---

#### Phase 4: Analysis & Documentation (5 min)

**Objective:** Understand what worked and what didn't

**Comparison Table:**

| Metric | Before | After | Change | % Change |
|--------|--------|-------|--------|----------|
| Pass rate (all graders) | ___% | ___% | +___% | +___% |
| Avg star rating | ___/5 | ___/5 | +___ | +___% |
| Avg response time | ___s | ___s | ±___s | ±___% |
| Avg tokens | ___ | ___ | ±___ | ±___% |
| Wrong routing | ___ | ___ | -___ | -___% |

**Trade-offs Analysis:**

```
What Improved:
- _______________________________
- _______________________________
- _______________________________

What Got Worse (if anything):
- _______________________________
- _______________________________

Why Trade-offs Are Acceptable:
_______________________________
_______________________________

Why Trade-offs Are NOT Acceptable:
_______________________________
_______________________________
```

**Decision:**

```
[ ] Ready for production
    Reasoning: _______________________________

[ ] Needs another iteration
    What to fix next: _______________________________

[ ] Needs major redesign
    Why: _______________________________
```

---

### Comprehensive Eval Report Template (10 min)

**Create your final deliverable:**

```markdown
# Evaluation Report: [Agent Name]

## Executive Summary
- **Date:** [Date]
- **Agent Version:** [Version number or description]
- **Dataset Size:** 20 cases
- **Overall Result:** [Pass/Needs Work/Major Issues]
- **Key Improvement:** +[X]% pass rate

---

## Baseline Metrics

### Pass/Fail Results
| Metric | Value |
|--------|-------|
| Cases passing all graders | ___/20 (___%) |
| Cases with 4+ stars | ___/20 (___%) |
| Average star rating | ___/5 |

### Grader Breakdown
| Grader | Pass Rate |
|--------|-----------|
| [Grader 1] | ___/20 |
| [Grader 2] | ___/20 |
| [Grader 3] | ___/20 |

### Performance (Multi-Agent Only)
| Metric | Value |
|--------|-------|
| Avg response time | ___s |
| Avg tokens | ___ |
| Wrong routing incidents | ___ |

---

## Issues Identified

### Issue 1: [Issue Name]
**Evidence:**
- Grader: [Which grader flagged this]
- Failed cases: [#1, #3, #7]
- Pattern: [Description]
- Trace evidence: [What traces showed]

**Impact:**
- User experience: [Description]
- Frequency: ___/20 cases (___%)

### Issue 2: [Issue Name]
**Evidence:**
- [Same structure as above]

### Issue 3: [Issue Name]
**Evidence:**
- [Same structure as above]

---

## Changes Made

### Change 1: [Change Description]
**What:** [Specific change made]
**Why:** [Reasoning based on evidence]
**Expected Impact:** [What you hoped to improve]
**Method:** [Optimize button / Manual / Both]

**Before Prompt:**
```
[Original prompt text]
```

**After Prompt:**
```
[Improved prompt text]
```

### Change 2: [Change Description]
[Same structure]

### Change 3: [Change Description]
[Same structure]

---

## After Metrics

### Pass/Fail Results
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Cases passing all graders | ___% | ___% | +___% |
| Cases with 4+ stars | ___% | ___% | +___% |
| Average star rating | ___/5 | ___/5 | +___ |

### Grader Breakdown
| Grader | Before | After | Change |
|--------|--------|-------|--------|
| [Grader 1] | ___/20 | ___/20 | +___ |
| [Grader 2] | ___/20 | ___/20 | +___ |
| [Grader 3] | ___/20 | ___/20 | +___ |

### Performance (Multi-Agent Only)
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Avg response time | ___s | ___s | ±___s |
| Avg tokens | ___ | ___ | ±___ |
| Wrong routing | ___ | ___ | -___ |

---

## Key Improvements

### What Worked Well
1. **[Improvement 1]**
   - Metric: [Specific metric that improved]
   - Impact: [Quantified improvement]
   - Why: [Root cause addressed]

2. **[Improvement 2]**
   - [Same structure]

3. **[Improvement 3]**
   - [Same structure]

---

## Trade-offs & Limitations

### Trade-offs Accepted
1. **[Trade-off description]**
   - What improved: [Metric]
   - What got slightly worse: [Metric]
   - Why acceptable: [Reasoning]

### Outstanding Issues
1. **[Issue still present]**
   - Why not fixed yet: [Reasoning]
   - Plan to address: [Future iteration]

---

## Production Readiness Assessment

### Checklist
- [ ] Pass rate > 90%
- [ ] No critical failures on typical cases
- [ ] Response time < 5 seconds
- [ ] Token usage within budget
- [ ] No wrong routing on common queries
- [ ] Human ratings avg > 4/5 stars
- [ ] All graders aligned with human judgment

### Decision

**[X] Ready for Production**
- Reasoning: [Why you believe it's ready]
- Monitoring plan: [How you'll track in production]

**OR**

**[ ] Needs Another Iteration**
- Key blockers: [What prevents deployment]
- Next steps: [Specific actions for next iteration]
- Timeline: [When to re-evaluate]

**OR**

**[ ] Needs Major Redesign**
- Fundamental issues: [What's broken]
- Redesign plan: [Approach to fix]

---

## Next Iteration Recommendations

### Immediate Next Steps
1. [Action item 1]
2. [Action item 2]
3. [Action item 3]

### Future Improvements
1. [Enhancement 1]
2. [Enhancement 2]
3. [Enhancement 3]

### Dataset Expansion
- Add [X] cases for [scenario type]
- Include more [edge case type]
- Test [new feature/capability]

---

## Lessons Learned

### What Worked
- [Learning 1]
- [Learning 2]

### What Didn't Work
- [Learning 1]
- [Learning 2]

### Process Improvements
- [Change to eval process for next time]

---

## Appendix

### Dataset Overview
[Brief description of your 20 test cases]

### Grader Criteria
**[Grader 1 Name]:** [Exact criteria]
**[Grader 2 Name]:** [Exact criteria]
**[Grader 3 Name]:** [Exact criteria]

### Sample Failing Cases (Before)
[Show 1-2 examples of failures]

### Sample Passing Cases (After)
[Show how those same cases now pass]

---

**Report Author:** [Your name]
**Date:** [Date]
**Agent Version:** [Version]
```

---

## Part 9: Consolidation & Transfer (5 min)

### Retrieval Practice (5 min)

**Quick self-check (no stakes, just checking understanding):**

1. **What's the recommended workflow for starting evaluations?**
   - Answer: Start with 5 component-level cases, build graders to define quality, then expand to 20 diverse cases

2. **Name the 5 evaluation features in AgentKit:**
   - Answer:
     1. Datasets UI
     2. Human Feedback
     3. Automated Graders
     4. Optimize Button
     5. Traces

3. **What are the 3 best practices from OpenAI?**
   - Answer:
     1. Start simple and early
     2. Use real data
     3. Align your LLM graders

4. **When should you click the Optimize button?**
   - Answer: After identifying patterns in failures through evals

5. **What do traces help you debug?**
   - Answer: Multi-agent routing, tool call issues, token waste, timing problems

---

### Connection to Real Projects (5 min)

**Discussion Prompts:**

**Think about your capstone project:**
- "How will you use evaluations in your project?"
- "What will be the first 10 cases you test?"
- "Which graders will matter most for your use case?"

**Think about production deployment:**
- "How often will you run evals once deployed?"
- "What metrics will you track over time?"
- "How will you collect real user data for your dataset?"

**Reflection:**
- "What surprised you most about evaluations today?"
- "What will you do differently tomorrow based on what you learned?"
- "What's still confusing or unclear?"

---

### The Three Golden Rules (5 min)

**Commit these to memory - they're the foundation of quality agents:**

#### 1. Start Simple and Early

**What it means:**
- Create evals from day 1, not after building is "done"
- Start with 5 component cases, build graders, then expand to 20
- Don't wait for perfect - start with good enough
- Grow dataset as you discover issues

**Why it matters:**
- Catch problems early when they're cheap to fix
- Build quality in, don't bolt it on later
- Faster iterations = faster learning

**Action:** Tomorrow, start with a 5-case component test, build graders, then expand to 20 cases

---

#### 2. Use Real Data

**What it means:**
- Use actual user queries from logs, tickets, transcripts
- Include real failure modes you've seen
- Capture the messiness: typos, ambiguity, edge cases
- Don't rely on synthetic or imagined test cases

**Why it matters:**
- Synthetic data misses real-world complexity
- Users do unexpected things
- Edge cases from production are your best teachers

**Action:** Review your support logs/user feedback - pull 5 real queries for your next dataset

---

#### 3. Align Your LLM Graders

**What it means:**
- Compare grader outputs to your own human ratings
- Refine criteria when graders disagree with humans
- Test grader consistency across edge cases
- Document your quality standards
- Target 85%+ agreement with human judgment

**Why it matters:**
- Graders that don't match human standards are useless
- Alignment is iterative - first versions are always rough
- Well-aligned graders save massive time at scale

**Action:** For each grader you create, manually check the first 20 results and refine criteria

---

### Key Takeaways Summary

**What You Can Do Now:**

✅ **Create systematic evaluations** instead of ad-hoc testing
✅ **Use data to drive decisions** instead of guessing
✅ **Scale quality checks** with automated graders
✅ **Optimize based on evidence** using the Optimize button
✅ **Debug complex systems** using traces
✅ **Build quality loops** that continuously improve agents
✅ **Make production-ready agents** with measurable quality

---

## 📖 Resources & References

### Official OpenAI Video

**Build Hour: AgentKit - Full Session**
- Full video: [Watch on YouTube](http://www.youtube.com/watch?v=sAitLFLbgDA)

**Evaluation Section (starts at 24:29):**
- Overview of evaluations: [24:29](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1469s)
- Datasets UI demo: [26:33](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1593s)
- Human feedback columns: [27:48](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1668s)
- Automated graders: [28:45](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1725s)
- Optimize button: [29:52](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1792s)
- End-to-end traces: [31:23](http://www.youtube.com/watch?v=sAitLFLbgDA&t=1883s)
- Best practice: Start simple and early: [33:47](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2027s)
- Best practice: Use real data: [34:33](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2073s)
- Best practice: Align LLM graders: [34:45](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2085s)
- Dataset size recommendation (10-20): [35:34](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2134s)
- RAMP case study: [37:06](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2226s)
- HubSpot case study: [38:24](http://www.youtube.com/watch?v=sAitLFLbgDA&t=2304s)

### Official Documentation
- [AgentKit Overview](https://openai.com/index/introducing-agentkit/)
- [Agent Builder Documentation](https://platform.openai.com/docs/guides/agent-builder)
- [Evaluation Best Practices](https://platform.openai.com/docs/guides/evaluation-best-practices)

---

## 💡 Tips & Best Practices

### Creating Great Test Cases

**✅ Do:**
- Cover all major use cases
- Include edge cases (unusual but valid)
- Include error cases (should fail gracefully)
- Use real user language (typos, ambiguity)
- Vary complexity (simple to complex)

**❌ Don't:**
- Make all cases similar
- Use only "perfect" inputs
- Ignore error handling
- Create synthetic/unrealistic scenarios
- Skip coverage of rare but critical cases

---

### Writing Effective Grading Criteria

**✅ Do:**
- Be specific and measurable
- Give examples of pass/fail
- Test criteria on edge cases
- Refine based on disagreements
- Document your reasoning

**❌ Don't:**
- Use vague language ("good", "helpful")
- Make criteria too strict
- Ignore context and nuance
- Set and forget - always iterate
- Expect perfection on first try

---

### Using the Optimize Button

**✅ Do:**
- Review suggestions critically
- Understand WHY changes help
- Test before/after
- Keep what works from original
- Iterate multiple times

**❌ Don't:**
- Blindly accept all suggestions
- Skip the comparison step
- Ignore domain requirements
- Expect one-click perfection
- Forget to measure impact

---

### Reading Traces Effectively

**✅ Do:**
- Look for patterns across multiple traces
- Check timing for each span
- Track token usage
- Identify routing decisions
- Note tool call results

**❌ Don't:**
- Focus on single traces only
- Ignore timing data
- Overlook token waste
- Miss routing issues
- Skip failed tool calls

---

## 🎯 Common Pitfalls & How to Avoid Them

### Pitfall 1: "I need 1000 test cases before I start"

**Why it's wrong:** Quality matters more than quantity. 1000 bad test cases teach you less than 10 good ones.

**What to do instead:** Start with 10-20 diverse, high-quality cases. Add more as you discover gaps.

---

### Pitfall 2: "My graders keep failing everything"

**Why it happens:** Criteria are too strict or unclear.

**What to do instead:**
1. Compare grader results to your own ratings
2. If grader is stricter than you - soften criteria
3. Add examples of acceptable vs. unacceptable
4. Test on edge cases

---

### Pitfall 3: "Optimize button made things worse"

**Why it happens:** Suggestions don't always help - they're based on patterns, not magic.

**What to do instead:**
1. Always compare before/after metrics
2. Understand what changed and why
3. Keep original version for rollback
4. Modify suggestions to preserve what works
5. Accept that iteration is required

---

### Pitfall 4: "All my cases are passing but users still complain"

**Why it happens:** Test cases don't cover what users actually do.

**What to do instead:**
1. Add real user queries from logs
2. Include actual failure cases
3. Test edge cases users discovered
4. Add human feedback metrics
5. Expand dataset based on production issues

---

### Pitfall 5: "I don't have time for evals"

**Why it's wrong:** Evals save time by catching bugs before production.

**What to do instead:**
1. Start small (5 component cases, then build graders, then expand to 20)
2. Automate with graders early (saves hours later)
3. Build eval as you build agent (not after)
4. Think of evals as faster iteration, not overhead

---

## 🔧 Troubleshooting Guide

### Issue: "Datasets UI won't open"

**Solutions:**
- Refresh Agent Builder
- Make sure you clicked on an Agent node (not Start or other nodes)
- Check you have edit permissions on the workflow
- Try a different browser

---

### Issue: "Grader results are inconsistent"

**Solutions:**
- Make criteria more specific
- Add examples of pass/fail to criteria
- Test grader on same case multiple times
- If still inconsistent, use rule-based instead of LLM-based
- Document edge cases in criteria

---

### Issue: "Optimize button doesn't suggest changes"

**Possible reasons:**
- Not enough evaluation data (need failures to learn from)
- No patterns in failures (each case fails differently)
- Graders and human feedback don't agree
- Prompt is already near-optimal

**Solutions:**
- Run more test cases
- Add more graders and human feedback
- Identify clearer failure patterns
- Try manual improvements if optimization isn't helping

---

### Issue: "Traces don't show what I expect"

**Solutions:**
- Make sure traces are enabled in evaluation settings
- Check you're looking at the right run
- Expand all spans to see details
- Refresh the trace view
- Verify workflow executed (check for errors)

---

### Issue: "Can't decide between accepting or rejecting optimization"

**Framework for decision:**
1. Does it address the failure pattern? (Yes = lean accept)
2. Does it contradict requirements? (Yes = reject)
3. Do metrics improve when tested? (Yes = accept)
4. Do you understand why it helps? (No = investigate more)
5. Are there negative side effects? (Yes = modify)

---

## 🎊 Congratulations!

**You've completed Evaluation Mastery for AgentKit.**

You now have the skills to:
- ✅ Build systematic evaluation datasets
- ✅ Use human and automated quality checks
- ✅ Optimize agents based on evidence
- ✅ Debug complex multi-agent systems
- ✅ Make data-driven deployment decisions
- ✅ Build sustainable quality loops

**These skills are the foundation of production-ready AI agents.**

 in Session 9!** 🚀
