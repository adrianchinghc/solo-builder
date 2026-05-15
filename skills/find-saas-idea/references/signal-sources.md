# Signal Sources — Mining Instructions

This is the detailed playbook for each of the 10 signal sources. Use these exact techniques inside each Phase 1 subagent.

---

## 1. Paid-but-painful (weight 1.0)

**What it proves:** Money is already changing hands; only execution is broken. Highest predictive value because WTP is settled.

**Where to mine:**
- G2.com — filter by category, sort by "Lowest rated," filter for verified buyers, recent reviews (last 12 months)
- Capterra — same pattern, broader vertical-SaaS coverage
- TrustRadius — strongest for mid-market and enterprise complaints
- Trustpilot — consumer software
- SiteJabber — consumer software, fintech, e-commerce platforms
- ProductHunt comments on launches that hit top 5 but have angry follow-up reviews
- Reddit: `r/SaaS`, `r/SaaSSales`, `r/ProductManagement` "alternatives to X" threads

**Search patterns:**
- `site:g2.com [category] "would not recommend"` (or "frustrating," "missing feature," "deal breaker")
- `site:capterra.com [category] 2 stars`
- `"alternatives to [incumbent]" site:reddit.com`

**What to extract:** Verbatim 2-3 star review quotes (NOT 1-star — those are usually noise). The diagnostic phrase is "good but..." or "I switched because..." The "but" and "because" are product specs.

**Trap to avoid:** Don't mine 1-star reviews. They're disproportionately shipping defects, billing complaints, and rage posts. The signal is in 2-3 stars — the buyer cared enough to articulate a specific gap.

---

## 2. Workaround templates (weight 1.0)

**What it proves:** A non-technical buyer drew the MVP spec for you and other buyers paid for it. Strongest pre-built validation in the stack.

**Where to mine:**
- Notion Template Gallery — `notion.so/templates`, sort by category, look for high-popularity templates
- Etsy "Digital Downloads" — search `[niche] template`, `[niche] spreadsheet`, `[niche] tracker`. Filter to "Bestseller" badge. Etsy is *radically* underrated as a signal source; thousands of templates sell 5-figure copies at $5-30 each.
- Gumroad — `gumroad.com/discover`, sort by sales, filter by software/business categories
- Airtable Universe — `airtable.com/universe`
- Make.com / Zapier public template galleries
- ClickUp / Monday template marketplaces
- r/Notion, r/Airtable, r/spreadsheets — "I built this template for X"

**Search patterns:**
- `site:etsy.com [niche] template bestseller`
- `site:gumroad.com [niche] template`
- `site:notion.so/templates [niche]`

**What to extract:** Template name, price, sales count (if visible), buyer reviews. Each successful template = one SaaS opportunity. Buyer reviews on templates often say "would love this as an app" or "wish it auto-updated" — explicit upgrade signals.

**Trap to avoid:** Generic productivity templates (a "todo list" template selling 50,000 copies) don't translate — the audience won't pay $20/month for an app version of something they already have a $5 template for. Look for templates solving *specific role-based problems* (e.g., "Pediatric Speech Therapy Session Tracker").

---

## 3. Search whitespace (weight 0.9)

**What it proves:** Buyers are searching with commercial intent and the SERP can't satisfy them.

**Where to mine:**
- Google Keyword Planner (free with Google Ads account)
- Ahrefs / SEMrush / Ubersuggest (if accessible)
- Google Trends — sustained upward slope over 24+ months, not viral spikes
- AnswerThePublic
- Google Autosuggest — type "software for [vertical]," "app to [verb] [noun]," "tool for [niche profession]"

**Diagnostic queries:**
- Modifiers that signal commercial intent: "software for," "app to," "tool that," "best [X] for [persona]," "[task] automation," "alternative to [X]"
- SERP failure modes worth exploiting:
  1. Top 10 results are all listicles ("10 best X tools") with no clear winner
  2. Top results are Reddit/Quora threads, not commercial products
  3. Top result is a generic horizontal product weakly fit for the specific persona

**What to extract:** Keyword, monthly search volume, SERP composition (% listicles, % commercial product pages, % community content). Note any vertical-specific modifiers that have volume but no purpose-built product (e.g., "scheduling software for music teachers" — Calendly is generic; vertical winner is wedged here).

**Trap to avoid:** High-volume head terms ("project management software") are unwinnable. Focus on long-tail with specific persona/vertical modifiers.

---

## 4. Community-stated unmet need (weight 0.7)

**What it proves:** Explicit verbal demand. Lower weight than paid signals because words are cheaper than dollars.

**Where to mine:**
- Reddit advanced search: `site:reddit.com "is there a tool that"`, `"anyone know an app for"`, `"I wish there was"`, `"how do you all handle"`, `"looking for software that"`
- Hacker News: `hn.algolia.com` search for "Ask HN: what app do you wish existed," "tools we should build"
- Indie Hackers Forum — `indiehackers.com/forum`, "Ideas and Validation" category
- Twitter/X advanced search: quoted phrases `"why is there no app for"`, `"someone please build"`
- Discord communities — domain-specific servers (search disboard.org by topic)
- Facebook Groups — domain-specific (search graph.facebook.com)
- Circle / Slack communities — domain-specific

**What to extract:** The verbatim ask, the niche it came from, the engagement on the post (upvotes/replies — indicates whether others share the pain). Cluster across multiple posts asking the same thing.

**Trap to avoid:** A single tweet or reddit post is anecdote, not signal. Require ≥5 distinct posts saying substantively the same thing across ≥2 communities to count.

---

## 5. Dead competitor archaeology (weight 0.8)

**What it proves:** The problem is real (someone built for it) but hard (they failed). If you can identify their failure mode and avoid it, you inherit validated demand.

**Where to mine:**
- ProductHunt launches from 18-36 months ago that hit top 5 — check current state. Dead landing page? Stale Twitter? Zombie product?
- Crunchbase — filter by "Closed" status, by category
- r/SaaS "I shut down" / "lessons from failure" posts
- IndieHackers "Failure Stories"
- Wayback Machine (`web.archive.org`) — verify the dead-end vs pivot
- Tech crunch / TechCrunch "shutdown" / "wind down" / "acqui-hired" search

**Search patterns:**
- `site:producthunt.com [category]` then check current state of top results from 2022-2024
- `"shutting down" [category] site:twitter.com`
- `site:indiehackers.com "I'm shutting down"`

**What to extract:** Product name, what problem they solved, what their landing page said, ProductHunt launch-day comments (what users wanted vs got), explicit failure reason if posted. Then categorize the failure: distribution, ICP wrong, premature scale, technical debt, founder burnout, market too small, free alternative emerged.

**Trap to avoid:** If they failed because the market was too small, you cannot fix that with better execution. Filter for failures caused by *correctable* errors (distribution, ICP, build cost, timing).

---

## 6. Regulatory / platform-shift windows (weight 0.9)

**What it proves:** Forced demand with a deadline. Buyers *must* buy something or face consequences.

**Where to mine:**
- Federal Register (US): `federalregister.gov`
- EUR-Lex (EU): `eur-lex.europa.eu`
- Platform changelogs (read weekly):
  - Stripe: `stripe.com/changelog`
  - Shopify: `shopify.dev/changelog`
  - Apple: WWDC announcements, App Store Review Guidelines updates, App Intents docs
  - Meta: `developers.facebook.com/blog`
  - Google: `developers.google.com/news`
  - Salesforce: release notes
- State-level data privacy laws (CA CPRA, TX TDPSA, CO CPA, etc.)
- Industry regulators: SEC, FINRA, HIPAA updates, FDA software-as-medical-device rules, FTC enforcement actions

**Recent examples (2024-2026) to look for analogs of:** EU AI Act compliance, state privacy law cascades, App Store Connect API changes, Twitter/X API deprecation aftermath, Stripe new compliance requirements, OpenAI/Anthropic enterprise compliance needs.

**What to extract:** Regulation name, effective date, who it applies to, what new capability or report it requires, whether incumbents already serve it.

**Trap to avoid:** Heavily regulated areas (healthcare, finance, legal) require domain expertise to navigate. If you don't have it, partner or skip. But adjacent compliance tooling (e.g., "DPA generator for SaaS companies subject to TDPSA") can be tractable.

---

## 7. Expert-validated friction (weight 0.8)

**What it proves:** Domain practitioners — the actual buyers — have specific recurring complaints about their workflow.

**Where to mine:**
- Industry-specific subreddits: r/Accounting, r/LawFirm, r/Nursing, r/Construction, r/RealEstate, r/Veterinary, r/Dentistry, r/PropertyManagement, r/Bookkeeping, r/Optometry, etc.
- Industry-specific Slack/Discord: Pavilion (B2B sales/ops), RevGenius, Operators Guild, MeasureCamp (analytics), etc.
- LinkedIn posts in specific job-role filters — look at high-engagement complaint posts from people in target roles
- Trade publications and their forums: Modern Restaurant Management, Construction Dive, Modern Healthcare, Accounting Today, ABA Journal
- Practice management forums for specific professions

**Search patterns:**
- `site:reddit.com/r/[profession] "I hate"`, `"why is there no"`, `"every day I"`
- LinkedIn search: filter by job title, search for posts containing "frustration," "workaround"

**What to extract:** Profession, specific workflow step that fails, what they currently do, who else replied confirming the same pain.

**Trap to avoid:** Don't pick a vertical you can't credibly speak to. If you can't get a 15-minute call with someone in the profession in your first week, the distribution problem is unsolved.

---

## 8. Job-posting demand (weight 0.9)

**What it proves:** A company is paying a human to compensate for a missing tool. They have budget *and* the problem is ongoing enough to justify a hire.

**Where to mine:**
- LinkedIn Jobs — filter by role, read JDs in detail
- Indeed — same
- Wellfound (formerly AngelList Talent) — startup-heavy
- We Work Remotely
- Built In

**Diagnostic JD phrases:**
- "build custom solutions"
- "manage workarounds"
- "stitch together multiple systems"
- "manually reconcile"
- "custom scripts in [tool]"
- "experience with [tool A] and [tool B] integration"

**Search patterns:**
- LinkedIn: filter by "Marketing Operations Manager" + posted last 30 days + count results
- Indeed: `"manage workflows in Zapier" [role]`

**What to extract:** Role name, company size/segment, JD phrase indicating tool gap, salary range (proxy for budget). If 100+ companies are hiring for the same role with the same workaround language, you have a SaaS opportunity.

**Trap to avoid:** Some roles exist independent of tool gaps (e.g., "Customer Success Manager" exists regardless of CS software). Look for *operations* / *coordinator* / *analyst* roles whose JDs read like tool-replacement specs.

---

## 9. Support-burden patterns (weight 0.8)

**What it proves:** A captive audience with an existing billing relationship is asking the same questions a tool could solve.

**Where to mine:**
- Shopify Community Forums — `community.shopify.com`. Search "how do I" + sort by activity
- Salesforce Trailblazer Community — same pattern
- HubSpot Community
- Notion Help Community
- Airtable Community
- WordPress.org support forums
- QuickBooks Community
- App-store / marketplace search-no-results queries (where surfaceable)

**What to extract:** Recurring question, official response (often "you'll need a third-party app for this"), upvote / view count, age of thread (if a 3-year-old thread still gets activity, the gap is structural).

**Why this signal is special:** Marketplace app-store opportunities have built-in distribution — list in the Shopify App Store or Salesforce AppExchange and customers find you by searching for their problem. The audience-free distribution problem is partially solved by the marketplace itself.

**Trap to avoid:** Some marketplaces (Salesforce AppExchange) have high listing barriers (security review, partner fees). Cost the entry barrier into the build estimate.

---

## 10. Adjacent-vertical drift (weight 0.7)

**What it proves:** A solution pattern has been proven horizontally; an analogous vertical has the same workflow but no purpose-built tool.

**Where to mine:**
- Look at horizontal SaaS that succeeded broadly (Calendly, Stripe, Mailchimp, Notion, Linear, Webflow).
- For each, list the verticals that have a near-identical workflow but use the generic tool with friction:
  - Calendly → vertical scheduling for therapists (SimplePractice exists), tutors, music teachers, dog groomers, pet sitters, contractors with site visits
  - Mailchimp → vertical email for restaurants, nonprofits, faith organizations, real estate agents
  - Stripe → vertical billing for [usage-based niche]
  - Notion → vertical workspace for [niche role]

**Validation requirement:** For each adjacency, verify (a) the niche has its own trade community/conference (proves it's a real vertical buyer), (b) the generic tool has reviews from this niche complaining about specific gaps (back to signal #1), and (c) there isn't already a winner in the niche-specific version.

**Trap to avoid:** "Slack for [niche]" or "Notion for [niche]" without a specific workflow gap is brand transplant, not product. The vertical bet requires identifying a workflow generic tools can't handle (e.g., HIPAA compliance for therapist scheduling).

---

## Cross-source notes

**On corroboration:** A candidate problem appearing across 3+ source types is dramatically stronger than 10 signals from one source type. Weight the diversity of sources, not just the count.

**On dating:** Prefer signals from the last 12 months. Pain from 2019 may have been solved already. If you cite an older signal, verify the gap still exists today by spot-checking the current SERP / G2 / marketplace.

**On AI as a wedge:** The opportunity is rarely "use AI to do X." The opportunity is "X workflow has these specific frictions that didn't have a cost-effective solution until AI made it feasible." Lead with the workflow, not the tech.

**On B2B vs prosumer:** For 90-day revenue with no audience, B2B SMB (5-200 employee companies, $50-500/mo price points) is the most reliable lane. Prosumer can work but requires more polish and higher volume to hit revenue numbers. Enterprise is incompatible with 90-day revenue regardless of distribution.
