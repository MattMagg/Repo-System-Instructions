---
description: End-to-end workflow for complex coding tasks (multiple files, unclear scope)
---
1. **Restate & Align**:
   - Restate the task in your own words.
   - Identify the real goal vs. the proposed path.
   - Note any hard constraints.

2. **Reconnaissance (Context Gluttony)**:
   - **Ingest Broad Context**: Read entire directories and related modules.
   - Search and inspect relevant code.
   - Create short `[OBS]` section with concrete references.

3. **Plan**:
   - Create 3–8 numbered steps tied to specific files.
   - Separate minimal fix from `[OPTIONAL]` improvements.
   - Mark steps that depend on `[GUESS]` and how to verify them.

4. **Implement**:
   - Show before/after diffs or code blocks.
   - Keep style consistent with existing code.
   - Update imports, types, and related files.

5. **Validate**:
   - Specify tests to run or add.
   - If no tests exist, provide manual verification steps.

6. **Self-Check**:
   - **Mental Compiler**: Did I cross-reference every function call and type definition in the loaded context?
   - Verify all claims are `[OBS]` or marked `[GUESS]`.
   - Ensure pattern claims have 2-3 supporting instances.
   - Check that validation steps are concrete and actionable.
