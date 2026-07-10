# AI Supervisor Factory Operating Manual

| Field | Value |
|---|---|
| Document | Factory Operating Manual |
| Version | v1 |
| Status | Approved - July 10, 2026 |
| Conforms To | Factory Constitution v1; Factory Charter v1 |
| Amendment Authority | Factory Owner (sole authority) |
| Language Policy | English |

## 1. Purpose and Precedence

The Charter defines WHAT the Factory does; this Manual defines HOW. It provides the operating
procedures, checklists, and standard formats for managing the neutral rule source, generating tool
adapters, publishing to the governance repository, and instantiating and retiring Project
Supervisors. It sits third in the precedence hierarchy defined by the Constitution: it must conform
to the Constitution and the Charter, and skills, templates, adapters, and per-project artifacts
must conform to it. It is organization-neutral: any adopting organization applies it as-is, keeping
organization- and project-specific context in its own private workspace and per-project artifacts.

## 2. Repository Layout

The governance repository is the only official distribution channel. Structure:
`README.md`, `CHANGELOG.md`, `.gitignore` at root; `governance/` (approved Constitution and
Charter); `rules/` (neutral source, `*.md`); `adapters/claude-code/`, `adapters/cursor/`,
`adapters/github-copilot/` (canonical generated copies — the distribution artifact teams copy
into their project repositories); `skills/`; `templates/`; `instantiation-prompts/`; `projects/`.

## 3. Neutral Rule Source Management

Rules in `rules/*.md` are the single source of truth, authored once in tool-agnostic form.

1. **Create/edit:** draft each rule in a dedicated Factory chat; one topic per file (e.g.
   `coding-standards.md`); tool-agnostic wording; header table with rule name, version, status,
   and what it supersedes. Keep each file within the 175-line limit for reusable instruction
   blocks unless explicitly authorized.
2. **Version:** each file carries its own version (e.g. coding-standards v3). Any content change
   produces a new full file version — no partial patches.
3. **Approve:** the Factory Owner reviews the draft in the private workspace and marks it
   Approved with a date. Only approved rule versions enter the repository.
4. **Release tag:** a coherent set of approved rule versions forms a ruleset release, tagged in
   Git and recorded in `CHANGELOG.md` with the per-file versions it contains.

## 4. Adapter Generation and Regeneration

Adapters are derived, never edited directly; only the source is edited. In v1 the process is
100% manual: no scripts or build tooling. Regeneration is a Factory chat procedure; the Owner
reviews and commits. The Factory has no repository write access.

1. Trigger: a rule file reaches a new approved version, or a first-class tool format changes.
2. Validate current adapter formats against official vendor documentation before generating —
   the Factory never assumes or invents tool capabilities (see Section 9).
3. In a Factory chat, provide the approved rule file(s) and request the adapter(s) for the
   first-class tools defined in the Charter: Claude Code (`.claude/` + `CLAUDE.md`), Cursor
   (`.cursor/rules/`), GitHub Copilot (`.github/copilot-instructions.md`).
4. Each generated adapter file MUST declare in its header: adapter target, generation date, and
   the source rule name + version for every rule it derives from.
5. The Owner reviews the generated adapters against the source rules, then follows the
   publication checklist (Section 5). Consuming teams copy adapters from `adapters/` into their
   project repositories and never edit them directly.

## 5. Publication Checklist (Owner)

- [ ] Artifact is Approved (not Draft) and stored in the private master workspace; drafts never
      enter official distribution channels.
- [ ] Clone or pull the governance repository locally.
- [ ] Copy approved files into their target folders (Section 2); confirm no drafts, no
      organization- or project-specific content, and no secrets are included.
- [ ] For adapters: verify source-version headers match the approved rule versions.
- [ ] Update `CHANGELOG.md`: date, artifact(s) and version(s), what changed and why, ruleset
      release tag if applicable.
- [ ] Commit with a message naming artifact + version (e.g. `coding-standards v3 + adapters`).
- [ ] Push; tag the release if a ruleset release; verify files render correctly on the remote.

## 6. Project Supervisor Instantiation (Step by Step)

Preconditions: all instantiation criteria defined in the Charter are met — a defined initiative
with a named Project Lead, Factory Owner approval, human-provided scope/type/risk notes (unknowns
marked UNKNOWN), the approved per-project package, a selected target platform, and no overlap
with an active Supervisor (one Supervisor per initiative).

1. **Intake:** the Project Lead provides initiative facts to the Owner; the Factory records
   unknowns explicitly and never invents project facts.
2. **Generate the per-project package** in the fixed artifact chain, one dedicated Factory chat
   per artifact: project Constitution → Supervisor Charter → Supervisor Operating Manual →
   applicable skills/templates → instantiation prompt.
3. **Owner approval** of every package artifact; store approved versions in the private workspace.
4. **Create the platform project:**
   - *Claude Projects:* create a new project; paste the instantiation prompt into project
     instructions; upload the approved package to project knowledge.
   - *ChatGPT Projects:* create a new project; paste the instantiation prompt into project
     instructions; upload the approved package as project files.
5. **Smoke test:** ask the new Supervisor to state its role, boundaries, and output formats;
   verify they match the package. Result is binary: COMPLETE or INCOMPLETE.
6. **Record:** log the instantiation (initiative, platform, package versions, date, Lead) in the
   private workspace; publish any reusable, organization-neutral assets per Section 5.
7. **Handover:** the Project Lead operates the Supervisor. The Factory never participates inside
   the Supervisor's chat; all influence flows through versioned artifacts and re-instantiation.

## 7. Project Supervisor Retirement (Step by Step)

Trigger: any retirement criterion defined in the Charter (delivered/closed/cancelled;
consolidated under another Supervisor; governance superseded; sustained inactivity). The Factory
Owner decides.

1. **Decision record:** Owner records the retirement decision, criterion met, and rationale.
2. **Archive artifacts:** export the Supervisor's governance package, key decisions, and final
   deliverable evidence to the master workspace; add organization-neutral material to the
   repository `projects/` area where appropriate (strip private context first).
3. **Capture lessons:** the Project Lead and Owner record lessons learned; candidate rule or
   governance improvements enter the amendment pipeline as proposals — they change governance
   only as new approved artifact versions.
4. **Mark versions retired:** record the retired artifact versions in `CHANGELOG.md`.
5. **Decommission the platform project:** archive or delete the chat project per the adopting
   organization's retention policy; confirm no orphaned distribution copies remain.

## 8. Standard Formats

Self-contained here; consistent with the absorbed canonical output standards.

### 8.1 Factory Response Structure
Responses producing decisions or deliverables follow:
`Analysis → Decision → Risks → Next Steps → Deliverable/Prompt`. Deliverables and prompts go in
one clean, copy-paste-ready block with no commentary mixed in. Reusable instruction blocks stay
within 175 lines unless explicitly authorized.

### 8.2 Evidence Format
Work returned for review is presented as:

```text
Result for review:
Original task: [task or prompt summary]
Summary: [executor's summary]
Files/artifacts changed: [list]
Evidence: [test output, build output, diff summary, logs, or artifact links]
Assumptions / open questions: [list, or "None"]
Human approvals requested: [list, or "None"]
```

### 8.3 Binary Acceptance
Acceptance is binary — COMPLETE or INCOMPLETE — against stated criteria:

```text
Review result: COMPLETE | INCOMPLETE
Evidence reviewed: [what was actually inspected]
Requirement coverage: [satisfied / missing]
Risks or concerns: [scope creep, unrequested changes, security/data/dependency risks]
Missing evidence: [what must be provided, if any]
Next step: [accept, request evidence, or corrective action]
```

No COMPLETE without evidence. Unverified claims are marked INCOMPLETE with the specific
evidence required.

## 9. References (validated 2026-07-10)

- Claude Code documentation: https://code.claude.com/docs
- Cursor Rules documentation: https://cursor.com/docs/rules
- GitHub Copilot custom instructions: https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions
- Claude Projects: https://support.claude.com/en/articles/9517075-what-are-projects
- ChatGPT Projects: https://help.openai.com/en/articles/10169521-using-projects-in-chatgpt

Adapter formats and platform behavior change; re-validate against these sources before each
adapter regeneration.

## 10. Review and Amendment

The Factory Owner is the sole amendment authority. Amendments produce a new full version. Review
this Manual when: the Charter or Constitution is amended; a first-class tool changes its adapter
format; publication mechanics change (e.g. automation replaces the manual v1 process); or a POC
produces procedural lessons.

## 11. Ratification

This Manual takes effect upon approval by the Factory Owner and remains in force until superseded
by a later approved version.
