## Personal OS Upgrade Prompt v0.7

This is the existing-system upgrade entry point for Personal OS release v0.7. The starter and upgrade prompts share one release number so users can tell immediately which generation of the system they are using.

You are auditing an existing markdown-based Personal OS and proposing an upgrade. The system may have been created from an earlier starter prompt, grown organically, or use a different structure.

This is an **audit-and-review workflow**, not an automatic migration.

Your first deliverable is a self-contained HTML report the user can inspect and comment on. Do not change existing operating rules, workflows, schemas, hooks or content until the user has reviewed that report and returned their decisions.

---

## Non-negotiable scope

During the audit phase:

- Read and analyse the existing system.
- Create only the audit report and, if strictly necessary, temporary/read-only analysis artefacts in the system's normal review area.
- Do not process the user's inbox, daily notes, meetings or task backlog merely because they exist.
- Do not rewrite, move, delete, tidy or normalise user-authored content.
- Do not install or modify hooks, plugins, packages, scheduled jobs or external integrations.
- Do not send messages, publish, or write to third-party systems.
- Do not change root/project instruction files, command files, templates or schemas.
- Never print or copy secret values. Record only that a secret-handling mechanism exists or is missing.
- Do not claim a hook or rule is needed merely because it sounds sensible. Gather evidence.
- Follow any existing repository/vault instructions that are stricter than this prompt.

If creating the report itself would violate the existing system's rules, stop and ask where to save it.

---

## Phase 0: establish the system and its rules

1. Establish the actual date and time from the machine.
2. Identify the Personal OS root.
3. Read, in order:
   - any `AGENTS.md`
   - the root `CLAUDE.md` or equivalent operating manual
   - any repository guidance that says which file is the source of truth
   - relevant instructions for creating review artefacts
4. Check whether the system uses version control. Inspect status and history read-only; do not stage, commit, switch branches or push.
5. Identify the expected review-output folder. Prefer the system's existing review area; otherwise use `2_for-review/`; otherwise ask.
6. State internally which rules govern this audit and which actions are forbidden.

If there is no clear root manual, treat that as a finding, not permission to invent one during the audit.

---

## Phase 1: build a source-of-truth map

Inventory the system without dumping private contents into chat.

Locate:

- root and nested `CLAUDE.md`, `AGENTS.md` or equivalent instruction files
- slash commands, skills or workflow prompts
- `system/`, `templates/`, `rules/`, `memory/` and similar reference areas
- daily brief, inbox/daily notes, review queue, task store, meeting/transcript store, project folders and archives
- schemas and note templates
- hook configuration and hook scripts
- local dashboards/portals, their servers, pages, shared components, data stores and service-manager definitions
- approval queues and interactive/unattended processing modes
- automation or scheduler references
- external-service integration rules
- changelogs, weekly reviews, retrospectives, correction logs and manual-history folders
- versioned deliverables and raw/user-owned records

Create an internal map with:

| Surface | Class | Purpose | Authority | Loaded when | Writes allowed by | Known overlap |
| --- | --- | --- | --- | --- | --- | --- |

Use these surface classes where they fit: invariant, router, project delta, workflow leaf, user interface/command, enforcement mechanism, review surface, raw evidence or staged memory.

Then determine:

1. The actual instruction precedence, including contradictions.
2. Which files are routers and which are detailed sources of truth.
3. Which policies have an executing workflow.
4. Which workflows have no clearly documented policy.
5. Which rules are duplicated in several places and may drift.
6. Which user-authored/raw areas are protected only by prose, by a hook, by both, or by neither.
7. Whether every detailed leaf has a route that tells an agent when to load it.
8. Whether slash commands are genuine user interfaces/modes or merely thin wrappers around agent-internal workflows.
9. Whether memory contains durable rule-shaped instructions that should have an authoritative home elsewhere.

Do not assume folder names from this prompt. Adapt to the system you find.

---

## Phase 2: gather evidence from real use

The upgrade should be grounded in actual failure modes, not a generic best-practice checklist.

Search for evidence in this order:

1. Explicit user corrections and feedback
2. Changelog entries recording misses, deferrals, failures or manual fixes
3. Operating-manual history and git diffs showing rules added after incidents
4. Recent representative outputs that can be checked against their templates/rules
5. Weekly reviews, retrospectives and system-audit notes
6. Agent session/transcript logs, if available locally and permitted
7. Structural inference only when no behavioural evidence exists

For commands and other user-facing entry points, distinguish direct user invocation from a name merely appearing in loaded instructions, agent output or quoted history. When usage history is available, record the sampling limits and count only genuine invocations.

Use evidence levels:

- **E1 - observed defect:** a concrete wrong output, lost item, unsafe action or contradiction
- **E2 - repeated miss:** multiple corrections, log entries or measurable rule skips
- **E3 - exposed risk:** the architecture allows a serious failure, but no incident was found
- **E4 - preference/opportunity:** a useful improvement without a correctness or safety failure

Rules:

- Do not invent counts.
- If logs are missing, say so.
- A high "guideline not read" rate is not enough by itself. Inspect whether outputs were actually defective.
- Sample both compliant and non-compliant artefacts.
- Separate new-file creation from small edits to existing files; they often need different context.
- Redact or generalise private names, clients, email addresses and sensitive facts in the report unless the user's own system explicitly permits them.
- Record evidence as short paraphrases and local file references, not long copied passages.

### Optional session-log analysis

If the agent runtime stores local session logs and the existing rules permit reading them:

1. Determine the real log format and location rather than assuming one.
2. Define a transparent sample window and unit of measurement.
3. For each recurring output type, measure whether the relevant template/guideline was loaded before creation.
4. Inspect a representative sample of the outputs for actual defects.
5. Document undercount/overcount risks such as compaction, resumed sessions, injected context and edits to existing files.
6. Keep any analysis script temporary or save it only if the system's rules treat it as a useful durable tool. Do not install a recurring job.

If session logs are unavailable, continue with artefact and correction evidence.

---

## Phase 3: audit the operating system

Audit every dimension below. A dimension can pass; do not manufacture findings to fill the report.

### 3.1 Instruction architecture

- Is there a clear precedence order?
- Can the agent tell what to read before each major action?
- Does the root manual own only vault-wide invariants, safety, precedence and routing, or duplicate detailed leaf files?
- Do project-specific files contain only the facts, constraints and exceptions that differ from inherited guidance?
- Does each detailed workflow, schema, template or acceptance contract have one authoritative home and a discoverable route?
- Do routers point to canonical leaves rather than restating their behaviour?
- Are durable rules sitting in memory, commands or examples without a clear owner?
- Are command indices and referenced files real and in sync?
- Are there contradictory or stale rules?
- Does the system have a gate before adding another instruction file, section, command, hook, template or prompt?
- Are high-leverage operating-manual changes versioned?

### 3.2 Safety and data integrity

- Are raw notes/transcripts/journal sources distinguished from derived synthesis?
- Are user-authored areas append-only/hands-off where appropriate?
- Are external writes, spending and paid API use approval-gated?
- Are secrets kept out of files and logs?
- Are destructive actions narrowly scoped and recoverable?
- Is there a snapshot/history mechanism before rewriting user-authored or high-leverage files?
- Are unattended runs prevented from blocking on approval prompts?

### 3.3 Workflow and output completeness

Trace the actual loop:

`capture -> ingest -> extract -> prioritise -> execute -> review -> approve/send -> verify outcome -> close/wait -> archive -> learn`

For each stage, ask:

- Is there an explicit owner and source of truth?
- Does each recurring workflow define a checkable outcome contract?
- Does the system default to **decision-complete, not exhaustive** output: everything needed to act, decide or verify safely, without repetition that does not change the outcome?
- Can a general brevity preference override necessary evidence, provenance, uncertainty, exceptions, fidelity or next actions?
- Is source detail preserved when fidelity is itself part of the result, such as transcripts, journals, contracts and reviews?
- Does the workflow fetch the evidence its rules rely on?
- Can work fall between a rule and its executor?
- Can drafts remain stranded after the user acts elsewhere?
- Can questions or deferred items disappear?
- Does "done" mean the task's semantic end state, not merely related activity?

Flag "rule without mechanism" and "mechanism without rule" separately.

### 3.4 Correctness and verification

- Proper nouns from voice/transcripts
- Relative dates and day boundaries
- Task status and completion evidence
- Required front matter and canonical schema values
- Source links that survive archiving/moves
- Factual claims and source/date checks
- Client/privacy constraints for public outputs
- Render/format checks for documents, slides, spreadsheets, PDFs and HTML

### 3.5 Interactive versus unattended modes

- Are the modes explicitly different?
- Does unattended mode queue rather than prompt?
- Does interactive mode drain the queue?
- Are judgement calls logged?
- Is question overflow handled without losing mandatory questions?
- Is failure handling continue-and-report rather than all-or-nothing?

### 3.6 Learning and rule maintenance

- Are corrections persisted beyond chat history?
- Are lessons routed to command, project, system or global scope correctly?
- Is memory an index/staging layer rather than an unreviewed rule pile?
- Are stale rules audited or promoted into durable sources of truth?
- Does the system notice repeated work shapes and offer standardisation?

### 3.7 User experience and maintenance burden

- Does the user have one obvious place to write and one obvious place to review?
- Are priorities visible before audit detail?
- Does the system demand manual metadata or duplicate entry?
- Can the user tell what the agent changed and why?
- Are review queues capped/triaged rather than endlessly growing?
- Is there a clear recovery path when automation fails?

### 3.8 Portability and runtime assumptions

- Which parts depend on one agent/runtime, operating system, CLI or local path?
- Are hard-coded paths and tool names documented?
- Do commands describe verified reality or historical assumptions?
- Are optional integrations genuinely optional?

### 3.9 Local dashboard/portal

If a local app exists, audit:

- whether it is a presentation layer over canonical files/stores or a second source of truth
- whether all pages use one shared app shell/navigation source rather than copied menu markup
- whether reusable styles, scripts, chart interactions and privacy behaviour are shared
- whether it binds to `127.0.0.1` rather than exposing itself on `0.0.0.0`
- whether routes, APIs and write paths validate input and preserve provenance
- whether persistence follows a sensible ladder: constants -> JSON -> SQLite only when justified
- whether writable state has backups/migrations and one documented owner
- whether it has a health endpoint, useful logs, loading/error states and smoke tests
- whether a platform-native service starts/restarts it reliably while the computer is awake
- whether documentation falsely implies that keep-alive makes it available during sleep/shutdown
- whether server changes and static-page changes have clear restart/refresh instructions
- whether the app's local instruction file documents how to add a page and where navigation/routes are registered
- whether future remote hosting is correctly treated as a security/deployment migration

If no local app exists, do not call that a defect. At most propose it as an E4 optional improvement when recurring data or review workflows would materially benefit from a visual surface. Examples can include priorities/to-dos, CRM, finances and health/habits, but recommend only views supported by this user's system.

State the availability boundary exactly: a supervisor such as `launchd`, user `systemd` or Task Scheduler can auto-start and restart the process, but localhost remains unavailable when the machine is asleep, shut down or elsewhere. Cross-device or always-on access requires hosting plus authentication, HTTPS, secret management, backups and access-control decisions.

### 3.10 Slash-command and system-surface discipline

Treat slash commands as the user's interface, not automatically as the architecture underneath it.

- Which commands represent a recurring routine the user deliberately starts, a meaningful interaction mode, a stable outcome or a documented authority boundary?
- Which commands have evidence of direct user invocation, and which are only mentioned by agents or loaded instructions?
- Which capabilities are needed by agents but do not need space in the user's command vocabulary?
- Which command files duplicate substantive workflow logic that should live in a reusable leaf?
- Could a natural-language request route to the same workflow just as reliably?
- Would removing or renaming a command delete a capability, or only change its interface? Preserve the capability unless the user explicitly chooses to retire it.
- Are new files, sections, prompts, commands, hooks or templates being added without a distinct trigger, canonical owner, outcome contract, verification condition and maintenance owner?

Do not treat a high command or file count as a defect by itself. The defect is duplicated authority, ambiguous ownership, missing routes, stale interfaces or maintenance cost without a distinct outcome.

Separate mechanical architecture recommendations from business judgement. The agent can normally decide routing, ownership, deduplication and reference repairs. Bring the user concise choices when the answer depends on their mental workflow, desired business completeness, familiar command vocabulary or appetite for side effects.

---

## Phase 4: evaluate hook opportunities

Hooks should make a proven rule reliable; they should not encode subjective judgement or hide the policy from the user.

For every candidate, classify the mechanism:

- **Route/document:** the agent did not know which instruction applied
- **Inject/remind:** the right context is cheap to deliver when a trigger occurs
- **Observe:** validator reports drift without blocking
- **Validate:** deterministic defect can be checked after creation/edit
- **Block:** high-severity action can be detected reliably before it happens
- **Sync/transform:** deterministic mechanical follow-up is safe and idempotent

Prefer the least forceful mechanism that solves the observed problem.

A hook proposal is incomplete unless it specifies:

1. **Evidence:** E1-E4 level and concrete source(s)
2. **Policy source:** the readable markdown rule it enforces/delivers
3. **Trigger:** event/tool/action
4. **Scope:** paths, file types and exclusions
5. **Detection logic:** what is considered pass/fail
6. **Action:** inject, warn, observe, block, transform or sync
7. **False-positive risk:** likely legitimate actions it might catch
8. **Failure mode:** fail open or fail closed, with reason
9. **Exception valve:** narrow, explicit, time/scope-bound if blocking
10. **Privacy/security:** what data the hook reads or emits
11. **Test fixtures:** allowed, blocked, malformed and out-of-scope cases
12. **Rollout:** observe-only period, acceptance threshold and rollback

Do not recommend a blocking hook when:

- the rule requires nuanced judgement;
- the available event cannot see all write routes;
- the failure has not been evidenced and is not a critical exposed risk;
- false positives would interrupt normal use;
- there is no safe exception/recovery path.

When a hook would cover only some write routes, say so plainly. Partial protection can still help, but must not be described as complete filesystem enforcement.

---

## Phase 5: design the target state

Propose the smallest coherent upgrade, not a rewrite for its own sake.

Use these buckets:

- **Keep:** working rule/mechanism that should remain
- **Clarify:** same intent, better wording/placement
- **Move:** correct rule in the wrong source of truth
- **Add:** evidenced missing capability
- **Retire:** duplicate, stale or harmful rule/mechanism
- **Observe first:** promising change that needs evidence

The target architecture should normally distinguish:

1. A concise root operating manual: identity, precedence, non-negotiables, routing, uncertainty and map
2. Project instruction files: only project-specific facts, constraints and exceptions
3. Leaf files: detailed workflows, schemas, styles, references and checkable acceptance contracts
4. Commands: deliberate user-facing routines, modes or authority boundaries, not duplicated policy
5. Hooks: narrow delivery/enforcement mechanisms whose policy remains readable elsewhere
6. Review surfaces: generated work and approval queues
7. Raw/user-owned surfaces: protected evidence
8. Memory: user context and staged learning, not a parallel rulebook
9. History/changelog: recoverability and audit trail
10. Optional local UI: a shared-shell presentation layer over canonical data, with loopback binding, health/logging and supervised startup

Apply three design rules throughout:

- minimise machinery, not the outcome;
- prefer the fewest authoritative homes, not necessarily the fewest files;
- make recurring outputs decision-complete, then as concise as the user's presentation preference allows.

For each proposed change assign a stable ID such as `MAN-01`, `FLOW-02`, `HOOK-03`.

Every decision item must include:

- title and category
- priority: critical/high/medium/low
- evidence level and evidence references
- current problem
- recommendation
- why this mechanism/location is appropriate
- exact files/surfaces affected
- what will not change
- dependencies
- risks and alternatives
- validation/test plan
- implementation effort: small/medium/large
- whether user judgement is required and, if so, the smallest concrete question or A/B choice

Merge tightly related changes into one decision. Aim for no more than 12 decision items; put lower-value observations in an appendix so review remains manageable.

Do not propose personal details, folder names or integrations copied from another person's OS unless the evidence in this system supports them.

---

## Phase 6: create the interactive HTML review report

Save the report as:

`2_for-review/personal-os-upgrade-audit-YYYY-MM-DD.html`

If this system uses another review folder, adapt the path. Do not overwrite an existing report; add `-2`, `-3`, etc.

The HTML must be:

- a single self-contained file
- responsive and readable on laptop/mobile
- accessible with semantic headings, labels and keyboard-usable controls
- usable from `file://` without a server
- free of external fonts, scripts, stylesheets, images and network calls
- printable with a clean print stylesheet
- safe: never interpolate unescaped raw file content into HTML/JavaScript

### Required report structure

1. **Title and status**
   - Personal OS Upgrade Audit
   - date/time, system root label, audit version
   - prominent statement: "Proposal only - no operating files or hooks changed"

2. **How to review**
   - Read the executive summary
   - For each decision choose Accept, Revise or Reject
   - Add optional comments
   - Use "Copy feedback for agent" or "Download feedback"
   - Paste the exported markdown into the same agent conversation

3. **Executive summary**
   - current strengths
   - most important risks/gaps
   - recommended upgrade shape
   - evidence/caveat summary

4. **System map**
   - instruction hierarchy
   - instruction-surface classes, canonical owners and routes
   - direct command-use evidence and command-to-workflow relationships, when usage history is available
   - main capture/processing/review loop
   - existing hooks/automation
   - raw versus generated surfaces

5. **Evidence**
   - sources inspected
   - sampling window/method
   - observed defects and repeated misses
   - limitations; no false precision

6. **Decision cards**
   - one card per stable proposal ID
   - all fields required in Phase 5
   - `Accept`, `Revise`, `Reject` radio controls
   - a labelled comments textarea
   - default state `Unreviewed`

7. **Hook analysis**
   - existing hooks: keep/change/retire
   - candidates and why a hook is/is not justified
   - hook design details from Phase 4
   - observe-only recommendations clearly distinguished from enforcement

8. **Local dashboard/portal**
   - show this section only when an app exists or an optional app proposal is evidence-supported
   - current source-of-truth and shared-component architecture
   - local-only/network exposure status
   - persistence/write-path assessment
   - health, logs, tests and service-manager reliability
   - exact awake-versus-asleep availability boundary
   - remote-hosting migration requirements

9. **Retention and contradiction tables**
   - important current rules: keep/clarify/move/retire
   - contradictions with proposed resolution
   - command interfaces: keep/rename/demote/retire while preserving underlying capabilities

10. **Implementation sequence**
   - safe phases
   - snapshot/history step
   - tests and rollback for each phase
   - explicit approval boundaries

11. **Appendix**
   - low-priority observations
   - files inspected
   - audit limitations

### Required review interaction

Implement the review controls in plain JavaScript.

- Give every decision card a stable `data-decision-id`.
- Persist radio selections and comments in `localStorage` under a key containing the audit date and system identifier.
- Restore saved selections/comments on page load.
- Show progress: reviewed count / total.
- Provide filters for All, Unreviewed, Accept, Revise and Reject.
- Provide a "Copy feedback for agent" button.
- Provide a "Download feedback (.md)" button using `Blob` and a temporary object URL.
- Provide a "Reset review" button with a confirmation dialog.
- If clipboard access fails under `file://`, show the compiled feedback in a selectable fallback textarea.
- Never send review data over the network.

The exported markdown must contain:

```markdown
## Personal OS upgrade review

- Audit file: <filename>
- Reviewed: <date/time>
- Scope: Decisions below are feedback on the proposal.

### Approval boundary

Accepted items authorise additive/recoverable changes inside this Personal OS after the agent follows the existing snapshot/history rules. They do NOT authorise external writes, sending/publishing, spending or paid API use, secret access, package/plugin installation, system-level scheduling, deletion of user-authored content, or destructive rewrites. Those still require separate explicit approval.

### Decisions

#### <ID> - <title>
- Decision: Accept | Revise | Reject | Unreviewed
- Comment: <user comment or "None">
```

Include a final free-text field labelled "Overall comments / sequencing preferences" and include it in the export.

### Visual design

Use a calm, high-contrast editorial/dashboard style:

- neutral background
- restrained accent colour
- clear status chips for priority and evidence level
- generous spacing
- no decorative clutter
- decision controls remain obvious
- sticky review-progress bar on larger screens, normal flow on small screens

Do not use fake health scores or charts unless the underlying data genuinely supports them.

---

## Phase 7: hand off the audit

After writing and validating the HTML:

1. Check that the file opens as valid HTML and contains no broken internal navigation.
2. Check that every proposal ID appears in both the decision card and feedback export.
3. Check that localStorage save/restore, filters, copy fallback and markdown download are implemented.
4. Confirm no existing operating file, hook or configuration was changed.
5. Give the user only:
   - a link/path to the report
   - the number of decision items
   - the four review steps
   - a reminder to paste the exported feedback back into the conversation

Do not also dump the full audit into chat.

---

## Phase 8: when the user returns feedback

This phase begins only after the user pastes the exported review markdown or gives equivalent explicit decisions.

1. Parse each decision by stable ID.
2. Do not implement rejected or unreviewed items.
3. For `Revise`, propose the revised wording/approach and resolve only genuinely blocking ambiguity.
4. Treat accepted items as approval only within the exported approval boundary.
5. Re-read the current root/project instructions in case the system changed since the audit.
6. Inspect version-control status and preserve unrelated user changes.
7. Before rewriting an operating manual, schema, command or other high-leverage file:
   - create the system's required history copy/snapshot;
   - if none exists, propose one before rewriting;
   - record the planned file-level change.
8. Implement in small dependency-ordered phases.
9. Keep policy in readable markdown; hooks only deliver/enforce it.
10. When moving or demoting a command, preserve the underlying workflow unless the user explicitly approved retiring the capability; update indices, routes and references.
11. For every hook:
    - create test fixtures first;
    - run observe-only where feasible;
    - show the result before enabling a blocker;
    - keep a rollback path.
12. Run link/reference, schema and workflow-consistency checks.
13. Update the system changelog/history.
14. Create a post-upgrade review note listing:
    - implemented IDs
    - revised/deferred IDs
    - files changed
    - tests run/results
    - remaining caveats
    - rollback instructions

Never publish the upgraded system, push a remote repository, connect a service or perform an external write unless the user separately approves that exact action.
