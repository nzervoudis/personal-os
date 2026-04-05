---
type: retrospective
created: 2026-02-26
---

## The Origin Story: Building a Personal OS with Claude Code

This is the real account of how this system came to be - reconstructed from the actual conversation logs of the first three weeks (8-26 February 2026). It's part field notes, part build log, part "here's what I learned." All quotes are verbatim.

---

## Night Zero: The Architecture Session (8 Feb, midnight)

The first session started just after midnight on a Saturday. The vault was essentially blank - two meeting transcripts, an idea note, and two briefing documents prepared by asking Claude Desktop to summarise earlier conversations. Those briefs contained the *context* (business profile, CRM needs, how the day-to-day works) but deliberately excluded the *solution* - the idea was to get fresh eyes on the architecture.

> "There are some things that are still fairly set in my mind, like the fact that I want to use Obsidian and the fact that I want to use the Obsidian daily note concept as my inbox where I kind of do a raw dump of thoughts during the day and then that gets processed and refined."
>
> "Besides that, I've tried to exclude things so that I can get your input on what we should be building."

Claude read the briefs and came back with what would become the system's thesis:

> "The biggest leverage in this system isn't the vault structure - it's the **processing loop**. The vault structure mostly needs to stay out of your way. The real value is: (1) Capture is effortless, (2) Processing is automated but human-approved, (3) The system accumulates context over time, (4) Proactive nudging actually reaches you."
>
> "The CRM brief reinforces this - the problem isn't 'where do I store contact info,' it's 'things quietly slip when I'm busy and no system nags me effectively.'"

The structure got shaped with practical corrections:

> "My CRM would not be just people, it would also be companies, and there would be specific opportunities that are a link between people and companies."

And on projects:

> "There should definitely be a folder with projects. In a way, there's a lot of over time things that start as pipeline items will become projects. Now projects are not just my billable projects. There's also things that are more ongoing. For example, my data product management community."

Then came the discipline that would define the whole build:

> "Anyway, perhaps what it would make sense is to not really think about this very much yet until we've done the interviews. And then after that, you can give me a recommendation around next steps."

Don't over-plan. Interview first, build after. A seven-step game plan was agreed: Interview, CLAUDE.md upgrade, CRM seed, daily processing test, post-meeting processing test, automate, Slack nudging. "Steps 1-5 are the Sunday target. 6-7 can come during the week."

The last message before bed:

> "That sounds good. Can you also put this game plan in the 2026-02-08 daily note that I've created just so I have it there as well?"

The system's first heartbeat - a plan written into a daily note at 2am.

---

## Day One: The Big Build (8 Feb, morning to evening)

Woke up and immediately started trying to wire up more integrations - Gmail, Google Calendar. Discovered they weren't available as MCPs for Claude Code (only the web version). That got parked. Then the real work began.

Went for a walk with the interview questions Claude had prepared, came back around midday, and dropped what would later be described as:

> "Okay, so I've just added a shitload of things in today's daily note."

The daily note was a massive voice dump - everything that had been living in a human head or scattered across other tools, dictated via Wispr Flow in one go. The kind of raw, stream-of-consciousness input that would become the system's signature:

- Contacts and follow-ups from the last two months ("check if email was sent to [person]", "intro [person A] to [person B]")
- Content ideas for LinkedIn, Substack, and guest articles
- CRM context: who works where, what the relationship is, what the next step should be
- Project statuses: a client KYC project, a community migration, an infographics course
- Notes migrated from a previous vault - markdown files and screenshots that needed sorting into the right folders
- Conference information to pull from Notion
- A whole description of the current LinkedIn drafting workflow

The instruction was clear:

> "I want you to make sure you go through everything and, basically, have some kind of action against each thing. When I say action, I mean action for you, so it might be action to create or update an existing note, it might be to ask me follow-up questions, it might be to create a todo, and so on."

Claude presented 45 numbered actions for approval. Corrections came back fast - factual fixes, folder naming preferences, structural decisions:

> "Anytime I mention an article, these are not LinkedIn posts. They fall under either Substack or guest articles. So under content, we should have LinkedIn, Substack, and guest articles for now. Another subfolder under content would be DPM community webinars. And another subfolder would be YouTube."

### Lessons through friction

Every major convention emerged from something going wrong.

**The H1 rule.** Claude created a daily note with `# 2026-02-08` at the top:

> "Because I view my notes in Obsidian, the file title acts as the #h1. So keep that in mind when creating notes - right now '2026-02-08' appears twice for me, because it's both the title and the h1."

**The sacred space rule.** Claude overwrote raw notes when updating the daily note:

> "Ok also, you replaced the other text in my daily note - please restore it. Once you've done that, I will use the top of the note (above any AI-written content) as my 'raw' working notes dump. Make sure to never replace that during the day - only when it's time to 'process' the note or if I explicitly ask you to."

**The tone calibration.** After Claude signed off with "Enjoy the walk":

> "'Enjoy the walk.' comes across as a bit passive aggressive - let's go for a warmer (but not too bubbly) tone please."

**The batch approval pattern.** Claude kept asking for permission one file at a time:

> "I'd like for you instead of me approving these one by one for giving me a full list of actions I want you to execute and for me to then approve them all at once."

**The parallel execution insight.** Claude was sequentially fetching web pages, asking for permission each time:

> "It's quite annoying that I'm waiting for you to do some processing, and then you ask me 'Hey, can I fetch this article?' And then I look away, and then you ask to fetch another article. I'd rather you know, I'd look away, and you've got 15 minutes worth of work to do, not 5 seconds, because then I need to be on top of you constantly."

### The Notion breakup

The decision to leave Notion came mid-conversation, almost casually but completely decisive:

> "Go to my Notion CRM where I have a pipeline list of companies list of people also ingest that in so that we can switch to Markdown as our single source of truth because I don't want to keep using Notion."

By the end of the day: 70 people notes, 37 company notes, 18 opportunity notes, 6 conference notes - all pulled from Notion via MCP. Content folder structure created. System files drafted. Projects folder set up. Temp folder from the old vault fully migrated and deleted.

The vault went from nearly empty to 130+ files in a single afternoon.

### The token limit discovery

Claude also discovered that background agents couldn't get interactive permission approval - all four parallel agents launched for the big build failed. Everything had to be done in the foreground. And importing a single full meeting transcript consumed the entire context window.

The reaction was practical:

> "It's a little bit concerning that you hit your token limit just from importing one meeting transcript. Could it be that there is a more efficient way to do it?"

The answer was a Python script - the first time the system reached for code rather than pure LLM processing.

---

## Day Two: From Dump to System (9 Feb)

By Sunday, the system was already being used for real work. After a call with a prospective client, the vault was used to draft a follow-up email - pulling in links, community invitations, personalised context. When the first draft came back too rigid:

> "I didn't really like the summary you give at the start it felt very rigid I want to go for something warmer and it can be shorter as well."

Granola (a meeting notes tool) was connected alongside Otter, starting the pattern of pulling transcripts from multiple sources.

Then came the meta-moment - stepping back to assess what had been built:

> "In the to-dos for the Personal OS, I want your honest assessment of what's been done so far, what else is left to achieve the objectives that we discussed I had for my Personal OS, and to surface any gaps. I also want your input on how we should prioritize. How can I start getting value out of this Personal OS sooner than later? In effect, I'm expecting you to act as both a product manager for this and an engineering lead."

And when Claude suggested a daily processing dry run:

> "I think we've actually already done a version of the daily note processing dry run because you've already taken what was in my February 8th notes and out of that you've created to-dos and a lot of other things."
>
> "Honestly, even if the daily note remains a chaotic mess full of half-baked thoughts, I'm okay with it as long as the more refined version of all those make their way to the right place. In a way, it's not dissimilar to a bronze/ silver / gold layer of a data warehouse."

There it is - the data warehouse analogy. The daily note is the raw/bronze layer. Processing extracts and refines into silver. The CRM, task notes, content pipeline - those are the gold layer. The person who builds data products for a living was building one for himself.

---

## The Next Two Weeks: Iteration and Evolution

The system was live and being used for real work from day two. But the architecture kept evolving - sometimes through deliberate design, more often through discovering what didn't work.

### Token economics (11 Feb)

An early attempt to maximise the daily token budget:

> "Is there a way for you to auto-wake yourself at 5am my time? I'll be asleep but I want the token usage window to start then (rather than at 9am when I start working)"

This was the first sign of treating Claude Code as a finite resource to be optimised - a theme that would recur. The initial setup auto-scanned the vault on every session start, burning ~10% of the daily allowance before any real work began. That got replaced with opt-in commands.

### Tasks: from one page to a whole folder (12 Feb)

The system started with a single `TODOs.md` file - a flat markdown list. Within days it was obvious this didn't scale. The trigger was catching Claude adding inline checkboxes to a planning document:

> "I am concerned you are adding to-do's in a Markdown file like that. As we've said, all to-do's need to be in the tasks folder. What we need here is links to those to-do's."

By 12 Feb, the task system had been migrated to individual task notes in `tasks/`, each with YAML front matter (status, due date, owner, area). The inspiration came partly from studying how Teresa Torres structured her own personal OS:

> "I took some notes on Teresa Torres' Personal OS methodology. I really like how she maintains separate context files for different domains and they are in her global CLAUDE.md and for project CLAUDE.md files and can be referenced as and when they're needed. So for example, if we're on a writing task, you can go into a writing style guide."

65+ task notes and 7+ idea notes were migrated out of the old flat list - a proper task management system emerged, with planning documents *linking to* task notes rather than containing checkboxes.

### The two-document setup (14 Feb)

The daily note kept accumulating both raw input and Claude's structured summaries in the same file. It was getting messy. The fix was splitting into two documents:

> "What I want is to keep the Daily Note a dump of my thoughts and I want you to create the Daily Brief. So that means migrate things like 'Top Priorities', 'Do Today', 'Follow Ups' and so on into the Daily Brief."
>
> "Do tell me if you think there is a purpose in also trying to condense or summarize the Daily Note. If it's helpful to you, helpful to me. I don't think for me it's that helpful."

The result: `daily-brief.md` (Claude-maintained dashboard with priorities, tasks, questions, follow-ups) and daily notes (raw scratch pad, never touched by Claude). The daily brief became the system's main interface - a structured view of the day updated in real time.

### Process commands: autopilot and on-screen (14 Feb)

The processing workflow needed two modes - one for when the user is at the keyboard, one for when they walk away. After considering various names (including some Star Trek-inspired options):

> "I love the Star Trek suggestions. I think what I'd rather do is we call both process. And one is process autopilot. The other is process on screen. Because otherwise I'm going to forget what they're called. There's no way I'll remember helm and start using helm. It's also a bit ambiguous as to what it entails. I want function over form with these things."

The two commands share a core workflow but diverge on interaction: `/process-onscreen` pauses for approval and asks questions in the terminal; `/process-autopilot` runs everything autonomously and puts questions in the daily brief for later.

The same conversation established that the core processing logic should live in a shared file, not be duplicated across commands:

> "I don't mind having a single source of truth for the majority of the process using instructions, in the sense that I want to avoid a situation where we make updates only to process on screen, but actually it's on core bits that should be part of the process autopilot workflow as well."

### Fresh vs. stale (14 Feb)

With more items accumulating in the review folder, a simple innovation:

> "I'm conscious that there's a lot of things that are in flight that maybe have been in the in-flight folder for a while. So let's split that section of the daily brief into two parts: fresh things, and things that have been ready to review for two days."

This created the stale-item pattern - anything in the review folder for 2+ days gets flagged separately so it's visible but doesn't crowd out fresh work.

### Auto-content: 25 articles in one night (14-15 Feb)

One of the more ambitious experiments. After connecting course transcripts, office hours recordings, and lightning lesson recordings:

> "Based on everything you know about my business, I want you to do some really in-depth work. Put it in a new project folder called 'auto-content'. What I want you to do is draft 25 articles that I can put on my Substack that are based off the ideas that I write and teach about."

Claude generated 68 candidate topics, narrowed to 25, then drafted all 25 articles in batches of 5 using parallel agents. The session burned through multiple context windows (auto-compacting and continuing several times) but produced 25 draft articles in a single overnight session.

(I haven't posted any of them, but some are quite good - I did give Claude Code access to my whole [ROI of Data & AI course](https://maven.com/nick-zervoudis/dpm-value-course/?utm_source=personalos) after all 😉)

### Weekly reviews (16 Feb)

Pipeline tracking prompted the first structured review:

> "Maybe one thing we can think about is having a weekly or monthly review of achievements, not briefs, but more like an inverse of it. Like, here's the key things we achieved this week."
>
> "Another thing I want to start tracking is the number of new B2B prospects that I either reach out to or have an initial conversation with or that I sent a proposal to."

Weekly reviews became auto-created on the first Sunday processing run - wins, pipeline activity, content output, and areas to improve. The first review (W07) covered a week that included a new client accelerating, a partnership secured, and course validation from a 10* student review.

### Guest article for a major publication (16-18 Feb)

A guest article opportunity tested the system's ability to support a real creative workflow - from pitch to draft, using course transcripts as source material, respecting specific editorial guidelines (1,000-1,300 words), and iterating on positioning:

> "I think his audience tends towards more technical people, but he also has a very wide reach. I want you to suggest a few different articles, keeping in mind all the constraints mentioned in the page above."

---

## What Emerged

### Design principles (discovered, not planned)

1. **Voice-first, ADHD-native.** The entire input method was dictated via Wispr Flow. Stream-of-consciousness dumps, corrections mid-sentence. The system had to tolerate messy input and produce clean output.

2. **Learning through friction.** Every convention came from something going wrong - the H1 rule, the sacred space rule, the tone calibration, the batch approval pattern. Not designed upfront, earned through use.

3. **Function over form.** Pragmatic over elegant, every time. Simple markdown lists over Obsidian Bases tables. Manual categorisation over complex metadata schemas. When Claude went down a research rabbit hole about Obsidian plugins:

   > "Look, you've been asking me to read a million different documents around Obsidian bases. I don't think you need to do this much research. Tell you what, park this for now."

4. **The Notion breakup was inevitable.** The vault started as a complement to Notion but became the replacement within hours. Once you have an AI that can read, write, and search markdown files, a separate SaaS tool for CRM is friction, not value.

5. **Execute, don't plan.** The system was built by using it, not by designing it. The daily processing workflow was "tested" by processing a real day's notes. The CRM was "seeded" by importing real contacts for real follow-ups.

### The human-AI collaboration pattern

From the very first session, the roles were clear:
- **Nick**: source of truth, decision-maker, raw input via voice
- **Claude**: organiser, executor, drafter, nudger

Nick dumps thoughts. Claude structures them. Nick corrects. Claude adjusts. The asymmetry was established on night zero and has held ever since.

### What the Personal OS actually is

It's not a note-taking system. It's not a CRM. It's not a task manager. It's a **data product** - built by someone who builds data products - where the raw input is a human life (calls, thoughts, commitments, ideas, relationships) and the output is structure, follow-through, and nothing slipping through the cracks.

---

## Timeline Summary

| When | What happened |
|------|-------------|
| **8 Feb 00:25** | Founding session. Architecture agreed in under 2 hours. Seven-step game plan. Bed at 2am. |
| **8 Feb morning** | MCP integration attempts (Gmail/Calendar - parked). Walk with interview questions. |
| **8 Feb afternoon** | The Big Build. 130+ files created. Notion CRM fully migrated. System files drafted. Content structure created. |
| **8 Feb evening** | First real daily note processing. Webinar planning. Meeting transcript conventions established. Token limits discovered. |
| **9 Feb** | System used for real work (client follow-up email). Granola connected. Meta-assessment: "act as both a product manager and an engineering lead." |
| **10-11 Feb** | Daily processing loop operational. Email drafting, CRM updates, LinkedIn post drafts - all running through the vault. Token optimisation begins. |
| **12 Feb** | Tasks migrated from single page to individual notes in `tasks/`. Teresa Torres' methodology adopted for context files. Personal OS planning file created. |
| **14 Feb** | Two-document setup (daily brief + daily note). Process commands created (`/process-autopilot`, `/process-onscreen`). Fresh vs. stale review items. 25 Substack articles drafted overnight. |
| **16 Feb** | First weekly review. B2B pipeline tracking. First `/process-autopilot` run. |
| **16-18 Feb** | Guest article project. Course transcript organisation. System files fleshed out as context documents. |

---

## Looking Back

The whole thing was built in a weekend. Not planned for months, not spec'd out in a project plan. A blank vault, a 2am architecture session, and a "shitload of things" dumped into a daily note.

Three weeks later, it processes daily notes, manages a B2B pipeline, drafts emails, tracks community webinars, maintains a CRM of 70+ people, and runs weekly reviews. The CLAUDE.md has been rewritten half a dozen times. The folder structure has been renamed twice. The processing workflow has been through at least four iterations.

But the core thesis from night zero still holds: the biggest leverage isn't the vault structure - it's the processing loop.
