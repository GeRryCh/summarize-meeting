---
name: detailed-summary
description: "Use this skill when the user wants a detailed, comprehensive meeting summary that captures nearly every aspect of the discussion. Unlike the standard summarize-meeting skill which condenses to 10-20%, this skill preserves 50-70% of the original content. Triggers include: 'detailed summary', 'detailed meeting summary', 'full summary', 'comprehensive summary', 'detailed recap', or any request emphasizing that every detail matters. The summary is always written in the original language of the transcription. The output is saved to a file in the format the user specifies (docx, pdf, pptx, etc.)."
---

# Detailed Meeting Summary

## Overview

This skill processes meeting transcription notes and produces a **comprehensive, detailed** summary in the **original language of the meeting**. Unlike a standard summary, this captures nearly every aspect of the discussion — arguments, reasoning, alternatives considered, nuances, and context. It is designed for meetings where almost every detail matters (e.g., development planning, architecture reviews, sprint retrospectives, incident post-mortems).

## Workflow

### Step 1: Read the transcription

- If the user provides a file path, read the file.
- If the user pastes text directly, use that as the transcription.

### Step 2: Detect the language

Identify the language of the transcription from its content. All output **must** be written in that same language. Do not translate.

### Step 3: Produce the detailed summary

Generate a comprehensive summary with these sections (use section titles in the detected language):

1. **Meeting Title** — infer from context or use a descriptive title.
2. **Date & Participants** — extract if mentioned; omit if not available. If roles or teams are mentioned, include them next to each participant.
3. **Executive Summary** — 4-6 sentence high-level overview covering the meeting's purpose, main outcomes, and overall direction.
4. **Detailed Discussion Log** — this is the core section. For each topic discussed, create a subsection with:
   - **Topic title** as a subheading.
   - **Context / Background** — why this topic was raised, any prior context mentioned.
   - **Discussion** — a thorough account of the conversation: who said what, the arguments made, concerns raised, alternatives proposed, and how the discussion evolved. Preserve the reasoning and logic behind positions, not just conclusions. Use attributed points (e.g., "[Person] raised that...") when speakers are identifiable.
   - **Outcome** — what was decided, agreed upon, or left open for this topic.
5. **Decisions Made** — numbered list of every concrete decision reached, with a brief note on the reasoning behind each decision.
6. **Action Items** — table with columns: Responsible Person, Task, Context/Details, Deadline (if mentioned), Priority (if mentioned or inferable).
7. **Risks & Concerns Raised** — anything flagged as a risk, blocker, worry, or potential issue, along with who raised it and any proposed mitigation.
8. **Open Questions / Parking Lot** — questions that were asked but not answered, topics deferred to a future meeting, and items explicitly marked for follow-up.
9. **Key Quotes** — notable verbatim quotes that capture important positions, commitments, or context that would be lost in paraphrasing. Attribute each quote to the speaker if identifiable.
10. **Next Steps & Follow-up Schedule** — any scheduled follow-ups, next meeting dates, review checkpoints, or milestones mentioned.

**Rules:**
- **Be thorough** — aim for roughly 50-70% of the original transcription length. Capture the reasoning, not just the conclusions.
- Preserve the original meaning; do not add opinions or external information.
- Maintain attribution — when a speaker is identifiable, note who said or proposed what.
- Include dissenting opinions and minority views, not just the consensus.
- Capture numbers, dates, metrics, version numbers, service names, and any other concrete details verbatim.
- Use professional tone matching the formality of the original transcription.
- If the transcription is informal (e.g. Slack-style), maintain a slightly more structured but still approachable tone.
- Omit sections that have no relevant content rather than leaving them empty.

### Step 4: Save the main summary to file

- Ask the user for the desired output format if not already specified (docx, pdf, pptx, etc.).
- Use the corresponding document skill (e.g. the `docx` skill for .docx files, `pdf` skill for .pdf, `pptx` skill for .pptx) to create and save the file.
- Use a sensible default filename like `detailed-meeting-summary-YYYY-MM-DD.{ext}` unless the user specifies one.

#### Formatting requirements (especially for .docx)

The generated document must be professionally formatted. Follow the corresponding document skill closely and ensure:

- **Heading styles**: Use proper Word heading styles (`Heading1`, `Heading2`, `Heading3`) for all section titles and topic subsections — never plain bold text. This ensures headings appear in the navigation pane and Table of Contents.
- **RTL / Bidi support**: If the meeting language is RTL (Hebrew, Arabic, etc.), set `bidi: true` on every paragraph and text run, and set section-level `bidi: true`. Do not rely solely on right-alignment (`jc: right`) — that is not sufficient for proper RTL rendering.
- **Table of Contents**: Because the document is long, include a Table of Contents after the title block.
- **Styled title block**: The document title should be visually prominent (large font, color, centered) with a separator line underneath, followed by the date.
- **Bullet lists**: Use Word's built-in numbering system (`LevelFormat.BULLET`) — never insert unicode bullet characters manually.
- **Numbered lists**: Use Word's built-in numbering system (`LevelFormat.DECIMAL`) — never hardcode "1.", "2." as text.
- **Tables**: Use `WidthType.DXA` for all table and cell widths (never percentages). Include a styled header row (dark background, white text), cell padding/margins, and alternating row shading for readability.
- **Block quotes**: For the Key Quotes section, use indented, italicized paragraphs with a left border or shading to visually distinguish them.
- **Header and footer**: Include a running header with the document title (small, grey, italics) and a footer with page numbers.
- **Page breaks**: Insert page breaks before major sections (Detailed Discussion Log, Action Items, Key Quotes) to improve readability.
- **Font**: Use Arial as the default font (universally supported, good for both LTR and RTL).
