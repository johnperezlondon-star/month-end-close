# Month-End Close Tool

> AI-powered workflow automation for the finance close. Task board, checklist, timeline, analytics — GPT-4o writes the CFO status update.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python&logoColor=white)
![OpenAI](https://img.shields.io/badge/GPT--4o-OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-UI-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![Status](https://img.shields.io/badge/Status-Portfolio%20Ready-brightgreen?style=flat-square)

---

## The business problem this solves

The month-end close is one of the most stressful and poorly managed processes in any finance team:

- **No visibility** — the CFO doesn't know which tasks are blocked until it's too late
- **Status updates are manual** — someone spends 30 minutes every morning writing a close status email
- **Checklists live in Excel** — outdated by lunchtime, different versions for different people
- **Blockers go unescalated** — a task blocked on IT for two days quietly kills the D+5 deadline

This tool replaces all of that. One platform. Live task data. GPT-4o writes the status report. The CFO gets a professional update in under 10 seconds.

---

## Live demo

**[View the interactive UI demo →](app_demo.html)**

All four views fully functional. Task board pre-loaded with June 2024 close data. Click "Generate AI status" to see GPT-4o produce a CFO update from the live task data.

---

## Sample AI output

Given a task board with 3 blocked tasks and 7 in progress, GPT-4o produces:

> *The June 2024 month-end close is progressing with **16 of 28 tasks complete (57%)** as of **Day 4** of the 5-day close window. The overall position is at moderate risk — three tasks are currently blocked and require immediate management intervention to meet the **D+5** board pack deadline.*
>
> *The most critical blocker is the balance sheet reconciliation suite, overdue since D+3, awaiting a GL extract from IT. The revenue recognition journals are also blocked pending Legal sign-off on contract amendments — this item should be escalated to the General Counsel today...*

---

## Four views in one tool

| View | Purpose | Audience |
|------|---------|---------|
| Task board | Kanban with blocker notes | Finance team daily stand-up |
| Close checklist | Linear task list by close day | Individual task owners |
| Timeline | Gantt D+1 to D+7 | Controller / FC Lead |
| Analytics | Six-period trend data | CFO / Finance Director |

---

## Project structure

```
month-end-close/
├── data/
│   └── tasks.json              # Task definitions — editable per period
├── close_engine.py             # Task state management, period reset, blocker detection
├── ai_narrative.py             # GPT-4o status generation
├── email_engine.py             # Email dispatch to CFO (SMTP or SendGrid)
├── slack_notifier.py           # Slack webhook notifications
├── app.py                      # Streamlit multi-view UI
├── requirements.txt
├── .env.example
└── README.md
```

---

## Quickstart

### Step 1 — Install Python
Download from [python.org](https://python.org/downloads). Tick "Add Python to PATH" during installation.

### Step 2 — Download and open terminal in folder
Download ZIP → unzip → open terminal in the folder.

### Step 3 — Install packages
```bash
pip install streamlit openai pandas python-dotenv
```

### Step 4 — Add your OpenAI API key
Rename `.env.example` to `.env` and add:
```
OPENAI_API_KEY=sk-your-key-here
```

### Step 5 — Run the app
```bash
streamlit run app.py
```

---

## Task data format

Tasks are defined in `data/tasks.json`. Each task has:

```json
{
  "id": "T001",
  "title": "Bank reconciliation",
  "owner": "Sarah M.",
  "category": "Reconciliations",
  "due_day": 2,
  "priority": "High",
  "status": "complete",
  "blocker_note": null,
  "dependencies": []
}
```

To configure for your team: edit `tasks.json` with your own task list, owners, and due days. The rest of the tool adapts automatically.

---

## How the AI status works

The `generate_status()` function in `ai_narrative.py`:

1. Reads all tasks from the current state
2. Groups by status (complete / in progress / blocked / not started)
3. Extracts blocker notes and identifies overdue items
4. Sends a structured summary to GPT-4o with a prompt specifying CFO audience, formal tone, and 3-paragraph structure
5. Returns the narrative — ready to paste into an email or Slack

The prompt uses temperature 0.3 for consistent, professional output and always leads with blockers — because that's what the CFO cares about.

---

## Email and Slack integration

`email_engine.py` sends the AI-generated status via SMTP (or SendGrid). Configure recipient, subject, and schedule in `.env`.

`slack_notifier.py` posts to a Slack channel via webhook. Set `SLACK_WEBHOOK_URL` in `.env`. Can be triggered manually from the UI or run on a schedule.

---

## Requirements

```
streamlit>=1.28
openai>=1.0
pandas>=2.0
python-dotenv>=1.0
```

---

## Roadmap

- [ ] ERP integration — auto-pull task completion from SAP/Oracle journal status
- [ ] Automated daily status email at 9am via scheduler
- [ ] Dependency mapping — block Task B automatically when Task A is blocked
- [ ] Multi-period comparison — compare June close with May and April
- [ ] Teams integration alongside Slack

---

## Skills demonstrated

| Area | What this project shows |
|------|------------------------|
| Finance process | Month-end close workflow, D+n scheduling, blocker management, CFO communication |
| AI / prompt engineering | GPT-4o status generation, blocker-first narrative, escalation recommendations |
| Product thinking | Four views for four different stakeholders from one data model |
| Python / Streamlit | Task state management, period reset logic, multi-tab UI |
| Integrations | Email dispatch, Slack webhooks |

---

## About

Third project in a Finance AI portfolio. The first two tools (Variance Analyser and Reconciliation Tool) focus on data automation. This one focuses on process automation — a different skill set that completes the picture.

*Part of a 3-project portfolio:*
- [Variance Analyser](https://johnperezlondon-star.github.io/variance-analyser/)
- [Reconciliation Tool](https://johnperezlondon-star.github.io/recon-ai/)
- [Month-End Close Tool](https://johnperezlondon-star.github.io/month-end-close/) ← you are here

*Connect on [LinkedIn](#) · GitHub: [johnperezlondon-star](https://github.com/johnperezlondon-star)*

---

## Licence

MIT — free to use, adapt, and build on.
