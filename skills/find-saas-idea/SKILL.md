---
name: find-saas-idea
description: Use when the user asks "find me a SaaS idea," "what should I build," "research a profitable niche," "give me app ideas," "find a startup idea," "I want to build something but don't know what," "find an underserved market," or any open-ended request for product opportunities. Triggers a multi-phase autonomous research pipeline across 10 demand-signal sources, clusters findings into candidate problems, scores them against audience-free distribution and 90-day revenue feasibility, and returns a ranked shortlist with evidence citations.
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# Find SaaS Idea

## Core principle

Generate ideas from demonstrated buyer behavior, never from founder intuition. Every recommendation must trace back to a primary-source signal where money is already changing hands, time is being wasted on workarounds, or buyers are explicitly asking for a solution that doesn't exist. Score for *distribution-solvable* opportunities over technically-interesting ones — for a no-audience founder targeting 90-day revenue, the binding constraint is reaching the first 10 paying customers, not the build.

## Grounding Principles

Before mining signals, anchor your search in these principles:

**1. Build in proven categories, not novel ones.** Every idea surfaced by this skill should have existing paying customers somewhere. If nobody is paying for anything in this space, treat it as a yellow flag. Novel markets require education budgets and long sales cycles — both are fatal for a 90-day revenue target.

**2. Apply domain knowledge where you have it.** If you deeply understand a specific industry, workflow, or pain point, bias your search there. Domain expertise compounds into competitive advantage — you'll build a better product, speak the buyer's language, and spot signals others miss.

**3. The four-filter pre-screen.** Before committing to deep research on any direction, apply this quick filter:
- Would I use this myself? (If yes, you're your own first user and QA tester)
- Can I see it already works somewhere? (Look for products with paying customers, not just idea threads)
- Are those products acquiring customers without massive marketing spend? (True organic demand, not manufactured)
- Is it simple enough to maintain as a solo dev or tiny team?

**4. Validate through behavior, not opinions.** Community comments, template purchases, job postings, and competitor reviews reveal what people actually do. Surveys and "would you use this?" questions reveal what people say they would do. This skill mines behavior signals, not opinion signals.

**5. Be wary of API dependency.** An idea whose core value is entirely dependent on a third-party API (especially an LLM API) carries platform risk. The provider can change pricing, deprecate endpoints, or ship the feature themselves. Identify what the defensible layer is before building.

**6. You don't need to love the idea.** Passion helps with persistence. But market demand, distribution clarity, and unit economics matter more. A boring idea in a profitable niche beats an exciting idea with no clear path to the first 10 customers.

## When to invoke

Trigger phrases the user might say: "find me a SaaS idea," "what should I build," "research a niche," "find a profitable product idea," "underserved market," "validated startup idea," "what app should I build," "I have no idea what to build."

Do NOT trigger when the user has already identified a specific idea and wants validation — that's `validate-saas-idea`. Do NOT trigger when they want MVP scope — that's `scope-mvp`.

## The signal stack

This skill mines ten distinct signal sources, ranked by predictive value for 90-day revenue. Each source answers a different question about buyer behavior. Detailed mining instructions for each are in `references/signal-sources.md` — load that file once when starting the research pass.

| # | Signal | What it proves | Weight |
|---|--------|----------------|--------|
| 1 | Paid-but-painful (G2/Capterra/Trustpilot 2-3⭐) | WTP confirmed, execution gap | 1.0 |
| 2 | Workaround templates (Notion/Etsy/Gumroad bestsellers) | Buyer drew the MVP spec themselves | 1.0 |
| 3 | Search whitespace (high-volume queries, weak SERPs) | Demand without commercial supply | 0.9 |
| 4 | Community-stated unmet need (subreddit / Discord / IH forum) | Explicit verbal demand | 0.7 |
| 5 | Dead competitor archaeology (ProductHunt graveyard) | Validated problem, failed execution | 0.8 |
| 6 | Regulatory / platform-shift windows | Forced demand with deadline | 0.9 |
| 7 | Expert-validated friction (industry-specific forums) | Niche pain from practitioners | 0.8 |
| 8 | Job-posting demand (LinkedIn / Indeed) | Buyer has budget, problem is recurring | 0.9 |
| 9 | Support-burden patterns (marketplace help forums) | Captive audience with billing relationship | 0.8 |
| 10 | Adjacent-vertical drift (proven horizontal → niche vertical) | Pattern transfer with reduced risk | 0.7 |

## The 5-phase workflow

Execute phases in order. Use the TodoWrite tool to create a todo per phase before starting. Dispatch parallel subagents within Phase 1 since the signal sources are independent.

### Phase 1: Signal harvesting (parallel)

Read `references/signal-sources.md` first for the exact queries, sites, and techniques per source.

Dispatch one subagent per signal source via the Agent tool, all in a single message for parallelism. Each subagent receives:
- The seed (if user provided one: a domain, vertical, or constraint; if not: "open" — mine across categories)
- The specific source it owns (e.g., "G2 2-3 star reviews in B2B project management category")
- Output format: structured list of raw complaints/signals with primary-source URL and verbatim quote where possible

Subagents return raw signals. Do not let them cluster or score — that happens centrally in Phase 2.

### Phase 2: Clustering and theme extraction

Aggregate all raw signals into a single working set. Cluster by *problem*, not by *source*. A complaint on G2 about "no way to track recurring tasks across projects" and a $29 Notion template called "Recurring Task Tracker for PM Teams" are the same problem from two angles — they corroborate, not duplicate.

A cluster needs at least 3 corroborating signals from at least 2 different source types to qualify as a candidate problem. Single-source signals get parked in a `weak-signals.md` working file for later review but do not advance to scoring.

For each qualifying cluster, write a one-paragraph problem statement in the buyer's own language, with cited evidence (URLs + verbatim quotes).

### Phase 3: Cross-cutting filter pass

Apply the four filters to every candidate problem. Drop any that fail any filter. See `references/scoring-rubric.md` for the exact pass/fail criteria.

1. **Willingness-to-pay**: Is anyone already paying for an adjacent or inferior solution? Required: ≥1 named competitor or template with evidence of paid transactions. If the answer is "nobody pays for anything here," this is a yellow flag — proceed only with a specific defensible reason (e.g., new regulatory requirement creating forced demand).

2. **Audience-free reachability**: Can the first 100 customers be reached in under 30 days through a *named, public, non-audience-dependent* channel? Required: name the specific subreddit, Slack community, conference, LinkedIn cohort filter, directory, or marketplace category. "Run paid ads" does not count — that requires capital and skill. "Cold email a list of 500 dental practices scraped from Google Maps" does count.

3. **Hair-on-fire urgency**: Is this problem in the buyer's top 3 priorities? Test: do complaint quotes use urgent language ("nightmare," "every day," "losing money," "can't ship," "blocking me")? Mild language ("would be nice," "kinda annoying") fails this filter.

4. **Hidden-incumbent identification**: What do buyers use today? Excel? A VA? Manual process? Another SaaS? Required: name the actual incumbent and identify the specific failure mode you would exploit. "Build a better X" without naming X is automatic fail.

### Phase 4: Scoring and ranking

For each candidate that survived Phase 3, compute a composite score per `references/scoring-rubric.md`. The rubric weights:
- Signal strength (weighted sum across the 10 sources, normalized 0-10)
- Distribution clarity (0-10, based on specificity of the channel named in filter #2)
- Build feasibility for a solo technical founder using AI tooling, 90-day horizon (0-10)
- Defensibility against the named incumbent (0-10)
- Recurring-revenue fit — does the problem recur such that subscription billing is natural? (0-10)

Composite = weighted average. Surface the top 5 candidates regardless of absolute score, but flag any with composite < 6.0 as "borderline — present for awareness, not recommendation."

### Phase 5: Output

For each of the top 3 candidates, produce a structured idea card with these exact sections, in this order:

1. **One-sentence pitch** in the form "X for Y who can't Z." Specific. No buzzwords. No "AI-powered" unless AI is the literal product.
2. **The buyer** — role, company size/segment, what they're doing today, where they congregate online.
3. **The pain quote** — verbatim from one of the source signals, with citation.
4. **Evidence stack** — bulleted list of all corroborating signals across sources, with URLs. Minimum 3 sources, ideally 5+.
5. **Existing incumbent** — what they use today, why it fails them.
6. **WTP signal** — price points of adjacent paid solutions, with citations.
7. **Distribution path** — named channel(s) for first 100 customers, with specific tactics.
8. **Why this works for no-audience founder** — explicit defense of the audience-free reachability claim.
9. **Composite score** — with breakdown by dimension.
10. **Kill criteria** — what would cause you to walk away from this idea after a week of deeper validation. Be specific.

After the top 3, list candidates 4-5 with a single-line summary each.

End the response with a single explicit recommendation: which idea to take to `validate-saas-idea` next, and why.

## Quick reference

```
TRIGGER → Read signal-sources.md → Dispatch 10 parallel subagents (one per source)
        → Aggregate → Cluster (≥3 signals, ≥2 sources) → Apply 4 filters
        → Score per rubric → Top 5 ranked → Top 3 with full cards → Recommend next step
```

## Common mistakes to avoid

Generating ideas without primary-source citations. Every claim must have a URL. If you cannot cite, do not include.

Letting "I think this is a good idea" leak into the output. The skill's job is to surface what the data says, not what you'd find clever. Subjective adjectives ("exciting," "innovative," "huge market") are forbidden in idea cards.

Recommending ideas that require an audience. A consumer app requiring virality, a creator tool requiring an influencer launch, or a developer tool requiring a Show HN moment all fail filter #2. Suppress these even if the signal is strong.

Confusing signal source overlap with signal corroboration. If three different G2 reviews say the same thing, that's one source × three data points, not three sources. The ≥2-source rule means ≥2 different *source types* (review site + community + template marketplace, etc.).

Anchoring on a single seed when the user said "open." If the user explicitly said no category preference, intentionally diversify the harvest — at least three different broad domains (B2B SaaS, vertical SaaS, prosumer, professional services tooling, e-commerce infrastructure).

Skipping the kill criteria section to look more confident. Honest kill criteria make the recommendation stronger, not weaker.

## Red flags — STOP and re-run

- Idea card has fewer than 3 cited sources
- Distribution path says "social media" or "content marketing" without naming a specific channel and tactic
- Composite score is invented rather than computed from the rubric
- Recommended idea requires a personal audience the user does not have
- All five candidates came from the same signal source
