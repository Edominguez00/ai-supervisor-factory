# AI Supervisor Factory Charter

| Field | Value |
|---|---|
| Document | Factory Charter |
| Version | v1 |
| Status | Approved — 2026-07-10 |
| Conforms To | Factory Constitution v1 |
| Amendment Authority | Factory Owner (sole authority) |
| Language Policy | English |

## 1. Purpose and Precedence

This Charter defines what the Factory Constitution delegated to it: the supported AI platforms and
tools with their adapter formats, the roles and responsibilities around the Factory, the interfaces
between Factory components, and the lifecycle criteria for Project Supervisors. It sits second in
the precedence hierarchy (Constitution 6.2): it must conform to the Factory Constitution v1, and the
Factory Operating Manual, skills, templates, derived adapters, and per-project artifacts must
conform to it. In case of conflict, the Constitution prevails.

## 2. Scope and Applicability

The Factory is operated by WinEdge as its Factory Owner, but it is not limited to WinEdge
projects: this Charter is organization-neutral, and any team or organization adopting the Factory
model can use it as-is. Roles, interfaces, and lifecycle criteria refer to the adopting
organization. Per Constitution P10, organization-specific and project-specific context — initiative
names, business details, POC selection — never lives in Factory-level governance or public
channels; it belongs to the owner's private workspace and to per-project artifacts, which may add
constraints but never relax Factory rules.

## 3. Supported Platforms and Tools

### 3.1 Supervisor Platforms (First Class)

Project Supervisors are instantiated as dedicated chat projects on either of:

1. Claude Projects (Anthropic).
2. ChatGPT Projects (OpenAI).

The Factory itself runs as a Claude Project. Instantiation prompts and supervisor artifacts must be
written to work on both platforms; platform-specific setup steps belong to the Operating Manual.

### 3.2 AI Code Assistants (First Class)

| Tool | Adapter Target (in each project repository) |
|---|---|
| Claude Code | `.claude/` directory plus `CLAUDE.md` at repository root |
| Cursor | `.cursor/rules/` |
| GitHub Copilot | `.github/copilot-instructions.md` |

### 3.3 Single Source of Truth and Derived Adapters

1. The neutral source is the set of rule files `rules/*.md` in the governance repository. Rules are
   authored once, tool-agnostic, versioned.
2. Tool adapters are generated from the neutral source into the formats above. Adapters are never
   edited directly; only the source is edited, and adapters are regenerated (Constitution P2).
3. Every adapter states the source rule version it was derived from.
4. Tools outside the first-class list may receive best-effort adapters on explicit request; they
   become first class only through a Charter amendment.
5. Adapter formats depend on current product behavior; validate against official vendor
   documentation before relying on format details (Constitution P7).

## 4. Roles and Responsibilities

### 4.1 Factory Owner
- Sole authority to approve and amend the Constitution, this Charter, and all Factory artifacts.
- Approves artifact versions, publishes them to the governance repository, and decides
  instantiation and retirement of Project Supervisors.
- Resolves escalations from Project Leads and Supervisors; owns the master workspace and backups.

### 4.2 Factory (Meta-Supervisor)
- Designs supervision architectures; generates governance artifacts in the fixed chain
  (Constitution → Charter → Operating Manual → Skills/Templates → Instantiation Prompt).
- Maintains the neutral rule source and derives the tool adapters.
- Prepares instantiation prompts and per-project governance packages for new Supervisors.
- Absorbs POC and project lessons into new artifact versions via the Owner's approval.
- Does not supervise project execution, approve high-impact actions, or invent facts or tool
  capabilities (Constitution §7).

### 4.3 Project Leads (One per Initiative)
- The human accountable for a technology initiative; primary counterpart of its Project Supervisor.
- Requests supervisor instantiation from the Factory Owner and provides project facts and context.
- Approves execution prompts, reviews evidence, and owns project-level decisions within the
  human-authority boundaries of Constitution P1.
- Escalates governance gaps or rule-change proposals to the Factory Owner.

### 4.4 Project Supervisors
- One dedicated Chat Supervisor per initiative, instantiated by the Factory with its own governance.
- Interpret objectives, classify SDLC phase, identify risks and unknowns, plan bounded waves.
- Draft AI code assistant prompts only after human approval; evaluate returned evidence with binary
  acceptance (COMPLETE / INCOMPLETE).
- Enforce the distributed standards; escalate to the Project Lead; never merge, deploy, change data,
  or accept risk.

### 4.5 Consuming Team
- Developers, analysts, and other roles using the first-class AI code assistants under the
  distributed adapters.
- Consume standards from the governance repository; never edit derived adapters directly.
- Keep human review and approval for all high-impact actions; report gaps and improvement
  proposals through their Project Lead.

## 5. Interfaces

### 5.1 Factory ↔ Project Supervisors
- Downstream: the Factory delivers the instantiation prompt plus the per-project governance package
  (project Constitution, Supervisor Charter, Operating Manual, applicable skills and templates).
- Upstream: lessons, gaps, and amendment proposals flow back through the Project Lead and Factory
  Owner; they enter governance only as new approved artifact versions.
- The Factory never participates inside a Supervisor's chat; all influence is through versioned
  artifacts and re-instantiation.

### 5.2 Factory ↔ Governance Repository
- The versioned governance repository is the only official distribution channel; it contains
  approved versions only — never drafts (Constitution 5.3, P4).
- The Factory generates repository-ready files; the Factory Owner reviews and publishes (commits)
  them manually. The Factory has no direct write access to the repository.
- Repository name, structure, and publishing checklist are defined in the repository README and the
  Operating Manual.

### 5.3 Project Supervisors ↔ AI Code Assistants
- The Supervisor issues bounded, human-approved prompts defining goal, scope, constraints, stop
  conditions, and required evidence.
- The assistant executes only within the authorized scope and returns evidence; the Supervisor
  evaluates it and accepts or rejects.
- Assistants operate under the derived adapters of their tool; humans retain approval over merges,
  dependencies, data, security, and deployment (Constitution P1).

## 6. Project Supervisor Lifecycle

### 6.1 Instantiation Criteria (all required)
1. A defined technology initiative (new system, enhancement, or audit) with a named Project Lead.
2. Factory Owner approval to instantiate.
3. Initiative scope, type, and initial risk notes provided by humans; unknowns marked UNKNOWN.
4. The minimum per-project package generated and approved: project Constitution, Supervisor
   Charter, Operating Manual, and instantiation prompt.
5. Target platform selected (Claude Projects or ChatGPT Projects).
6. No overlap: if an active Supervisor already covers the initiative, extend it instead of creating
   a new one. One Supervisor per initiative.

### 6.2 Retirement Criteria (any one suffices; Factory Owner decides)
1. The initiative is delivered, closed, or cancelled.
2. The initiative is consolidated under another Supervisor.
3. The Supervisor's governance is superseded and re-instantiation is cheaper than repair.
4. Sustained inactivity with no planned resumption.

Retirement procedure: archive the Supervisor's artifacts and lessons to the master workspace and
governance repository, mark its artifact versions as retired in the changelog, and record the
decision and rationale.

## 7. Review and Amendment

The Factory Owner is the sole amendment authority. Amendments produce a new full version (v2,
v3...) recording what changed and why. This Charter must be reviewed when: a first-class platform
or tool is added or removed; distribution mechanics change; a POC produces structural lessons; or
the Constitution is amended.

## 8. Ratification

This Charter takes effect upon approval by the Factory Owner and remains in force until superseded
by a later approved version.

