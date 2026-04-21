# Personal OS

A system for running your work and personal life from a single set of plain text files. You talk, the AI does the organising. No manual maintenance, no apps to keep in sync, no dashboards to update.

Built with Obsidian + Claude Code. Shared because it might work for you too.

---

## The problem it solves

Running a solo consultancy means most of my work is fuzzy: chase this person, mention something to someone, draft a follow-up, prepare for a call. Nobody assigns me work. There's always more to do than I can hold in my head.

Add ADHD to that. Information comes from meetings, emails, WhatsApp, LinkedIn DMs, face-to-face conversations. Before this, my to-dos were scattered across Jira, paper, my head, and a Claude chat from last Tuesday.

AI note-takers were a real unlock - suddenly I could extract tasks from meeting transcripts. But the friction remained: download the transcript, paste it into a chat, give a lot of context. The AI helped with thinking but not with doing. And there was no global picture - no single place to ask "what should I work on right now?" and get a real answer.

## The stack

Three components:

- **Obsidian** - a free markdown editor. This is the vault (the filing cabinet). Everything is just `.md` files in folders on your machine. No database, no cloud dependency, no vendor lock-in.
- **Claude Code** - the engine. This is what reads your notes, extracts tasks, updates your CRM, prepares your daily brief, drafts emails, and does research. It runs in your terminal.
- **Wispr Flow** - voice-to-text. I dictate into any text field. My daily notes are pure voice dumps. I rarely type anything. (You can use my link to get [1 month of Pro access for free](https://wisprflow.ai/r?NICK494) - which will also give me 1 month for free if you end up dictating more than 2k words.)

The key insight: build a dumb system (just files) and let AI do the smart part. Your only job is to talk.

## How it works

### The two-document setup

This is the core design decision. There are two documents that matter each day:

1. **Daily note** (`1_inbox/YYYY-MM-DD.md`) - this is your scratch pad. Raw stream of consciousness. Voice dumps, meeting notes, random thoughts. No structure required. You write into this; Claude never touches it.

2. **Daily brief** (`0_daily-brief/daily-brief.md`) - this is your dashboard. Claude maintains it. You don't edit it directly. It shows: today's priorities, overdue tasks, follow-ups, questions Claude needs you to answer, things ready for you to review.

Separation of concerns: one document for the AI to write to, one for you to write into.

### Processing

When you run `/process-autopilot`, Claude reads your daily note and does everything it can:

- **Reads the entire note first** and builds a manifest of every actionable item before touching anything - no more dropping items at the bottom of long notes
- Sorts by priority: things you said "do this" come first, then time-sensitive items, then everything else
- Extracts action items and creates task notes (each task is its own file with metadata - status, priority, due date, related people)
- Creates or updates CRM records for anyone you mention
- Drafts emails, research briefs, or other lightweight outputs immediately
- **Verifies** after processing that every item got a disposition (done, deferred with reason, or not applicable) - no silent drops
- Updates the daily brief with everything that changed

You can walk away while this runs. Any questions Claude has go into the daily brief for you to answer later - it doesn't pause and wait for you in the terminal.

There's also a **no-double-defer rule**: if you explicitly asked Claude to implement something and it deferred it, it can't defer it again next time. It either executes it or escalates with a real explanation of what's blocking it.

### The CRM that maintains itself

Every time you mention a person in your daily notes or meeting transcripts, their CRM record gets updated. You never open the CRM directly. It tracks relationships and stays current as a side effect of you doing your work.

Each person has a markdown file with their role, company, how you know them, and a running log of interactions. Wiki-style links connect people to companies, companies to opportunities, tasks to people.

### The "slow track" (async work)

With a normal ChatGPT or Claude web chat, you're in a live back-and-forth. Close the tab and it's gone. Everything is synchronous - you have to be there.

This setup has a slower track. Think of it like having someone on your team:

- Claude prepares things for you to review and puts them in a folder (`2_for-review/`). Drafts, research, analysis - you get to them on your own schedule.
- Claude flags questions it needs answered and puts them in the daily brief. You answer them when you're ready.
- Claude can work on things in the background while you do other things.

No real-time pressure. Async by design.

### Context hierarchy

There's a `CLAUDE.md` file at the root of the vault - like a system prompt in a text file. It tells Claude how the vault works, what the conventions are, where things live.

Each project can also have its own `CLAUDE.md`. Claude reads the global one always, but only loads project context when working in that folder. System files (writing styles, goals, processing rules) get loaded on demand - not all at once.

### The thinking layer (optional)

The operational layer tells you what to do. The thinking layer is where you develop how you think.

Instead of dated journal entries, you have living documents on topics you care about - decisions you're working through, questions you keep returning to, things that don't have a clean answer yet.

Each note has three sections: current position, open questions, and an archive. When something relevant comes up in your daily notes, the AI routes it to the right note and rewrites the current position. The old version gets archived.

After each processing run that touches journal notes, Claude generates commentary for each topic - observations, patterns from your previous thinking, questions worth sitting with. Related entries get one holistic note; clearly different topics get separate ones. You can pick these up async and continue the thinking in a terminal session if you want to go deeper.

### Self-improving

At the end of a working session, you run `/assimilate` - a command that tells Claude to review the session and persist anything worth keeping: corrections, new conventions, confirmed preferences. It writes directly to the system files that govern its own behaviour.

## What works well

- Zero-maintenance CRM
- Morning briefings that actually reflect what you need to do
- Voice-first input - almost no typing required
- Async work via the review folder - work product doesn't live trapped inside a chat
- Meeting transcripts get processed automatically (Granola syncs transcripts directly into the vault)

## What's still rough

- MCP integrations (Calendar, Slack) are still flaky
- Mobile experience is limited - this is a laptop-first workflow
- Context window means session handoffs sometimes lose state
- Relies on Claude Code, which requires a subscription and terminal comfort
- Singleplayer: not designed for multiplayer or collaborative use

---

## The philosophy

**This is a starting point, not a finished product.** I don't mean "I'm still working on this" (though I am). I mean YOU need to be the one to evolve it for your own use.

The starter prompt gives you a working system on day one. What makes it yours is what happens after.

I could've turned this into a more rigid template/product/whatever, but that would've defeated the point of all this. The aim is to build a personal OS that thinks the way you do, and that works in a way that works for you.

Every convention in my vault came from something going wrong, or from me realising that a different way would be better (and then testing it out). The rule "never overwrite the daily note" came from Claude overwriting it. The rule "don't do mental arithmetic with dates" came from a near-miss. The rule "execute, don't plan" came from Claude preparing to-do lists when I just wanted the task done. None of it was designed upfront - it was earned through use.

The feedback loop is the point. When Claude gets something wrong, you correct it. When you run `/assimilate`, Claude writes that correction into the `CLAUDE.md` files that govern its own behaviour. Next session, it doesn't make that mistake again. You're not just using Claude - you're using Claude to train a better Claude, one that knows your specific conventions, your folder structure, your tone preferences, your context.

This starter prompt will help you skip some of the early lessons I learned, but it won't absolve you from the need (and joy!) of experimentation.

Some guiding principles I suggest you keep in mind:

- **Function over form.** Resist the urge to design the perfect system before you start. Use it for a week, then fix what's broken.
- **Correct, don't work around.** When something feels off, say so. The system should adapt to you, not the other way around.
- **The files are dumb; the AI is smart.** Markdown files have no opinions. The intelligence lives in how Claude reads and writes them. If Claude's behaviour isn't right, the fix is in `CLAUDE.md` - not in adding more structure to your notes.

For a closer look into how this was built - including verbatim quotes (sanitised), false starts, and the design principles that emerged - check out [origin story](origin-story.md).

---

## Getting started

### Prerequisites

1. **Obsidian** - download at https://obsidian.md (free)
2. **Claude Pro subscription** - you need access to Claude Code, which comes with Claude Pro. Best $20/mo you can spend.
3. Create an empty folder somewhere on your machine. This will become your Obsidian vault. It can also be inside Google Drive / iCloud if you want to sync across devices.
4. (Optional, highly recommended) **Wispr Flow** or similar advanced speech-to-text app. You can use my link to [try Wispr Flow Pro free for 1 month](https://wisprflow.ai/r?NICK494).

### How to use the starter prompt

1. Open the empty folder you created in Claude Code
2. Copy the full contents of `starter-prompt.md`
3. Paste it into Claude Code and let it run

**Note:** The prompt is written for Claude Code. It may need minor adjustments for other tools (Codex, etc.).

---

## Changelog

### v0.5
- **Extraction manifest**: Processing now reads the entire daily note first and builds a numbered manifest of every actionable item before touching anything. Items are sorted by priority (explicit "do this" requests first), processed in that order, then verified against the original note. No more silent drops at the bottom of long notes.
- **No double-defer rule**: Items the user explicitly asked to be implemented cannot be deferred more than once. On the second encounter, they either get executed or escalated with a real explanation of what's blocking them.
- **Multi-day catch-up**: If processing hasn't run for more than a day, it now picks up all unprocessed daily notes in chronological order - not just today's.

### v0.4
- **Journal commentary**: after processing journal entries, Claude now generates commentary notes in `2_for-review/`. Each note includes observations, patterns from comparing your current thinking against the archive, and analysis to help you think the topic through further. Related entries are grouped into one holistic commentary; clearly different topics (e.g. business strategy vs personal life) get separate notes.

### v0.3
- **Journaling / thinking layer module**: optional module that creates living evergreen notes on topics you keep returning to. Each note has a current position, open questions, and an archive of previous thinking. Reflective content in daily notes gets routed here automatically during processing.

### v0.2
- CRM module, content pipeline module, and weekly reviews added as optional modules selected during setup interview.

### v0.1
- Initial release: vault structure, daily note processing, daily brief, task management, `/process-autopilot`, `/assimilate`.

---

## Hope this helps!

I'd love to hear your feedback if you end up using it.

**Nick Zervoudis**
nick@valuefromdata.ai

PS: You may be interested in the [free online community](https://community.valuefromdata.ai/join?invitation_token=e9039c67ffd40061d34499bffc67b7f222eface7-f78394af-0df8-4b2d-8b29-78306d8edf9b) I run for data & AI professionals interested in the strategic and non-technical side of data & AI work, and/or my [articles on Substack](https://blog.valuefromdata.ai/) and/or my [videos on YouTube](https://www.youtube.com/@nickzervoudis).
