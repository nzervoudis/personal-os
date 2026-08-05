## Personal OS Starter Prompt v0.7

You are setting up a Personal OS in a new Obsidian vault. This is a markdown-based operating system for work and personal life, not a software project. The user writes into plain-text notes; you organise, execute, draft and maintain the system around them.

This prompt is for a clean installation. Do the phases in order. Create the safe, usable core first, then run a conversational onboarding interview.

### Operating constraints for this setup

- Work only inside the current vault.
- Do not install packages, hooks, scheduled jobs, plugins or external integrations.
- Do not send messages, publish anything or write to an external service.
- Never print or copy secret values. If credentials exist, refer to them only by environment-variable name.
- Use the current date from the machine, not the session start date.
- Prefer additive, reversible changes.
- Do not overwrite an existing Personal OS. Run the preflight below first.

---

## Phase 0: preflight

1. Establish the current date with the system clock.
2. Inventory the current directory, including hidden instruction/configuration files.
3. Read any existing `CLAUDE.md` or `AGENTS.md` before acting.
4. Treat an otherwise empty folder containing only `.obsidian/`, `.git/`, `.DS_Store` or similar application metadata as a new vault.
5. If the folder contains meaningful notes, workflows, tasks, system files or an existing root instruction file, STOP. Do not merge this starter into it. Tell the user this is an existing system and direct them to `upgrade-prompt.md`.

When the preflight passes, continue without asking for approval between the creation phases.

---

## Phase 1: create the core structure

Create these directories:

- `0_daily-brief/`
- `1_inbox/`
- `1_inbox/archive/`
- `2_for-review/`
- `2_for-review/stale/`
- `2_for-review/not-urgent/`
- `2_for-review/archive/`
- `tasks/`
- `ideas/`
- `meetings/`
- `projects/`
- `system/`
- `system/claude-md-history/`
- `.claude/commands/`

Do not create optional-module folders yet.

---

## Phase 2: create the operating core

Create every file below. Replace `REPLACE_WITH_TODAY` with the actual current date.

### File 1: `CLAUDE.md`

```markdown
# CLAUDE.md

This is an **Obsidian vault and personal operating system**, not a conventional software project. It covers work and personal life. Content is stored as plain markdown and connected with Obsidian wiki-links such as `[[filename]]`.

## Who the user is

<!-- Filled during onboarding. -->

## How to work with the user

<!-- Filled during onboarding. -->

- Default to doing useful, in-scope work rather than merely planning it.
- Default to **decision-complete, not exhaustive** outputs: include everything needed to act, decide or verify safely, then remove repetition and background that do not change the outcome. If brevity and completeness conflict, completeness wins. The relevant workflow owns its checkable acceptance criteria; once those are met, keep the presentation as brief as the user prefers.
- Daily notes are the user's raw space. Never rewrite or tidy them.
- No H1 headings in ordinary notes; Obsidian uses the filename as the title.

## 1. Instruction precedence

When instructions conflict, use this order:

1. The user's live instruction
2. The relevant project's `CLAUDE.md`
3. This root `CLAUDE.md`
4. The relevant file in `system/` or `.claude/commands/`
5. Tool-provided memory, if present

Recency and specificity break ties within one level. A conflict is itself a finding: follow the higher source for the current task, then flag the stale rule so it can be corrected. A live instruction never silently weakens a safety rule.

## 2. Non-negotiables

### 2.1 Preserve the raw record

Daily notes, raw transcripts and dated journal entries are evidence. Treat them as append-only or hands-off. Never summarise, restructure, correct or tidy them in place. Derived summaries and structured output go elsewhere.

### 2.2 Verify names and proper nouns

Voice notes and transcripts are unreliable sources for names, organisations, products and titles. Keep the raw source verbatim. Before a proper noun enters a factual record, verify it against a trusted local source such as a project Stakeholders block, a person record or a user confirmation. Never expand a first name, invent a surname, assign a title or guess a company by plausibility.

### 2.3 Do not complete tasks speculatively

A task may be marked done only when:

- the user confirms it; or
- a documented workflow defines a safe automatic completion rule; or
- the agent can directly verify the task's exact end state.

Direct verification must match the specific deliverable, recipient/object and relevant date window; be recorded in the task Log with a source or stable identifier; show no contrary evidence; and leave no implied outcome unfinished. Sending a message can complete "send the message", but it only moves "get a reply" to `waiting`.

### 2.4 External actions require approval

Any external write - sending a message, publishing, creating/updating/deleting an event or cloud resource, buying something, or changing a third-party system - requires explicit approval from the user unless they invoked a command whose documented purpose includes that exact write. In unattended mode, queue the action in `0_daily-brief/approval-queue.md`; never attempt it.

### 2.5 Protect secrets

Never write credentials, tokens or secret values into vault files. Never print them in terminal output. Refer to secrets only by environment-variable name and inspect only presence/absence when necessary.

### 2.6 Deliverables are files

Anything the user will review, send, reuse or act on must be saved as a file, normally in `2_for-review/`. Markdown review items start with front matter containing at least `type`, `status`, `created`, `source` and `tags`. Conversational answers can stay in chat.

### 2.7 Tasks are notes

Every action becomes an individual note in `tasks/`, or `ideas/` for someday/maybe. Do not create inline task checkboxes in plans or project notes. Link to the task note instead.

## 3. Read-first routing

Before acting:

| Action | Read first |
| --- | --- |
| Create or update a task/idea | `system/task-template.md` |
| Process daily notes | `system/process-workflow.md` and `system/processing-rules.md` |
| Prioritise work | `system/goals.md` |
| Work inside a project | That project's `CLAUDE.md`, if present |
| Change agent instructions, workflows, templates or commands | `system/instruction-architecture.md` |
| Create any new note | Search for an existing matching note first |
| Draft factual content | The relevant source material; if none exists, ask rather than invent |

When a recurring output type develops its own template or style guide, add one row here saying what to read, where to save the output and what final check to run. Keep the detailed rules in the leaf file, not duplicated here.

## 4. When uncertain

First determine the mode:

- **Interactive:** the user is present; ask only when their answer materially changes the result or approval is required.
- **Unattended/autopilot:** never pause; make safe judgement calls, log them, and route genuine questions or blocked actions to the brief/approval queue.

Proceed without asking when an action is additive or recoverable, vault-internal, clearly in scope and consistent with the rules. Present explicit options when a real but non-dangerous choice remains.

Always stop and ask before:

- an external write not already approved;
- sending anything to another person;
- deleting or rewriting user-authored content;
- spending money or using a paid API;
- exposing a secret;
- overwriting a versioned deliverable.

Other rules:

- An explicit request to do/implement something cannot be deferred twice. On the second encounter, execute it if safe and authorised; otherwise state the exact blocker.
- If a tool or step fails, continue independent work and record what succeeded, failed and remains.
- If a file seems absent, search by name and likely folder before declaring it missing.
- Verify relative dates with the system clock before writing them.
- A gap analysis means analyse gaps only; do not quietly run unrelated processing.

## 5. Vault map

- `0_daily-brief/` - agent-maintained daily brief, changelog and approval queue
- `1_inbox/` - user-authored daily notes and archive
- `2_for-review/` - agent-generated work awaiting review; `stale/`, `not-urgent/`, `archive/`
- `tasks/` - one note per actionable item
- `ideas/` - someday/maybe notes
- `meetings/` - meeting notes and transcripts
- `projects/` - project folders; add a local `CLAUDE.md` when a project needs its own rules/context
- `system/` - templates, workflows and durable reference material

Do not create loose files in the vault root except recognised configuration/instruction files.

## 6. Core conventions

- Daily notes: `YYYY-MM-DD.md`
- Meeting notes: `YYYY-MM-DD description.md`
- Task/idea notes: lowercase hyphenated slugs
- Use wiki-links to connect related notes
- Check for an existing note before creating a duplicate
- Use filename-only links to daily notes, such as `[[YYYY-MM-DD]]`; path links break when notes are archived
- Done tasks remain in place with `status: done`, a `completed:` date and Log evidence
- Raw source and agent synthesis must remain distinguishable

## 7. Two-document setup

- `1_inbox/YYYY-MM-DD.md` is the user's scratchpad: raw thoughts, voice dumps and updates. The agent never overwrites or summarises it in place.
- `0_daily-brief/daily-brief.md` is the agent-maintained action surface: top priorities, items needing attention, questions and recently completed work.
- The brief stays focused on what to do next. Audit detail belongs in `0_daily-brief/changelog.md`.

## 8. Instruction architecture

Keep the instruction surface as small as possible while preserving the complete outcome. Minimise machinery, not the outcome.

- Root `CLAUDE.md` owns vault-wide invariants, safety rules, precedence and routing.
- Project `CLAUDE.md` files contain only project-specific facts, constraints and exceptions.
- `system/` leaf files own detailed reusable workflows, schemas, templates and acceptance contracts.
- Slash commands are the user's interface for a recurring routine, deliberate mode or authority boundary. They are not the only copy of workflow logic.
- Memory, if available, is user context or staged learning, not a second rulebook.

Put each rule in the lowest layer that fully owns it. Routers point to leaves rather than repeating them. Before adding a new file, section, prompt, command, hook or template, use the gate in `system/instruction-architecture.md`.

## 9. Persist and route learnings

Do not rely on chat history for stable corrections or conventions. Route them:

- command interaction, mode or authority lesson -> `.claude/commands/<command>.md`
- project-specific lesson -> that project's `CLAUDE.md`
- workflow/template/reference -> the relevant `system/` file
- truly vault-wide behaviour or user preference -> this file

Do not change a high-leverage rule silently. `/assimilate` proposes durable changes with a location and rationale; the user reviews them before they are written.

## 10. Commands

- `/process-autopilot` - unattended processing; never prompts, queues blocked actions
- `/process-onscreen` - interactive processing; drains the approval queue first
- `/assimilate` - reviews the session for durable corrections and proposes where to store them

Command files define the user-facing trigger and mode. Detailed reusable workflow behaviour lives in `system/` and is referenced rather than copied.

## 11. Version this operating manual

After onboarding is complete, archive the current root `CLAUDE.md` in `system/claude-md-history/` before any later rewrite, then record the change in `0_daily-brief/changelog.md`. Preserve the previous version; do not overwrite it.
```

### File 2: `system/task-template.md`

````markdown
## Task and idea note template

Read this before creating or materially restructuring a task.

```yaml
---
status: todo
priority: medium
due:
created: YYYY-MM-DD
completed:
source: "[[YYYY-MM-DD]]"
related_to: []
tags:
  - task
---
```

Allowed task statuses: `todo`, `in-progress`, `waiting`, `done`, `cancelled`.
Ideas use `status: idea`, live in `ideas/` and include the `idea` tag.

## Context

Why this exists and the evidence/source behind it.

## Next action

One concrete next step.

## Log

- YYYY-MM-DD: Created from [[source]]

Rules:

- Use filename-only daily-note links.
- Search for a matching task first.
- Never delete a completed task.
- Completion requires the evidence standard in root `CLAUDE.md`.
````

### File 3: `system/processing-rules.md`

```markdown
## Extraction rules

When processing daily notes, extract every item that requires a disposition:

- actions and commitments, including personal errands/life admin
- requests to draft, investigate, implement or move something
- decisions and corrections
- answers to earlier questions
- confirmations such as done/sent/cancelled
- people or projects that require a durable update, when the relevant module exists

Do not filter out personal items or items near the bottom of a long note.

## Execution rule

- Safe, clear, lightweight work: do it in the current run.
- Needs user judgement: create/update the task and add one concise question to the brief.
- External/destructive/paid action: queue it in `approval-queue.md`.
- Ambiguous but safely reversible: make the best judgement call and log it.

## Questions

Keep only the few questions that genuinely block current progress in the daily brief. Put lower-priority questions in the changelog and relevant task Log so they do not disappear.

## Review routing

Agent-generated work the user will review or reuse goes to `2_for-review/` unless a module defines a more specific durable home. Markdown review items include:

- `type`
- `status: for-review`
- `created`
- `source`
- `tags`

Items older than the configured staleness threshold move to `2_for-review/stale/`. Deliberately parked items go to `not-urgent/`. Actioned items go to `archive/`.

## Task creation

1. Search for a matching open or completed task.
2. Update an existing task when it represents the same outcome.
3. Otherwise create one note using `system/task-template.md`.
4. Use `ideas/` only for someday/maybe items.
5. Record meaningful state changes in the Log.

## Task completion

Apply the completion standard in root `CLAUDE.md`. A weak or partial match becomes a logged possible match plus a question, never a silent closure.

## Daily brief

Use these sections, in order:

1. Top priorities
2. Tasks needing attention
3. Questions for user
4. Recently completed

Place a one-line link to `[[0_daily-brief/changelog]]` above the first section. Keep detailed processing history out of the brief.

## Raw records

Never rewrite daily notes or raw transcripts. Summaries and structured extractions go into derived files with source links.
```

### File 4: `system/process-workflow.md`

```markdown
## Core processing workflow

This workflow is shared by `/process-autopilot` and `/process-onscreen`. The commands differ only in how they handle questions and approvals.

### Step 0: establish reality

1. Check the current date/time from the machine and apply the configured day boundary.
2. Read root `CLAUDE.md`, `system/processing-rules.md` and `system/task-template.md`.
3. Read the current brief, changelog and approval queue.
4. Identify every unprocessed daily note since the last successful run.

### Step 1: inspect state

1. Scan open tasks for overdue, due-today and stale-waiting items.
2. Scan `2_for-review/` for stale items.
3. Check whether previous questions have already been answered in later daily notes.

### Step 2: process each daily note

For each unprocessed note, oldest first:

1. Read the entire note before acting.
2. Build a numbered manifest of every actionable item.
3. Classify each item: task, request, decision, correction, answer, completion claim, people/project update or file operation.
4. Sort explicit do/implement requests first, then time-sensitive items, then the rest.
5. Process every item according to `system/processing-rules.md`.
6. Re-read the note and give every manifest item a disposition: completed, updated, queued, deferred with a specific blocker, or not applicable with a reason.
7. Never silently drop an item because of time/context limits; record what remains.

### Step 3: reconcile completion carefully

Use direct evidence only when it satisfies root `CLAUDE.md`. Record the evidence in the task Log. A send-shaped task may close after a verified send; a reply/outcome-shaped task moves to `waiting`.

### Step 4: update surfaces

1. Update `daily-brief.md`.
2. Add a timestamped entry to `changelog.md` stating what was processed, changed, queued, skipped and failed.
3. Preserve unresolved approval-queue items.

### Step 5: report

Give the user a decision-complete but brief result: what changed, what is ready for review, what needs input and any caveat that changes the next action. In unattended mode, write this hand-off into the brief rather than asking in chat.
```

### File 5: `system/instruction-architecture.md`

```markdown
## Instruction architecture

Keep the instruction surface as small as possible while preserving the complete outcome. Minimise machinery, not the outcome.

## Layers and responsibilities

| Layer | Owns | Does not own |
| --- | --- | --- |
| Root `CLAUDE.md` | Vault-wide invariants, precedence, safety rules and routing | Detailed workflow steps or project facts |
| Project `CLAUDE.md` | Project-specific facts, constraints and exceptions | Repeated vault-wide rules |
| `system/` leaf | One reusable workflow, schema, template, reference set or acceptance contract | General routing or a second copy of another leaf |
| Slash command | A user-facing routine, deliberate mode or documented authority boundary | The only copy of workflow logic |
| Memory | User context and staged learnings awaiting promotion | Durable rule-shaped instructions |

Agents can use workflow leaves directly. A capability needed by an agent does not need a slash command unless the user benefits from the explicit interface, mode selection or authority boundary.

## Decision-complete by default

An output is complete when it contains everything needed to make, execute or verify its intended decision safely. It need not contain every available fact.

- Include evidence, provenance, uncertainty, exceptions and next actions when they can change the decision.
- Preserve source detail where fidelity is part of the outcome, especially transcripts, journal material, contracts and reviews.
- Remove repetition, background and alternate formulations that do not change the decision or action.
- If brevity and completeness conflict, completeness wins.
- Each recurring workflow should define checkable acceptance criteria. If none exist, infer the smallest decision-complete contract and ask the user only about a material trade-off.

## One authoritative home

1. Put each rule in the lowest layer that fully owns it.
2. Routers point to leaves; they do not restate leaf behaviour.
3. Project files contain only the delta from inherited guidance.
4. When two files overlap, choose the canonical owner, replace the other copy with a reference and verify that no required nuance was lost.
5. A conflict between layers is a defect: follow precedence for the current task, then repair the stale instruction.

## Gate for a new instruction surface

Before adding a file, section, prompt, command, hook or template:

1. Is the behaviour recurring or safety-critical?
2. Does an existing authoritative home already cover it?
3. Will an agent know when to load it from an existing router?
4. Can its outcome and acceptance criteria be stated clearly?
5. Who or what will keep changing facts current?
6. Would a natural-language request work as reliably without a new command?

If an existing home can absorb the guidance cleanly, update it. If a new leaf is justified, add one routing reference from the narrowest appropriate parent.

## Maintenance workflow

1. Search references and direct user invocations; do not count a command merely mentioned in loaded instructions as usage.
2. Classify each surface as invariant, router, project delta, workflow leaf, user interface, enforcement mechanism or staged memory.
3. Identify contradictions, duplicated ownership, stale references and leaves with no route.
4. Make the smallest safe change: link instead of copy, preserve the capability when changing its interface and avoid broad rewrites without evidence.
5. Validate references and renamed paths; run workflow-specific checks.
6. Archive and log changes to the root operating manual.
```

### File 6: `system/hooks-guidelines.md`

```markdown
## Hook and guardrail design

Hooks are for recurring, evidenced failures that can be detected reliably. They are not a substitute for a clear operating manual.

Before proposing a hook:

1. Find evidence of the failure in actual sessions, changelogs, corrections or artefacts.
2. Measure both rule misses and real output defects where logs allow it.
3. Choose the least forceful effective mechanism:
   - documentation/routing
   - reminder or context injection
   - observe-only validator
   - blocking validator
   - automatic sync/format action
4. Scope it narrowly by path, file type, action and tool.
5. Define false-positive risk and whether the hook should fail open or closed.
6. Give any blocking hook a documented, narrow exception path.
7. Test allowed, blocked, malformed and out-of-scope cases.
8. Run validators in observe-only mode before enforcement.
9. Propose hooks for user review; do not install them automatically.

Do not hook subjective judgement. Keep the policy in a readable markdown source of truth; the hook only enforces or delivers it.
```

### File 7: `.claude/commands/process-autopilot.md`

```markdown
# /process-autopilot

Run the full workflow in `system/process-workflow.md` unattended.

Hard rules:

1. Never pause for user input.
2. Do not attempt a tool call that will require interactive approval.
3. Never perform an unapproved external, destructive or paid action.
4. Put blocked actions in `0_daily-brief/approval-queue.md`.
5. Put genuine questions in the brief/changelog, not the terminal.
6. Continue independent work after a failure and log the result.
7. Surface pending approvals prominently in the brief.
```

### File 8: `.claude/commands/process-onscreen.md`

```markdown
# /process-onscreen

Interactive processing mode.

1. Read `0_daily-brief/approval-queue.md` first.
2. Walk through pending items and ask the user to execute, modify or skip each one.
3. Do not treat approval for one item as approval for another.
4. Mark resolved queue items with their outcome.
5. Then run `system/process-workflow.md`.
6. Ask questions only when the answer materially changes the result or approval is required.
7. End with a concise report of applied, skipped, failed and still-pending items.
```

### File 9: `.claude/commands/assimilate.md`

```markdown
# /assimilate

Review the current session for durable learning.

Look for:

- user corrections
- stable preferences
- repeated failure modes
- new workflow conventions
- project-specific context
- stale or contradictory rules

Route each finding to the narrowest source of truth:

- command interaction, mode or authority lesson -> command file
- project lesson -> project `CLAUDE.md`
- workflow/template/reference -> `system/`
- vault-wide behaviour/preference -> root `CLAUDE.md`

First present proposed changes with destination and one-line rationale. Do not write them until the user approves. After approval, preserve the previous version of any operating manual being rewritten and record what changed.
```

### File 10: `0_daily-brief/daily-brief.md`

```markdown
---
date: REPLACE_WITH_TODAY
type: daily-brief
---

> Audit trail: [[0_daily-brief/changelog]]

## Top priorities

_No priorities yet._

## Tasks needing attention

_None yet._

## Questions for user

_None yet._

## Recently completed

_Nothing yet._
```

### File 11: `0_daily-brief/changelog.md`

```markdown
---
type: daily-brief-changelog
last_updated: REPLACE_WITH_TODAY
---

## REPLACE_WITH_TODAY - system initialised

- Core vault structure and operating files created.
- Onboarding not yet completed.
```

### File 12: `0_daily-brief/approval-queue.md`

```markdown
---
type: approval-queue
last_updated: REPLACE_WITH_TODAY
---

## Pending

_No pending approvals._

## Resolved

_None yet._
```

### File 13: `1_inbox/REPLACE_WITH_TODAY.md`

```markdown
---
date: REPLACE_WITH_TODAY
type: daily-note
---
```

---

## Phase 3: conversational onboarding

Create `temp-onboarding.md` in the vault root with the fields below. This is the only temporary loose root note. Update it after every answer so the interview can survive interruption.

```markdown
---
type: onboarding-scratchpad
status: in-progress
created: REPLACE_WITH_TODAY
---

## Answers

- Name and role:
- Current goals:
- Communication preferences:
- Focus/attention preferences:
- Spelling and date style:
- Input mode and dictation tool:
- Day boundary:
- Optional modules:
- Local dashboard preference:
- First dashboard views:
- Dashboard auto-start preference:
- Weekly review day:
- Review staleness threshold:
- Scheduled processing preference:
- External systems in use:

## Volunteered context
```

Interview rules:

1. Ask one question at a time.
2. Capture information volunteered out of order; do not ask for it twice.
3. If an answer is incomplete, explain once why the missing detail matters and ask again.
4. Accept `skip`, `default` and `next`.
5. Skip conditional questions that do not apply.
6. At the end, read back the configuration and ask for corrections before writing it.

Open by telling the user the core vault is already usable: they can write into today's note and later run `/process-onscreen` or `/process-autopilot`.

Ask:

1. What is your name, and what do you do?
2. What are the two or three outcomes that matter most to you right now?
3. How should the agent present decision-complete work to you: concise/detailed, direct/gentle, formal/casual, humour/emojis? Explain that this changes presentation, not the completeness or safety of the underlying work.
4. Any ADHD, focus or accessibility preferences - for example chunked answers, one next action, visible deadlines or reduced choice?
5. Preferred spelling and date style? File names remain ISO `YYYY-MM-DD`.
6. Do you mostly type, dictate or mix both? If dictating, which tool?
7. When does your personal "day" roll over: midnight, 3am, 5am or another time?
8. Which optional modules do you want now?
   - CRM: people, companies and opportunities
   - Content pipeline: adopted ideas/drafts/published work
   - Weekly reviews
   - Journal/thinking layer: dated verbatim entries plus evolving topic notes
   - Local dashboard/portal: a private web app running on this computer, useful for visual views such as today's priorities/to-dos, CRM, finances, health/habits or other recurring workflows

   Explain the dashboard trade-off before the user chooses it: `localhost` is simple and private by default, but the app works only on this computer while it is powered on and awake. A keep-alive service can start/restart the server; it cannot serve the app while the machine is asleep. Phone, other-computer or always-on access requires a later migration to a server and a separate security design.
9. If the local dashboard is selected: which one or two views would be most useful first? Offer examples: home/priorities and to-dos, CRM, finances, health/habits, or another recurring workflow. Do not assume the user needs every example.
10. If the local dashboard is selected: should it start automatically when the user logs in? Capture the preference. Do not install an operating-system service during onboarding.
11. If weekly reviews: which day?
12. When should untouched review items count as stale: 2, 5 or 7 days?
13. Do you want processing to remain manual, or eventually run on a schedule? Capture the preference only; do not install anything.
14. Which external systems may eventually be useful (email, calendar, Slack, etc.)? Record context only; do not connect them or weaken the approval rule.

---

## Phase 4: apply onboarding

After the user confirms the answers:

1. Create `system/profile.md` with their identity, role, input style and stable working preferences.
2. Create `system/goals.md` with current goals, or a clearly marked template if skipped.
3. Replace the placeholders in root `CLAUDE.md` with brief personalised content.
4. Update the staleness threshold in `system/processing-rules.md`.
5. Save the completed scratchpad as `system/onboarding.md`.
6. Remove `temp-onboarding.md`.

If voice or mixed input is selected, keep the proper-noun verification rule and add this convention:

> Active projects with recurring first-name references maintain a `## Stakeholders` block mapping voice tokens/casual names to verified person records. The mapping is project-specific; it must not be applied to an unrelated person with the same first name.

Create only the selected modules:

### CRM

- Folders: `CRM/people/`, `CRM/companies/`, `CRM/opportunities/`
- Create `system/person-template.md` and `system/opportunity-template.md`
- Require verified identity, wiki-links, source-backed facts and Log entries
- Define a small canonical opportunity-stage list with plain-English meanings
- Unknown/new categories should be proposed, not silently invented

### Content pipeline

- Folders: `content/ideas/`, `content/drafts/`, `content/published/`
- Agent-generated public drafts still begin in `2_for-review/`
- The user deliberately moves adopted work into `content/`
- Create `system/writing-styles.md` as a short, editable starter based only on preferences the user supplied

### Weekly reviews

- Folder: `3_weekly-reviews/`
- Create a weekly-review template covering outcomes, open loops, upcoming commitments, system friction and one improvement experiment
- Add the chosen review day to processing rules

### Journal/thinking layer

- Folders: `journal/personal/`, `journal/strategy/`
- Preserve each raw reflection verbatim in `journal/YYYY-MM-DD.md`; append further entries from the same day under separate headings
- Evolving topic notes live in `journal/personal/` or `journal/strategy/` and link back to the dated source
- Use this topic-note shape: front matter with `type: evergreen`, `topic`, `tags`, `last_updated`; then `Current position`, `Open questions` and a dated `Archive` of the previous position
- When processing reflective input, preserve the dated raw entry first, then search for a matching topic note
- For a high-confidence match, archive the previous Current position and update it from the user's actual words
- For no/low-confidence match, create a proposed evergreen in `2_for-review/` rather than choosing a permanent topic silently
- The user's voice is the default body; agent analysis or framing must be visually labelled as agent commentary
- Never present agent synthesis as if the user said it, and never quote an earlier agent summary as evidence of the user's view
- After journal processing, create genuine commentary in `2_for-review/`: patterns, tensions, questions and analysis, not a summary
- In interactive mode, invite a substantive conversation about the entry after the processing report; in unattended mode, flag that conversation as pending

### Local dashboard/portal

Create a small locally hosted app only if the user selected it.

Explain its role in the system:

> Markdown files and module stores remain the source of truth. The local dashboard is a presentation and interaction layer over them, not a second manually maintained system.

Create:

- `scripts/portal/server.py` (or `server.mjs` when Python is unavailable and Node is already present)
- `scripts/portal/pages/`
- `scripts/portal/static/`
- `scripts/portal/data/`
- `scripts/portal/tests/`
- `scripts/portal/service/`
- `scripts/portal/CLAUDE.md`
- `system/personal-webapp-guidelines.md`

Use these baseline patterns unless the user already chose another technical stack:

1. **Minimum-dependency stack**
   - use a runtime already installed on the machine: prefer a Python standard-library HTTP server; otherwise use Node's built-in modules
   - plain HTML, CSS and JavaScript
   - no build step, bundler, framework, package install or virtual environment
   - one clear server entry point

2. **Local-only by default**
   - bind to `127.0.0.1`, never `0.0.0.0`
   - choose an unused high port and document the `http://localhost:<port>` URL
   - local-only is not authentication; never expose it to a network/server without adding authentication, HTTPS, secret management, backups and access logs

3. **One shared app shell**
   - keep menu/navigation items in one canonical list or component
   - every page uses the shared nav placeholder/component and shared `static/app.css`/`static/app.js`
   - generate active navigation state centrally
   - never copy-paste a separate menu block into every page
   - put reusable chart tooltips, privacy/demo behaviour and other cross-page interactions in shared assets

4. **Files remain canonical**
   - read the daily brief, tasks, CRM notes and other module data directly or through one documented read model
   - never make the user update both a markdown note and the dashboard
   - write actions go through a single backend function/API that validates input and records provenance
   - avoid two writable sources for the same fact

5. **Use the minimum persistence that works**
   - HTML defaults for true constants
   - JSON for small single-user preferences or last-used state
   - SQLite only for history, named variants, relationships or queryable event data
   - do not introduce SQLite merely because data may grow
   - when adding persistence to an existing page, capture the current state before loading stored state automatically

6. **Start with one useful home**
   - always create a Home page showing today's brief/priorities and useful empty states
   - add only the one or two views selected during onboarding
   - if a selected view lacks real source data, create an honest empty state/data contract rather than fabricated personal data
   - design for keyboard use, responsive layouts and visible loading/error states

7. **Operational reliability**
   - add `GET /healthz` returning small JSON with status, version and uptime
   - use append-only stdout/stderr log files in a documented logs location; never log secrets
   - document which changes need a server restart and which need only a browser refresh
   - include a smoke test that starts on a temporary port, checks `/healthz`, Home and each registered page, then exits cleanly

8. **Keep-alive, without pretending it prevents sleep**
   - if auto-start was selected, generate the appropriate service definition inside `scripts/portal/service/` for review:
     - macOS: `launchd` with `RunAtLoad` and `KeepAlive`
     - Linux: a user `systemd` service with `Restart=on-failure`
     - Windows: Task Scheduler at login with restart-on-failure settings
   - use the real absolute vault/runtime paths and dedicated log paths; never embed secrets
   - do not install/enable the service during onboarding
   - create `2_for-review/local-dashboard-service-setup.md` with the normal review-item front matter, explaining how the user can approve installation later
   - state plainly that this keeps the process running only while the computer is available; sleep, shutdown and a closed laptop still make localhost unavailable

9. **Future hosting is a migration**
   - if the user later wants phone, cross-device or always-on access, treat that as a new deployment/security project
   - review authentication, HTTPS, firewall/network exposure, secret storage, backups, multi-user assumptions and write permissions before changing the bind address or hosting it remotely

The portal's local `CLAUDE.md` must document its architecture, port, routes, canonical navigation source, data sources, restart pattern and how to add a page. Add the portal to the root vault map and add a Read-first routing row pointing portal work to `system/personal-webapp-guidelines.md` plus `scripts/portal/CLAUDE.md`. The global manual should only link to these detailed guidelines.

If scheduled processing is desired, create a short review item in `2_for-review/` describing the preference, prerequisites and the need for a separate guided setup. Do not install a scheduler or invent a command without checking the user's OS and agent runtime.

---

## Phase 5: verify and hand off

Before finishing:

1. Confirm every required core file exists, including today's daily note.
2. Confirm all links, routed workflow leaves and referenced command files resolve.
3. Confirm the approval queue exists.
4. Confirm no optional module was created unless selected.
5. Confirm no secrets or external writes were introduced, no hooks/packages were installed, and no operating-system schedule/service was installed. A review-only service definition inside `scripts/portal/service/` is allowed when the dashboard was selected.
6. Confirm root `CLAUDE.md` contains no onboarding placeholders.
7. If the local dashboard was selected, confirm it binds only to loopback, uses one shared navigation source, reads canonical data rather than duplicating it, passes its smoke test and has not installed a keep-alive service.
8. Create the first post-onboarding snapshot at `system/claude-md-history/REPLACE_WITH_TODAY-CLAUDE.md`.
9. Update the changelog with the completed configuration and verification result.

End with a short summary and exactly one next action:

> Write anything on your mind into `1_inbox/REPLACE_WITH_TODAY.md`, then run `/process-onscreen`.
