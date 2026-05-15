---
name: find-mobile-app-idea
description: Use when the user asks "find me a mobile app idea," "what app should I build," "find a category to displace," "what are stale app incumbents," "find an app store opportunity," "mobile category research," or any open-ended request to discover mobile app opportunities. Runs a 5-phase category-displacement pipeline — harvests 20-40 candidate categories, profiles top-3 incumbents per category, applies two mandatory trap checks (rotting-incumbent + platform-migration), scores surviving categories on a 5-dimension rubric, and returns top-3 full opportunity cards plus a recommendation for which to take to validate-saas-idea.
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# Find Mobile App Idea

## Core thesis

App store ranking algorithms reward freshness, review velocity, and retention. Apps not updated in 18-24+ months bleed ranking even when they own keyword positions — because the store's freshness signal decays, review velocity drops to zero, and newer competitors accumulate more recent reviews at a faster rate.

This creates a structural displacement window for a solo builder with AI tooling: you don't need a bigger team or a better idea, you need a fresher build in the right category.

**Unit of work is the CATEGORY (or keyword cluster), not the individual app.** A category with 3 stale incumbents is a different opportunity than a category where only #3 is stale. Phase 2 profiles all three.

## Hardcoded assumptions (never ask the user)

These assumptions are baked in — do not ask the user to confirm them:

- Solo technical founder, AI-build-fluent (Claude Code, Cursor)
- No personal audience; distribution must be audience-independent
- 90-day revenue bias — the first paying user matters more than long-term defensibility
- Android-first when both stores are viable (lower review barrier, faster iteration cycles, broader global distribution)
- Builds fresh competitors — does NOT buy or acquire existing apps
- AI is a soft weight in opportunity selection, not a hard requirement; bake it in where it genuinely differentiates, not as a box-check

## When to invoke

**Trigger phrases:** "find me a mobile app idea," "what app should I build," "what mobile categories are winnable," "find stale incumbents," "app store opportunity," "mobile category research," "what apps are ripe for disruption," "I want to build an app but don't know what."

**Do NOT trigger when:**
- The user has a specific app idea and wants validation → `validate-saas-idea`
- The user has a validated idea and wants a build plan → `scope-mvp`
- The user has a built app and wants ASO → `aso`
- The user is asking about general mobile growth tactics → `mobile-app`

## Two mandatory failure-mode checks

Before recommending any category, two trap checks must pass. Failing either = drop the category, regardless of how stale the incumbents look.

**Trap A — Rotting-incumbent trap:** Incumbents are sometimes stale because the *category itself* is dying, not because they stopped caring. If the category's search volume has declined >30% over 24 months, or total category downloads are declining, the stale apps are a symptom of a decaying market — not an opportunity. See `references/category-traps.md` for detection methodology and worked examples.

**Trap B — Platform-migration trap:** The category may look winnable on-store while the actual user behavior has migrated to YouTube, web apps, Discord, Substack, or another platform. An app in this category will get installs but not retention. See `references/category-traps.md` for detection signals and worked examples.

Document the result of both checks for every category in your output. "PASS" without evidence is not acceptable.

## The 5-phase methodology

Use the Agent tool (or TodoWrite) to track phases. Phases 1-2 can run in parallel across categories; Phases 3-4 are sequential per category.

### Phase 1 — Category harvesting

**If the user provides seed categories:** Use them as the starting set, then expand to 20-40 candidates by generating adjacencies.

**If the user says "open":** Autonomously generate 20-40 candidate categories across both iOS and Android, drawn from:
- App Store / Google Play category trees (Utilities, Health & Fitness, Productivity, Lifestyle, Education, Finance, Food & Drink, Navigation, Music, Photo & Video)
- ASO keyword clusters with volume 500-5,000/mo and identifiable incumbents
- Persona-based search queries: "best app for [specific user problem]" searches that surface real apps
- Adjacencies to known-winning categories (e.g., if "habit tracking" is a winning category, "habit tracking for shift workers" is a candidate adjacency)

Candidates should span at least 4 different category trees. Do not generate 20 productivity apps and call it diverse.

Load `references/data-sources.md` now — it contains the iTunes Search API endpoints, google-play-scraper library usage, and paid tooling guidance needed for Phase 2.

### Phase 2 — Top-3 incumbent profiling

For each candidate category, identify the top-3 apps by ranking. Use iTunes Search API + google-play-scraper for public data. For download estimates, reference AppFigures / Sensor Tower / AppMagic — do NOT fabricate numbers; state "verify with [tool]."

For each of the top-3 apps per category, capture:

| Field | Source |
|-------|--------|
| Name + bundle ID + store URL | iTunes Search API / Play Store |
| Developer + last developer activity | App store listing + developer website |
| Last update date | App store listing (`updated` field) |
| Rating + review count | App store listing |
| Last-90-days review sentiment — top recurring complaints | App store reviews (public) |
| Monetization model | App store listing + onboarding (free / freemium / paid / subscription price) |
| Feature surface — what does the app actually do? | Store description + screenshots |

Staleness benchmark: last update date >18 months ago = stale; >24 months = highly stale; >36 months = possibly abandoned.

### Phase 3 — Two trap checks (mandatory drops)

Run both checks for every category. Document results explicitly.

**Check A — Category demand health:**
1. Run Google Trends for the primary keyword cluster (use `references/data-sources.md` for URL pattern). Look at the 24-month slope. Clearly downward (>30% decline in relative search interest) = fail.
2. If available via paid tool: check total category download trend over 12 months. Declining = additional failure signal.
3. Check: are any new entrants breaking into the top-10 in the last 12 months? If yes, category is alive even if incumbents are stale.

**Check B — Platform migration:**
1. Search Reddit for "[category keyword] don't use the app" / "just use YouTube for [category]" / "[category] Discord instead"
2. Check YouTube search volume for "[category keyword]" — if YouTube tutorials dominate the discovery path, in-app value may be replicated for free
3. Check whether strong web apps exist for the same use case (Google search "[category] web app")
4. Decision: if the dominant user behavior can be served by a competing platform without installing an app, and the app's core value is not meaningfully better in-app → fail

Drop categories that fail either check. Document: "Trap A: PASS/FAIL — [one-sentence evidence." "Trap B: PASS/FAIL — [one-sentence evidence]."

### Phase 4 — Displacement-viability scoring

Load `references/displacement-scoring.md` — it contains the full rubric, worked examples per band, and tie-breakers.

Score each surviving category 0-10 on five dimensions:

| Dimension | Weight | What it measures |
|-----------|--------|-----------------|
| Incumbent staleness | 0.25 | How stale are the top-3 apps? |
| Keyword winnability | 0.25 | Can a fresh app reach top-5 in 90 days? |
| Build feasibility | 0.20 | Solo + AI, 4-8 week MVP? |
| Monetization fit | 0.15 | Subscription $3-15/mo or premium $5-30? |
| AI wedge | 0.15 | Does AI enable a feature incumbent can't replicate? |

Composite = (D1×0.25) + (D2×0.25) + (D3×0.20) + (D4×0.15) + (D5×0.15)

Bands:
- **8.0+** → Strong recommendation
- **6.5-7.9** → Recommended with caveats (state the caveats explicitly)
- **5.0-6.4** → Borderline (surface but flag — do not lead with these)
- **<5.0** → Drop

### Phase 5 — Output

Produce full cards for the top-3 scoring categories. Candidates 4-5 get a single-line summary. End with an explicit recommendation.

## Full card format (top-3 categories)

Each full card must include all of the following sections, in this order:

**1. One-line pitch**
"Build a [thing] for [user] stuck with [stale incumbent]."
Specific. No buzzwords. No "AI-powered" unless AI is literally the product.

**2. The opening**
2-3 sentences with specific evidence of the displacement window: last update dates of the top-3 incumbents, rating trend, specific recurring complaints.

**3. Top-3 incumbents table**

| App | Last update | Rating (reviews) | Monetization |
|-----|-------------|-----------------|--------------|
| [Name] | [date] | [rating] ([count]) | [model + price] |

**4. Buyer/user profile**
Who downloads this type of app? What are they trying to accomplish? What does their behavior look like (daily use, weekly, event-driven)?

**5. Trap checks — evidence required**

```
Trap A (category demand health):
  Google Trends 24-month: [upward / flat / downward — with % estimate and URL]
  New entrants in top-10 last 12 months: [yes/no — names if yes]
  Verdict: PASS / DROP — [one-sentence reasoning]

Trap B (platform migration):
  Reddit check: [what was found]
  YouTube presence: [strong / moderate / weak for this category]
  Web app alternatives: [exist / don't exist — name them if they exist]
  Verdict: PASS / DROP — [one-sentence reasoning]
```

**6. Build pitch**
5-7 MVP features that directly address the recurring complaints identified in Phase 2. For each feature, one sentence: "Without [feature], the user cannot [JTBD step]." If there's an AI wedge, describe it specifically — what does AI do that the incumbent architecturally cannot?

**7. ASO attack plan**
5-10 primary keywords with rationale. Format: "[keyword] — [why: volume estimate, incumbent absence, intent alignment]." Note: verify estimates with AppTweak / ASOMobile before committing.

**8. Composite score with breakdown**
Show the dimension scores and weights, then the computed composite. Do not round scores to look cleaner.

**9. Kill criteria**
Specific, honest conditions under which you would walk away from this category after starting:
- "If the top-1 incumbent ships an update in the first 4 weeks after our launch, re-evaluate immediately — the displacement window may have closed."
- "If keyword CPI from Apple Search Ads exceeds $[X] in the first 3 weeks, the economics break."

## Output constraints

- Every claim cites a primary-source URL where possible (app store listing URL, Google Trends link, Reddit thread)
- No subjective adjectives: "exciting," "innovative," "huge market," "massive opportunity" are forbidden
- No recommendations whose distribution requires an existing audience
- Honest kill criteria are mandatory in every card — omitting them to look more confident is not acceptable
- When recommending paid tooling (AppTweak, Sensor Tower, AppMagic, AppFigures, ASOMobile): name the tool, state the approximate price tier, and say "verify pricing at [site]" — do not fabricate numbers from these tools

## Quick reference

```
TRIGGER → Load data-sources.md
        → Phase 1: Harvest 20-40 candidate categories
        → Phase 2: Profile top-3 incumbents per category (parallel across categories)
        → Phase 3: Trap checks — load category-traps.md
                   Drop failures → document reasoning
        → Phase 4: Score survivors — load displacement-scoring.md
                   Drop <5.0 composites
        → Phase 5: Top-3 full cards + candidates 4-5 one-liners
                 → Explicit recommendation → validate-saas-idea
```

## Common mistakes to avoid

**Fabricating download numbers.** iTunes Search API does not return download counts. google-play-scraper returns install range strings ("10,000+"), not exact counts. If you state a number, cite the tool and say "verify." If you can't verify, don't state it.

**Recommending a category that fails a trap check.** Trap checks are mandatory drops. "The incumbents are really stale though" is not an override. Document the failure and move on.

**Skipping kill criteria.** Honest kill criteria are what make this output useful. An output without kill criteria is a marketing document, not a research document.

**Single-source signals for keyword claims.** If you only have one source for "this keyword gets 2,000 searches/month," say "unverified estimate — check with AppTweak/Sensor Tower." Don't present single-source as fact.

**Treating "AI wedge" as automatic 10.** Ask: can the incumbent ship this AI feature in one sprint? If yes, score it 2-4, not 8-10. The wedge only counts if it requires a structural rebuild.

**Generating all candidates from the same category tree.** If all 20 candidates are Productivity apps, you've failed Phase 1. Diversify across at least 4 category trees.

## Red flags — stop and re-run

- Any full card lacks evidence for trap checks
- All top-3 candidates come from the same App Store/Play Store category
- Composite score was estimated rather than computed from dimension scores
- Kill criteria are absent from any full card
- A recommended category's top-1 incumbent was updated less than 6 months ago
- Distribution path for any recommendation requires an existing audience
