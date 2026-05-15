---
name: scope-mvp
description: Use when the user has a validated SaaS idea and asks "scope this MVP," "what should I build first," "give me a 90-day plan," "what's the smallest version of this," "build plan for this idea," "PRD for this," "design the MVP," or wants to convert a validated idea into a buildable 90-day plan. Produces a Jobs-To-Be-Done statement, a single-buyer-persona document, a ruthlessly minimal feature scope, a 90-day build-and-launch timeline with weekly milestones, a unit-economics model with revenue targets, and a parallel distribution-execution plan that runs concurrently with build, not after.
metadata:
  plugin: solo-builder
  version: "0.1.0"
---

# Scope MVP

## Core principle

An MVP is a hypothesis-test, not a small version of the eventual product. Its only job is to determine whether the buyers identified in validation will pay money to solve the problem identified in find-saas-idea. Everything that is not in service of that test is cut. Including features the founder finds interesting.

For a 90-day revenue target, the most common scoping failure is *sequential thinking* — build for 90 days, then launch. The correct approach is *parallel execution*: build and distribution start on day 1, the first cold email goes out before the first feature ships, the first pricing conversation happens before the first user signs up.

## Mobile app context

When scoping a **mobile app MVP** (iOS/Android), all seven components apply with these overrides:

**Distribution track starts with ASO, not cold email.** The Week 1 distribution track must include: TestFlight beta recruitment (target 50-100 users from personal network + 1-2 category-specific communities), keyword metadata finalized, screenshots and preview video drafted. The app must be submittable to stores by end of Week 3 to survive App Review latency and still launch in the Week 5-6 window.

**App Review latency is a hard constraint, not a risk.** First submissions typically take 1-3 days (App Store) and 1-7 days (Play Store). Plan at minimum one rejection-and-resubmission cycle: first submission Week 3, buffer for fix + resubmit, hard launch Week 5. Never schedule a community announcement for the same day as first submission. Any timeline that has "submit and launch same week" is wrong.

**Invoke `aso` immediately after this skill.** After producing the 7-component plan, the next step is `aso` — not starting to build. The ASO plan (keyword strategy, listing assets, launch sequence) must be complete before the first line of code is written, because the app name and description affect marketing from day 1 and are painful to change after launch.

**Parallel track difference.** For web SaaS, distribution runs concurrently with build starting Week 1 (cold emails, community participation). For mobile, Week 1-3 are build-dominated; distribution ramp starts Week 3 (beta recruitment, store submission) with full distribution launch at Week 5-6 (public launch + paid ASO, community posts). This is not sequential thinking — it's accounting for App Review as a fixed latency that cannot be compressed.

## When to invoke

Trigger phrases: "scope the MVP," "build plan for this idea," "what should I build first," "90-day plan for this," "PRD for [validated idea]," "design the MVP for [idea]." Also invoke automatically as the next step after `validate-saas-idea` produces a BUILD verdict.

Do NOT invoke before validation. If the user jumps straight to "scope the MVP for [idea]" without validation, run a 15-minute lightweight validation pass first to confirm the four critical inputs (named buyer, demand evidence, unit economics, distribution channel) are real before scoping.

## Inputs required

Confirm or extract from prior validation:
1. One-sentence product description
2. Named buyer persona (role, segment, where they congregate)
3. Top 3 pain points with primary-source citations
4. Named incumbent (what they use today)
5. Distribution channel with specific tactics for first 100 customers
6. Pricing hypothesis (range)

If any are missing, ask once via AskUserQuestion or pull from session context if a prior `validate-saas-idea` run produced them.

## The 7-component MVP scope

Produce all seven components in the final output. Use TodoWrite to track each.

### Component 1: Jobs-To-Be-Done statement

Write the JTBD in this exact form (Christensen / Strategyn):

"When I am [situation], I want to [motivation], so I can [expected outcome]."

Example: "When I am a solo bookkeeper with 15+ clients, I want to identify which clients are at risk of churning from my services, so I can proactively reach out before they shop around."

Then write the *progress statement* — what does the buyer's life look like when this job is done? Two sentences, specific and concrete. This becomes the homepage hero copy and the MVP success criterion.

### Component 2: Buyer persona (single, sharp)

One persona only. Resist the urge to write multiple. The MVP is built for one person.

Format:
- **Name and role** — give them a name to humanize ("Maya, solo bookkeeper")
- **Demographics that matter for the product** — only those that affect product decisions
- **Their day** — what does a Tuesday look like? Where does the pain show up?
- **Where they congregate online** — specific subreddits, communities, conferences, newsletters
- **What they already pay for** — software and services budget, named
- **Their alternative to your product** — what they use today (the named incumbent from validation)
- **Their trigger to switch** — what specific moment makes them open up to a new tool
- **Their decision criteria** — top 3 things they evaluate when choosing a tool
- **Their objection** — the top reason they would NOT buy

If you cannot fill any field with specifics, that's a validation gap — fix before continuing to Component 3.

### Component 3: Feature scope (the cut)

Write two lists.

**In the MVP (target: 5-8 features max):** Every feature must directly serve the JTBD. For each, write one sentence: "Without [feature], the buyer cannot [specific JTBD step]."

**Explicitly cut from MVP:** Features the founder thought of and decided to omit. For each, write the cut reason — "Not blocking the JTBD," "Adds 2+ weeks of build," "Solves a different persona's problem," etc. This list should be at least as long as the "In" list. If it isn't, the cut hasn't been ruthless enough.

**Rules for the cut:**
- No collaboration / team features (single-user MVP)
- No integrations beyond auth and Stripe unless the integration *is* the product
- No admin panels (you are the admin)
- No mobile app unless the workflow is fundamentally mobile
- No AI features unless AI is the literal product
- No notification infrastructure beyond transactional email
- No onboarding flow beyond a single welcome screen
- No analytics dashboard — use Plausible / PostHog hosted
- No marketing site beyond a single landing page

**Additional cut rules for mobile apps:**
- No background location or always-on microphone unless location/audio IS the core product — these trigger privacy review and can slow or block App Review
- No deep linking / universal links in MVP — add after core loop is validated
- No push notification personalization — ship one default notification message until retention data justifies complexity
- No Android widgets or iOS Live Activities / Dynamic Island integrations in MVP — compelling in demos, 2-4× the build time of a regular feature
- No Apple Watch or iPad-specific UI in MVP unless watchOS/iPadOS is the primary platform
- No web companion app unless cross-device is the core JTBD — maintain focus on the single platform
- Review request flow (SKStoreReviewController / Play In-App Review API) is NOT optional — it must be in the MVP; launching without it is 90 days of lost review velocity

**Build estimate:** For each MVP feature, estimate hours (with AI tooling). Sum. If total exceeds 200 hours (≈5 weeks of focused solo work), cut more. The MVP must ship in <6 weeks to leave time for distribution and iteration inside 90 days.

### Component 4: 90-day timeline with parallel tracks

Critical: build AND distribution run concurrently. Not sequentially.

Produce a week-by-week timeline as a table with three columns: Build track / Distribution track / Validation milestones.

Template:

| Week | Build | Distribution | Milestones |
|------|-------|--------------|------------|
| 1 | Foundation: auth, billing scaffolding, deploy pipeline. Landing page live. | First 50 cold emails to named prospect list. Join target communities. | 5 reply conversations |
| 2 | Core feature 1. | Continue outreach (50/week). Post in 2 target communities. | 10 demo bookings |
| 3 | Core feature 2. | First demo calls. Iterate landing page from feedback. | 3 verbal "I'd pay" |
| 4 | Core feature 3. | Soft launch to demo-call list. | First 3 paying customers (private beta) |
| 5 | Polish, onboarding, bug fixes from beta. | Continue outreach. Launch announcement to community. | 10 paying customers |
| 6 | Public-ready release. | Marketplace listing submitted (if applicable). | 20 paying customers |
| 7-9 | Iteration on top user requests. | Doubling down on highest-converting channel. | 35 paying customers |
| 10-12 | Retention features. Annual billing option. | Referral incentive. Case studies. | 50 paying customers / $5K MRR |

Customize this template to the specific idea. The point is: every week has parallel build + distribution activity, and every week has a measurable milestone.

**Mobile app timeline override:** The cold-email + demo-call distribution track above is for web SaaS. For mobile apps, replace with this template:

| Week | Build | Distribution | Milestones |
|------|-------|--------------|------------|
| 1 | Foundation: React Native/Expo scaffold, auth (Clerk/Supabase), RevenueCat IAP config, Crashlytics. | Finalize ASO keyword list. Draft all screenshot headlines. Recruit TestFlight beta list (target 50 users). | Keywords locked; beta list seeded |
| 2 | Core feature 1. Onboarding flow v1. | Write app description (first 3 lines + full). Brief designer on icon directions A/B/C. | Description approved; icon v1 in review |
| 3 | Core feature 2. Review request flow integrated. | Submit to TestFlight / Internal Testing (Android). Beta onboarding begins. Submit to App Review (iOS) + Play Review (Android). | First beta users active; store submissions in review |
| 4 | Polish + bug fixes from beta. Core feature 3. Paywall and subscription flow. | App Review buffer (plan for rejection + resubmit). Final screenshots produced. | App Review cleared; resubmit if needed |
| 5 | Public-ready release. | Public launch: community posts, Product Hunt (if relevant), personal network push. First review request prompts firing. | Launch day; first organic reviews |
| 6 | Week-8 update feature scoped and started. | Apple Search Ads exact-match long-tail campaign live ($500 cap). Respond to all reviews. | 20+ reviews; CPI data starting to appear |
| 7-9 | Ship week-8 update (freshness signal). Iterate on top beta feedback. | Double down on organic-surfacing keywords from App Analytics. Adjust ASA bids based on CPI data. | 50+ reviews; keyword rank movement visible |
| 10-12 | Retention features. Annual subscription option. | Week-12 update shipped. Referral prompt in post-purchase flow. | 100+ reviews; targeting top-5 for long-tail keywords |

### Component 5: Unit economics & revenue target

Concrete numbers, not ranges.

| Metric | Assumption | Source |
|--------|-----------|--------|
| Pricing | $X/month | From validation hypothesis |
| CAC | $Y | Channel-specific (cold email vs marketplace vs SEO) |
| Gross margin | Z% | Account for AI inference, hosting, payment processing |
| Monthly churn | A% | Conservative — high end of range until proven |
| LTV | computed | ARPU × GM / churn |
| LTV:CAC | computed | Must be ≥3:1 |
| Payback | computed | Must be <12 months |
| Day-90 target | $5K MRR (default) | Adjustable per user goal |
| Customers needed at day 90 | $5K / ARPU | Sets the distribution intensity target |

Then translate "customers needed" into "weekly conversion rate required" by week. If the math demands a >5% reply rate on cold outreach combined with >30% reply-to-demo and >50% demo-to-close, flag that the funnel is aggressive and reality may require adjusting (price up, lower target, longer timeline).

### Component 6: Distribution execution plan

Take the named channel from validation and convert to executable plan.

**For cold outreach:** Source for the prospect list, target count, email copy framework (problem-first opener, soft CTA, 4-touch sequence over 3 weeks), sending tool, daily/weekly volume target, expected reply rate, expected conversion to demo, expected demo close rate. Specific. Numeric.

**For marketplace:** Listing optimization (title, description, screenshots, video, reviews-acquisition plan), keyword targeting within the marketplace search, launch sequence (private beta → marketplace listing → review push to first 10 customers).

**For community participation:** Specific communities, contribution cadence (e.g., "answer 3 questions per week per community for 4 weeks before mentioning product"), what good participation looks like, what to never do.

**For SEO (only as parallel investment, not primary):** Specific 5-10 long-tail keywords, page templates, content cadence, expected timeline to first 100 organic visits/month.

### Component 7: Tech stack and build approach

Default stack for fastest 90-day ship with AI tooling:

- **Frontend:** Next.js + Tailwind + shadcn/ui (or Astro for content-heavy)
- **Backend:** Next.js API routes or Hono on Cloudflare Workers
- **Database:** Postgres on Supabase or Neon; SQLite via Turso for simpler cases
- **Auth:** Clerk, Supabase Auth, or BetterAuth
- **Payments:** Stripe with Stripe Customer Portal for self-serve management
- **Email:** Resend (transactional) + Loops (lifecycle)
- **Hosting:** Vercel, Cloudflare, or Railway
- **Analytics:** Plausible (privacy-friendly) or PostHog (more depth)
- **Error tracking:** Sentry
- **AI (if needed):** Anthropic API or OpenAI; consider Vercel AI SDK for streaming UX

**Build approach for solo founder + AI tooling:** Specify build mode — Claude Code / Cursor / Lovable / v0. For each feature in scope, note which tool will likely produce the first draft.

**Do not change the stack to satisfy curiosity.** "Let me try Rust" or "what if Bun" costs days. Pick boring and ship.

#### Mobile tech stack overrides

When building a native or cross-platform mobile app, replace the default web stack with the following:

**Framework decision (pick one, don't debate):**
- **React Native (Expo managed workflow) — recommended for solo AI-build-fluent founder.** Expo's managed workflow removes almost all native configuration overhead. Use Expo Router for navigation (file-based, same mental model as Next.js). Claude Code and Cursor generate RN/Expo code well. Android-first + iOS in the same codebase.
- **Flutter (Dart) — alternative.** Better performance for complex animations and graphics-heavy apps. Slightly higher AI codegen friction (Dart is less represented in training data than TypeScript). Choose if the app requires custom animations, games-adjacent UI, or if you have Flutter experience.
- **Native iOS/Android (Swift/Kotlin) — avoid unless required.** Double the codebase, double the maintenance. Only if the app requires hardware capabilities not exposed by RN/Flutter, or if category-leading UX requires native rendering at 120fps. Adds 40-60% build time minimum.

**Mobile-specific services:**

| Category | Tool | Price | Notes |
|----------|------|-------|-------|
| Subscriptions + IAP | **RevenueCat** | Free up to $2,500 MRR; ~$119/mo after | Non-negotiable for any subscription mobile app. Handles App Store + Play Store IAP, trial management, entitlements, webhook events. Replaces custom subscription management entirely. Verify at revenuecat.com/pricing. |
| Alternative to RevenueCat | Adapty | Free up to $1K MRR; cheaper after | Similar feature set; sometimes cheaper at scale. Verify at adapty.io/pricing. |
| Auth | Clerk (Expo SDK) | Free up to 10K MAU | Best Expo integration. OR Supabase Auth (built in if using Supabase backend). |
| Push notifications | Expo Notifications | Free | Wraps APNs (iOS) and FCM (Android). Upgrade to OneSignal if you need audience segmentation. |
| Backend | Supabase | Free tier generous | Postgres + Auth + Storage + Realtime. Works well with Expo. |
| Mobile analytics | Amplitude | Free up to 10M events/mo | Behavioral analytics, cohort retention analysis. OR PostHog (free self-hosted). |
| Crash monitoring | Firebase Crashlytics | Free | Integrate in first build, not after launch. `npx expo install expo-firebase-analytics` |
| CI/CD + store submission | EAS Build (Expo) | Free tier; $99/mo for higher concurrency | Builds and submits to both stores from CI. Required for consistent production builds. |

**Backend (if needed):** Supabase (Postgres + Auth + Storage + Realtime). Works well with Expo. For simpler apps (no server-side logic, local-first), SQLite via expo-sqlite is sufficient.

**What NOT to add to the mobile stack:**
- Do not add a custom push notification server — use Expo Notifications or OneSignal
- Do not self-host RevenueCat — use their hosted service; it's not worth the operational burden
- Do not add a web companion app in the MVP — maintain single-platform focus

## Output structure

A single document with these sections in order:

1. **The pitch** — one-line product description, refined
2. **The JTBD** — full statement + progress narrative
3. **The buyer** — single persona, all fields filled
4. **What you're building (and what you're not)** — In/Out feature lists
5. **The 12-week plan** — table with parallel tracks
6. **The numbers** — unit economics table with computed conclusions
7. **How you'll get to 50 customers** — distribution execution detail
8. **Tech stack and build mode** — decisions made, not options to debate
9. **Decision gates** — at week 2, 4, 6, what specific signal would mean stop / pivot / continue
10. **Day 1 actions** — the literal 5 things to do tomorrow morning

The day-1 actions list is what separates a plan from a document that gets bookmarked and never executed. Examples: "Buy domain. Set up Stripe account. Scrape first 100 prospects to a CSV. Write landing page first draft. Send 10 cold emails."

## Quick reference

```
VALIDATED IDEA → JTBD → Persona → Feature cut → Parallel timeline
              → Unit economics → Distribution plan → Stack → Day-1 actions
```

## Common mistakes to avoid

Sequential thinking — "I'll build for 60 days then launch." The MVP must ship by week 4-6, distribution starts week 1. Anyone who launches at day 90 has lost 88 days of distribution time and learned nothing about whether the market wants the product until it's too late to change it cheaply.

Persona drift — defining multiple personas because the founder is uncomfortable narrowing. One persona. The MVP can only fit one buyer's life perfectly.

Feature creep through "small additions." Every feature added in scoping is 2-3x what it looks like once shipped (because of edge cases, error states, support burden). The cut list should be longer than the keep list.

Vanity tech choices. New language, new framework, new auth provider — all cost days you don't have. Use boring proven tools.

Skipping the day-1 actions. The plan exists to be executed, not admired.

Generic pricing. "We'll figure out pricing later" means you'll undercharge. Set a specific number based on competitor anchors and the value-per-month math, even if it changes.

## Red flags — restart Component X

- More than 8 features in scope → restart Component 3
- Distribution starts after week 4 → restart Component 4
- LTV:CAC < 3:1 → restart Component 5 (raise price, lower CAC, or revisit validation)
- Persona has more than one role / segment → restart Component 2
- Day-1 actions list has fewer than 5 items or contains vague items → restart Component 7
