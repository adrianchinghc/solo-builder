---
name: automation-playbook
description: "Use this BEFORE advising on automation, removing the founder from operations, cron jobs, Zapier workflows, or building a business that runs without the founder. Trigger phrases: 'automate', 'remove myself', 'build robots', 'passive income', 'bus factor', 'hire contractors', 'delegate', 'productize'."
metadata:
  plugin: solo-builder
---

# Automation Playbook

## Why Automation Matters

The goal of automation is simple: **remove yourself from the equation.** Your product should generate revenue while you sleep, travel, or work on your next idea. Pieter Levels runs Nomads.com, Remote OK, and other properties with 700–2,000 automated scripts ("robots") running every day. His team page lists these robots alongside the few humans he works with. This is how one person outruns a team.

---

## What Is a "Robot"?

A robot is any task you used to do manually that you turned into a scheduled script. It runs every second, minute, hour, day, or week without you touching it.

**Examples of what robots can do:**
- Find cities popular among users → automatically organize meetups → post to Twitter and Slack 30/14/1 days before
- Scrape 100+ job boards → parse job listings → filter for remote-only → post to your job board → tweet the listing → email subscribers who want that job category
- Monitor server CPU, disk space, and error rates → SMS you immediately if anything breaks
- Screenshot pages → generate social share images with dynamic data overlaid
- Check if a user missed their goal deadline → email their accountability partner → charge their card if confirmed
- Log in to your telecom provider → download the monthly invoice → save as PDF → email to yourself → update your bookkeeping spreadsheet

You're not doing any of these. The robot does.

---

## The Golden Rule of Automation

**Only automate if the time saved > the time to build the automation.**

A task you do for 5 minutes once a month doesn't need to be automated. A task you do for 2 hours every day does. Rank your repetitive tasks by:
1. How much time they take per week
2. How simple they'd be to script

Start with the ones in the top-right quadrant (high time cost, easy to script). Don't spend 20 hours automating something that saves you 1 hour a year.

---

## Building Your First Robots

### Cron Jobs (For Developers)

A cron job is a scheduled script on your server. It's the backbone of automation.

```bash
# Run a PHP script every hour
0 * * * * php /srv/scripts/update-city-data.php >> /srv/logs/cron.log 2>&1

# Run every morning at 7am
0 7 * * * php /srv/scripts/send-daily-digest.php

# Run every minute (for real-time monitoring)
* * * * * php /srv/scripts/check-server-health.php
```

Use **Cronitor** to monitor whether your scheduled jobs actually run. If a cron job silently fails, you won't know until something breaks in production. Cronitor pings you if a job doesn't fire on schedule.

### Zapier (No-Code Automation)

Zapier connects web apps without code. A "Zap" is a trigger + action:

- **New Stripe payment** → Add row to Google Sheet + Send welcome email via MailChimp + Create Trello card for onboarding
- **New Typeform submission** → Email customer + SMS contractor + Log in Airtable
- **New RSS item in your niche** → Tweet it + Post to Slack

For non-developers, Zapier is effectively the robot builder. You can run a complex multi-step business on Zapier workflows without writing a single line of code.

---

## Monitoring: Know Immediately When Things Break

You can't fix what you don't know is broken. Set up monitoring before you automate anything else.

### UptimeRobot (Free)
- Checks your site every 5 minutes
- Alerts you by email, SMS, Slack, or Telegram if it goes down
- Shows uptime history and response times
- Free tier covers most indie products

### Page-Specific Monitoring
For each critical feature, set up a test that checks for an expected result:

Example: A robot opens `https://yoursite.com/cities?filter=safe+europe` and checks that "Amsterdam" appears in the results. If Amsterdam is missing, the filter is broken. You get an SMS.

This is more valuable than generic uptime monitoring — it catches silent failures where the site loads but the core feature is broken.

### Cronitor
Monitors whether your cron jobs actually executed. Not just whether the server is up, but whether the specific task ran and completed without errors.

---

## The Self-Help Dashboard

Every support ticket you answer manually is a failure of automation. Build a self-help dashboard that lets users:
- Cancel their account
- Get a refund
- Change their subscription plan
- Update their credit card
- Download their invoice

If users can solve these problems themselves at 2am, you don't get a support email. You don't hire a support person. The robot handles it.

---

## When You Do Need Humans

Some things aren't worth automating, or can't be fully automated. For those, use contractors — not employees.

**Lean contractor model:**

| Role | Structure | What they handle |
|---|---|---|
| Customer support | $2,500–4,000/month retainer | Edge cases the self-help dashboard can't handle |
| Dev on standby | $50–150/hour, invoice when used | Gets alerted by UptimeRobot when something breaks, fixes it without you |
| Bookkeeper / accountant | Monthly or quarterly | Transactions, taxes, compliance (mandatory once you hit $50K/year) |

**How to make contractors autonomous:**
- Give them access to all the tools they need (database, Stripe, email)
- Give them a clear process document for common situations
- Let robots route the right tasks to them automatically (a Zapier zap that detects a support ticket needing human review and creates a Trello card for the contractor)
- Pay them promptly — autonomous contractors who trust you require less management

---

## The Bus Test

> "If a particularly empowered individual in an organization is hit by a bus, will the organization suffer greatly? If yes, fail. If no, pass."

Your goal is to pass the bus test. Your business should be able to run for weeks without you before anyone notices.

**Setup for a bus-test-passing autonomous organization:**

1. Automate all repetitive scripts with cron jobs
2. Hire a dev on standby contract (ideally 2, so you have a backup)
3. Set up UptimeRobot alerts that page the dev directly
4. Hire a part-time contractor with access to payments to manage operations
5. Prepay your hosting and domain registrar 2–3 years in advance (Linode, Namecheap, Cloudflare) — so the site stays alive even if your credit card expires
6. Document everything that a human needs to do in a simple ops runbook

---

## AI Automation (The New Layer)

Since ~2022, AI has added a new dimension to automation. Processes that previously required a human because they needed language understanding or judgment can now be automated:

- **Content moderation:** LLMs that read user-submitted content and flag violations
- **Customer support:** AI that handles common support questions before escalating to a contractor
- **Data classification:** Vision models that categorize images, read receipts, or process documents
- **Content generation:** Auto-generating SEO-friendly city descriptions, job summaries, or product copy
- **Quality checks:** AI that reviews data inputs for anomalies before they hit the database

This creates the opportunity Pieter Levels describes as "the first billion-dollar company run by a single founder, with the help of millions of AI bots." Even if you don't go to a billion dollars, a one-person business running on AI automation can easily reach $1M+ ARR.

---

## Passive Income Is a Myth

Be honest with yourself: **passive income is compressed income.** You worked incredibly hard for 2–3 years to build something that now runs with 2 hours of maintenance per week. That's not passive — it's the payoff on compounded effort.

There will always be:
- Monthly situations that need your judgment
- Infrastructure that needs upgrading
- Competitors that force product improvements
- Tax and legal issues that need decisions

But the automation layer means those situations are exceptions, not your daily grind. And that gap — between the grind and the exceptions — is where you build your next product.

---

## Automation Priority Order

When your product starts making money, automate in this order:

1. **Monitoring first** — Know when things break before users do
2. **Payments and billing** — Refunds, upgrades, cancellations (self-service)
3. **Data collection** — Anything you're manually copying, importing, or exporting
4. **Notifications** — Alerts to users, contractors, yourself
5. **Content generation** — Social posts, emails, digests
6. **Reporting** — Weekly revenue/usage summaries to yourself

---

## Do This Today

Spend one week logging every task you do for your business. At the end of the week, circle the three tasks you did most often. For each one, ask: "Could a script or Zapier workflow do this instead?" If yes, build the automation this week.
