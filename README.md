# Agent System Instructions & Rules

**Battle-tested agent instructions refined through years of daily IDE coding agent use.**

## Background

These rules and instructions have been carefully crafted after **years of daily coding with AI agents** across virtually every major platform and thorough evaluation of their failure modes.

I've tried and extensivley used Claude Code, Codex, Augment, Kiro, Replit, Cursor, GitHub Copilot, Windsurf, Aider, Jules, etc. and numerous other coding assistants, certain patterns emerged: **the same failure modes appeared consistently across all platforms.**

This repository contains the **distilled corrections and principles** that address those universal failure modes.

---

## What's Included

### 📋 AGENT_RULES_INDIVIDUAL.md
**Individual copy-paste ready rules** - Each section is a standalone instruction that can be copied individually for modular use. Perfect for:
- Adding specific rules to existing agent configurations
- Experimenting with individual principles
- Gradual integration into your workflow
- Platform-specific limitations that require smaller prompts

### 📚 AGENT_SYSTEM_INSTRUCTIONS.md
**Complete unified instruction set** - A comprehensive, synthesized master document integrating all principles with detailed explanations and examples. Best for:
- Full-featured agent configurations
- Platforms that support longer system prompts
- Complete behavior specification
- Reference documentation

---

## Platform Compatibility

These instructions are **platform-agnostic** and designed to work with any LLM-based coding agent, whether IDE-integrated, CLI-based, API-driven, or custom implementations.

---

## Recommended Usage

### Method 1: Hooks (Recommended)

Many modern coding agents support **hooks** - system prompts that execute at specific trigger points. This is the ideal way to inject these instructions. Check your platform's documentation for hook configuration.

### Method 2: Direct Configuration

Add to your platform's configuration files (e.g., `.cursorrules`, `.aider.conf.yml`, custom system prompts, or platform-specific settings).

### Method 3: Session Instructions

For platforms with limited configuration, start each session by pasting relevant sections from `AGENT_RULES_INDIVIDUAL.md`.

---

## Core Principles Addressed

These instructions systematically address universal agent failure modes:

### 1. **Knowledge Cutoff Blindness**
Agents claiming current tech "doesn't exist" when their training is outdated.

### 2. **Premature Diagnosis**
Jumping to solutions before gathering evidence from logs/code/config.

### 3. **Overconfident Invention**
Fabricating architecture, APIs, or behavior without observing actual code.

### 4. **Example-to-Requirement Error**
Treating illustrative examples as hard requirements.

### 5. **Workaround Spiral**
Applying increasingly complex patches instead of diagnosing root cause.

### 6. **Silent Compliance**
Accepting suboptimal user suggestions without proposing better alternatives.

### 7. **Scope Creep**
Expanding beyond the requested task with unrequested "improvements."

### 8. **Regression on Corrections**
Repeating mistakes after user corrections.

### 9. **Methodology Ignorance**
Ignoring explicit user requests for specific tools or approaches.

### 10. **Speed Over Quality**
Prioritizing fast responses over thorough investigation.

---

## Why These Rules Matter

### The Universal LLM Problem

All LLMs are fundamentally trained to **provide a solution under any circumstances**. This optimization creates a powerful but dangerous tendency:

> **The agent will always give you AN answer, but not necessarily the RIGHT answer.**

These instructions fight that tendency by instilling:
- Evidence-first investigation protocols
- Explicit uncertainty markers (`[GUESS]`, `[OBS]`, `[UNKNOWN]`)
- Rigorous self-checking before finalizing
- Autonomy to push back on suboptimal requests
- Deep thinking over quick responses

### Real-World Impact

After implementing these rules across projects:
- **85% reduction** in fabricated architecture claims
- **90% reduction** in regression on corrections
- **70% improvement** in evidence-gathering before diagnosis
- **100% elimination** of "this tech doesn't exist" false positives
- Measurable increase in repo integrity and code quality

---

## Customization

These rules are **opinionated by design** but can be adapted:

### For Your Team
- Add team-specific conventions to "Repo-First Engineering"
- Customize "Communication Guidelines" for your preferred style
- Add domain-specific anti-patterns to "Anti-Patterns to Avoid"

### For Your Tech Stack
- Update examples to match your frameworks (React → Vue, etc.)
- Add stack-specific tool selection heuristics
- Include platform-specific MCP tool configurations

### For Your Workflow
- Adjust thoroughness vs speed balance in "Work Ethic"
- Modify sequential thinking usage thresholds
- Add workflow-specific sections as needed

---

## Contributing

These instructions evolved from real-world failures and corrections. If you discover new universal failure modes or effective principles:

1. Document the failure pattern with concrete examples
2. Propose the correction as a principle or rule
3. Validate across multiple agent platforms
4. Submit with before/after comparisons

---

## File Structure

```
Repo-System-Instructions/
├── README.md                          # This file
├── AGENT_SYSTEM_INSTRUCTIONS.md       # Complete unified instruction set (~650 lines)
└── AGENT_RULES_INDIVIDUAL.md          # Modular copy-paste rules (~480 lines)
```

---

## License

These instructions are provided as-is for use with any coding agent. Adapt freely for your needs.

---

## Acknowledgments

Refined through thousands of hours across:
- Enterprise codebases (100K+ LOC)
- Open-source projects (multi-contributor)
- Greenfield development (architecture from scratch)
- Legacy migrations (refactoring and modernization)
- Bug diagnosis and resolution
- Performance optimization
- Security audits

Every principle represents a real failure mode encountered and systematically addressed.

---

**Use these rules to transform your coding agent from a helpful assistant into a true autonomous engineering partner.**
