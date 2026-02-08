---
description: Generate a technical leader's brief from meeting transcription
---

# Technical Review

Read the meeting transcription provided by the user (file path or pasted text via "$ARGUMENTS"), then use the **technical-review** skill to produce a technical leader's brief.

This creates a Markdown file with technical highlights, risks, action items, delegated tasks, and decisions requiring follow-up. The output is always in English, regardless of the meeting's original language.

The file is saved as `meeting-tech-brief-YYYY-MM-DD.md` in the current directory unless the user specifies a different location.
