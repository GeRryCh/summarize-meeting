---
name: summarize-meeting
description: "Use this skill when the user wants to summarize a meeting from transcription notes, meeting minutes, or recorded transcript text. Triggers include: any mention of 'meeting summary', 'summarize meeting', 'meeting notes', 'transcription summary', 'meeting recap', or requests to produce a summary from a transcript. The summary is always written in the original language of the transcription. The output is saved to a file in the format the user specifies (docx, pdf, pptx, etc.) using the appropriate document skill."
---

# Meeting Summarization

## Overview

This skill processes meeting transcription notes and produces a structured, professional summary in the **original language of the meeting**. The result is saved to a file using the format requested by the user.

## Workflow

### Step 1: Read the transcription

- If the user provides a file path, read the file.
- If the user pastes text directly, use that as the transcription.

### Step 2: Detect the language

Identify the language of the transcription from its content. All output **must** be written in that same language. Do not translate.

### Step 3: Produce the summary

Generate a structured summary with these sections (use section titles in the detected language):

1. **Meeting Title** — infer from context or use a descriptive title.
2. **Date & Participants** — extract if mentioned; omit if not available.
3. **Executive Summary** — 2-4 sentence high-level overview.
4. **Key Discussion Points** — bulleted list of main topics discussed, with brief context for each.
5. **Decisions Made** — numbered list of concrete decisions reached during the meeting.
6. **Action Items** — table with columns: Responsible Person, Task, Deadline (if mentioned).
7. **Open Questions / Next Steps** — anything unresolved or scheduled for follow-up.

**Rules:**
- Keep the summary concise — aim for roughly 10-20% of the original transcription length.
- Preserve the original meaning; do not add opinions or external information.
- Use professional tone matching the formality of the original transcription.
- If the transcription is informal (e.g. Slack-style), maintain a slightly more structured but still approachable tone.
- Omit sections that have no relevant content rather than leaving them empty.

### Step 4: Save the main summary to file

- Ask the user for the desired output format if not already specified (docx, pdf, pptx, etc.).
- Use the corresponding document skill (e.g. the `docx` skill for .docx files, `pdf` skill for .pdf, `pptx` skill for .pptx) to create and save the file.
- Use a sensible default filename like `meeting-summary-YYYY-MM-DD.{ext}` unless the user specifies one.

#### Formatting requirements (especially for .docx)

The generated document must be professionally formatted. Follow the corresponding document skill closely and ensure:

- **Heading styles**: Use proper Word heading styles (`Heading1`, `Heading2`, etc.) for all section titles — never plain bold text. This ensures headings appear in the navigation pane and Table of Contents.
- **RTL / Bidi support**: If the meeting language is RTL (Hebrew, Arabic, etc.), set `bidi: true` on every paragraph and text run, and set section-level `bidi: true`. Do not rely solely on right-alignment (`jc: right`) — that is not sufficient for proper RTL rendering.
- **Styled title block**: The document title should be visually prominent (large font, color, centered) with a separator line underneath, followed by the date.
- **Bullet lists**: Use Word's built-in numbering system (`LevelFormat.BULLET`) — never insert unicode bullet characters manually.
- **Numbered lists**: Use Word's built-in numbering system (`LevelFormat.DECIMAL`) — never hardcode "1.", "2." as text.
- **Tables**: Use `WidthType.DXA` for all table and cell widths (never percentages). Include a styled header row (dark background, white text), cell padding/margins, and alternating row shading for readability.
- **Header and footer**: Include a running header with the document title (small, grey, italics) and a footer with page numbers.
- **Page break**: Insert a page break before the Action Items table if the document is long enough.
- **Font**: Use Arial as the default font (universally supported, good for both LTR and RTL).

### Step 5: Generate the Tech Leader brief (.md)

**Always** create an additional Markdown file alongside the main summary. This file is a personal brief for the technical leader.

Filename: `meeting-tech-brief-YYYY-MM-DD.md` (same date as the main summary), saved in the same directory.

The tech brief must **always be written in English**, regardless of the meeting's original language. This ensures it is universally readable across technical teams and tools.

The file must contain these sections (in English):

1. **Technical Highlights** — extract every technical topic discussed: architecture decisions, system design, infrastructure, tooling, libraries, APIs, performance, security, tech debt, migrations, incidents, etc. For each item provide a short summary of what was said and any conclusion reached.
2. **Technical Risks & Concerns** — flag anything that could become a blocker, a scalability issue, a security risk, or technical debt. Include items that were raised but not resolved.
3. **My Action Items** — a checklist (`- [ ]`) of action items that are assigned to the tech leader, or that clearly require tech leadership involvement (approvals, reviews, architectural decisions, unblocking others). If no name is mentioned but the task implies tech leadership responsibility, include it.
4. **Delegated Technical Tasks** — table with columns: Person, Task, Notes — for technical tasks assigned to other team members that the tech leader should track.
5. **Decisions Requiring Follow-up** — any technical decision that was deferred, needs validation, or needs to be communicated to stakeholders.

**Rules for the tech brief:**
- Focus exclusively on technical and engineering content; skip purely administrative or non-technical topics.
- Be specific — include service names, endpoint paths, library versions, metric values, or any concrete detail mentioned.
- The checklist in "My Action Items" must be copy-paste ready for a task tracker.
- If there is no technical content in the meeting, still create the file with a single note stating that no technical topics were discussed.
