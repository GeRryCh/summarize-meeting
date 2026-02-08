# summarize-meeting

A Claude Code plugin that summarizes meeting transcription notes and exports them to docx, pdf, pptx, or other file formats.

## Features

- **Automatic language detection** — the summary is written in the original language of the transcription
- **Standard & detailed modes** — concise summary (10-20%) or comprehensive summary (50-70%) of the original
- **Tech leader brief** — optional standalone technical review with highlights, risks, action items, dependencies, and metrics
- **Interactive workflow** — the `/start` command guides you through choosing summary type and optional technical review
- **Flexible export** — delegates to preinstalled document skills (docx, pdf, pptx, etc.)

## Installation

Install via the Claude Code plugin manager or load locally:

```bash
claude --plugin-dir ./summarize-meeting
```

## Commands

| Command | Description |
|---|---|
| `/start` | Interactive workflow — choose summary type, then optionally add a technical review |
| `/summarize-meeting` | Standard concise summary (10-20% of original length) |
| `/detailed-summary` | Comprehensive detailed summary (50-70% of original length) |
| `/technical-review` | Technical leader's brief only (English `.md` file) |

## Usage

**Interactive workflow (recommended):**

```
/start path/to/transcript.txt
```

**Direct standard summary:**

```
/summarize-meeting path/to/transcript.txt
```

**Direct detailed summary:**

```
/detailed-summary path/to/transcript.txt
```

**Technical review only:**

```
/technical-review path/to/transcript.txt
```

Or simply provide transcription text and ask Claude to summarize the meeting — the skill triggers automatically.

## Plugin Structure

```
summarize-meeting/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── start.md
│   ├── summarize-meeting.md
│   ├── detailed-summary.md
│   └── technical-review.md
├── skills/
│   ├── summarize-meeting/
│   │   └── SKILL.md
│   ├── detailed-summary/
│   │   └── SKILL.md
│   └── technical-review/
│       └── SKILL.md
└── README.md
```

## License

MIT
