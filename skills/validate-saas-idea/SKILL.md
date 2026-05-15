---
name: validate-saas-idea
description: Use when the user has a specific SaaS or app idea in hand and asks "is this a good idea," "validate this idea," "pressure test this," "should I build this," "find competitors," "check the market for this idea," or shares a one-line product concept and wants a rigorous gut-check before they invest build time. Runs a structured 60-90 minute deep-validation pass that goes further than find-saas-idea on a single candidate: surveys named competitors, estimates TAM, models unit economics, identifies the first 100 customers, and outputs a binary build / don't-build recommendation with kill criteria.
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# Validate SaaS Idea

## Core principle

A find-saas-idea output is a hypothesis. Validation is the deeper pass that tries to *kill* the hypothesis before code is written. The goal is not to confirm the idea — confirmation bias is the default failure mode. The goal is to surface, in 60-90 minutes of focused research, every reason the idea might fail, and then make an honest call.

Most validation passes fail because they ask "is there a market?" The correct question is "*who specifically* would buy this in week one, *where* are they, and *what specifically* are they paying for it today?" If those three questions can't be answered with named entities and citations, the idea is not validated.

## When to invoke

Trigger phrases: "validate this idea," "is this idea good," "pressure test this concept," "should I build this," "check the market for [idea]," "what do you think of this idea: [pitch]." Also invoke automatically as the next step after `find-saas-idea` produces a ranked shortlist and the user picks one.

Do NOT invoke when the user is still in idea-exploration mode (no specific candidate) — that's `find-saas-idea`. Do NOT invoke after validation has produced a build recommendation and the user wants implementation — that's `scope-mvp`.

## Inputs required before starting

Confirm the user has provided:
1. **One-sentence product description** — "X for Y who can't Z." If vague, ask once to crystallize.
2. **Hypothesized buyer** — role, segment, vertical. If absent, derive from the description and confirm.
3. **Pricing hypothesis** — even a rough range ($X-Y per month, freemium, usage-based, one-time). If absent, ask.

If any input is missing, ask once via AskUserQuestion. Do not proceed with vague inputs — validation depends on specificity.

## The 6-phase validation pass

Use TodoWrite to create a todo per phase. Execute in order.

### Phase 1: Competitor mapping

Map the entire landscape, not just direct competitors. There are four layers:

- **Direct competitors** — purpose-built tools for the same problem and segment
- **Indirect competitors** — generic horizontal tools the buyer is using today (Excel, Notion, Airtable, a VA, a generic SaaS)
- **Adjacent solutions** — tools that solve a related problem and could expand into this one
- **Failed competitors** — products that tried and shut down (see find-saas-idea signal #5)

For each named competitor, capture: name, URL, pricing (public price points only), positioning statement (from their homepage), funding stage if known, last meaningful update (proxy for life signs). 5-15 competitors is the right target. Fewer suggests poor research; more suggests the category is crowded.

If you cannot find 3+ named competitors or generic-tool incumbents in 30 minutes of search, the market is either too new (validate demand more aggressively) or non-existent (kill the idea).

### Phase 2: Demand evidence

Re-run a focused version of the find-saas-idea signal stack against this specific idea. You're looking for:

- Active complaints about the named direct/indirect competitors (paid-but-painful, signal #1)
- Templates / workarounds that match this problem (signal #2)
- Search queries the buyer would type to find this (signal #3)
- Community posts where someone literally asks for this product (signal #4)

Quantify where possible. "G2 has 47 reviews of [Competitor] in the last 6 months mentioning 'X is missing'" is a real signal. "There seems to be demand" is not.

If you cannot find at least 5 specific demand signals across at least 2 source types, demand is not validated. Stop and report.

### Phase 3: Unit economics model

Build a 12-month projection with realistic numbers. Use these defaults unless the user provides better data:

- **CAC**: For cold outreach to SMB, assume $50-150 fully-loaded. For paid acquisition, assume $200-800. For marketplace listings, assume $30-100 once ranked.
- **ARPU**: From the user's pricing hypothesis. Reality-check against named competitors.
- **Gross margin**: 80-90% for pure SaaS; lower if AI inference is a unit cost (model that explicitly — e.g., $0.50-2.00/user/month in inference costs for moderate AI usage).
- **Churn**: Assume 5-8% monthly for SMB without proven retention, 2-4% for established niches with high switching cost.
- **Sales cycle**: 0-14 days for self-serve <$50/mo, 14-45 days for $50-500/mo with human touch, 45-90+ days for $500+/mo.

Compute:
- LTV = ARPU × Gross Margin / Monthly Churn
- LTV:CAC — required ≥3:1, ideally ≥5:1
- Payback period — required <12 months, ideally <6
- Path to first $10K MRR — how many customers × ARPU, over what timeline

If LTV:CAC < 3:1 with realistic inputs, the business model is broken. Either pricing must go up, churn must drop (defensible reason?), or CAC must drop (named channel?). If none of these can be defended, kill the idea.

### Phase 4: First 100 customers — named

The most important phase. Generic claims like "we'll do content marketing" or "reach out on LinkedIn" fail.

Required output: a list of *named, reachable* prospects sufficient to plausibly produce the first 10 paying customers. Specifically:

- If the channel is a marketplace: identify the exact marketplace category, count current listings, and estimate the realistic share of category traffic a new listing can capture.
- If the channel is a community: name the specific subreddit/Slack/Discord with member count, post velocity, and rules around self-promotion.
- If the channel is cold outreach: build (or describe how to build in <1 week) a list of ≥500 named prospects. Source must be specific (e.g., "scrape NYC + LA + Chicago dental practices from Google Maps; filter for 3+ Google reviews; ~2,400 prospects expected").
- If the channel is SEO: identify 5-10 long-tail keywords with monthly search volume between 100-1000 each, weak SERPs, and a realistic ranking timeline.

If none of these can be specified, the idea fails on distribution regardless of demand strength. This is the most common failure point and the one most worth being honest about.

### Phase 5: Risk and kill-criteria identification

Surface the top 5 risks. For each, articulate (a) what would make this risk fatal, (b) what early signal would warn you, (c) what the kill criterion is.

Standard risks to evaluate:
- **Distribution risk** — channel doesn't actually work at hypothesized CAC
- **Willingness-to-pay risk** — buyers want it but won't pay enough
- **Build risk** — MVP takes 2x estimate
- **Incumbent response risk** — large incumbent ships your feature
- **Regulatory risk** — compliance burden you missed
- **Market size risk** — TAM is too small for $10K MRR even at 100% capture
- **Founder-market fit risk** — you can't credibly speak to the buyer

Honest kill criteria look like: "If after sending 200 cold emails over 3 weeks we haven't booked 10 discovery calls, the distribution hypothesis is dead." Not "if it doesn't work, we'll pivot."

### Phase 6: Build / don't-build call

Synthesize Phases 1-5 into a binary recommendation.

**BUILD** if:
- Demand evidence is strong and specific (Phase 2 cleared)
- LTV:CAC ≥ 3:1 with realistic inputs (Phase 3 cleared)
- First 100 customers have a named path (Phase 4 cleared)
- No catastrophic risk without a mitigation plan (Phase 5)

**DON'T BUILD** if any of the above is unresolved. Don't soften this. The cost of a "weak yes" is months of wasted build time.

**MAYBE — with conditions** if 3 of 4 are cleared and the 4th has a concrete cheap-to-test mitigation (e.g., "buy a list and send 50 cold emails this week; if reply rate is >5%, build").

## Output structure

Produce a single validation report with these sections:

1. **Idea restated** — one sentence, refined from the user's input
2. **Verdict** — BUILD / MAYBE / DON'T BUILD, in bold, on its own line
3. **Headline reasoning** — 2-3 sentences explaining the verdict
4. **Competitor landscape** — table of 5-15 named competitors with pricing and positioning
5. **Demand evidence** — bulleted, with primary-source URLs
6. **Unit economics** — table with CAC, ARPU, gross margin, churn, LTV, LTV:CAC, payback
7. **First 100 customers plan** — specific channel, specific prospects, specific tactics
8. **Top 5 risks with kill criteria** — table format
9. **What would change the verdict** — for MAYBE: the test to run; for DON'T BUILD: what conditions would make it BUILD; for BUILD: what signals would mean stop
10. **Recommended next step** — if BUILD, suggest invoking `scope-mvp`; if MAYBE, name the specific test; if DON'T BUILD, suggest re-running `find-saas-idea` with a refined seed

## Quick reference

```
INPUTS → Phase 1 (competitors) → Phase 2 (demand) → Phase 3 (economics)
       → Phase 4 (first 100) → Phase 5 (risks) → Phase 6 (verdict)
       → Report → Next step
```

## Common mistakes to avoid

Confirmation bias. The user invested emotional energy in the idea. The skill's job is to be the honest skeptic they wouldn't otherwise hear. If you find yourself defending the idea, restart Phase 5 risks.

Hand-waving the first-100 plan. "We'll do outbound" is not a plan. "Scrape Google Maps for dental offices in NYC, LA, Chicago, filter to practices with 3+ Google reviews, expect ~2,400 prospects, send a 3-email sequence with practice-specific opener" is a plan.

Optimistic churn assumptions. Without proven retention, assume the high end of the churn range. Lower it only when you have evidence.

Ignoring AI inference unit costs. If the product requires significant inference per user (e.g., agent runs, document processing), this is COGS and must be modeled. A 90% gross margin SaaS becomes a 60% gross margin SaaS quickly with naive AI usage.

Confusing TAM with serviceable market. The TAM may be billions; the realistic 90-day-revenue market is the slice you can reach through your named channel.

Soft verdicts. "It could work if everything goes right" is not a verdict. Force yourself to BUILD / MAYBE / DON'T BUILD.

## Red flags — STOP and report DON'T BUILD

- Cannot name 3+ competitors or incumbents in 30 minutes of search
- Cannot find 5+ demand signals across 2+ source types
- LTV:CAC < 3:1 with realistic inputs and no defendable lever to fix it
- First 100 customer plan reduces to "content marketing" or "social media" without specifics
- Idea requires the founder to have an audience they don't have
- Idea requires changing buyer behavior or category-creating (long, expensive)
