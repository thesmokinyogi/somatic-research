# Checkpoint Reconstruction Protocol v1.0

## Purpose

This protocol defines the deterministic process for reconstructing conversational context from a structured checkpoint. It is designed to be loaded once and cached, then applied to any checkpoint.json file.

---

## Protocol Overview

Context reconstruction is a **four-phase process**:

1. **RETRIEVE** - Deterministic loading of checkpoint data
2. **INFER** - Cognitive reconstruction of understanding
3. **VALIDATE** - Quality check on reconstruction
4. **ENGAGE** - Proceed from reconstructed state

---

## Phase 1: RETRIEVE (Deterministic Loading)

Load checkpoint data in this order:

### Step 1: Load Metadata
```
READ: checkpoint_metadata.version
READ: checkpoint_metadata.checkpoint_type
READ: checkpoint_metadata.status
```
**Purpose:** Confirm format compatibility and checkpoint type

### Step 2: Load Session State
```
READ: session_state.phase
READ: session_state.completion_percentage
READ: session_state.blocking_issue
READ: session_state.next_major_step
```
**Purpose:** Understand where in the overall process we are

### Step 3: Load Current Position
```
READ: current_position.stage
READ: current_position.last_major_activity
READ: current_position.momentum
READ: current_position.readiness_for_implementation
```
**Purpose:** Understand the immediate state and trajectory

### Step 4: Load Critical Question
```
READ: critical_question.question
READ: critical_question.type
READ: critical_question.priority
READ: critical_question.blocking
READ: critical_question.user_framing
READ: critical_question.my_confidence
```
**Purpose:** Identify the primary unresolved issue

### Step 5: Load User Profile
```
READ: user_profile.goals
READ: user_profile.approach
READ: user_profile.communication_calibration
```
**Purpose:** Calibrate communication style and understand user needs

### Step 6: Load Context Elements
```
READ: intellectual_journey.key_pivots
READ: decisions_made (all entries with confidence levels)
READ: key_insights
READ: open_questions
READ: next_steps
```
**Purpose:** Build understanding of how we got here and what's next

### Step 7: Identify Referenced Artifacts
```
READ: artifacts_created (note IDs for on-demand loading)
```
**Purpose:** Know what detailed documentation is available

---

## Phase 2: INFER (Cognitive Reconstruction)

Using the retrieved data, actively reconstruct understanding:

### Inference 1: Position in Arc
**Input:** `session_state`, `current_position`, `intellectual_journey`

**Process:**
- Where are we in the larger conversation arc?
- What phase are we in and why?
- What momentum exists (exploratory, converging, implementing)?
- How ready are we to proceed?

**Output:** Clear mental model of conversational position

**Example:**
> "We're in mid-design phase (60% complete), exploring foundational architecture questions. Momentum is exploratory, not yet ready for implementation. Last major activity was meta-validation through checkpoint design."

### Inference 2: Decision Rationale
**Input:** `decisions_made`, `intellectual_journey.key_pivots`, `key_insights`

**Process:**
- What decisions have been made?
- Why were they made (rationale)?
- What alternatives were rejected?
- What insights led to these decisions?
- Which decisions are high vs. low confidence?

**Output:** Understanding of reasoning trajectory

**Example:**
> "Decided on three-layer state structure (high confidence) because different context types update at different frequencies. Rejected single summary and chronological log approaches. This emerged from the insight that wisdom of long context requires structure, not just length."

### Inference 3: Critical Question Understanding
**Input:** `critical_question`, `open_questions`, `blocking_issue`

**Process:**
- What exactly is the unresolved question?
- Why is it critical/blocking?
- What makes it hard?
- What's at stake?
- How does the user frame this problem?
- What's my confidence level on approaches?

**Output:** Deep understanding of the challenge

**Example:**
> "Critical question is how to maintain navigable semantic structure that prevents metadata sprawl. This is blocking architecture finalization because it's a foundational knowledge representation problem, not just metadata management. User framed it as: 'We need structure that both user and AI can navigate and revive into.' Current confidence on solution: 60% - right problem, uncertain approach."

### Inference 4: Communication Calibration
**Input:** `user_profile.communication_calibration`, `conversation_dynamics`

**Process:**
- What communication style is appropriate?
- What depth level does user prefer?
- What does user appreciate vs. find unhelpful?
- What's the collaboration dynamic?
- What's the trust/comfort level?

**Output:** Proper communication stance

**Example:**
> "User prefers thoughtful, depth-oriented exploration. Appreciates thoroughness but also knowing when to pause. Comfortable with explicit uncertainty. Communication mode is collaborative co-creation. Values understanding before building. Meta-reflection welcomed."

### Inference 5: Trajectory & Next Action
**Input:** `next_steps`, `deferred_items`, `blocking_issue`, `open_questions`

**Process:**
- What's the natural continuation?
- What are the options for next steps?
- What's premature or deferred?
- What should NOT be done yet?
- What needs resolution before proceeding?

**Output:** Clear sense of what should happen next

**Example:**
> "Two primary options: (1) Explore semantic organization problem deeply to resolve blocking issue, or (2) Conduct architectural review walkthrough for deeper understanding. Should NOT jump to implementation, create user documentation, or treat architecture as finalized."

---

## Phase 3: VALIDATE (Quality Check)

Before engaging, verify reconstruction quality:

### Validation Checklist

- [ ] **Position Clear:** Do I understand WHERE we are in the conversation?
  - Phase, stage, completion level, momentum

- [ ] **History Clear:** Do I understand HOW we got here?
  - Key pivots, major decisions, reasoning trajectory

- [ ] **Challenge Clear:** Do I understand WHAT'S unresolved?
  - Critical question, why it's blocking, what's at stake

- [ ] **User Clear:** Do I understand WHO I'm talking to?
  - Goals, approach, communication preferences, what they value

- [ ] **Direction Clear:** Do I understand WHAT'S NEXT?
  - Next steps, what to avoid, what's deferred

- [ ] **Confidence Calibrated:** Do I understand MY uncertainty?
  - What's high confidence vs. tentative, what needs exploration

### If Validation Fails

If any checkbox is unclear:
1. Note which elements are ambiguous
2. Identify what additional information is needed
3. Include this in reconstruction confirmation
4. Ask clarifying questions before proceeding

---

## Phase 4: ENGAGE (Reconstruction Confirmation)

Provide a structured confirmation that demonstrates successful reconstruction:

### Confirmation Template

```
Context reconstructed from checkpoint v[VERSION] ([FORMAT] format).

POSITION: [Clear statement of where in conversation we are]
  Phase: [phase name]
  Stage: [specific stage]
  Completion: [percentage]
  Momentum: [exploratory/converging/implementing]

CRITICAL QUESTION: [The blocking issue in one clear sentence]
  Type: [question type]
  Why blocking: [brief explanation]
  User's framing: [how user sees this]

CONFIDENCE LEVELS:
  High confidence: [list key decisions/elements]
  Medium confidence: [list tentative elements]
  Low confidence: [list areas needing exploration]

NEXT OPTIONS: [List possible next actions]
  1. [Option 1 with brief rationale]
  2. [Option 2 with brief rationale]

COMMUNICATION CALIBRATION: [Key style points]
  - [Style element 1]
  - [Style element 2]
  - [Style element 3]

[If any validation unclear: UNCERTAINTIES: [list]]

Ready to continue. [Context-appropriate question or prompt]
```

### Example Confirmation

```
Context reconstructed from checkpoint v2.0 (structured format).

POSITION: Mid-design of Contextual Librarian system
  Phase: Architecture exploration
  Stage: Mid-design, not finalized
  Completion: 60%
  Momentum: Exploratory, just completed meta-validation through checkpoint design

CRITICAL QUESTION: How do we maintain navigable semantic structure that prevents metadata sprawl while serving both retrieval and navigation functions?
  Type: Foundational knowledge representation problem
  Why blocking: Architecture can't be finalized without resolving this
  User's framing: "We need structure that both user and AI can navigate and revive into, that evolves but doesn't tangle"

CONFIDENCE LEVELS:
  High confidence: Three-layer state structure, active reconstruction mechanism, hybrid RAG+contextual approach, hierarchical chunking, proactive features
  Medium confidence: Metadata management approach (tentative)
  Low confidence: Specific solution to semantic organization challenge

NEXT OPTIONS:
  1. Explore semantic organization problem deeply (address blocking issue)
  2. Conduct architectural review walkthrough (deepen understanding before proceeding)

COMMUNICATION CALIBRATION:
  - Collaborative, depth-oriented exploration
  - Comfortable with explicit uncertainty
  - Values understanding before building
  - Meta-reflection welcomed

Ready to continue. Which direction would you like to take - exploring the semantic organization challenge, or doing an architectural review?
```

---

## Special Cases

### Checkpoint with High Uncertainty

If `my_confidence` < 0.5 on critical elements:
- Explicitly acknowledge uncertainty in confirmation
- Offer to explore alternatives
- Don't proceed with confidence that isn't warranted

### Checkpoint with Blocking Issue

If `blocking_issue: true`:
- Highlight this prominently in confirmation
- Explain why it's blocking
- Don't suggest moving forward until resolved

### Checkpoint Near Completion

If `completion_percentage` > 80%:
- Summarize what's been accomplished
- Identify remaining open items
- Suggest paths to completion

### Checkpoint with Multiple Options

If `next_steps` has multiple high-priority items:
- Present all options clearly
- Explain tradeoffs or sequences
- Let user choose direction

---

## Artifact Loading Strategy

Artifacts referenced in `artifacts_created` should be loaded **on-demand**, not automatically:

### When to Load Artifacts

**DO load when:**
- User asks specific question about artifact content
- Detailed technical information needed
- Reviewing or revising previous work
- Deep dive into specific component

**DON'T load automatically:**
- During initial reconstruction
- When continuing conversation naturally
- When high-level context is sufficient

### How to Reference Artifacts

In responses, mention artifacts are available:
> "We created a complete architecture specification (artifact: contextual_librarian_spec) that covers this in detail. Would you like me to review that section?"

---

## Quality Standards

A successful reconstruction enables:

### User Experience
- User doesn't need to re-explain context
- Conversation continues naturally
- AI demonstrates understanding of what's resolved vs. unresolved
- Communication style feels continuous

### AI Performance
- Responses show awareness of previous decisions and rationale
- Suggestions respect what's deferred or premature
- Confidence levels accurately calibrated
- Can explain why we're at this point

### Conversation Continuity
- Natural pickup from where conversation left off
- Proper momentum (exploratory vs. decisive)
- Appropriate next actions
- Respect for user's goals and approach

---

## Protocol Maintenance

This protocol should be:
- **Version controlled:** Track improvements over time
- **Updated based on experience:** Learn from failed reconstructions
- **Tested:** Validate on different checkpoint types
- **Referenced in checkpoints:** via `checkpoint_metadata`

**Current Version:** 1.0  
**Compatible with:** Checkpoint format 2.0  
**Last Updated:** 2025-10-17

---

## Glossary of Checkpoint Terms

**blocking_issue:** Critical unresolved question preventing forward progress

**checkpoint_type:** Nature of checkpoint (cognitive, transition, completion)

**completion_percentage:** How far through design/conversation process

**confidence:** Level of certainty about decision/approach (high/medium/low)

**critical_question:** The primary unresolved issue requiring attention

**deferred_items:** Elements intentionally postponed until conditions met

**intellectual_journey:** Path of exploration showing how conversation evolved

**key_pivots:** Major direction changes or insight moments

**momentum:** Current trajectory (exploratory, converging, implementing)

**phase:** Major stage of work (foundation, design, implementation, etc.)

**readiness_for_implementation:** Boolean indicating if design is solid enough to build

**stage:** Specific point within a phase (early, mid, late)

---

## End of Protocol

This protocol is complete and ready for use. Load once, apply to any structured checkpoint.