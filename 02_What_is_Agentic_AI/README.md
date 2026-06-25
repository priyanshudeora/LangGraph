# What is Agentic AI? — Video Summary

> **Playlist:** LangGraph Agentic AI Series — **Video 2**  
> This video builds on Video 1 (Generative AI vs Agentic AI) and formally defines Agentic AI, its key characteristics, and core components.

---

## Table of Contents

1. [What is Agentic AI?](#what-is-agentic-ai)
2. [Generative AI vs Agentic AI](#generative-ai-vs-agentic-ai)
3. [Practical Example: AI HR Recruiter](#practical-example-ai-hr-recruiter)
4. [Six Key Characteristics](#six-key-characteristics)
5. [Five Core Components](#five-core-components)
6. [Conclusion](#conclusion)

---

## What is Agentic AI?

**Definition:** Agentic AI is a type of AI that can take up a task and goal from a user and then work towards completing it on its own with minimal human guidance. It plans tasks, adapts to changes, and seeks help only when necessary.

In simple words, Agentic AI is a **software paradigm** where:

1. You provide a **goal** to the system.
2. The system **thinks** about how to achieve that goal.
3. It handles **planning** and **execution** automatically.
4. **Human involvement remains minimal.**

This is fundamentally different from reactive paradigms like Generative AI chatbots, where the system only responds to what you ask — it cannot take initiative on its own.

---

## Generative AI vs Agentic AI

### Reactive (Generative AI) — Goa Travel Example

| Step | What You Do | What Chatbot Does |
|------|-------------|-------------------|
| 1 | Ask best way to reach Goa on the 15th | Answers that specific question (e.g., flight) |
| 2 | Ask about hotels for that duration | Gives hotel recommendations |
| 3 | Ask about places to visit based on weather | Answers that specific question |

**Pattern:** You ask → Chatbot answers. The entire process is **reactive** and **on-demand**.

### Proactive (Agentic AI) — Same Goa Trip

You tell the agent: *"I'm going to Goa between these dates."*

The agent then **automatically**:
- Finds the best way to reach Goa on those dates
- Recommends hotels
- Plans the full itinerary based on weather

**Pattern:** You give a goal → The system plans and executes. The process is **autonomous** and **proactive**.

---

## Practical Example: AI HR Recruiter

> **Note:** This example was also covered in Video 1. If you've seen it, skip to [Six Key Characteristics](#six-key-characteristics).

### Scenario

You are an HR recruiter tasked with hiring a **Backend Engineer** (2–4 years experience, remote). Your company provides an **Agentic AI chatbot** to help accomplish this.

### Step 1: Goal & Planning

You tell the agent your hiring requirements. The agent:
1. **Understands the goal**
2. **Develops a plan**, e.g.:
   - Draft a Job Description (JD)
   - Post JD on job platforms
   - Monitor applications
   - Adjust if applications are low
   - Screen candidates
   - Schedule interviews
   - Send offer letters
   - Start onboarding for accepted candidates

### Step 2: Execution (Autonomous)

The agent executes the plan step by step **without human intervention**:

| Step | Action |
|------|--------|
| **Draft JD** | Accesses company documents to understand tech stack, salary, responsibilities. Presents draft for your review. |
| **Post JD** | Asks permission, then posts on LinkedIn via API. Notifies you and begins monitoring applications. |
| **Adapt** | After 3 days with only 2 applicants, proactively suggests: (1) change "Backend Engineer" to "Full Stack Engineer" in JD, (2) run a LinkedIn ad. Takes permission and executes. |
| **Screen** | Uses resume parser tool. Reports: 2 strong, 3 partial, 3 weak matches. Asks to schedule interviews with strong candidates. |
| **Schedule Interviews** | Checks your calendar, drafts emails, sends to you and candidates, reminds you on interview day, sends suggested interview questions. |
| **Offer Letter** | Drafts offer from company documents, gets your approval, sends via email. |
| **Onboarding** | Monitors offer acceptance. On acceptance: sends welcome email, submits IT access request, provisions laptop, schedules intro meeting. |

### Key Takeaway from the Example

The agent is **highly autonomous** — you gave a goal, and it handled planning, execution, and adaptation. It only contacts you for **permission** on sensitive actions or when situations require human judgment. 

---

## Six Key Characteristics

Use these six traits to identify whether a system is truly Agentic AI:

### 1. Autonomy

**Definition:** The AI system's ability to make decisions and take actions on its own to achieve a given goal without needing step-by-step human instructions.

**Types of Autonomy in Agentic Systems:**

| Type | Example from HR Recruiter |
|------|---------------------------|
| **Execution autonomy** | Automatically executes plan steps: draft JD → post → screen → schedule → offer |
| **Decision-making autonomy** | Decides how many candidates to shortlist and on what basis |
| **Tool usage autonomy** | Decides which tool to use when (email, calendar, resume parser, LinkedIn API) |

**Autonomy is also proactive:** The agent monitors job applications and, without being asked, realizes applications are low and suggests changes.

#### Controlling Autonomy

Autonomy must be controlled because unchecked autonomy can be dangerous:

| Control Method | Description | Example |
|----------------|-------------|---------|
| **Scope limits** | Define what tools/actions the agent can perform independently | Agent can screen resumes but must ask before rejecting anyone |
| **Human-in-the-loop** | Insert checkpoints requiring human approval | Agent drafts JD but asks before posting on platforms |
| **Override controls** | Allow users to stop, pause, or change behavior | Command "pause hiring" stops the agent until "start hiring" |
| **Guardrails & policies** | Hard rules and ethical boundaries | No interviews on weekends; no informal language in emails |

**Risks of uncontrolled autonomy:**
- Sending offer letters with incorrect salaries/terms without approval
- Biased shortlisting (nationality, age) violating hiring laws
- Spending unlimited money on LinkedIn ads without permission

---

### 2. Goal-Oriented

**Definition:** The AI system operates with a persistent objective in mind and continuously directs its actions to achieve that objective rather than just responding to isolated prompts.

- The goal acts as a **compass** — it ensures autonomy is directed correctly.
- Without a goal, the system cannot function autonomously.
- **Autonomy and goal-orientation go hand in hand.**

#### Types of Goals

| Type | Example |
|------|---------|
| **Independent goal** | "Hire a Backend Engineer" |
| **Goal with constraints** | "Hire a Backend Engineer from India" / "Remote only" / "Budget: $X" |

#### Goal Storage (Conceptual)

Goals are stored in the agent's **memory**:

```json
{
  "goal": "Hire Backend Engineer",
  "constraints": {
    "experience": "2-4 years",
    "remote": true,
    "stack": ["Python", "Django", "AWS"]
  },
  "status": "active",
  "created_at": "2026-06-01",
  "progress": {
    "jd_created": true,
    "posted_on": ["LinkedIn", "Naukri"],
    "applications": 8,
    "interviews_scheduled": 2,
    "hired": false,
    "onboarding": false
  }
}
```

When hiring completes, status becomes `"completed"`.

#### Midway Goal Changes

Goals can be altered mid-process. Example: After 7 days with no applicants, change from "hire Backend Engineer" to "find a Freelancer" — the agent adapts its planning and execution accordingly.

---

### 3. Planning

**Definition:** The agent's ability to break down a high-level goal into a structured sequence of actions and subgoals.

Agentic AI systems operate in two steps:
1. **Planning** — figure out how to achieve the goal
2. **Execution** — implement the plan step by step

This is an **iterative loop**: if execution reveals a step is unnecessary or wrong, the agent returns to planning and creates a revised plan.

#### Planning in Three Steps

**Step 1: Generate Multiple Candidate Plans**

The agent does not make a single plan — it generates **multiple candidate plans**:

| Plan A | Plan B |
|--------|--------|
| Draft JD → Post on LinkedIn/Naukri → Promote → Hire | Post on other portals → Internal referrals → Hiring agency |

Planning is essentially a **search problem**: initial state (need engineer) → final state (engineer hired), with multiple paths between them.

**Step 2: Evaluate Plans**

| Criterion | How It's Used |
|-----------|---------------|
| **Efficiency** | Which plan is faster to execute? |
| **Tool availability** | Reject plans requiring tools not available (e.g., no Google Search API) |
| **Cost** | Avoid hiring agency route if budget is constrained |
| **Risk** | Which plan has higher failure risk? |
| **Alignment with constraints** | LinkedIn may have more remote candidates than internal referrals |

**Step 3: Select Best Plan**

- **Human-in-the-loop:** Ask supervisor which plan to choose
- **Pre-programmed policy:** Agent selects based on internal rules

---

### 4. Reasoning

**Definition:** The cognitive process through which an agentic AI system interprets information, draws conclusions, and makes decisions — both while planning and executing.

**Human analogy:** Phone stolen → interpret info → conclude thief may misuse number → decide to call Airtel to block the number. Same capability exists in AI agents when environment gives feedback.

#### Reasoning During Planning

| Task | Why Reasoning Is Needed |
|------|-------------------------|
| **Goal decomposition** | Breaking "hire Backend Engineer" into actionable steps |
| **Tool selection** | Deciding Google search is needed to find salary for 2–4 years experience |
| **Resource estimation** | Estimating time, dependencies, and risks |

#### Reasoning During Execution

| Task | Why Reasoning Is Needed |
|------|-------------------------|
| **Decision making** | Out of 3 partial-match candidates, interview 2 or all 3? |
| **Human-in-the-loop** | Unsure about salary — search Google or ask human? |
| **Error handling** | LinkedIn server down — wait and retry, notify human, or post elsewhere? |

---

### 5. Adaptability

**Definition:** The agent's ability to modify its plans, strategies, and actions in response to unexpected conditions while staying aligned with the goal.

**Example:** After 3 days with few applications, the agent adapts by:
1. Running LinkedIn ads
2. Modifying JD from "Backend Engineer" to "Full Stack Engineer"

#### When Adaptability Is Required

| Situation | Example |
|-----------|---------|
| **Tool failures** | Calendar API down → message human directly for availability |
| **External feedback** | Low application count from LinkedIn environment |
| **Goal changes** | Switch from hiring Backend Engineer to finding a Freelancer |

Agentic systems never get stuck — they find alternate paths when blocked.

---

### 6. Context Awareness

**Definition:** The agent's ability to understand, retain, and utilize relevant information from ongoing tasks, past interactions, user preferences, and environmental cues to make better decisions through a multistep process.

Without context, a multi-day hiring process breaks down — if you return after 4 days asking "how many applicants?", the agent must remember the JD was posted on LinkedIn.

#### Types of Context Stored

| Context Type | Example |
|--------------|---------|
| **Original goal** | Hire Backend Engineer with 2–4 years experience, remote |
| **Progress & history** | JD finalized, posted on LinkedIn, 8 applications, 2 interviews scheduled |
| **Human-agent conversation** | Chat history between recruiter and agent |
| **Environment state** | LinkedIn job posted, 8 applicants, ad budget ending in 2 days |
| **Tool responses** | Resume parser: "Candidate B has 3 years Django + AWS experience" |
| **User preferences** | Company prefers remote candidates; send interview questions via Google Doc |
| **Guardrails/policies** | Don't send offer letter without approval; don't auto-run paid ads |

#### Memory Types

| Memory | Stores | Example |
|--------|--------|---------|
| **Short-term** | Current session info | Tool response: Candidate B has 3 years experience |
| **Long-term** | Persistent across sessions | Guardrail: never send offer without approval; user preferences; goal tracking |

Context awareness is implemented through **memory** — covered in detail when studying LangGraph.

---

## Five Core Components

Every Agentic AI application has five high-level components:

```
┌─────────────────────────────────────────────────────────┐
│                    SUPERVISOR                           │
│         (Human-in-the-loop, guardrails, escalation)     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   ┌──────────┐    ┌──────────────┐    ┌──────────┐     │
│   │  BRAIN   │───▶│ ORCHESTRATOR │───▶│  TOOLS   │     │
│   │  (LLM)   │    │  (Manager)   │    │ (Hands/  │     │
│   └──────────┘    └──────────────┘    │  Legs)   │     │
│        │                 │            └──────────┘     │
│        └────────┬────────┘                             │
│                 ▼                                       │
│           ┌──────────┐                                  │
│           │  MEMORY  │                                  │
│           └──────────┘                                  │
└─────────────────────────────────────────────────────────┘
```

### 1. Brain (LLM)

The **backbone** of LLM-based Agentic AI systems. The LLM performs:

| Function | Description |
|----------|-------------|
| **Goal interpretation** | Understand what the user wants |
| **Planning** | Break goals into subgoals and steps |
| **Reasoning** | Draw conclusions during planning and execution |
| **Tool selection** | Decide which tool to use for each step |
| **Communication** | Natural language generation and understanding with humans |

> Note: Non-LLM agents (e.g., reinforcement learning agents) exist, but this series focuses on **LLM-based** Agentic AI.

---

### 2. Orchestrator

The **project manager** / **nervous system** — executes the plan step by step. Built using frameworks like **LangGraph**, CrewAI, or AutoGen.

| Responsibility | Description |
|----------------|-------------|
| **Task sequencing** | Determine order of step execution |
| **Conditional routing** | Based on step 2 output, go to step 3 or step 4 |
| **Retry logic** | If LinkedIn is down, retry after some time |
| **Looping & iteration** | Repeat steps when needed |
| **Delegation** | Decide when to involve LLM vs human |

---

### 3. Tools

The **hands and legs** — how the agent interacts with the external world:

| Tool Type | Example |
|-----------|---------|
| **APIs** | LinkedIn Job API, Calendar API, Email API |
| **Data tools** | Resume parser, database updates |
| **Knowledge base (RAG)** | Company documents for JD drafting and offer letters |

Any external action (API call, email, database change) happens through tools.

---

### 4. Memory

Stores all context the agent needs:

| Type | Stores |
|------|--------|
| **Short-term** | Current session messages, tool calls, immediate decisions |
| **Long-term** | Goals, past interactions, user preferences, cross-session decisions, progress tracking |

---

### 5. Supervisor

Implements **human-in-the-loop** — connects the agent with humans:

| Role | Example |
|------|---------|
| **Approval gates** | Notify human before sending offer letter or running LinkedIn ads |
| **Guardrail enforcement** | Ensure agent follows defined policies |
| **Escalation** | Guardrail says "hire only from IITs/NITs" but agent finds an exceptional non-IIT candidate → alerts human |

---

### Deeper Architecture (Beyond Beginner Level)

The five components are a high-level overview. Internally, the Brain may contain sub-components:

- **Planner** — generates multiple candidate plans
- **Evaluator** — evaluates and selects the best plan

These will be explored in depth when building with LangGraph.

---

## Conclusion

### Quick Checklist: Is It Agentic AI?

Ask these six questions — if all answers are **yes**, the system is Agentic AI:

| # | Question |
|---|----------|
| 1 | Is it **autonomous**? |
| 2 | Is it **goal-oriented**? |
| 3 | Can it **plan**? |
| 4 | Can it **reason**? |
| 5 | Can it **adapt**? |
| 6 | Is it **context-aware**? |

### What We Covered

1. **Definition** of Agentic AI
2. **Practical scenario** — AI HR Recruiter
3. **Six key characteristics** — Autonomy, Goal-oriented, Planning, Reasoning, Adaptability, Context Awareness
4. **Five core components** — Brain, Orchestrator, Tools, Memory, Supervisor

This theoretical foundation will be essential when practically coding and building agents in the rest of this LangGraph playlist.

---

*Next up: Hands-on agent building with LangGraph.*
