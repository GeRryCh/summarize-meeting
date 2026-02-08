---
description: Interactive meeting summarization workflow with optional technical review
---

# Start Meeting Summary Workflow

This is an interactive workflow that guides the user through summarizing a meeting and optionally generating a technical leader's brief.

## Workflow

### Step 1: Read the transcription

- If the user provides a file path or pasted text via "$ARGUMENTS", use that as the transcription.
- If no transcription is provided, ask the user to provide a file path or paste the transcription text.
- Keep the full transcription content available for reuse in later steps.

### Step 2: Ask which summary type

Present the user with a choice:

1. **Standard summary** — concise, covers the key points (10-20% of the original length)
2. **Detailed summary** — comprehensive, captures nearly every aspect of the discussion (50-70% of the original length)

Wait for the user to choose before proceeding.

### Step 3: Generate the chosen summary

- If the user chose **(1) Standard**, use the **summarize-meeting** skill with the transcription.
- If the user chose **(2) Detailed**, use the **detailed-summary** skill with the transcription.

Complete the summary and save it to a file before moving on.

### Step 4: Ask about technical review

After the summary is saved, ask the user:

> Would you also like a technical leader's brief? This creates a separate English `.md` file with technical highlights, risks, action items, dependencies, and metrics.

Wait for the user to respond.

### Step 5: Generate technical review if requested

- If the user says **yes**, use the **technical-review** skill with the same transcription.
- If the user says **no**, thank them and end the workflow.
