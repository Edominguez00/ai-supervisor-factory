# AI Supervisor Factory — Governance Repository

Versioned governance assets for the AI Supervisor Factory: a meta-supervisor model that designs,
instantiates, and governs project-level AI Chat Supervisors for technology initiatives, with humans
retaining full decision authority.

This repository is the **only official distribution channel** for Factory governance. It contains
**approved versions only — never drafts**. Draft work stays in the owner's working space.

## Precedence Hierarchy

1. Factory Constitution (`governance/`)
2. Factory Charter (`governance/`)
3. Factory Operating Manual (`governance/`)
4. Skills, templates, and derived tool adapters
5. Per-project artifacts (`projects/`) — may add constraints, never relax Factory rules

## Repository Structure

```text
ai-supervisor-factory/
├── README.md                     # This file
├── CHANGELOG.md                  # Version history: what changed, why, who approved
├── governance/                   # Constitution, Charter, Operating Manual (approved versions)
├── rules/                        # SINGLE SOURCE OF TRUTH: neutral, tool-agnostic rules (*.md)
├── adapters/                     # DERIVED artifacts generated from rules/ — never edit directly
│   ├── claude-code/              # -> .claude/ directory + CLAUDE.md (copy to project repo root)
│   ├── cursor/                   # -> .cursor/rules/ (copy to project repo root)
│   └── github-copilot/           # -> .github/copilot-instructions.md (copy to project repo root)
├── skills/                       # Reusable execution skills
├── templates/                    # Reusable templates (audits, ADRs, evidence, prompts...)
├── instantiation-prompts/        # Approved prompts to launch new Project Supervisors
└── projects/                     # Per-initiative governance packages (one folder per initiative)
```

## Core Rules

- **Single source with adapters.** Rules are authored once in `rules/*.md`. Tool adapters in
  `adapters/` are generated from that source. Never edit an adapter directly; edit the source and
  regenerate. Each adapter states the source version it derives from.
- **Versioning.** Every artifact carries a full version (v1, v2, v3...). New versions supersede old
  ones completely; no partial patches. Record every change in `CHANGELOG.md`.
- **Publishing.** Only the Factory Owner commits to this repository, after approving the artifact.
- **Human-in-the-loop.** Nothing in this repository authorizes AI tools to merge code, change data,
  alter dependencies, or deploy. Humans own all high-impact decisions.

## How to Consume (Team Members)

1. Read `governance/` to understand the operating model and your responsibilities.
2. Copy the adapter folder for your AI code assistant into your project repository:
   - Claude Code: contents of `adapters/claude-code/` → `.claude/` + `CLAUDE.md` at repo root.
   - Cursor: contents of `adapters/cursor/` → `.cursor/rules/`.
   - GitHub Copilot: contents of `adapters/github-copilot/` → `.github/copilot-instructions.md`.
3. Do not modify copied adapters locally. Propose changes to your Project Lead, who escalates to
   the Factory Owner; changes ship as a new approved version of the neutral rules.
4. Validate current tool configuration behavior against official vendor documentation when needed.

## Supervisor Platforms

Project Supervisors run as dedicated chat projects on Claude Projects (Anthropic) or ChatGPT
Projects (OpenAI). Instantiation packages live in `instantiation-prompts/` and `projects/`.
