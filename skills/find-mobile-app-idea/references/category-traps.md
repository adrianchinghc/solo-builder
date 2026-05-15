# Category Traps — Failure Mode Reference

Reference file for `find-mobile-app-idea`. Load this when running Phase 3 trap checks.

Two traps are checked for every candidate category before scoring. Failing either = drop the category, regardless of how compelling the incumbent staleness looks.

---

## Overview

**Why these traps exist:**

The displacement thesis is: stale incumbents → open ranking window → fresh app wins organic traffic. Both traps represent cases where this chain breaks — not because of execution failure, but because of structural mismatch between the thesis and the category's reality.

**Trap A (rotting-incumbent)** breaks the first link: incumbents are stale not because of developer neglect but because the *category* is declining. Building into a declining category means you're competing for a shrinking pie.

**Trap B (platform-migration)** breaks the last link: even if you win ranking, you don't win users — because users have migrated to a competing platform that doesn't involve downloading an app at all.

Categories failing either trap are dropped immediately. The instinct to keep them ("but the incumbents are really stale") is exactly the instinct these traps are designed to override.

---

## Trap A: The Rotting-Incumbent Trap

### What it is

Incumbents in a declining category don't update because the return on investment dropped to zero. When download velocity falls, the incentive to maintain and market the app falls with it. Stale apps in a declining category look identical to stale apps in a healthy category — until you check the category-level demand signal.

The failure mode: you build a fresh app, win the keyword, and discover that the keyword generates 200 downloads/month — down from 2,000/month three years ago. You win the category and earn nothing.

### How to detect

**Primary check — Google Trends 24-month slope:**

Use the Google Trends URL pattern from `data-sources.md`:
```
https://trends.google.com/trends/explore?q=CATEGORY_KEYWORD&date=today+5-y
```

Interpret the 24-month slope (the right half of the 5-year chart):
- Upward or flat (±10%) → PASS
- Gradual decline (10-30%) → flag; look for sub-niches growing within the declining macro-category
- Sharp decline (>30% over 24 months) → FAIL — document the percentage and URL

**Secondary check — new entrant presence:**

Search both stores for apps in the category launched in the last 12 months. If new entrants are breaking into the top-10, the category is alive regardless of macro-trend signals. New entrants suggest developers are still finding the category worth building for.

**Tertiary check (requires paid tool) — category download trend:**

If AppMagic or AppFigures is accessible, check total category downloads over 12 months. A >20% decline in download volume across the category, independent of any individual app, is a structural decline signal.

### Decision rule

Drop if:
- Google Trends 24-month slope shows >30% decline AND
- No new entrants have broken into the top-10 in 12 months

The AND is important — a declining search trend with active new entrants may indicate the search behavior shifted (e.g., people search differently now) while the category itself is fine.

Pass if:
- Trend is flat or growing
- OR trend is declining but new entrants are active (investigate further: sub-niche may be growing)

### Worked example — category to drop: "QR code scanner"

**Situation:** Multiple QR scanner apps last updated 2-4 years ago. Looks like a clean displacement opportunity.

**Trap A check:**
- Google Trends for "qr code scanner app": sharp downward slope over 24 months, approximately 60% decline from peak
- Reason: iOS 11 (2017) added native QR scanning to the Camera app; Android cameras added it by 2019. The entire category's addressable demand was absorbed by OS-native functionality
- New entrants: almost none in the last 12 months

**Verdict: FAIL** — Incumbents aren't stale due to developer neglect; they're stale because the category was commoditized by the OS. Drop.

---

### Worked example — category to keep: "Menstrual cycle tracking"

**Situation:** Flo (dominant incumbent) faced significant privacy controversy (2021 FTC complaint, data selling concerns). Several secondary apps haven't updated in 18+ months.

**Trap A check:**
- Google Trends for "period tracker app": flat to slight upward trend over 24 months
- Category download trend: stable per AppMagic (verify independently)
- New entrants: Clue expanded features; multiple privacy-focused newcomers launched in 2022-2024

**Verdict: PASS** — Category is not declining. The staleness of secondary incumbents reflects competitive attrition around Flo's dominance, not category decay. The privacy controversy is a trust gap, not a category gap. Keep.

---

## Trap B: The Platform-Migration Trap

### What it is

Some categories have migrated: users still want the value, but they now get it from YouTube, a subreddit, a Discord community, a newsletter, or a web app — without downloading anything. An app competing in this space gets installs from users who don't know better, then churns them when they discover the free alternative is better.

The failure mode: you build, launch, and hit 10,000 installs — but 90-day retention is 3% because users discover they'd rather watch YouTube or browse a subreddit for the same content.

### How to detect

**Primary check — Reddit search:**

Run the search patterns from `data-sources.md`:
```
site:reddit.com "[category keyword]" "just use YouTube"
site:reddit.com "[category keyword]" "don't need the app"
site:reddit.com "[category keyword]" "Discord server"
```

Three or more independent posts saying substantially the same thing (don't need the app, prefer YouTube, use a website instead) = fail signal.

**Secondary check — YouTube search volume vs. app search volume:**

Use Google Trends to compare:
```
https://trends.google.com/trends/explore?q=[category]+app,[category]+youtube&date=today+5-y
```

If the "[category] youtube" line is growing while "[category] app" is flat or declining → migration is in progress.

**Tertiary check — web app competitive set:**

Google search "[category keyword] web app" and "[category keyword] website." If strong, well-reviewed web alternatives exist (and they're not just the same company's web version of their mobile app), the category has viable off-platform alternatives.

### Decision rule

Drop if:
- Multiple Reddit posts confirm users have migrated off-platform AND
- The app's core value is achievable on the competing platform without meaningfully worse UX

Pass if:
- No clear migration signal found
- OR migration exists but the in-app value is genuinely better (offline access, notifications, personalization, real-time features that require a native app)

### Worked example — category to drop: "Learn guitar"

**Situation:** Several guitar tutorial apps haven't updated in 2+ years. Category search volume is present. Looks like an opportunity.

**Trap B check:**
- Reddit search for "learn guitar app": multiple posts saying "honestly just use JustinGuitar.com" or "YouTube tutorials are way better than any app" with 100+ upvotes
- YouTube comparison trend: "learn guitar youtube" has 3× the relative search volume of "learn guitar app"
- Web app check: JustinGuitar.com is a well-structured, free web app with a structured curriculum that rivals any paid app
- What in-app advantages remain: progress tracking, structured curriculum, offline access — but JustinGuitar has a paid app that covers these for users who want them

**Verdict: FAIL** — The dominant discovery and learning behavior for guitar is YouTube + free web resources. An app must offer something genuinely unavailable there (AI adaptive curriculum, real-time feedback via microphone, gamification layer) to overcome the migration. A generic guitar tutorial app does not pass Trap B. Drop. A narrowly scoped AI pitch correction or fingering feedback tool might pass — evaluate as a different category.

---

### Worked example — category to keep: "Expense tracking / personal finance"

**Situation:** Several expense tracking apps are stale. Web apps like YNAB exist. Checking for migration.

**Trap B check:**
- Reddit search: posts discuss *which* app to use, not whether to use an app at all; no "just use a spreadsheet instead" consensus (some spreadsheet advocates but not dominant)
- YouTube comparison: "expense tracker app" holds steady vs. "expense tracker youtube" which is mostly "how to use [specific app]" tutorials
- Web app check: YNAB has a strong web app, but YNAB users still use the mobile app for receipt scanning and real-time transaction entry
- In-app value: receipt scanning, real-time bank transaction push notifications, quick entry widget — these are genuinely worse on web/YouTube

**Verdict: PASS** — No platform migration. The core value (real-time, on-the-go transaction tracking) is fundamentally mobile. The in-app experience is better than alternatives for the primary use case. Keep.

---

## Edge cases and judgment calls

**Category is declining overall but a sub-niche is growing:**

Example: "fitness tracker apps" is flat-to-declining, but "strength training tracker apps" is growing. Narrow the category to the sub-niche and re-run Trap A on that scope. If the sub-niche passes, proceed with the narrowed category as your unit of work.

**Google Trends data is noisy or seasonal:**

Use the 5-year view to see the envelope, not individual monthly spikes. A "meditation app" category that spikes every January (New Year's resolutions) and troughs every August is seasonal, not declining. Look at the year-over-year envelope: is January 2024 higher or lower than January 2023?

**Platform migration is partial:**

Some users moved to YouTube; power users still prefer apps. Acceptable outcome: proceed if the app's value proposition serves the power-user segment that specifically needs in-app capabilities (offline, notifications, progress tracking, personalization). State the segment narrowing explicitly in the category card.

**The competing platform is the developer's own web app:**

If YNAB or Headspace has a web app, that's NOT a migration signal — it's product expansion. The question is whether users are leaving the entire product (app + web) for a competitor platform. Ignore same-company web/mobile parity.

**Two failure modes interact:**

A category can fail both traps simultaneously. "Learn vocabulary / flashcard apps" may have declining search interest (Trap A — Duolingo absorbed most of the demand) AND meaningful migration (Trap B — Quizlet web app, Anki web interface). Double failures are still one drop — document both for completeness.
