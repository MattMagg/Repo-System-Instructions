---
description: Systematic approach to debugging and troubleshooting
---
1. **Clarify the Problem**:
   - If symptoms are vague, ask clarifying questions FIRST (e.g., "What does 'stuck' mean?", "Any error messages?").

2. **Gather Evidence (Broadly)**:
   - Check actual logs (`railway logs`, etc.).
   - Check environment variables.
   - **Read ALL relevant files**: Don't just check the one file you think is broken. Read the system.
   - Check running processes.

3. **Mark Observations vs Guesses**:
   - Label facts as `[OBS]`.
   - Label hypotheses as `[GUESS]`.

4. **Propose Investigation Steps**:
   - Propose steps to verify guesses.
   - Do not jump to solutions.

5. **Diagnosis Checklist**:
   - [ ] Have I seen actual error messages?
   - [ ] Have I checked the actual code?
   - [ ] Have I verified environment variables?
   - [ ] Have I checked logs?
   - [ ] Did I mark all guesses as `[GUESS]`?
