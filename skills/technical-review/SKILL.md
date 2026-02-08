---
name: technical-review
description: "Use this skill when the user wants a technical leader's brief from meeting transcription notes. This extracts only technical and engineering content: architecture decisions, risks, action items, delegated tasks, dependencies, and metrics. Triggers include: 'technical review', 'tech brief', 'technical summary', 'tech leader brief', 'engineering summary'. The output is always in English and saved as a Markdown file."
---

# Technical Review

## Overview

This skill processes meeting transcription notes and produces a **technical leader's brief** — a focused, technical-only analysis in **English** designed for engineering leaders to quickly understand technical discussions, risks, action items, and decisions requiring follow-up.

Unlike the general meeting summary, this extracts and highlights only technical and engineering content.

## Workflow

### Step 1: Read the transcription

- If the user provides a file path, read the file.
- If the user pastes text directly, use that as the transcription.

### Step 2: Generate the technical leader's brief

Extract and analyze all technical content from the transcription. Generate a Markdown file with these sections (always in English):

1. **Technical Highlights** — extract every technical topic discussed: architecture decisions, system design, infrastructure, tooling, libraries, APIs, performance, security, tech debt, migrations, incidents, etc. For each item provide a detailed summary of what was said, arguments for and against, and any conclusion reached.

2. **Technical Risks & Concerns** — flag anything that could become a blocker, a scalability issue, a security risk, or technical debt. Include items that were raised but not resolved. Note who raised each concern if identifiable.

3. **My Action Items** — a checklist (`- [ ]`) of action items that are assigned to the tech leader, or that clearly require tech leadership involvement (approvals, reviews, architectural decisions, unblocking others). Include context for each item.

4. **Delegated Technical Tasks** — table with columns: Person, Task, Context, Deadline, Status — for technical tasks assigned to other team members that the tech leader should track.

5. **Decisions Requiring Follow-up** — any technical decision that was deferred, needs validation, or needs to be communicated to stakeholders. Include the reasoning discussed and what information is needed to finalize.

6. **Dependencies & Blockers** — cross-team or external dependencies mentioned, and anything currently blocking progress.

7. **Metrics & Data Points** — any numbers, benchmarks, SLAs, error rates, performance figures, or quantitative data mentioned during the meeting.

**Rules:**
- Focus exclusively on technical and engineering content; skip purely administrative or non-technical topics.
- Be specific — include service names, endpoint paths, library versions, metric values, or any concrete detail mentioned.
- The checklist in "My Action Items" must be copy-paste ready for a task tracker.
- The output is **always in English**, regardless of the meeting's original language.
- If there is no technical content in the meeting, still create the file with a single note stating that no technical topics were discussed.
- Omit sections that have no relevant content rather than leaving them empty.

### Step 3: Save the technical brief

- Save the file as `meeting-tech-brief-YYYY-MM-DD.md` where YYYY-MM-DD is today's date.
- Save in the current directory unless the user specifies a different location.
- Inform the user that the technical brief has been created and provide the file path.
