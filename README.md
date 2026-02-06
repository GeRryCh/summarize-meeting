# summarize-meeting

A Claude Code plugin that summarizes meeting transcription notes and exports them to docx, pdf, pptx, or other file formats.

## Features

- **Automatic language detection** — the summary is written in the original language of the transcription
- **Structured output** — executive summary, key discussion points, decisions, action items, and open questions
- **Tech leader brief** — automatically generates a separate `.md` file with technical highlights, risks, your personal action items as a checklist, and delegated tasks to track
- **Flexible export** — delegates to preinstalled document skills (docx, pdf, pptx, etc.)

## Installation

Install via the Claude Code plugin manager or load locally:

```bash
claude --plugin-dir ./summarize-meeting
```

## Usage

Invoke the command inside Claude Code:

```
/summarize-meeting:summarize-meeting path/to/transcript.txt
```

Or simply provide transcription text and ask Claude to summarize the meeting — the skill triggers automatically.

## Plugin Structure

```
summarize-meeting/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── summarize-meeting.md
├── skills/
│   └── summarize-meeting/
│       └── SKILL.md
└── README.md
```

## License

MIT
