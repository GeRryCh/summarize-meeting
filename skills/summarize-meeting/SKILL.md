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

### Step 4: Save to file

- Ask the user for the desired output format if not already specified (docx, pdf, pptx, etc.).
- Use the corresponding document skill (e.g. the `docx` skill for .docx files, `pdf` skill for .pdf, `pptx` skill for .pptx) to create and save the file.
- Use a sensible default filename like `meeting-summary-YYYY-MM-DD.{ext}` unless the user specifies one.
