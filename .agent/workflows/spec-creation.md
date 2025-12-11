---
description: Create comprehensive, execution-ready specification documentation for any given topic
---

# Specification Creation Workflow

## Objective

Create specification documentation for this repo that enables **any agent with no prior context** to execute the implementation flawlessly, without bugs or ambiguity.

The user's request for the spec topic is provided below these instructions.

---

## Execution Phases

### Phase 1: Research

Research the topic using MCP tools to gather official documentation and best practices. Analyze this repo to understand relevant integration points and current patterns.

### Phase 2: Specification Authoring

Create a spec folder at `docs/<topic-kebab-case>-spec/` containing:

- **[GEMINI.md]** as the entry point (autoloaded by agents entering the folder) — should provide overview and index to other documents
- Additional documents as needed based on topic complexity

Structure and name documents however makes sense for the topic. Use your judgment on scope and depth.

### Phase 3: Quality Assurance

Before finalizing, verify against these checklists:

**Zero-Ambiguity Checklist**:
- [ ] Every step has exact commands or code samples
- [ ] No "you could" or "consider" language—only definitive instructions
- [ ] All file paths are absolute or relative to project root
- [ ] All dependencies and prerequisites explicitly listed with versions
- [ ] All configuration values have specific examples
- [ ] Error handling and rollback procedures documented for critical steps

**Execution-Ready Checklist**:
- [ ] An agent with no prior context can follow without clarification
- [ ] All code samples are complete and copy-paste ready
- [ ] All external references have direct URLs
- [ ] Success criteria are measurable and specific

---

## Output Format

Specification documents should use:
- Clear markdown headers
- Code blocks with language tags
- Tables for structured comparisons
- Diagrams where they clarify architecture or flow
- Cross-links between related documents