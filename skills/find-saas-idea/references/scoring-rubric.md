# Scoring Rubric

Apply this rubric to every candidate that survived the four cross-cutting filters in Phase 3. Compute the composite score from the five dimensions below, each scored 0-10, with the specified weights.

## Dimension 1: Signal strength (weight 0.25)

Sum the source weights from `signal-sources.md` for every source where this problem has at least one corroborating signal. Normalize:
- 0-1.5 raw → score 2
- 1.6-3.0 → score 4
- 3.1-4.5 → score 6
- 4.6-6.0 → score 8
- 6.1+ → score 10

A score of 10 requires signals from at least 6 of the 10 sources.

Bonus +1 (cap at 10): if the problem appears in both #1 (paid-but-painful) and #2 (workaround templates) — these two together are the strongest possible combination.

## Dimension 2: Distribution clarity (weight 0.30)

Highest-weighted dimension because distribution is the binding constraint for a no-audience founder targeting 90-day revenue.

| Score | Criterion |
|-------|-----------|
| 10 | Marketplace channel exists where buyers actively search (Shopify App Store, Salesforce AppExchange, Notion Templates, etc.) and competition is winnable |
| 8 | Specific community with ≥1000 active members where direct, non-spammy participation is the channel (specific subreddit, Slack, Discord) AND a named cold outreach list of ≥500 prospects is available |
| 6 | Either community OR cold outreach is solid but not both; or distribution requires a 30-60 day content effort |
| 4 | Distribution depends on SEO that will take 3-6 months to rank |
| 2 | Distribution requires paid ads as the primary channel |
| 0 | Distribution requires an existing audience the founder doesn't have |

Anything scoring 4 or below should not be in the top 3 regardless of other dimensions.

## Dimension 3: Build feasibility (weight 0.20)

For a solo technical founder with AI tooling, 90-day MVP horizon.

| Score | Criterion |
|-------|-----------|
| 10 | MVP shippable in 2-3 weeks. Single-page web app + database + Stripe. No real-time, no integrations beyond auth. |
| 8 | MVP in 4-6 weeks. Standard CRUD plus one external API integration. |
| 6 | MVP in 6-10 weeks. Multiple integrations, moderate domain complexity, or significant UX work. |
| 4 | MVP in 10-12 weeks. Heavy domain logic, regulatory complexity, or platform-specific (e.g., native mobile required). |
| 2 | Requires >12 weeks even with AI tooling. Complex algorithms, ML training, multi-sided marketplace, deep platform integrations. |
| 0 | Requires capabilities the founder doesn't have (e.g., hardware, FDA approval, marketplace liquidity from day one). |

## Dimension 4: Defensibility against incumbent (weight 0.10)

Lowest-weighted dimension for a 90-day revenue target because defensibility matters more at month 18 than month 3. But filter out completely undefendable plays.

| Score | Criterion |
|-------|-----------|
| 10 | Incumbent is Excel / manual / VA. Switching from Excel to a tool is a one-way door for the buyer. |
| 8 | Incumbent is a generic horizontal SaaS (Notion, Airtable). Vertical specialization is your wedge — incumbent won't follow because the segment is sub-scale for them. |
| 6 | Incumbent is a vertical-specific SaaS with poor UX or 10+ year-old tech. Modern UX is your wedge. |
| 4 | Incumbent is a well-funded modern competitor; your wedge is a specific feature gap. |
| 2 | Incumbent is dominant and well-executed; your wedge is price. |
| 0 | No clear wedge. |

## Dimension 5: Recurring-revenue fit (weight 0.15)

Does the problem recur such that monthly subscription billing is natural?

| Score | Criterion |
|-------|-----------|
| 10 | Daily or weekly use. Workflow tool, monitoring tool, CRM, dashboard. Subscription is obvious. |
| 8 | Use 2-4 times per month with ongoing value (compliance reports, monthly close, weekly planning). |
| 6 | Use 1-2 times per month or seasonal. Retention requires re-engagement. |
| 4 | Use a few times per year. Subscription model fights against use pattern; one-time / usage billing more natural. |
| 2 | One-time use. Subscription not viable. |

A score of 4 or below means revisit the business model — could be one-time + service, marketplace, or transaction fee instead of subscription. Doesn't disqualify but changes the math.

## Composite score

`Composite = (D1×0.25) + (D2×0.30) + (D3×0.20) + (D4×0.10) + (D5×0.15)`

Bands:
- 8.0+ → Strong recommendation
- 6.5-7.9 → Recommended with caveats
- 5.0-6.4 → Borderline; surface but flag explicitly
- <5.0 → Drop

## Tie-breakers

If two candidates score within 0.3 of each other, prefer in this order:
1. Higher distribution clarity (D2) score
2. Higher recurring-revenue fit (D5) score
3. Higher signal strength (D1) score
4. Lower build feasibility (D3) score (faster to ship = revenue sooner)

## Honesty check

Before finalizing scores, ask: would a skeptical investor give this candidate this score given the evidence presented? If your score is more generous than the evidence supports, lower it. Inflated scores in service of "having a recommendation" defeat the purpose of the rubric.
