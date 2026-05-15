# Data Sources — App Intelligence

Reference file for `find-mobile-app-idea`. Load this at the start of Phase 2 (incumbent profiling).

---

## iTunes Search API

Free, unauthenticated. Returns app metadata including last update date, rating, review count, and pricing. Does **not** return download counts.

**Search endpoint:**
```
https://itunes.apple.com/search?term=QUERY&country=us&entity=software&limit=50&genreId=GENRE_ID
```

Key parameters:
- `term` — search query (e.g., "habit tracker", "expense tracker")
- `country` — two-letter ISO country code (`us`, `gb`, `au`, `ca`)
- `entity` — use `software` for iPhone apps, `iPadSoftware` for iPad
- `limit` — max 200 per request
- `genreId` — optional category filter (6000=Business, 6013=Health & Fitness, 6007=Productivity, 6014=Games, etc.)

**Lookup endpoint (by bundle ID or App Store ID):**
```
https://itunes.apple.com/lookup?bundleId=com.example.app&country=us
https://itunes.apple.com/lookup?id=123456789&country=us
```

**Key response fields:**
- `trackName` — app name
- `bundleId` — reverse-DNS identifier
- `trackViewUrl` — App Store listing URL
- `currentVersionReleaseDate` — last update date (ISO 8601)
- `averageUserRating` — average rating across all versions
- `userRatingCount` — total ratings count
- `price` — 0.0 for free
- `formattedPrice` — "Free" or price string
- `sellerName` — developer name
- `artistViewUrl` — developer profile URL
- `version` — current version string

**Rate limits:** Approximately 20 requests/minute unauthenticated. Add a 3-second delay between batches. No API key required.

**Example curl — search for habit tracker apps:**
```bash
curl "https://itunes.apple.com/search?term=habit+tracker&country=us&entity=software&limit=10" \
  | python3 -m json.tool | grep -E '"trackName"|"currentVersionReleaseDate"|"averageUserRating"|"userRatingCount"'
```

**Example curl — lookup specific app by bundle ID:**
```bash
curl "https://itunes.apple.com/lookup?bundleId=com.example.habitapp&country=us" \
  | python3 -m json.tool
```

---

## google-play-scraper (Node.js)

npm package for scraping Google Play Store data. Returns app metadata, reviews, and rankings. Install: `npm install google-play-scraper`.

**Key methods:**

**`app()` — full app details:**
```javascript
const gplay = require('google-play-scraper');

const result = await gplay.app({ appId: 'com.example.app', lang: 'en', country: 'us' });
// Key fields:
// result.title — app name
// result.updated — last update timestamp (Unix ms)
// result.score — average rating (0-5)
// result.ratings — total ratings count
// result.installs — install range string e.g. "10,000+" — NOT an exact count
// result.free — boolean
// result.priceText — "Free" or price string
// result.developer — developer name
// result.developerWebsite — developer URL
// result.version — current version
```

**`search()` — ranked search results:**
```javascript
const results = await gplay.search({
  term: 'habit tracker',
  num: 20,
  lang: 'en',
  country: 'us',
  fullDetail: true  // includes all metadata per result
});
```

**`reviews()` — paginate reviews:**
```javascript
const { data, nextPaginationToken } = await gplay.reviews({
  appId: 'com.example.app',
  sort: gplay.sort.NEWEST,
  num: 100,
  lang: 'en',
  country: 'us',
  paginate: true
});
// data[0].text — review text
// data[0].score — rating (1-5)
// data[0].date — Date object
```

**Important:** The `installs` field returns a string range ("10,000+", "1,000,000+"), not an exact count. Never report this as an exact number. Use it only as an order-of-magnitude signal.

---

## Paid ASO tooling — download estimates and keyword data

These tools provide download estimates, keyword volume, and competitive intelligence. Prices change — verify at each tool's pricing page before recommending to users.

**AppFigures** — appfigures.com
- Best for: download and revenue estimates per app over time
- Entry tier: approximately $15-40/month (verify at appfigures.com/pricing)
- Relevant for: confirming that a category is generating real revenue, not just downloads

**Sensor Tower** — sensortower.com
- Best for: category-level trend data, top keyword movers across a category
- Very expensive: approximately $200+/month (verify at sensortower.com/pricing)
- Use case: one-off category validation sessions, not a monthly subscription unless at scale
- Tip: some data is available via their public blog and app intelligence reports without a subscription

**AppTweak** — apptweak.com
- Best for: keyword difficulty scores, volume estimates, competitor keyword gap analysis
- Price: approximately $90-300/month (verify at apptweak.com/pricing)
- Strongest tool for keyword-level research; recommended if budget allows one paid ASO tool

**AppMagic** — appmagic.rocks
- Best for: download + revenue estimates with freemium access
- Freemium tier has limited data; paid approximately $50-200/month (verify at appmagic.rocks)
- Accessible entry point for download trend validation

**ASOMobile** — asomobile.io
- Best for: keyword and competitor analysis at a lower price point
- Price: approximately $20-100/month (verify at asomobile.io/pricing)
- Strong for long-tail keyword discovery

**Rule for all paid tools:** Never fabricate numbers attributed to these tools. If you have verified data, cite it. If you're estimating, say "estimated via [tool] — verify before acting." If you don't have access to the tool, say "verify with [tool name] (approx $X/mo)" and note the price tier.

---

## Google Trends — category demand health check

Used in Phase 3 (Trap Check A) to verify category demand is not in structural decline.

**URL pattern for direct comparison:**
```
https://trends.google.com/trends/explore?q=KEYWORD&date=today+5-y&geo=US
```

Replace `KEYWORD` with the primary category keyword (URL-encode spaces as `%20`). Use the 5-year view to see the 24-month slope in context.

**How to interpret:**
- **Upward slope over 24 months** → category growing; safe to proceed
- **Flat (±10% over 24 months)** → category stable; safe to proceed
- **Gradual decline (10-30% over 24 months)** → caution flag; look for sub-niches growing within the declining category
- **Sharp decline (>30% over 24 months)** → Trap A triggered; drop the category unless you can identify a specific sub-niche with a flat/growing trend

**Comparing app vs. competing platform:**
To check Trap B (platform migration), compare relative interest:
```
https://trends.google.com/trends/explore?q=meditation+app,meditation+youtube&date=today+5-y
```
If the competing-platform term is growing while the app term is declining, platform migration is likely.

**Gotchas:**
- Google Trends shows *relative* search interest (0-100 scale), not absolute volume
- Seasonal categories (tax prep, holiday apps) will show spikes — use the 5-year view to see the envelope, not individual spikes
- New categories may show rising trends even with low absolute volume; validate with a keyword tool before treating as high-opportunity

---

## Reddit and community signals — platform-migration check

Used in Phase 3 (Trap Check B). These searches surface whether users have shifted behavior away from apps in a given category.

**Search patterns (run these in Google, not Reddit's internal search):**
```
site:reddit.com "[category keyword]" "don't use the app"
site:reddit.com "[category keyword]" "just use YouTube"
site:reddit.com "[category keyword]" "Discord server"
site:reddit.com "[category keyword]" "website instead"
site:reddit.com "[category keyword]" "no need for an app"
```

**Subreddits to check directly:**
- r/cordcutters — signals about moving off proprietary apps
- r/nosurf — anti-app sentiment across categories
- Platform-specific subreddits: r/Fitness (fitness apps), r/personalfinance (finance apps), r/productivity (productivity apps)
- The category's own subreddit (e.g., r/habitica, r/meditation) — read the pinned posts and top threads from the last 6 months

**What a passing check looks like:**
Reddit threads discuss which apps are best — not whether to use an app at all. YouTube content exists but as a supplement ("tutorials for using [app]"), not a replacement ("just watch YouTube instead of downloading anything").

**What a failing check looks like:**
Multiple threads saying "honestly just go to YouTube," "the [category] subreddit has everything you need," or "I deleted all my [category] apps and use [Discord/website] now." Three or more independent posts saying substantially the same thing = Trap B triggered.
