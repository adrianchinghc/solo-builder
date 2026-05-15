# Displacement-Viability Scoring Rubric

Reference file for `find-mobile-app-idea`. Load this at the start of Phase 4 (scoring).

---

## Dimension 1: Incumbent staleness (weight 0.25)

Measures how stale the top-3 apps are. The more stale, the larger the freshness signal gap a new app can exploit.

| Score | Criterion |
|-------|-----------|
| 10 | All top-3 apps last updated >24 months ago, developer shows no activity (no social posts, no website updates, no response to recent reviews) |
| 8 | 2 of top-3 apps stale >18 months; one semi-active (1-2 updates per year, minimal developer engagement) |
| 6 | Top-1 dominant and actively maintained; top-2 and top-3 stale >18 months — a challenger must beat the active leader, not just the zombies |
| 4 | Top-2 apps actively maintained (updates every 1-3 months), clear developer investment; top-3 stale |
| 2 | Dominant app has frequent updates (<6 weeks between updates), excellent review scores (4.7+), and active developer community or social presence |
| 0 | Category has a monopoly app with Apple/Google editorial feature ("App of the Day," "Featured" badge), or native OS integration that makes third-party apps structurally disadvantaged |

**Scoring notes:**
- "Last update date" comes from `currentVersionReleaseDate` (iOS) and `updated` (Android)
- Do not conflate app version bumps with meaningful updates. A version bump with "bug fixes" that contains no user-visible change is not a freshness signal to the ranking algorithm in the same way a new feature update is
- Check developer activity beyond the app itself: Twitter/X account, website blog, support email response rate — these indicate whether the team is still alive and might respond to competition

---

## Dimension 2: Keyword winnability (weight 0.25)

Can a fresh app with zero reviews reach the top-5 for the primary keyword cluster within 90 days? This is the binding constraint for a no-audience founder.

| Score | Criterion |
|-------|-----------|
| 10 | Primary keywords have <5 apps with updates in the last 12 months in the top-20; at least one high-intent keyword with estimated volume ≥500/mo is functionally uncontested |
| 8 | 5-10 active competitors, but a clear long-tail wedge exists: 3+ phrases with ≥200/mo volume where incumbents rank but haven't updated keyword metadata in 12+ months |
| 6 | Competitive primaries (all top-5 apps are active), but 10+ long-tail phrases are genuinely open (<3 active competitors in top-10) with combined estimated volume ≥500/mo |
| 4 | All high-volume keywords dominated by 3+ well-reviewed, recently-updated apps; long-tail volume too low (<200/mo combined) to drive meaningful installs |
| 2 | Category primaries are effectively brand terms owned by incumbents ("Spotify," "Duolingo"), and generic alternatives have <100/mo estimated volume |
| 0 | Keyword volume is too low to generate meaningful organic install velocity: the entire keyword cluster has <50/mo estimated searches across all relevant terms |

**Scoring notes:**
- Keyword volume estimates come from AppTweak, ASOMobile, or Sensor Tower — always say "verify with [tool]" since these are estimates
- "Keyword winnability" is partly about volume and partly about incumbent freshness for specific terms. An incumbent ranking #1 for a keyword but not having updated in 18+ months is "winnable" — they're coasting on historical authority
- Android vs. iOS split matters: a category may be winnable on Android (where keyword metadata is weighted more heavily in the description) but not on iOS (where keyword field + title are primary signals). Specify which platform the score applies to if they differ significantly

---

## Dimension 3: Build feasibility — solo + AI, 4-8 week MVP (weight 0.20)

Can a solo technical founder using AI coding tools (Claude Code, Cursor, v0) ship a working MVP in 4-8 weeks?

| Score | Criterion |
|-------|-----------|
| 10 | MVP is a single-function utility: one screen, one clear output, minimal state. Comparable to a calculator, timer, or converter app. 2-3 weeks to ship |
| 8 | Standard CRUD-plus: form-based input, list view, detail view, one external API integration (e.g., weather, maps, health data). 4-5 weeks |
| 6 | Moderate complexity: real-time sync, offline-first with conflict resolution, significant UX craft required (e.g., complex animations, gestures, custom UI components), or moderately complex data model. 6-8 weeks |
| 4 | Requires on-device ML model inference, complex audio/video processing, intensive background processing, or intricate multi-party synchronization across devices |
| 2 | Requires proprietary licensed data (financial, medical, mapping at scale), hardware integration (Bluetooth LE, NFC pairing), or real-time collaborative features with operational transforms |
| 0 | Not buildable solo in 8 weeks with any AI tooling: complex algorithms requiring specialized expertise, FDA/CE medical device classification, or core value requires marketplace liquidity from day one |

**Scoring notes:**
- "AI tooling" assumption means React Native (Expo) or Flutter for cross-platform; Claude Code or Cursor for code generation; v0/Lovable for UI scaffolding
- A native iOS-only or Android-only app reduces score by 1-2 points due to toolchain overhead (Xcode, provisioning profiles, separate codebases)
- Auth + RevenueCat + Supabase is a standard backend scaffold that adds ~1 week regardless of app complexity — factor this in

---

## Dimension 4: Monetization fit (weight 0.15)

Does the category have proven willingness to pay at subscription $3-15/month or premium $5-30 one-time?

| Score | Criterion |
|-------|-----------|
| 10 | Category norm is subscription $3-15/mo; incumbents are already charging and users are already paying (evidence: paid app revenue estimates or review mentions of subscription cost) |
| 8 | Category skews premium $5-30 one-time; incumbents demonstrate paid demand; upgrade path to subscription add-ons is a natural extension |
| 6 | Mixed: some apps are freemium-converting-to-subscription, some are free-with-ads; conversion path is real but requires effective onboarding to demonstrate value before paywall |
| 4 | Category is dominated by free-with-ads or free-with-no-clear-business-model apps; subscription requires significant behavior change from users; WTP is unproven |
| 2 | Incumbents have tried paid/subscription and reverted to free; user reviews consistently complain about pricing; strong free alternatives (including OS-native features) suppress WTP |
| 0 | No monetization signal; no incumbent has ever charged for anything in this category; or OS-native feature makes the entire category effectively free |

**Scoring notes:**
- Evidence of WTP: check if incumbents have subscription prices visible in their store listings; look for review mentions of "worth the price" or "too expensive" (both indicate WTP exists); check if premium versions have a meaningful review gap from free versions
- The 30% Apple/Google revenue cut affects net margin, not user WTP — score WTP on gross price, but flag the cut in unit economics (handled in `validate-saas-idea`)

---

## Dimension 5: AI wedge (weight 0.15)

Does AI enable a feature that the incumbent architecturally cannot replicate without rebuilding their core?

This is a soft bonus dimension. A category without an AI wedge can still score high overall. Do not force-fit AI.

| Score | Criterion |
|-------|-----------|
| 10 | AI enables a category-defining feature that is architecturally incompatible with the incumbent's 4-6 year old codebase — e.g., on-device personalization from usage patterns, AI-generated adaptive content, or natural language replacing a form-heavy workflow that the incumbent built its entire UX around |
| 8 | AI enables a significant UX leap (e.g., camera-based input replacing manual data entry) that the incumbent has not shipped and would require a major UX overhaul to adopt — their brand identity is tied to the old flow |
| 6 | AI improves accuracy or quality of an existing feature (e.g., better classification, smarter suggestions) in a way that's a meaningful UX improvement — incumbent could ship this in 1-2 quarters if motivated |
| 4 | AI is additive but not differentiating: chatbot, summarization, "ask AI" button — incumbent could add this in a sprint; users may not perceive material value difference |
| 2 | AI is cosmetic: visual filter, tone adjustment, minor text polish — easily replicated, low perceived value |
| 0 | No meaningful AI opportunity in this category; the core value is deterministic (calculator, converter, timer) or requires human judgment that AI cannot meaningfully assist |

**Scoring notes:**
- The question is not "can AI be used here?" (almost always yes) but "does AI create an unbridgeable gap that protects against incumbent response?"
- Score 10 requires *architectural* incompatibility — the incumbent would need to rebuild major systems to match. Score 8 requires *strategic* incompatibility — they could rebuild but it would invalidate their brand or UX patterns. Scores 4-6 are nice-to-have, not moat.

---

## Composite formula

```
Composite = (D1 × 0.25) + (D2 × 0.25) + (D3 × 0.20) + (D4 × 0.15) + (D5 × 0.15)
```

**Bands:**
- **8.0+** → Strong recommendation — present as primary candidate
- **6.5-7.9** → Recommended with caveats — present but state the caveats explicitly in the card
- **5.0-6.4** → Borderline — surface for awareness but flag clearly; do not lead the output with these
- **<5.0** → Drop — do not include in the output

---

## Worked examples

### Example 1 — Strong (composite 8.4): "Habit tracking for shift workers"

**Context:** Category is habit tracking, but narrowed to shift workers (nurses, factory workers, retail staff) who have irregular schedules that standard habit apps don't support.

| Dimension | Score | Evidence |
|-----------|-------|----------|
| D1: Incumbent staleness | 9 | Top-3 apps (Habitica, Streaks, Done) last updated 4-22 months ago depending on platform; Habitica iOS last updated 22 months ago |
| D2: Keyword winnability | 8 | "habit tracker for nurses" — estimated 300/mo, weak competition; "shift work habit app" — effectively uncontested; primary "habit tracker" term is competitive but long-tail wedge is real |
| D3: Build feasibility | 8 | Core MVP: schedule-aware streak tracking with shift pattern input; standard CRUD + notification scheduling; 4-5 weeks with React Native + Expo |
| D4: Monetization fit | 7 | Habitica, Streaks, Done all have paid tiers or subscription; WTP established in category; shift-worker persona less price-sensitive on productivity tools |
| D5: AI wedge | 9 | AI can predict optimal habit scheduling based on shift pattern + historical completion data — Habitica's gamification system is architecturally incompatible with adaptive scheduling; incumbents built around fixed daily streaks |

**Composite:** (9×0.25) + (8×0.25) + (8×0.20) + (7×0.15) + (9×0.15) = 2.25 + 2.00 + 1.60 + 1.05 + 1.35 = **8.25** → Strong

---

### Example 2 — Recommended with caveats (composite 7.0): "Sleep sounds / white noise"

**Context:** Classic utility category. Multiple incumbents, some well-maintained, but strong staleness in the bottom of the top-10.

| Dimension | Score | Evidence |
|-----------|-------|----------|
| D1: Incumbent staleness | 7 | Top-1 (Calm) and top-2 (Headspace) actively maintained; top-3 through top-10 increasingly stale; displacement target is top-3 within subcategory "white noise for babies" not overall sleep |
| D2: Keyword winnability | 6 | "white noise for babies" — moderate competition; "pink noise sleep aid" — fewer active competitors; primary "sleep sounds" is dominated by Calm/Headspace; long-tail is the path |
| D3: Build feasibility | 9 | Audio player + timer + background playback + mix controls; React Native + expo-av; 3 weeks |
| D4: Monetization fit | 8 | Calm ($69.99/yr), numerous apps at $0.99-9.99/mo; WTP very well established |
| D5: AI wedge | 5 | AI could generate adaptive soundscapes; Calm could add this in one sprint; not architecturally incompatible |

**Composite:** (7×0.25) + (6×0.25) + (9×0.20) + (8×0.15) + (5×0.15) = 1.75 + 1.50 + 1.80 + 1.20 + 0.75 = **7.00** → Recommended with caveats

**Caveats to state:** Top-1 and top-2 (Calm, Headspace) are well-funded and active — displacement is only viable in the long-tail subcategory, not the primary category. Keyword competition is real. The AI wedge is weak; differentiation must come from niche positioning (babies, ADHD, tinnitus), not AI novelty.

---

### Example 3 — Borderline (composite 5.3): "Basic photo editor"

**Context:** High-volume category with strong, well-maintained incumbents.

| Dimension | Score | Evidence |
|-----------|-------|----------|
| D1: Incumbent staleness | 3 | VSCO, Snapseed, Lightroom Mobile all have recent updates; no meaningful staleness across top-5 |
| D2: Keyword winnability | 3 | "photo editor" — dominated by well-reviewed, recently-updated apps with massive review counts; no viable long-tail wedge found |
| D3: Build feasibility | 7 | Basic filters + crop + export is buildable; anything competitive requires custom GPU shaders or ML models |
| D4: Monetization fit | 7 | Adobe at $9.99/mo; others at $2.99-6.99/mo; WTP proven |
| D5: AI wedge | 6 | AI subject removal, generative fill — but Google Photos, Samsung, and Snapseed already have this; not a wedge |

**Composite:** (3×0.25) + (3×0.25) + (7×0.20) + (7×0.15) + (6×0.15) = 0.75 + 0.75 + 1.40 + 1.05 + 0.90 = **4.85** → Drop

**Why it dropped:** D1 and D2 are both below 4. Incumbent staleness is absent; keyword winnability is near zero. The build is feasible but there's no displacement window.

---

## Common scoring mistakes

**Over-weighting staleness when keyword volume is insufficient.** A score of 10 on D1 with a score of 2 on D2 produces a composite of ≤6.0 maximum across all possible other scores. Staleness creates a *window*; keywords determine whether you can get *traffic*. Both must be present.

**Treating "AI feature" as automatic 10.** Ask: can the incumbent ship this in one sprint without rebuilding anything? If yes, score 4 or less. The AI wedge only matters if it requires structural change on the incumbent's part.

**Ignoring Android vs. iOS split in keyword winnability.** Android indexing is heavier on description text; iOS is heavily weighted on title + subtitle + keyword field. A keyword that's winnable via description optimization on Android may require title-level placement on iOS. If the stores differ significantly, note which platform the D2 score applies to.

**Compositing without showing dimension scores.** Always show the dimension-by-dimension breakdown. A composite of 7.2 with two scores of 3 and three scores of 10 tells a very different story than a composite of 7.2 with all scores between 6 and 8. The distribution matters.

**Anchoring on "this is a big market."** Total addressable market is irrelevant if D2 (keyword winnability) is ≤2. A massive market with no organic discovery path is not an opportunity for a no-audience solo founder.

---

## Tie-breakers

When two candidates score within 0.3 composite points of each other:

1. **Prefer higher D2 (keyword winnability)** — organic discovery is the engine; without it, everything else is speculation
2. **Prefer higher D3 (faster build)** — faster to ship means revenue sooner and more time for iteration inside the 90-day window
3. **Prefer higher D1 (more stale incumbents)** — a more durable displacement window if the keywords can be won
4. **Prefer lower D4 score (lower WTP)** only if the AI wedge (D5) is ≥8 — a weak monetization category with a strong AI wedge can be compensated by commanding premium pricing for the AI differentiation
