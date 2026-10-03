# AI Email Intelligence & Scheduling Agent

A self-hosted AI automation system that analyzes incoming emails, extracts actionable information such as deadlines and events, creates Google Calendar entries, and delivers scheduled mobile notifications.

## Overview

This project combines n8n, Gmail, an LLM, Google Calendar, and ntfy to turn important emails into structured actions and reminders.

### Architecture

```text
Gmail
  ↓
Gmail Trigger
  ↓
Get Full Email
  ↓
AI Agent + Groq LLM
  ↓
Structured JSON Extraction
  ↓
Deadline Detection
  ↓
Google Calendar
  ↓
Scheduled Reminder Workflow
  ↓
ntfy Mobile Notification
```

## Main Workflows

### 1. Email Intelligence

`workflows/email-intelligence.json`

The workflow:

- Detects newly received Gmail messages
- Retrieves the full email content
- Uses an LLM to classify and extract useful information
- Produces structured JSON
- Detects whether a deadline exists
- Creates a Google Calendar event for deadlines

Extracted fields include:

- Category
- Importance
- Summary
- Action required
- Action
- Deadline date
- Deadline time
- Event title
- Event date
- Event time
- Reply requirement

### 2. Deadline Reminder

`workflows/deadline-reminder.json`

The reminder workflow:

- Runs on a daily schedule
- Checks Google Calendar for the following day's events
- Identifies deadline events
- Sends a formatted mobile notification through ntfy

Example notification:

```text
📌 AI/ML Innovation Hackathon
📅 04 Oct 2026
⏰ 10:00 PM
```

## Technologies

- n8n
- Docker
- Gmail API
- Google Calendar API
- Groq LLM
- ntfy
- WSL2
- Windows

## Self-Hosted Setup

The project uses Docker Compose to run n8n locally.

```bash
docker compose up -d
```

n8n is exposed locally on port `5678`.

> Credentials are intentionally not included in this repository. Configure your own Gmail, Google Calendar, and Groq credentials inside n8n.

## Workflow Import

Import the JSON files from the `workflows/` directory into your n8n instance.

After importing, configure your own:

- Gmail OAuth credential
- Google Calendar OAuth credential
- Groq API credential
- ntfy topic

The public workflow exports use placeholders instead of personal account information.

## Security

Do not commit:

- API keys
- OAuth client secrets
- passwords
- n8n credential data
- personal notification topics
- private account information
- n8n runtime data

The `.gitignore` file excludes local n8n runtime data.

## Project Structure

```text
ai-email-intelligence-agent/
├── README.md
├── docker-compose.yml
├── .gitignore
└── workflows/
    ├── email-intelligence.json
    └── deadline-reminder.json
```

## Future Improvements

- Daily email digest
- Priority-based notifications
- Duplicate deadline detection
- Natural-language queries
- Countdown reminders
- Separate event and deadline handling
- Richer notification formatting

## License

This project is provided as an educational and portfolio project.
