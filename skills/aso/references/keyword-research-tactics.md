# Keyword Research Tactics

Reference file for `aso`. Load when writing Component 1 (keyword strategy).

---

## AppTweak workflow

AppTweak is the strongest tool for keyword-level research. Approximate price: $90-300/month (verify at apptweak.com/pricing).

**Competitor keyword gap analysis:**
1. Enter the top-3 stale incumbent bundle IDs or app names in AppTweak's "Keyword Gap" or "Competitor Keywords" tool
2. Export all keywords the incumbents currently rank for
3. Filter to keywords where: (a) the incumbent ranks in positions 1-10, AND (b) the incumbent's last update date is >12 months ago
4. These are "abandoned keywords" — incumbents rank on historical authority but are no longer refreshing metadata for them
5. Cross-reference with volume estimates: filter to keywords ≥200/mo estimated searches
6. Output: your long-tail wedge list of 15-25 phrases

**Finding keyword volume and difficulty:**
1. AppTweak "Keyword Overview" → enter candidate term → see estimated monthly searches + keyword difficulty (0-10 scale, lower = easier)
2. Viable threshold for a new app in 90 days: difficulty <5/10
3. Target sweet spot: difficulty 2-4, volume 200-1,000/mo — competitive enough to matter, weak enough to win

**Tracking competitor keyword rank changes:**
- AppTweak "Rank History" per keyword — shows whether incumbent has been losing rank on a term (falling from #1 toward #5-10 = the window is opening)
- Combine with update date: falling rank + no update in 12+ months = high-confidence opportunity

---

## Sensor Tower workflow

Sensor Tower is best for category-level data and absolute download estimates. Very expensive: $200+/month (verify at sensortower.com/pricing). Recommend for one-off research sessions, not a monthly subscription at the solo-builder stage.

**Category keyword trend analysis:**
1. Store Intelligence → select category → "Top Keywords" → see what keywords are driving the most downloads in the category
2. Sort by "Installs" (how many installs each keyword is driving) rather than volume — a keyword that drives installs is worth more than one with high search volume but low conversion
3. Compare against AppTweak data to cross-validate volume estimates

**Download trend validation for Trap A:**
- App Intel → search category → "Downloads" over 12 months → if category total downloads are declining >20%, reinforces Trap A
- Per-app download trends: select an incumbent → download trend → falling installs + no recent updates = staleness confirmed

**Public blog / reports (free tier):**
Sensor Tower publishes category-level data reports (top apps by download, quarterly trends) on their blog. Check sensortower.com/blog for recent reports before subscribing — you may get enough signal for free.

---

## ASOMobile workflow

ASOMobile is a lower-cost alternative with strong keyword discovery. Approximate price: $20-100/month (verify at asomobile.io/pricing).

**Long-tail discovery:**
1. Enter 3-5 seed keywords → "Related Keywords" → expands to 50-100 related phrases
2. Filter by: volume threshold (set minimum to 100/mo), difficulty (set maximum to 40/100 — ASOMobile uses 0-100 scale, not 0-10 like AppTweak)
3. Export and cross-reference against competitor keyword analysis

**Competitor keyword analysis:**
1. Enter competing app → "Competitor Analysis" → see full keyword list the app ranks for
2. Sort by difficulty (ascending) to find easy wins
3. Look for keywords where multiple stale incumbents all rank but none have updated metadata

**Difficulty score calibration:**
ASOMobile uses a 0-100 difficulty scale (vs. AppTweak's 0-10). Calibrate:
- 0-30 = viable for new app with no reviews
- 31-50 = achievable with 100+ reviews and active optimization
- 51-70 = achievable with 1,000+ reviews — plan for months 3-6, not launch
- 70+ = avoid in first 90 days

---

## AppFigures workflow

AppFigures is better for download/revenue estimates than keyword strategy. Approximate price: $15-40/month (verify at appfigures.com/pricing).

**Validating keyword-to-install conversion:**
- App Search Rankings → select competitor app → see which keywords it ranks for AND how those rankings correlate with install spikes
- A keyword where the incumbent lost rank (dropped from #2 to #7) and installs dropped proportionally = that keyword is driving real installs, not just vanity ranking

**Revenue estimate validation:**
- Market Summary → search category → estimated revenue per app → confirms whether incumbents are making money, which validates D4 (monetization fit) in displacement scoring
- Individual app revenue over time → if revenue is declining despite stable rankings, users are churning (bad retention) — or the category is commoditizing

---

## Free and low-cost alternatives

**App Store Connect Search Ads suggested bids (iOS, free):**
When you run even a $10 test campaign on Apple Search Ads (ASA), the "Suggested Bid" column for each keyword provides a rough proxy for keyword value and competitiveness. High suggested bids = high competition. Use this before paying for a keyword tool.

**Google Play Console search terms (Android, free after soft-launch):**
After your app is live, Play Console shows organic search terms driving installs. This is the most accurate keyword data you'll ever have — your actual users searching. Use this to identify which long-tail terms are converting and double down in your description.

**Appfollow free tier:**
appfollow.io — limited free tier for competitor keyword tracking; useful for confirming that a specific incumbent has stopped ranking for a target term.

**AppBot free tier:**
appbot.co — review analytics, including review volume over time per app. Useful for confirming that a competitor's review velocity is declining (fewer new reviews per month = declining engagement signal).

---

## Long-tail discovery process (step-by-step)

This is the full workflow to build your 15-25 keyword long-tail wedge list:

1. **Start with 3-5 seed keywords** — the obvious terms for your category (e.g., "habit tracker," "daily routine," "streak counter")

2. **Run each through AppTweak or ASOMobile "related keywords"** — expect 50-200 results per seed

3. **Filter aggressively:**
   - Volume: ≥200/mo estimated searches
   - Difficulty: <5/10 (AppTweak) or <40/100 (ASOMobile)
   - Incumbent presence: check which apps rank for each term

4. **Flag "abandoned keywords":**
   - Keyword is ranked by a stale incumbent (last updated >12 months)
   - Incumbent rank has been slipping or stable-but-stagnant
   - These are your highest-priority targets — you're not fighting active competition, you're filling a vacuum

5. **Check persona specificity:**
   - "habit tracker for nurses," "routine tracker for shift workers," "habit app for ADHD" — specificity reduces competition and increases intent alignment
   - A user searching a specific term converts at 3-5× the rate of a generic term

6. **Build the 15-25 phrase list:**
   - Sort by: (abandoned by stale incumbent) > (persona-specific) > (high volume) > (low difficulty)
   - Target: 5+ phrases where you're the only app actively optimizing

7. **Allocate across metadata fields (iOS):**
   - App Name: 1 primary keyword (30 chars total — every character counts)
   - Subtitle: 1 secondary keyword + differentiator (30 chars)
   - Keyword Field: remaining long-tail phrases, comma-separated, no spaces after commas, no repeats of Name/Subtitle terms (100 chars total)

---

## iOS vs. Android keyword differences

**iOS keyword architecture:**
- Keyword field (100 chars) + App Name (30 chars) + Subtitle (30 chars) = searchable surface
- Only these three fields are indexed for search
- Description is NOT indexed for App Store Search — it's conversion copy only
- Keyword field: no spaces after commas, no repeated terms, no competitor brands
- Instruct user to verify this against current App Store Connect documentation — Apple updates indexing rules periodically

**Android keyword architecture:**
- App Title (30 chars) + Short Description (80 chars) + Full Description (4,000 chars) = all indexed
- No separate keyword field — keywords live in the description
- Google indexes the full description text with NLP — you don't need to list every keyword explicitly; natural inclusion of keyword clusters works
- This means Android descriptions can be more prose-like; iOS descriptions are conversion copy (not indexed) and should be optimized for conversion, not keyword density

**Practical implication:**
The same keyword may rank differently on iOS vs. Android. A keyword won on Android through description optimization may require name-level placement on iOS. Always specify platform when reporting keyword strategy.
