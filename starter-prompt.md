## Personal OS Starter Prompt v0.6

You are setting up a Personal OS in an empty Obsidian vault. This is a markdown-based personal operating system - not a software project. It covers both work and personal life. All content is plain markdown interconnected via Obsidian's wiki-style links [[filename]].

Do everything below IN ORDER. Create all files first, then run the interview. Do not pause for approval between phases - just execute.

---

PHASE 1: CREATE FOLDER STRUCTURE

Create these directories:

- 0_daily-brief/
- 1_inbox/
- 1_inbox/archive/
- 2_for-review/
- 2_for-review/stale/
- 2_for-review/not-urgent/
- tasks/
- ideas/
- system/
- meetings/
- projects/
- .claude/commands/

---

PHASE 2: WRITE FOUNDATIONAL FILES

Create each of the following files with the exact content specified. Most files use sensible defaults - PHASE 3 will update them based on the user's answers.

### FILE 1: CLAUDE.md (in the vault root)

Write this file at the root of the vault:

```
# CLAUDE.md

This is an **Obsidian Vault** - a personal operating system covering both work and personal life. All content is plain markdown interconnected via Obsidian's wiki-style links `[[filename]]`. Personal errands, appointments, and life admin are in scope alongside business tasks.

## Who You Are

<!-- PLACEHOLDER: This section will be filled in during the interview below. -->

## How to Work With You

<!-- PLACEHOLDER: Communication preferences will be added during the interview. -->
- Spelling: British (changed during interview if you prefer otherwise)
- Date format in note bodies: `YYYY-MM-DD` (ISO). File names always use ISO regardless.
- Day boundary: midnight. Anything written between 00:00 and your boundary is treated as the previous day.
- No H1 headers in notes - Obsidian uses the filename as the title
- Daily notes are your space - Claude never overwrites or deletes your content. All structured output goes in `0_daily-brief/daily-brief.md`.

## Processing Style

- Default to execution over planning. Do not pause for approval on routine items unless explicitly told to.
- Keep all generated content (emails, descriptions, briefs, notes) short and concise by default.
- Never mark tasks or deliverables as done unless the user has explicitly confirmed or reviewed them.
- **Persist all learnings**: When a mistake is corrected, a workflow is improved, or a convention is agreed, write it to a durable file immediately - never rely on chat history alone. Route learnings to the right place: if it applies to a specific command, save it in that command's file (`.claude/commands/<name>.md`); if it's vault-wide, add it to CLAUDE.md. Use `/assimilate` at the end of sessions to capture what's worth keeping.
- **Spot repetition, offer to standardise**: when you notice the user (or you) doing the same kind of work for the third time, surface it and ask whether to make it a template, script, system file, or slash command. Don't silently keep redoing it.
- **Backlink, don't relocate**: when creating a project hub, link to existing notes from where they already live - never move them out of `journal/`, `2_for-review/`, `tasks/`, etc. just to gather them under a project. The hub is a view; the notes stay home.

## Vault Notes

- **Obsidian LaTeX rendering**: Triple dollar signs (`\$\$\$`) render as LaTeX math blocks in Obsidian. If you need to write three consecutive dollar signs (e.g. in financial notes), escape them (`\$\$\$`) or substitute with `£££`. Single dollar signs (`$100K`) are fine.

## Vault Structure

- `0_daily-brief/` - `daily-brief.md` (Claude-maintained structured view of the day) and `changelog.md` (audit trail of brief updates)
- `1_inbox/` - Daily notes (YYYY-MM-DD.md), archive/
- `2_for-review/` - Items Claude has produced that need your review. `stale/` for items past the staleness threshold without action. `not-urgent/` for deliberately parked items.
- `tasks/` - Individual task notes with front matter metadata
- `ideas/` - Someday/maybe items (same format as tasks, status: idea)
- `system/` - Context files: profile, goals, processing rules, workflow definitions
- `meetings/` - Meeting notes and transcripts
- `projects/` - Project folders

## File Naming Conventions

- Daily notes: `YYYY-MM-DD.md`
- Meeting notes: `YYYY-MM-DD description.md`
- Task/idea notes: `lowercase-hyphenated-slug.md` (e.g. `follow-up-sarah-proposal.md`)
- Files are interconnected via Obsidian wiki-style links `[[filename]]`

## Two-Document Setup

- `0_daily-brief/daily-brief.md` - Claude-maintained structured view. Updated during processing. Opens with **Top priorities first** - no preamble, no changelog inline. Contains: priorities, tasks needing attention, questions for user, recently completed items.
- `0_daily-brief/changelog.md` - Audit trail of every change to the brief. Newest entries at the top. The brief itself just has a one-line pointer to this file - keeping the brief itself focused on what to do next.
- `1_inbox/YYYY-MM-DD.md` - User's scratch pad. Raw thoughts, answers, stream of consciousness. Claude never overwrites user content or adds summaries to daily notes.

## Task Management Rules

- All actionable TODOs must be individual task notes in `tasks/` - never use inline checkboxes (`- [ ]`) in planning docs, project files, or other notes
- Planning documents should **link to** task notes using `[[task-name]]`, not duplicate them as checkboxes
- Reference `system/task-template.md` for front matter format when creating tasks

## Obsidian CLI

If the `obsidian` CLI is installed and Obsidian is running, prefer it over raw file tools for these operations:

- **Search**: `obsidian search query=<text>` - full-text search. Add `path=<folder>` to scope.
- **Read a file**: `obsidian read path=<path>`
- **Daily notes**: `obsidian daily:path` (get path), `obsidian daily:read`, `obsidian daily:append content=<text>`
- **Create a note**: `obsidian create name=<name> content=<text>` or `path=` for exact location
- **Append to a note**: `obsidian append path=<path> content=<text>`
- **Backlinks**: `obsidian backlinks file=<name>` - all files linking to a note
- **Move/rename** (updates wiki-links automatically): `obsidian move path=<path> to=<dest>` or `obsidian rename`

Use Read/Edit/Write tools for reading file content, precise edits with line numbers, and bulk operations. Use Glob/Grep for pattern matching and regex search.

Note: the CLI prints a loader line to stderr - ignore it.

## Commands

**`/process-autopilot`** - Hands-free processing. Reads daily notes, extracts a full manifest of every actionable item before processing, executes what it can, and flags the rest in the daily brief. Questions go to the brief, not the terminal. Use when stepping away from the screen.

The workflow is defined in `system/process-workflow.md`. Rules and format conventions are in `system/processing-rules.md`.

**`/assimilate`** - Review the current session and persist anything worth remembering to CLAUDE.md or command files. Run at the end of sessions where you corrected Claude, agreed a new convention, or made a structural decision. See `.claude/commands/assimilate.md`.

## System Files

- `system/profile.md` - Who you are and what you do
- `system/goals.md` - Current goals (read when prioritising)
- `system/processing-rules.md` - Extraction rules, daily brief format, task workflow conventions
- `system/process-workflow.md` - Core processing steps for /process-autopilot
- `system/task-template.md` - Reference when creating task or idea notes
- `system/onboarding.md` - Record of how this vault was configured (created by the interview, kept as reference)

## Vault Operations

- Always check for existing files before creating new ones (use Glob/Grep first)
- Check the most recent daily note pattern before assuming a path
- Never mark tasks or deliverables as done unless the user has explicitly confirmed or reviewed them
- When converting relative dates ("next Friday", "this Thursday") to YYYY-MM-DD, always verify using the `date` command - never do mental arithmetic
```

### FILE 2: system/task-template.md

Write this file. It contains YAML front matter examples - write them exactly as shown, including the triple-dash delimiters:

```
## Task/Idea Note Template

Reference for Claude when creating task and idea notes.

Front matter format:

---
status: todo          # todo | in-progress | waiting | done | cancelled
priority: medium      # low | medium | high | urgent
due:                  # YYYY-MM-DD or blank
created: YYYY-MM-DD
completed:            # YYYY-MM-DD, filled when status -> done
source: "[[YYYY-MM-DD]]"  # where this came from
tags:
  - task
---

Sections to include in each task note:

## Context
[Why this task exists, any background needed]

## Next action
[The concrete next step]

## Log
- YYYY-MM-DD: Task created from [[source]]

Notes:
- status: idea is for someday/maybe items. Ideas live in the ideas/ folder.
- completed gets a date stamp when status changes to done.
- Tags always include "task" (or "idea"). Add project names or categories as additional tags.
```

### FILE 3: system/processing-rules.md

```
## Extraction Rules

When processing daily notes, extract:
- Action items and commitments - **including personal errands and life admin** (this is a personal OS, not just a work tool)
- People mentioned (if CRM module is enabled, create/update CRM notes)
- Follow-ups needed
- Decisions made

**Do not filter items based on whether they seem "work-relevant".** If the user mentions it as an action, it is an action.

## Task Creation Workflow

During daily note processing:
1. Check if a matching task already exists in `tasks/` (by filename or tags)
2. If found: append to Log section, update fields as needed
3. If not found: create new task note with front matter filled from context
4. If it is a someday/maybe item: create in `ideas/` with status: idea
5. Done tasks: set `status: done`, `completed: YYYY-MM-DD`, append to Log. Never delete.

## Execution Rule

- Lightweight tasks that need no clarification: execute immediately (draft it, write it, do it)
- Tasks needing user input: create a task note, add to "Questions for user" in the daily brief
- Ambiguous or deep-research tasks: create a task note, flag it

## No Double-Defer Rule

An item the user explicitly asked to be implemented or executed cannot be deferred more than once. If it was deferred in a previous run and appears again, execute it this time. If it genuinely cannot be done, escalate with a clear explanation of what's blocking it - not just "deferred".

## Daily Note Rules

- Never delete or overwrite user content in daily notes
- Daily notes are the user's raw input space
- All structured output goes in `0_daily-brief/daily-brief.md` (and audit trail in `0_daily-brief/changelog.md`)

## Daily Note Archiving

During processing, move any daily notes in `1_inbox/` older than 7 days to `1_inbox/archive/`. This keeps the inbox showing only the last week of notes.

## 2_for-review Triage

Items in `2_for-review/` that have been sitting for **2 days** without action should be moved to `2_for-review/stale/`. (This threshold is set during the interview - update here if you change it.) Items the user has explicitly decided to park (not urgent, revisit later) go in `2_for-review/not-urgent/`. Flag stale items in the daily brief.

## Daily Brief Format

The daily brief (`0_daily-brief/daily-brief.md`) uses these sections in order:

1. **Top priorities** - the top items to focus on. Always first thing in the brief, no preamble.
2. **Tasks needing attention** - overdue, due today, or flagged
3. **Questions for user** - anything Claude needs answered to proceed
4. **Recently completed** - done items from the last day or two

The brief itself opens with a one-line pointer to the changelog (e.g. `> Audit trail: [[0_daily-brief/changelog]]`) **above** the Top priorities section. The changelog itself lives in a separate file - see below.

Keep it simple. Use markdown tables or bullet lists - whichever is clearest. Done items stay visible with a checkmark for the current day, then get cleared when the brief flips to the next day.

## Changelog

Every meaningful update to the daily brief gets a changelog entry in `0_daily-brief/changelog.md` (NOT inline in the brief). Entries are timestamped, newest at the top, and describe what was processed / changed / queued for review. This keeps the brief focused on "what to do next" while still preserving the full audit trail for debugging.

## Question Audit at Brief Flip

When flipping the brief to a new day (or starting a fresh autopilot run), do a quick pass over the previous day's daily notes (`1_inbox/`) before carrying forward "Questions for user" entries. If the user answered a question in their notes - even partially - update or clear that question rather than re-listing it. Stale questions that the user has already addressed accumulate fast and erode trust in the brief.

## Task Completion

- When the user says something is done, find the task note, set status to done, set completed date
- Add a log entry noting completion
- Update the daily brief
```

### FILE 4: system/process-workflow.md

```
## Processing Workflow

This is the workflow for `/process-autopilot`. It runs hands-free - any questions go to the daily brief, not the terminal.

### Step 0: Establish the date

Check the real current date using `date` in the terminal. Do not rely on session start date - sessions may span overnight.

If the user has set a non-midnight day boundary (see CLAUDE.md "How to Work With You"), apply it: anything happening between 00:00 and the boundary is treated as the previous day.

### Step 1: Check state

1. Read `0_daily-brief/daily-brief.md` - check if it exists and what date it covers
2. If no brief exists or the date is stale: build a fresh brief (and run the question audit - see Step 4)
3. Read today's daily note (`1_inbox/YYYY-MM-DD.md`) if it exists
4. If no daily note exists for today, create one with front matter only

### Step 2: Scan tasks

1. Check `tasks/` for overdue items (due date before today, status not done/cancelled)
2. Check `tasks/` for items due today
3. Check for stale waiting tasks (status: waiting, no log update in 7+ days)

### Step 3: Process daily notes

Read `system/processing-rules.md` for extraction rules.

**Multi-day processing**: If the last run was more than 1 day ago, process ALL unprocessed daily notes in chronological order - not just today's. Check for any notes in `1_inbox/` dated since the last brief date.

#### Step 3a: Extract manifest (BEFORE any processing)

For each daily note to be processed:

1. **Read the entire note first.** Do not start processing after reading the first section.
2. **Extract every actionable item** into a numbered manifest. An "item" is anything that requires action: a task, a piece of feedback, a draft request, a CRM update, a file move, a question answer, a "done"/"sent" confirmation, a request to investigate or implement something.
3. **Categorise each item**: task, feedback, content-request, CRM-update, file-operation, question-answer, implementation-request.
4. **Sort by priority**: items the user explicitly said "implement"/"execute"/"do this" come first. Then time-sensitive items. Then everything else. Do NOT process in note order - process in priority order.
5. **Check the deferred list** in the current daily brief changelog. If any item in the manifest matches something previously deferred, flag it - these get priority (see "No double-defer rule" below).

#### Step 3b: Process items from manifest

For each item in the manifest:

1. **Triage**:
   - Lightweight, no clarification needed: execute immediately (draft it, write it, do it)
   - Needs user input: create task, add to "Questions for user" in the brief
   - Deep research or ambiguous scope: create task, flag it

2. **Extract** in chunks:
   - Action items: task notes in `tasks/`
   - People mentioned: create/update CRM notes (if CRM module enabled)
   - Follow-ups needed: task notes
   - Decisions made: update relevant project/system files
   - If the journal module is enabled: route reflective content to evergreen notes in `journal/`, then generate journal commentary (see journal rules in CLAUDE.md)

#### Step 3c: Verify manifest (AFTER all processing)

After processing all items from the manifest:

1. **Re-read the daily note.**
2. **Compare against the manifest.** Every item must have a disposition: done, deferred (with reason), or not applicable (with reason).
3. **Flag any gaps** in the daily brief changelog. If an item was missed, either action it now or add it to "Questions for user" with an explanation.
4. If context limits are approaching and items remain unprocessed, list them explicitly in the changelog as "Not yet processed (context limit) - carry forward" rather than silently dropping them.

#### No double-defer rule

An item that the user explicitly asked to be implemented, executed, or planned **cannot be deferred more than once**. If it was deferred in a previous run and appears again (either because the user re-raised it or because it's still on the deferred list):

- **Execute it in this run**, even if it means spending significant time on it.
- If it genuinely cannot be done (e.g. requires permissions, external dependency, or would take the entire session), escalate it to "Questions for user" with a clear explanation of what's blocking it - not just "deferred".
- Never silently carry forward a deferred item with the same "deferred" status. Each carry-forward must either change status (to blocked/escalated) or get done.

### Step 4: Update daily brief

When flipping the brief to a new day, **first run the Question Audit** (see processing-rules.md): scan the previous day's daily notes for direct answers to carried-forward "Questions for user" entries. Update or clear those before re-listing them.

Then update `0_daily-brief/daily-brief.md` with:
- A one-line pointer to the changelog at the top: `> Audit trail: [[0_daily-brief/changelog]]`
- Top priorities (FIRST visible section - no preamble)
- Tasks needing attention (overdue, due today, flagged)
- Questions for user (after the audit pass)
- Recently completed items

Append a timestamped entry to `0_daily-brief/changelog.md` (newest at the top) describing what was processed, what changed, what was deferred, and what the user should review.

### Step 5: Check for stale review items

Look at `2_for-review/` for any items past the staleness threshold (default 2 days, see processing-rules.md). Move them to `2_for-review/stale/` and flag them in the daily brief.
```

### FILE 5: 0_daily-brief/daily-brief.md

Write this file, but replace REPLACE_WITH_TODAY with today's actual date (check using `date` in the terminal, format YYYY-MM-DD):

```
---
date: REPLACE_WITH_TODAY
type: daily-brief
---

> Audit trail of changes to this brief lives in [[0_daily-brief/changelog]].

## Top Priorities

_No priorities set yet. Run `/process-autopilot` or add items to your daily note._

## Tasks Needing Attention

_None yet._

## Questions for User

_None yet._

## Recently Completed

_Nothing completed yet._
```

### FILE 6: 0_daily-brief/changelog.md

```
---
type: daily-brief-changelog
description: Audit trail for daily-brief.md updates. Newest entries at the top.
---

## System initialised

- Vault structure created.
- All foundational system files written.
- Daily brief seeded.
```

### FILE 7: .claude/commands/assimilate.md

```
# /assimilate

Review the current session and persist anything worth remembering to durable files.

## What to look for

1. **Corrections**: Anything the user corrected you on (wrong folder, wrong tone, wrong assumption)
2. **New conventions**: Naming patterns, workflow changes, structural decisions
3. **New context**: Key facts about projects or people that came up and aren't already documented
4. **Preferences confirmed**: Communication style, formatting, tool usage patterns
5. **Mistakes to avoid**: Things that went wrong and how to prevent them next time

## How to persist

1. Read `CLAUDE.md` and any relevant command files in `.claude/commands/`
2. Check if the learning already exists - don't duplicate
3. If it updates an existing entry, edit it in place
4. If it's new, add it to the right file:
   - Command-specific lessons → `.claude/commands/<name>.md`
   - Project-specific conventions → that project's `CLAUDE.md` if it has one
   - Vault-wide patterns → root `CLAUDE.md`

## Rules

- Only persist things that are **stable and confirmed** - not in-progress experiments
- Don't persist session-specific context (current task state, temporary decisions)
- Be concise - one line per lesson where possible
- Tell the user what you wrote and where
```

---

PHASE 3: INTERVIEW

All files are now created. The vault is functional - the user can start using it immediately. But it works better with personalisation.

**The rules below apply to PHASE 3 ONLY. Outside this interview, the normal Claude Code conversation style applies.**

### How the interview works

1. **One question at a time.** Ask, wait for the answer, then move to the next. Never dump the full list.
2. **Capture volunteered information.** If the user answers a future question while replying to an earlier one (e.g. mentions their name, dictation tool, and goals all in one message), record it in the scratchpad. When you reach that question later, **don't re-ask** - just confirm: "Earlier you mentioned X - confirming?"
3. **Push gently on incomplete answers.** If the response doesn't actually answer the question, ask once more, with context for why it matters. Example: user replies "consultant" to the name question → "Got the role - what name should I use in your profile and on drafts I generate for you?" Don't loop forever - if they push back twice and still don't answer, accept the default and note it for revisit.
4. **Accept "skip", "default", or "next".** Treat these as "use the default and move on." Don't force a substantive answer.
5. **Skip conditional questions when not applicable.** Only ask the weekly review day question if the weekly review module was chosen.
6. **Confirm before writing.** After all questions, summarise the gathered answers and ask "Anything to change before I write the files?" - one final escape hatch.

### Set up the scratchpad

Before asking the first question, create `temp-onboarding.md` in the **vault root** with this content:

```
---
type: onboarding-scratchpad
status: in-progress
note: This file is temporary. It exists only during the interview and gets deleted once the vault is fully configured. Don't edit it manually.
---

## Answers gathered

- Name + role:
- Top goals:
- Communication preferences:
- ADHD / focus preferences:
- Spelling:
- Date format:
- Voice or typing:
- Day boundary:
- Optional modules:
- Weekly review day (if applicable):
- Scheduled autopilot preference:
- For-review staleness threshold:

## Notes from user

(volunteered info captured out of order)
```

Update this file as answers come in. Don't show its contents to the user unless they ask.

### Open the interview

Say something like:

"Your vault is set up and ready to use. You can open it in Obsidian right now - start dumping thoughts into a daily note at `1_inbox/YYYY-MM-DD.md` and run `/process-autopilot` whenever you want me to process it.

Before you dive in, I'll ask a handful of questions to personalise the system. I'll ask one at a time. Most have a sensible default - if you don't care, just say 'skip' and we'll move on. You can always come back and change things later."

### The questions

Ask these in order. Skip any whose answer the user has already volunteered (just confirm).

---

**Q1: What is your name and what do you do?**

> I'll create a profile at `system/profile.md` and use your name on drafts I generate. The "what you do" answer doesn't have to be a job title - whatever framing makes sense to you (e.g. "solo consultant in data and AI", "PM at a fintech", "freelance writer working on a novel").

---

**Q2: What are your top 2-3 goals right now?**

> Work, personal, or a mix - whatever's actually on your mind. I'll save these to `system/goals.md` and read them when prioritising your tasks. If you're not ready to commit, say skip and I'll leave it as a template you can fill in later.

---

**Q3: How should I communicate with you?**

> For example: direct and concise, or more detailed? Any tone preferences (formal, casual, dry humour OK, no emojis, etc.)? This shapes how I write briefs, drafts, and updates.

---

**Q4: Do you have ADHD, or any focus or attention preferences I should know about?**

> Common things people ask for: chunked responses, single next action only, no long lists, surface overdue items first. Or maybe none of those apply - that's fine too.

---

**Q5: What spelling should I default to?**

> I'll use this for everything I draft for you (emails, posts, notes, reports).
>
> Common options: British (`organise`, `colour`), American (`organize`, `color`), Canadian, Australian.
>
> **Default: British.**

---

**Q6: What date format do you prefer?**

> File names always use ISO (`YYYY-MM-DD.md`) for sortability - this only affects how I write dates inside notes, briefs, and emails.
>
> - `2026-05-07` (ISO, recommended - unambiguous, sorts correctly)
> - `07/05/2026` (UK / European)
> - `05/07/2026` (US)
> - `7 May 2026` (long form)
>
> **Default: ISO.**

---

**Q7: Do you mostly dictate your daily notes or type them?**

> This matters because voice-first workflows have different gotchas - homophones get confused, surnames get mangled, fragments instead of edited prose. If you say voice, I'll:
> - Treat your daily notes as voice transcripts (won't penalise missing punctuation or weird capitalisation)
> - In project files, optionally maintain a "Stakeholders" block mapping casual first names to full CRM records (surnames in transcripts are unreliable)
>
> Options: voice / typing / mixed. **Default: typing.**
>
> (If you dictate, what tool? Wispr Flow, macOS Voice Control, etc. - just so I can mention it in your profile.)

---

**Q8: When does your day end?**

> Default is midnight - works for most people. If you regularly work past midnight and "tomorrow at 1am" to you means the coming morning (not the day after), set this later. I use it to decide which `1_inbox/YYYY-MM-DD.md` file to write to and how to interpret "today" / "tomorrow" in your notes.
>
> - **Midnight** - strict calendar day
> - **3am** - light night-owl
> - **5am** - heavier night-owl, common for solopreneurs and creatives
>
> **Default: midnight.**

---

**Q9: Do you want any of these optional modules?**

> Each adds folders and rules. You can enable any combination - or none.
>
> - **CRM** - track people, companies, opportunities (`CRM/people/`, `CRM/companies/`). Good if you do sales, networking, or freelance work.
> - **Content pipeline** - drafts, ideas, published content folders (`content/ideas/`, `content/drafts/`, `content/published/`). Good if you write or create regularly.
> - **Weekly reviews** - auto-generated weekly review notes (`weekly-reviews/`). Good for reflecting on progress.
> - **Journal / thinking layer** - living evergreen notes on topics you keep returning to. Not a diary - documents that get rewritten as your views evolve. Good if you have open dilemmas or recurring questions.
>
> Tell me which (if any) you want.

---

**Q10 (only if weekly reviews module chosen): What day of the week works for your weekly review?**

> I'll auto-create the weekly review file every week on this day (or first autopilot run after it).
>
> - **Sunday** - review the week just ended, plan ahead
> - **Friday** - wrap up, fresh start Monday
> - **Monday** - kick off the week
>
> **Default: Sunday.**

---

**Q11: Quick context first - I'll be using `2_for-review/` for anything I draft for you to look at: emails, posts, research, analysis, deliverables. Items sit there until you action them (approve, edit, send, file).**

> If something has been sitting too long without you touching it, I'll auto-move it to `2_for-review/stale/` so the active folder stays clean. Stale items still surface in your daily brief - they just don't crowd the main view.
>
> How long before something counts as "stale"?
> - **2 days** (assumes daily triage)
> - **5 days**
> - **7 days** (if you batch reviews weekly)
>
> **Default: 2 days.**

---

**Q12: Want to run `/process-autopilot` automatically every morning?**

> What it does: at the scheduled time, your machine reads your latest daily note, extracts tasks, updates your CRM, drafts replies, and prepares your daily brief - all without any prompts. By the time you sit down, the day is structured.
>
> Two heads-ups before you decide:
> 1. **Your machine has to be powered on and logged in** at the scheduled time. If it's asleep, the run is missed (it'll catch up next time).
> 2. **Autopilot can't ask questions mid-run** - anything ambiguous gets logged in `0_daily-brief/changelog.md` and `0_daily-brief/approval-queue.md` for you to review later.
>
> Options:
> - **Yes, 5am daily** (most common)
> - **Yes, custom time** (you say when)
> - **No, I'll run it manually**
>
> If you say yes: I'll **capture the preference** in your config, but I won't auto-install the schedule - you'll need to set up the cron / launchd / Task Scheduler entry yourself. I'll give you the exact one-line command to run when we wrap up.
>
> **Default: no.**

---

### After all questions are answered

1. **Confirm**: read back the gathered answers and ask "Anything to change before I write the files?"

2. **Update files based on answers**:
   - `system/profile.md` (created): name + role + voice tool if applicable
   - `system/goals.md` (created): top goals (or template if skipped)
   - CLAUDE.md "Who You Are" and "How to Work With You" sections updated with name, communication preferences, ADHD notes, spelling, date format, voice-or-typing, day boundary
   - If voice: add the Stakeholders-block convention to CLAUDE.md (`When creating a project hub, maintain a ## Stakeholders block mapping casual first names used in voice transcripts to full CRM records. Voice transcripts mangle surnames - the mapping disambiguates.`)
   - `system/processing-rules.md` 2_for-review section updated with chosen staleness threshold
   - If weekly reviews: create `weekly-reviews/` directory, add weekly review section to CLAUDE.md and processing-rules.md (specify the chosen day)
   - If CRM: create `CRM/people/` and `CRM/companies/` directories, add CRM section to CLAUDE.md
   - If content: create `content/ideas/`, `content/drafts/`, `content/published/` directories, add content section to CLAUDE.md
   - If journal: create `journal/personal/` and `journal/strategy/` directories, add journal section to CLAUDE.md (see Journal CLAUDE.md block below), then ask the journal follow-up question
   - If scheduled autopilot = yes: see Schedule handoff below

3. **Save the onboarding record**: copy the contents of `temp-onboarding.md` to `system/onboarding.md` (kept as a permanent reference of how the vault was configured)

4. **Delete `temp-onboarding.md`** from the vault root.

5. **Final summary**: tell the user what was created, what to do first, and (if scheduled autopilot was selected) hand them the schedule command.

### Journal CLAUDE.md block (add this section if journal module is selected)

```
## Journal / Evergreen Notes

Journal content lives in `journal/`. Two subfolders:
- `journal/personal/` - relationships, lifestyle, identity, location decisions
- `journal/strategy/` - business positioning, growth, offerings, frameworks

**Format**: Each note is an evergreen note on a single topic - not a dated entry, but a living document that gets rewritten as thinking evolves.

Front matter:

---
type: evergreen
topic: [Topic name]
tags: [personal/strategy, ...]
last_updated: YYYY-MM-DD
---

## Current position
[Always the latest thinking - rewritten on each update, not appended]

## Open questions
[Live questions; remove when resolved, add new ones as they emerge]

## Archive
### YYYY-MM-DD - [one-line summary of what changed]
[Full snapshot of the previous Current position section]

**During processing**: If a daily note contains reflective content - an explicit "journal:" label, more than ~150 words of first-person reasoning, or recurring-theme language ("I keep thinking about...", "I haven't decided...", "on one hand / on the other") - route it to the relevant evergreen note. Search `journal/` for an existing note on that topic first. If none exists, create a draft in `2_for-review/journal-[topic-slug].md` for the user to name and file.

**Journal commentary**: After updating any journal notes in a processing run, generate commentary for each updated note (or group of related notes) and save to `2_for-review/journal-commentary-[topic-slug].md`. Group related entries into one holistic commentary rather than point-by-point notes; if entries are clearly different topics (e.g. business strategy vs personal relationships), write separate commentary files. Commentary should include: observations about what came up, patterns noticed by comparing the current position against the archive, questions worth sitting with, and your own analysis to help think the topic through further. This is not a summary - it is genuine engagement with the ideas. The user may choose to continue the thinking async from the review folder, or start a terminal session to go deeper.
```

### Journal follow-up question (ask this if journal module chosen, before the final summary)

Say: "One last thing. The thinking layer works best when it has something real to start with. What's something you keep coming back to - a decision you haven't made yet, a dilemma with no clean answer, or a question that's been sitting with you? Work, personal, or anything in between."

Take their answer and create their first evergreen note in the appropriate `journal/` subfolder. Tell them what you created and where.

### Schedule handoff (if scheduled autopilot = yes)

Tell the user:

"Your scheduled autopilot preference is captured. To actually wire it up, run **one** of the following yourself - I won't auto-install it because OS-level scheduling has too many edge cases (permissions, sleep behaviour, login state) for me to handle reliably.

**On macOS** (recommended - launchd):

Create `~/Library/LaunchAgents/com.user.personalos-autopilot.plist` with a `<dict>` entry calling `claude` with `/process-autopilot` at your chosen time, then `launchctl load` it. Search `launchd personalos starter prompt` or ask me in a fresh session and I'll generate the file.

**On Linux** (cron):

Add a line like `0 5 * * * cd /path/to/vault && claude -p "/process-autopilot"` to `crontab -e`.

**On Windows** (Task Scheduler):

Use Task Scheduler GUI - daily trigger at your chosen time, action: run `claude -p "/process-autopilot"` in your vault directory.

**Important reminder**: your machine must be powered on and logged in at the scheduled time. If it's asleep, the run is missed (autopilot will catch up next time it runs)."

### Final summary

After all the above, give a short summary: what was created, what their next step is (write a daily note, run `/process-autopilot`), and a reminder that they can always update preferences by editing CLAUDE.md or running `/assimilate` after a session where they corrected you.
