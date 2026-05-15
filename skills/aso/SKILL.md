---
name: aso
description: Use when the user asks about "aso plan for my app," "how do I rank for [keyword]," "launch strategy for my app," "App Store Optimization," "review velocity tactics," "displacing [incumbent app]," "aso strategy," "app store keywords," or any question about getting an app to rank, convert, or acquire users through app store channels. Converts a category-displacement opportunity into an executable ASO plan covering keyword strategy, listing assets, visual conversion, review velocity, launch sequencing, and platform-policy compliance.
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# ASO — App Store Optimization

## Core thesis

ASO for a solo builder displacing stale incumbents is fundamentally different from ASO for an established app. The established app optimizes for efficiency — small improvements to already-ranked keywords. The displacement attacker has no ranking history, no reviews, and no brand. The win vector is different:

1. **Freshness signals first.** Update velocity, review velocity, and retention are ranking inputs. A new app updated every 2-3 weeks for 6 months out-freshens an incumbent that hasn't touched its metadata in 18 months.
2. **Long-tail first.** Do not compete on primary keywords in the first 90 days. Win the 15-25 hyper-specific phrases where incumbents stopped optimizing. Accumulate installs and reviews. Then let the algorithm graduate you upward.
3. **Metadata precision.** Incumbents often have stale keyword fields, sub-optimal titles, and screenshots that haven't been updated in years. Every character of your metadata is intentional; theirs is an artifact of when someone cared enough to update it.
4. **Listing conversion before traffic.** Getting ranked matters nothing if your listing doesn't convert. Fix screenshot 1, app name, and description first 3 lines before worrying about keyword rank position.

This skill encodes the specific displacement-attack playbook, not generic ASO advice.

## Inputs required before starting

If any of the following are missing, ask once via AskUserQuestion before proceeding:

- App name (or 2-3 candidate names being considered)
- Category and primary keyword cluster (from `find-mobile-app-idea` output, or user-provided)
- Named top-3 incumbents (app names + last update dates)
- Platform: iOS / Android / both
- Monetization model (free / freemium / subscription price / premium price)
- Target launch date

Do not proceed with generic inputs ("my productivity app"). Specificity is required for useful output.

## When to invoke

**Trigger phrases:** "aso plan for my app," "how do I rank for [keyword]," "app store keywords," "App Store Optimization," "review velocity tactics," "displacing [incumbent]," "aso strategy," "launch ASO," "how do I get organic downloads."

**Invoke automatically** as the next step after `scope-mvp` produces a build plan for a mobile app.

**Do NOT invoke:**
- Before `find-mobile-app-idea` has identified a viable category (you need named incumbents and keyword cluster)
- Before `scope-mvp` has established the feature scope (you need a real app to plan for)
- For web/SaaS distribution planning (this skill is app-store-specific)

## Six required output components

All six components must appear in the output, in order. Do not skip or abbreviate any component. The output is a single document with a Day-1 actions checklist at the end.

Load reference files at the component where they're needed:
- Component 1 → load `references/keyword-research-tactics.md`
- Components 2-3 → load `references/listing-asset-specs.md`
- Component 4 → load `references/review-velocity-playbook.md`
- Component 6 → load `references/platform-policy-risk.md`

---

## Component 1: Keyword strategy and prioritization

Load `references/keyword-research-tactics.md` before writing this component.

**Primary cluster (5-8 keywords):**

Score each keyword on three dimensions — estimated monthly search volume, difficulty (0-10 where 10 = unwinnable in 90 days), and intent alignment (does searching this term lead to installing an app like yours?). Present as a table:

| Keyword | Est. volume/mo | Difficulty | Intent alignment | Priority |
|---------|---------------|------------|-----------------|----------|
| [keyword] | verify with AppTweak | X/10 | high/medium/low | primary/secondary/skip |

Tooling: AppTweak (~$90-300/mo, verify at apptweak.com), Sensor Tower ($200+/mo, verify), ASOMobile (~$20-100/mo, verify at asomobile.io), AppFigures (~$15-40/mo, verify). Never invent volume numbers — always say "verify with [tool]."

**Long-tail wedge (15-25 phrases):**

These are hyper-specific phrases where incumbents rank but have stopped optimizing — stale keyword field entries, unchanged descriptions, no recent updates. A fresh app with intentional optimization can rank for these within 4-8 weeks.

Identify them by:
1. Checking what keywords stale incumbents rank for (via AppTweak competitor keyword analysis)
2. Filtering to keywords where the ranking app was last updated >12 months ago
3. Prioritizing phrases with estimated volume 100-1,000/mo and difficulty <5/10

**Brand-defense terms:**

Identify generic descriptors adjacent to each incumbent's brand name (e.g., if Habitica is a competitor, terms like "gamified habit tracker" or "RPG habit app"). Do NOT use competitor brand names as keywords — Apple prohibits competitor trademarks in keyword fields; Google prohibits using others' brand names deceptively. Use generic descriptors of what makes the incumbent distinctive.

**Platform-specific notes:**
- **iOS:** Keywords live in: App Name (30 chars), Subtitle (30 chars), Keyword Field (100 chars comma-separated). Do not repeat terms across these three sources — the algorithm deduplicates. Primary keyword in name, secondary keyword in subtitle, long-tail phrases in keyword field.
- **Android:** No keyword field. Keywords live in: App Title (30 chars), Short Description (80 chars, fully indexed), Full Description (4,000 chars, fully indexed). Integrate keyword clusters naturally across description — do not stuff.

---

## Component 2: Listing optimization assets

Load `references/listing-asset-specs.md` for exact character limits and format requirements.

**App name strategy:**
- Must contain the primary keyword
- iOS: 30 chars max. Format: "[Primary Keyword] — [Differentiator]" or "[Brand] — [Primary Keyword]"
- Android: 30 chars max. Same principle
- Test 2-3 name candidates against the keyword + brand clarity trade-off

**Subtitle (iOS) / Short Description (Android):**
- iOS subtitle: 30 chars, searchable. Include secondary keyword. "For [specific user type]" or "[Key benefit] + [secondary keyword]"
- Android short description: 80 chars, searchable. More room — lead with benefit, include secondary keyword

**Description — first 3 lines (critical):**
This is the only copy most users read before deciding to install. Must answer: who is this for, what does it do, and why is it better than what they're using now. Write 3 concrete lines. No marketing fluff. Example structure:
```
Line 1: [Specific user type] who [problem state] — this app [core solution].
Line 2: Unlike [category generic], [app name] [specific differentiator].
Line 3: [Social proof or key number]: [claim with basis].
```

**Full description structure:**
1. Problem statement (1 paragraph) — the pain the user has today, in their language
2. Solution statement (1 paragraph) — what the app does, specifically
3. Key features (bulleted list, 5-7 items) — lead with user benefit not technical spec
4. Social proof (1 paragraph) — reviews, download count (once real), awards
5. Call to action (1-2 lines) — "Download free" or price + what they get

**iOS keyword field (100 chars):**
- Comma-separated, no spaces after commas
- No words that appear in your app name or subtitle (wasted space)
- No competitor brand names
- Prioritize nouns and adjectives over verbs (search behavior skews toward "[noun] app" not "app that [verb]s")
- Example: `habit,tracker,streak,daily,routine,goal,reminder,productivity,health`

**iOS Promotional Text (170 chars):**
- NOT indexed for search — conversion copy only
- Updatable without App Review submission — use for launch campaign messaging, seasonal offers, limited-time pricing
- Update this every 2-4 weeks during launch period to stay fresh

---

## Component 3: Visual conversion assets

Load `references/listing-asset-specs.md` for exact pixel dimensions and format requirements for all assets.

**App icon:**

Present 3 candidate icon directions with rationale:
- Direction A: [describe visual concept + psychological hook — e.g., "minimal single-color mark, uses negative space to imply the action"]
- Direction B: [describe visual concept — e.g., "character/mascot that embodies the product emotion"]
- Direction C: [describe visual concept — e.g., "literal representation of core output, screenshot-in-icon style"]

A/B test plan: use Apple Product Page Optimization (PPO — available in App Store Connect, runs split test on live users) or Google Play Store Listing Experiments. Run icon test first — it affects click-through from search results before any copy is seen.

**Screenshots (5-10 slots available; first 3 do 90% of conversion work):**

**Screenshot 1 — Core value statement:**
- Headline overlay (bold, 24-30px equivalent): [write the actual headline copy — e.g., "Track habits that fit your shift schedule"]
- UI shown: the primary screen of the app, showing the core feature in use (not the splash screen, not the onboarding)
- No icon repetition, no marketing adjectives, no company name

**Screenshot 2 — Problem → solution contrast:**
- Show what the user's experience was before (frustrated, manual, broken) and after (clean, automated, resolved)
- Side-by-side or before/after layout
- Headline: [write the actual headline copy]

**Screenshot 3 — Social proof:**
- Pull a real review quote (once you have one) or use a meaningful metric ("10K users tracking daily" — when true) or a third-party recognition
- Headline: [write the headline that introduces the proof]

**Screenshots 4-10:** Feature highlights, secondary persona scenarios, platform-specific features (widgets, live activities, complications). Write headlines for each.

**App preview video (15-30 seconds):**
Structure:
- **0-3s (hook):** The gotcha moment — the most surprising or immediately compelling thing the app does. This must work muted with captions.
- **4-15s (core value demo):** Live UI walkthrough of the primary JTBD — show the app actually working, not marketing slides
- **16-25s (secondary value or social proof):** Supporting feature or review quote
- **25-30s (CTA):** "Download free" or "Try free for 7 days" with price visibility

Caption all text — most app preview views are muted.

**Feature graphic (Android only):**
1024×500px. Primary keyword in headline. Keep text away from outer 20% of edges (gets cropped on some device sizes). Do not repeat the app icon in the feature graphic — most templates do this and it wastes the most visible above-the-fold real estate.

---

## Component 4: Review velocity and freshness signals

Load `references/review-velocity-playbook.md` before writing this component.

**First-30-days review acquisition:**

Trigger `SKStoreReviewController` (iOS) / Play In-App Review API (Android) at detected positive moments:
- After user completes their first successful core JTBD action (not just onboarding)
- After user returns for their 3rd session within 7 days
- After user achieves a goal or milestone within the app

Do NOT trigger: on first launch, during onboarding, after an error, when user is mid-task.

See `references/review-velocity-playbook.md` for exact Swift and Kotlin code patterns.

**Review reply strategy:**
Respond to every review in the first 60 days — positive and negative. Response text is indexed; use it for keyword reinforcement without stuffing. See `references/review-velocity-playbook.md` for response templates.

**Update cadence as freshness signal:**
Ship meaningful updates every 2-3 weeks for the first 6 months. Each update:
- Resets the "Updated" date visible on your listing (stale competitors show "3 years ago"; yours shows "2 days ago")
- Triggers re-indexing of your keyword field (iOS)
- Provides "What's New" text opportunity (keyword-rich)

Write "What's New" text as a mini-pitch, not a changelog. Lead with user benefit + include 1-2 keywords naturally.

**Crash-free rate and retention as indirect ranking signals:**
- Target crash-free rate: ≥99.5% — crashes suppress rankings on both platforms
- Target D1 retention: ≥40%, D7: ≥20%
- Monitoring tools: Firebase Crashlytics (free), Sentry (free hobby tier up to volume limits)

---

## Component 5: Launch sequence and ranking-arc tactics

**Pre-launch (4-6 weeks before launch date):**
- Recruit TestFlight beta cohort (iOS): target 50-100 users from personal network, relevant subreddits, or communities. These users provide early crash data and, more importantly, convert to your first review wave at launch.
- Soft-launch country strategy: consider Canada, Australia, or New Zealand first for initial store submission — smaller market, less competition noise, real user data. If category dynamics differ significantly by market, test domestically from day 1.
- Finalize all listing assets before submission — first impressions in App Review and in the market are hard to revise.

**Week 1-2 (launch week):**
- Front-load downloads from non-paid sources to seed download velocity: personal network, beta users converting, Product Hunt launch (if relevant), targeted subreddit post in category-specific communities (if guidelines allow), press/newsletter outreach
- Do NOT launch paid campaigns this week — install quality from organic sources is better for ranking signals than ad-sourced installs at launch

**Week 3-6:**
- Begin targeted Apple Search Ads (Search Match: OFF — use exact match only for long-tail keyword list from Component 1)
- Begin Google App Campaigns (asset-based, let Google optimize across your screenshots and video)
- Budget cap: $500-1,000/month maximum for validation phase. CPI ceiling: never exceed 3× your projected LTV
- Track CPI by keyword. Cut any keyword with CPI > your ceiling by week 5

**Week 7-12:**
- Review App Analytics (iOS) / Play Console organic search terms to identify which keywords are driving installs organically
- Double down on organic-surfacing keywords with additional content in description and What's New
- Cut paid spend on keywords where organic is already working
- Competitor monitoring: check if any stale incumbents have updated during your launch window — if yes, re-evaluate keyword winnability for affected terms

**Updates weaponized:**
Ship meaningful updates at weeks 4, 8, and 12. These are not patch bumps — each should include a user-visible new feature or significant UX improvement, with keyword-rich What's New text. Plan these updates on day 1; they should be scoped into the build plan from `scope-mvp`.

---

## Component 6: Platform-policy risk register

Load `references/platform-policy-risk.md` before writing this component.

**App Store Review Guidelines — critical sections for subscription apps:**

- **3.1.2 — Subscription clarity:** Price, billing period, and free trial terms (if any) must be clearly visible before the user subscribes. Common rejection: pricing in small gray text; trial terms buried in body copy. Paywall design must prioritize price legibility.
- **5.1.1(v) — Sign-up wall prohibition:** Users must be able to access basic functionality before being required to create an account. Pure onboarding-to-paywall flow with no preview = rejection risk.
- **AI-content disclosure:** Emerging requirement (verify current guidelines at developer.apple.com/app-store/review/guidelines/). Apps using AI to generate user-facing content may need to disclose this within the app.

**Google Play Policy — critical sections:**

- **Subscription cancellation visibility:** Cancellation path must be reachable in ≤2 taps from within the app. Apple's cancellation is system-level; Google requires in-app access.
- **Deceptive listings:** Screenshots must match current live UI. Using mockups, competitor screenshots, or AI-generated UI that doesn't exist = policy violation.
- **Data Safety section accuracy:** What you declare must match what you collect. Under-declaration = rejection or removal.

**Pre-submission compliance checklist** (do this before every first submission and after every major feature addition):

- [ ] Privacy policy URL is live and accessible from the store listing
- [ ] All data collection declared in iOS Privacy Nutrition Label / Android Data Safety section matches actual implementation
- [ ] Subscription price, billing period, and free trial terms visible before paywall commit
- [ ] "Cancel subscription" path reachable in ≤2 taps from within the app (Android mandatory; good practice for iOS)
- [ ] All screenshots show current live UI, not mockups or future-state
- [ ] Age rating correctly set (err toward higher rating if uncertain)
- [ ] App preview video shows current live UI
- [ ] No competitor brand names in iOS keyword field or in app description keyword stuffing
- [ ] AI-generated content disclosure added if applicable
- [ ] App does not crash on fresh install on a physical device (test both iOS and Android)
- [ ] App Review notes filled in for any potentially confusing flows

**Rejection-recovery playbook:**
- Read the full rejection reason before acting. Map it to the specific guideline number.
- Make only the minimal change that addresses the stated rejection — do not bundle unrelated changes.
- In resubmission notes to reviewer: explain what you changed and why it now complies. Reviewers read these.
- Appeal (if rejection seems incorrect): "Reply to reviewer" in App Store Connect (iOS) or Play Console appeal form. Cite the specific guideline text supporting your position.

**Strategic risk — platform ships native feature:**
The highest-order risk in any category-displacement play. If Apple/Google announces a native equivalent at WWDC or Google I/O, evaluate within 2 weeks whether your differentiator survives native competition. Native wins on default status, not quality — your app needs to be significantly better AND discoverable. See `references/platform-policy-risk.md` for historical examples and hedging strategies.

---

## Output structure

Produce a single document with all six components in order, using the headings above. End with:

**Day-1 Actions (10-15 specific items to do this week, before any other build work):**

Example items:
1. Finalize app name with primary keyword — test in iTunes Search API
2. Write and lock the App Name + Subtitle (iOS) / App Name + Short Description (Android) — total time: 2 hours
3. Create keyword list in Google Sheet: 5-8 primary + 15-25 long-tail, with estimated volume column (to fill in with AppTweak/ASOMobile later)
4. Brief a designer (or open Figma) on icon directions A, B, C — create first pass this week
5. Draft all screenshot headlines (1-10) — just the copy, not the final assets yet
6. Write description first-3-lines — get feedback from 1-2 people in the target audience
7. Draft "What's New" template for first 6 updates — headlines only
8. Set up Firebase Crashlytics in the project now (5 mins with Expo plugin)
9. Create RevenueCat account and configure products before any IAP code is written
10. Identify 3 communities where you will recruit TestFlight beta users — prepare outreach message
11. Book App Review slots in calendar: submit week 3, buffer week 4, launch week 5

---

## Quick reference

```
INPUTS → Load keyword-research-tactics.md → Component 1 (keywords)
       → Load listing-asset-specs.md → Component 2 (listing) + Component 3 (visuals)
       → Load review-velocity-playbook.md → Component 4 (reviews)
       → Component 5 (launch sequence)
       → Load platform-policy-risk.md → Component 6 (policy risk)
       → Day-1 actions checklist (10-15 items)
```

---

## Common mistakes to avoid

**Treating ASO as a one-time setup.** Metadata, screenshots, and "What's New" are ongoing. An app that doesn't update keyword metadata in response to search trend changes within 6 months is doing static ASO — which is what your stale incumbents are doing.

**Optimizing for high-volume keywords in week 1.** You will not rank for "habit tracker" in 90 days with zero reviews. Start with the long-tail and graduate upward as your review count grows.

**Not having screenshot 1 communicate the core value in 3 seconds.** Scroll past your listing in the search results. What does screenshot 1 say when it's 100px tall on a phone screen? If it says "App Name" and a pretty gradient, it says nothing.

**Launching without a review-request flow.** The review prompt is 2 hours of work. Not having it in your first build is 90 days of lost review velocity. There is no excuse for launching without it.

**Ignoring crash-free rate.** Crashes suppress rankings on both platforms. A crash rate of 2% may feel minor but is visible to the algorithm. Fix crashes before worrying about keywords.

**Running Search Match on Apple Search Ads.** Search Match casts a wide net and burns budget on irrelevant terms. Use exact match on your long-tail keyword list exclusively until you have data showing which terms convert.

---

## Red flags — pause and fix before publishing

- App name does not contain primary keyword
- Description first 3 lines describe the company, not the user's problem
- No review request flow in the build plan (see `scope-mvp`)
- Launch plan has zero non-paid download source in weeks 1-2
- Any screenshot shows UI that doesn't exist in the current app version
- Paywall does not show price and billing period before user commits
