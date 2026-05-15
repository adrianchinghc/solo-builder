# Design: Mobile App Skills — `find-mobile-app-idea` + `aso` + Audit

**Date:** 2026-05-15  
**Status:** Approved

---

## What we're building

Two new skills and an audit report for the `solo-builder` Claude Code plugin. Target user: solo technical founder, AI-build-fluent, no personal audience, 90-day revenue bias, ships iOS + Android (Android-first when both viable).

---

## Approved file inventory

**New files (10):**
```
skills/find-mobile-app-idea/SKILL.md
skills/find-mobile-app-idea/references/data-sources.md
skills/find-mobile-app-idea/references/displacement-scoring.md
skills/find-mobile-app-idea/references/category-traps.md
skills/aso/SKILL.md
skills/aso/references/keyword-research-tactics.md
skills/aso/references/listing-asset-specs.md
skills/aso/references/review-velocity-playbook.md
skills/aso/references/platform-policy-risk.md
AUDIT-existing-skills.md
```

**Updated files (1):**
```
CLAUDE.md  — two new routing rows added
```

**Unchanged files:**
- `plugin.json` — exists, satisfactory
- `README.md` — exists, satisfactory
- `skills/mobile-app/SKILL.md` — parallel path (TikTok content-first growth), not part of category-displacement chain

---

## Skill pipeline

```
find-mobile-app-idea
    → validate-saas-idea  (saas-idea-hunter plugin)
    → scope-mvp           (saas-idea-hunter plugin)
    → aso
```

The existing `mobile-app` skill is a separate path: content-first validation (TikTok gotcha moment, influencer scaling) — unrelated to category-displacement arbitrage.

---

## Skill 1: `find-mobile-app-idea`

### Core thesis
App store ranking algorithms reward freshness, review velocity, and retention. Apps not updated in 18-24+ months bleed ranking, opening displacement windows for fresh builders with AI tooling. Unit of work = **category (or keyword cluster)**, not individual app.

### Two mandatory failure-mode checks (drop on failure — no exceptions)
1. **Rotting-incumbent trap** — incumbents may be stale because the *category* is dying, not just them. Verify 24-month search volume trend + category download trend before recommending.
2. **Platform-migration trap** — category may look winnable on-store while real demand has moved to YouTube, web apps, Discord, etc. Check where users actually live.

### Five-phase methodology

| Phase | Work |
|-------|------|
| 1 — Category harvesting | User provides seeds OR "open" → 20-40 candidates from store category trees, ASO keyword clusters, persona queries, adjacencies |
| 2 — Top-3 incumbent profiling | Per category: name + bundle ID + URLs, developer activity, last update, rating/reviews, 90-day sentiment, monetization model, feature surface. Public APIs only; paid download signals flagged as "verify with [tool]" |
| 3 — Trap checks (mandatory) | Check A: Google Trends 24-month slope + store traffic trend. Check B: off-platform migration signals. Drop on failure regardless of incumbent staleness |
| 4 — Displacement-viability scoring | 0-10 per dimension: incumbent staleness (0.25), keyword winnability (0.25), build feasibility (0.20), monetization fit (0.15), AI wedge (0.15). Bands: 8.0+ strong, 6.5-7.9 caveats, 5.0-6.4 borderline, <5.0 drop |
| 5 — Output | Top 3 full cards + candidates 4-5 one-liner + explicit recommendation for which to take to `validate-saas-idea` |

### Full card format (per top-3 category)
- One-line pitch: "Build a [thing] for [user] stuck with [stale incumbent]"
- The opening (specific evidence of staleness + opportunity)
- Top-3 incumbents table (name, last update, rating, monetization)
- Buyer/user profile
- Trap checks with evidence (both must pass)
- Build pitch: 5-7 MVP features + AI wedge if applicable
- ASO attack plan: 5-10 primary keywords with rationale
- Composite score with dimension breakdown
- Explicit kill criteria

### Reference files
- `data-sources.md` — iTunes Search API + rate limits, google-play-scraper, AppFigures/Sensor Tower/AppTweak/AppMagic tier guidance, Google Trends, Reddit/community platform-migration signals
- `displacement-scoring.md` — Full rubric, worked examples per band, common scoring mistakes, tie-breakers
- `category-traps.md` — Deep dive on both failure modes with worked examples

### Hardcoded assumptions (never ask)
- Solo technical founder, ex-dev, AI-build-fluent
- No personal audience
- 90-day revenue bias
- Android-first when both stores viable
- Builds fresh — does NOT buy/acquire apps
- AI is soft weight in opportunity selection, not hard requirement

### Output constraints
- Every claim cites primary-source URL where possible
- No subjective adjectives ("exciting," "innovative," "huge market")
- No recommendations requiring an existing audience
- Honest kill criteria mandatory in every card
- Paid tooling: name + approximate price tier + "verify pricing"

---

## Skill 2: `aso`

### Core thesis
ASO for a solo builder displacing stale incumbents differs from established-app ASO. Win vector: freshness signals (update velocity, review velocity, retention) + hyper-specific long-tail keywords where incumbents stopped optimizing.

### Inputs required (ask once if missing)
App name (or candidates), category, primary keyword cluster, named top-3 incumbents, platform (iOS / Android / both), monetization model, target launch date.

### Six required output components

| # | Component |
|---|-----------|
| 1 | Keyword strategy — primary cluster (5-8 kws, scored), long-tail wedge (15-25 phrases), brand-defense (generic descriptors near incumbent names, not trademark infringement), tooling recs (AppTweak, Sensor Tower, ASOMobile, AppFigures — user verifies numbers) |
| 2 | Listing optimization assets — app name + subtitle/short desc with exact char budgets; description (first 3 lines + full structure); iOS keyword field (100-char rules); iOS promotional text (170 chars, updatable without review) |
| 3 | Visual conversion assets — icon (3 directions + A/B test plan via PPO/Google Experiments); screenshots (first 3 = 90% of conversion: headline + UI + social proof); app preview video (15-30s hook); Android feature graphic |
| 4 | Review velocity + freshness signals — SKStoreReviewController / Play In-App Review API timing; review reply strategy (every review, first 60 days); update cadence (every 2-3 weeks, first 6 months); crash-free rate + retention as indirect ranking signals; monitoring recs (Firebase Crashlytics, Sentry) |
| 5 | Launch sequence + ranking-arc tactics — pre-launch (TestFlight beta, soft-launch country strategy); week 1-2 (seed download velocity, non-paid sources); week 3-6 (Apple Search Ads / Google App Campaigns on long-tail only, explicit budget caps); week 7-12 (double down on organic-surfacing keywords); weaponized updates at weeks 4, 8, 12 |
| 6 | Platform-policy risk register — App Store hot zones (3.1.2 subscription clarity, 5.1.1(v) sign-up walls, AI-content disclosure); Google Play hot zones (Subscriptions/Cancellations, deceptive behavior, sensitive permissions); pre-submission compliance checks; rejection-recovery playbook |

### Output structure
Single document, six components in order, concrete recommendations not templates. Ends with Day-1-actions checklist (10-15 specific items to do this week before any other build work).

### Reference files
- `keyword-research-tactics.md` — AppTweak/Sensor Tower/ASOMobile/AppFigures workflows; long-tail discovery; competition-difficulty interpretation
- `listing-asset-specs.md` — Exact pixel dimensions, char budgets, file format requirements for every asset on both platforms. Instructs skill to verify against Apple/Google docs (specs change)
- `review-velocity-playbook.md` — In-app review API integration patterns, timing strategies, review-response templates, policy line on review incentivization (forbidden both platforms)
- `platform-policy-risk.md` — App Store Review Guidelines + Google Play Policies most likely to bite solo builder shipping subscription app in competitive category; "platform shipped native feature" strategic risk

---

## CLAUDE.md routing additions

Two rows added to existing routing table:

| If the user asks about... | Invoke |
|---|---|
| Find a mobile app category / displace stale app incumbents | `solo-builder:find-mobile-app-idea` |
| ASO / App Store Optimization / keyword ranking / displacing an incumbent app | `solo-builder:aso` |

The existing `Mobile app growth` → `solo-builder:mobile-app` row stays unchanged.

---

## Audit: `validate-saas-idea` + `scope-mvp`

**Source:** Local copies in `skills/validate-saas-idea/SKILL.md` and `skills/scope-mvp/SKILL.md`.

**Output:** `AUDIT-existing-skills.md` — diff-like list of recommended edits per skill. No modifications to the source skills.

### `validate-saas-idea` audit scope
- Sections that transfer cleanly to mobile context
- Sections needing mobile-specific additions:
  - ASO difficulty assessment
  - Platform policy risk + store rejection risk
  - Mobile CAC channels (Apple Search Ads, Google App Campaigns vs cold outreach)
  - Mobile unit economics: Apple/Google 30% → 15% revenue cut, IAP vs subscription accounting

### `scope-mvp` audit scope
- Tech stack overrides for mobile: React Native vs Flutter vs native iOS/Android decision, mobile auth, push notification infrastructure, mobile analytics (RevenueCat, Adapty, Amplitude Mobile)
- Mobile-specific MVP feature cut rules
- 90-day timeline differences: TestFlight + Play Console review timelines add 1-3 days per submission, must be planned around
