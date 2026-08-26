# Automation Engineering

Documenting my journey into automation engineering — building workflows, connecting APIs, and learning software fundamentals to solve real-world operational bottlenecks.

## Background
Junior AI Automation Developer based in South Africa, building toward remote automation engineering work while growing Nova Draft, my automation practice. Started after seeing repetitive manual processes firsthand while managing operations at a car wash.

## What I'm building
- n8n workflow automation (lead capture, scoring, routing)
- API integrations (Slack, Gmail, Google Sheets, Resend)
- Multi-tenant database architecture (Postgres/Supabase)
- Python fundamentals (FNB App Academy)

## Log
Entries below, most recent first.

---
---

### Self-Hosted n8n Migration & Lead Capture Automation

Built a full lead-capture automation: a webhook receives form submissions, scores each lead hot/warm/cold based on message content, then routes to Slack, email, and Google Sheets depending on score.

Midway through, my n8n Cloud trial expired, forcing a full migration to a self-hosted instance on Railway (Postgres + n8n containers). Every credential had to be rebuilt from scratch:

- **Slack** — created a Slack App, configured Bot Token Scopes, installed it to the workspace, invited the bot into the target channel.
- **Google Sheets** — set up a Google Cloud Console project, configured the OAuth consent screen, and resolved an "ineligible test user" error caused by a stray typo in my email.
- **Email delivery** — hit `ECONNREFUSED` and `ENETUNREACH` errors trying to send via Gmail SMTP. Root cause: Railway blocks outbound SMTP ports by default (common anti-spam measure on cloud hosts). Fixed by switching to the Resend API (HTTPS-based, not blocked).

One stubborn bug: a Filter node kept discarding valid leads no matter how I configured the condition (tried `exists`, `is not empty`, direct field references). Eventually gave up on the visual node and moved the same validation logic into the Code node instead — a good reminder that sometimes a code workaround beats fighting a UI node.

**What I learned:** infrastructure constraints (blocked ports, expired trials, encryption keys not persisting across restarts) often cause more debugging time than the actual logic does. Documenting the root cause — not just the fix — makes the next migration faster.

## Certifications
- n8n Level 1 Certified

![n8n Level 1 Certificate](./certificates/n8n-level-1.png)

