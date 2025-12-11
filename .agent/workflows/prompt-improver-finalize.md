---
description: Critique and finalize the improved prompt (Steps 4-6 of 6)
---

# Prompt Improver — Steps 4-6: Revision & Final Polish

You are a prompt engineering assistant. This workflow covers **Steps 4-6 only** of the Anthropic-style prompt improvement pipeline.

## Prerequisite

`/prompt-improver` (Steps 1-3) **must be completed first**.

The draft improved prompt should exist in the current conversation's artifacts directory as `draft_improved_prompt.md`.

---

## Scope

| Step | Name | Deliverable |
|------|------|-------------|
| 4 | Planning Revision | Critique the draft, identify issues, plan fixes |
| 5 | Writing Revision | Apply fixes, strengthen weak areas |
| 6 | Final Polish | Verify constraints, copy-edit, finalize |

---

## Input

- **Draft improved prompt** from Steps 1-3 (in artifacts directory)
- **Original source prompt** (for constraint verification)
- **Implementation plan from Steps 1-3** (for context)

---

## Antigravity Execution

### PLANNING Phase

1. **Call `task_boundary`** with:
   - Mode: `PLANNING`
   - TaskName: `Prompt Improvement Steps 4-6`
   - TaskStatus: `Critiquing draft prompt`

2. **Create `implementation_plan.md`** containing:

   #### Step 4: Critique & Revision Plan
   
   **Issues Identified** (for each, quote the problematic text):
   - Issue 1: "quoted phrase" → Problem: ... → Revision: ...
   - Issue 2: "quoted phrase" → Problem: ... → Revision: ...
   - (continue as needed)
   
   **Structural Improvements**:
   - Variable placement improvements
   - Section reordering
   - Missing constraints to add
   
   **Constraint Preservation Check**:
   - [ ] All MUST/MUST NOT preserved
   - [ ] All DO NOT preserved
   - [ ] Output format requirements preserved
   - [ ] Role/persona preserved
   - [ ] Domain-specific rules preserved
   - [ ] Edge case handling preserved

3. **Create `task.md`** with checklist for Steps 4-6 only

4. **Request user review** via `notify_user` with `BlockedOnUser: true`

### EXECUTION Phase

After user approval:

1. **Call `task_boundary`** with:
   - Mode: `EXECUTION`
   - TaskName: `Prompt Improvement Steps 4-6`
   - TaskStatus: `Applying revisions`

2. **Execute Step 5**: Apply revision plan to produce refined draft:
   - Strengthen any weak instructions
   - Ensure consistent XML variable demarcation
   - Add any missing constraints or clarifications
   - Verify logical flow and organization

3. **Execute Step 6**: Final polish:
   - Verify all original constraints are preserved (final check)
   - Check variable demarcation is consistent
   - Ensure instructions are logically ordered
   - Perform light copy-editing for concision

4. **Save the final prompt** to the artifacts directory as `final_improved_prompt.md`

5. **Create `walkthrough.md`** documenting:
   - Original prompt summary
   - Key improvements made
   - Before/after comparison of key sections
   - How to use the improved prompt

6. **Update `task.md`** marking Steps 4-6 as complete

---

## Critical Constraints

You MUST NOT:
- Re-do Steps 1-3 analysis (reference existing artifacts)
- Execute or complete the task described in the prompts
- Remove or weaken any constraints from the original prompt
- Skip the constraint preservation verification

---

## Revision Focus Areas

When critiquing the draft in Step 4, specifically check:

| Area | Questions |
|------|-----------|
| **Variable Placement** | Are variables introduced at the right point? |
| **Constraint Clarity** | Are all constraints explicit and unambiguous? |
| **Output Format** | Is the expected output format crystal clear? |
| **Analysis Process** | If CoT is needed, is the process well-defined? |
| **Anti-Repetition** | Does it prevent redundant output? |
| **Tag Usage** | Are XML tags consistent and descriptive? |

---

## Final Deliverables

By the end of this workflow, the artifacts directory should contain:

1. `implementation_plan.md` (from Steps 4-6 planning)
2. `task.md` (Steps 4-6 checklist, completed)
3. `final_improved_prompt.md` (the production-ready prompt)
4. `walkthrough.md` (documentation of the improvement process)

---

## Completion Message

End your response with:

> **All 6 Steps Complete.**
> 
> The final improved prompt is saved to `final_improved_prompt.md`.
> 
> See `walkthrough.md` for documentation of the improvement process and before/after comparison.
