---
name: saas-metrics
description: "You MUST invoke this before advising on SaaS metrics, dashboards, churn, MRR tracking, LTV, CAC, cohort analysis, or runway. Use before answering 'what metrics should I track?', 'is my churn bad?', 'how do I calculate LTV?', or 'what does my dashboard need?'"
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# SaaS Metrics Playbook

## The Rule: Metrics Should Drive Decisions

Only track metrics you will act on. A dashboard with 40 metrics is noise. At each stage, 3–5 numbers tell you nearly everything you need to know.

---

## Stage-Based Priority Metrics

### Pre-Revenue / 0 to $1K MRR

You have no data yet. Proxy metrics only.

| Metric | What it tells you |
|--------|------------------|
| Signups per week | Is anyone showing up? |
| Activation rate (hit the "aha moment") | Are people getting value? |
| Free-to-paid conversion rate | Do people think it's worth paying? |
| Time to first value (TTFV) | Is onboarding working? |

**Decision rule**: If activation rate is <20%, fix onboarding before spending on growth.

---

### Early ($1K–$10K MRR)

| Metric | Target / Benchmark |
|--------|-------------------|
| MRR | Track weekly. Growth rate matters more than number |
| Net MRR growth rate | >10%/mo = on track; <5%/mo = something's broken |
| Churn rate (monthly) | <5%/mo for SMB; <2%/mo for mid-market |
| Activation rate | >40% is healthy; below means onboarding problem |
| Support ticket volume | Leading indicator of product gaps |

**What to ignore**: LTV, CAC, payback period — too little data to be meaningful.

**Decision rule**: If MRR is flat 2 months in a row, check churn first, then acquisition second.

---

### Growth ($10K–$50K MRR)

| Metric | Target / Benchmark |
|--------|-------------------|
| Net MRR growth rate | >15%/mo to compound meaningfully |
| Monthly churn | <3%/mo (higher = you're filling a leaky bucket) |
| NRR (Net Revenue Retention) | >100% = expansion > churn; this is the holy grail |
| CAC by channel | Which channel acquires cheapest? |
| CAC payback period | <12 months for sustainable growth |
| LTV | Must be >3x CAC or the unit economics don't work |
| Activation rate by cohort | Are newer cohorts activating better? |

**Decision rule**: If NRR <100%, fix retention before scaling acquisition. Every marketing dollar is partially wasted while customers churn faster than you acquire.

---

### Scale ($50K+ MRR)

| Metric | Why it matters |
|--------|---------------|
| ARR | Annual view smooths out noise |
| Logo churn vs revenue churn | Losing small customers hurts less than losing big ones |
| NRR by segment | Which customer size retains best? |
| CAC by channel, by cohort | Channels degrade over time — watch for it |
| LTV by acquisition channel | Some channels bring better customers |
| Runway | Months until zero — know this number always |
| Gross margin | SaaS should be 70%+; if not, understand why |

---

## Core Metric Definitions

### MRR (Monthly Recurring Revenue)

**Formula**: Sum of all active subscription revenue normalized to monthly

- Monthly plans: price × customers
- Annual plans: annual price ÷ 12 × customers
- Do NOT include one-time payments (setup fees, consulting) in MRR

**MRR Movements to track separately:**
- **New MRR**: Revenue from new customers
- **Expansion MRR**: Upgrades, upsells, seat additions from existing customers
- **Contraction MRR**: Downgrades from existing customers
- **Churned MRR**: Revenue lost from cancellations
- **Net New MRR** = New + Expansion − Contraction − Churned

### Churn Rate

**Logo churn** (customer count): Customers lost ÷ customers at start of period

**Revenue churn** (MRR): MRR lost from cancellations ÷ MRR at start of period

**Net Revenue Retention (NRR)**: (Starting MRR + Expansion − Contraction − Churn) ÷ Starting MRR

NRR >100% means existing customers are growing your revenue even with no new acquisitions. This is the most important retention metric.

**Churn benchmarks by segment:**
| Segment | Good monthly churn |
|---------|-------------------|
| SMB (<$500/mo ACV) | <5% |
| Mid-market ($500–$5K/mo ACV) | <2% |
| Enterprise (>$5K/mo ACV) | <1% |

### CAC (Customer Acquisition Cost)

**Formula**: Total sales + marketing spend ÷ new customers acquired (same period)

Track CAC by channel separately — blended CAC hides what's working.

| Channel | Typical CAC range |
|---------|------------------|
| Organic / SEO | Low ($50–$500) but slow |
| Content + PLG | $100–$1K |
| Paid (Google/Meta) | $200–$2K |
| LinkedIn outbound | $500–$5K |
| Sales-assisted | $1K–$20K+ |

### LTV (Lifetime Value)

**Simple formula**: ARPU ÷ Monthly churn rate

Example: $100/mo ARPU, 3% monthly churn → LTV = $100 ÷ 0.03 = $3,333

**LTV:CAC ratio benchmarks:**
- <1:1 = losing money on every customer
- 1:1–3:1 = marginal; need to fix before scaling
- 3:1+ = healthy; scale
- 5:1+ = may be underinvesting in growth

### CAC Payback Period

**Formula**: CAC ÷ (ARPU × gross margin)

This tells you how many months until a customer recoups their acquisition cost.

**Benchmarks:**
- <6 months = very strong
- 6–12 months = solid
- 12–18 months = acceptable if churn is low
- 18+ months = risky; cash-intensive

### Runway

**Formula**: Cash in bank ÷ monthly burn rate

Burn rate = cash out − cash in per month

Always know your runway. Update it monthly. 12+ months is comfortable; under 6 is danger territory.

---

## Cohort Analysis

Cohort analysis shows how groups of customers acquired in the same period behave over time. It separates signal from noise.

### Revenue Cohorts (Most Important)

Group customers by acquisition month. Track their MRR each month after signup.

What to look for:
- **Flattening curve** = customers who stay are staying long-term (good)
- **Continuous decline** = customers keep churning; product isn't sticky
- **Rising curve** = expansion revenue; customers grow their spend (best case)

If month-6 revenue from a cohort is >80% of month-1, retention is strong.
If month-6 is <50% of month-1, you have a serious retention problem.

### Activation Cohorts

Group by signup week. Track what % reach the activation event (e.g., created first project, connected integration, invited teammate).

If recent cohorts are activating at lower rates than older ones, something changed (pricing, messaging, product, audience quality).

---

## Building Your Dashboard

### What to Build at Each Stage

**0–$10K MRR: Spreadsheet is fine**
- Track MRR, new MRR, churned MRR, and customer count weekly in a Google Sheet
- You don't need software yet — complexity obscures the signal at this stage

**$10K–$50K MRR: Add a metrics tool**
- Baremetrics, ChartMogul, or ProfitWell connect directly to Stripe
- Auto-calculate MRR movements, churn, NRR, and cohorts
- Set up weekly email digests; don't check obsessively

**$50K+ MRR: Segment by plan and channel**
- LTV and CAC by acquisition channel
- NRR by customer segment (SMB vs mid-market vs enterprise)
- Monthly finance review: P&L, runway, gross margin

### Dashboard Anti-Patterns

- **Vanity metrics**: Signups, page views, DAU without conversion context
- **Blended CAC**: Hides which channels are efficient
- **Ignoring NRR**: MRR growth that masks rising churn is a ticking clock
- **Over-engineering early**: Waiting for "the right tool" before tracking anything

---

## When to Act on Metrics

| Signal | Action |
|--------|--------|
| Churn spike (>20% above baseline) | Customer interviews this week. Don't guess. |
| Activation rate drops 2 weeks in a row | Check if a recent change broke onboarding |
| CAC rising for a channel | Pause spend. Investigate audience saturation or copy fatigue |
| NRR drops below 100% | Prioritize retention over acquisition immediately |
| Runway <6 months | Reduce burn or start fundraising/revenue push now |
| LTV:CAC >5:1 | You're underinvesting in growth — accelerate spend |

---

## Common Mistakes

- Tracking MRR as cash received (include annual subs normalized to monthly)
- Counting free trial users in churn denominator (only count paying customers)
- Ignoring expansion revenue — upsells can offset churn entirely
- Running ads without knowing CAC payback period
- Confusing revenue churn with logo churn (a big customer churning is not the same as a small one)
- Optimizing for gross MRR growth while ignoring NRR — growth can be hollow
