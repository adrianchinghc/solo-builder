---
name: hacker-news
description: "Use this BEFORE advising on a Hacker News launch, writing a Show HN post, or using HN for distribution. Invoke before answering 'how do I launch on HN?', 'what should my Show HN say?', or any Hacker News growth question."
metadata:
  plugin: solo-builder
---

# Hacker News Launch Playbook

## Why Hacker News Matters

Hacker News (news.ycombinator.com) is the "hard core" of the tech startup world. Getting to the front page means **50,000–100,000 visitors and 1,000+ simultaneous users** — 5–10x the scale of a Product Hunt launch. The audience is technical, skeptical, and brutally honest. They'll find every flaw in your product and business model. But they'll also be the ones most likely to become power users, write about you, or introduce you to the right people.

---

## The "Show HN" Format

The most effective way to launch a new product on Hacker News is the **"Show HN:"** prefix. It's a dedicated section for makers showing off what they built, and the community is explicitly invited to engage with submissions there.

**Format:**
```
Show HN: [Personal, authentic description of what you made]
```

**Bad (marketing-speak):**
```
Petsy.com - The best food delivery for pets
```

**Good (personal, direct):**
```
Show HN: I made a site that lets you subscribe to pet food delivery
```

**Why it works:** HN users despise marketing language. "I made a site that..." signals you're a real builder, not a startup PR team. It also signals you're open to feedback, not just broadcasting.

---

## The First Hour Is Everything

HN ranking is heavily weighted toward **early upvotes**. Your submission lives on the "New" page for roughly one hour before it's buried.

**The strategy:**
1. Submit your Show HN
2. Tell 4–6 friends to find it on the New page and upvote it within the first 60 minutes
3. Spread those upvotes out — 5 upvotes in the first 10 minutes looks like a voting ring; 5 over 60 minutes looks organic
4. Once it reaches the front page, **do nothing** — let the organic momentum take over

**Why not more votes?** HN has sophisticated anti-manipulation detection. If it detects a voting ring, it discounts those votes and the post drops instantly. The algorithm is sensitive. 5–10 genuine-seeming upvotes in the first hour is usually enough to get to the front page if the title is good.

---

## Writing the Title

The title is your only lever. HN doesn't use images, thumbnails, or taglines.

**Rules:**
- Personal and authentic ("I made / I built / I launched")
- No jargon, buzzwords, or startup-speak
- Describe the action the product does, not what it "is"
- Under 80 characters
- Don't use adjectives like "best", "amazing", "revolutionary"

**Examples:**

| Bad | Good |
|---|---|
| "AI-powered productivity platform for teams" | "Show HN: I built a tool that finds duplicates in your email inbox" |
| "Disruptive SaaS solution for hairdressers" | "Show HN: Booking software for hairdressers that focus on African hair" |
| "Remote OK: The world's leading remote job board" | "Show HN: I scraped 100+ job boards to find remote-only jobs" |

---

## How HN Moderation Works

HN has human moderators who actively intervene:

- **Controversy filter:** If a post gets more comments than upvotes, it's flagged as controversial and auto-dropped from front page. Don't submit something that will generate angry debate without genuine interest.
- **Mod discretion:** Mods can manually discount votes or remove posts that don't fit HN's mission. Overly promotional posts get axed.
- **Zeitgeist sensitivity:** HN favors posts that fit the current tech conversation. AI, developer tools, privacy, remote work, and bootstrapping do well. Generic SaaS rarely trends.

---

## Surviving the HN Comment Section

HN is famously harsh. They will:
- Find technical flaws in your architecture
- Question your business model
- Predict your failure for specific reasons
- Compare you unfavorably to 5 alternatives you've never heard of

**How to respond:**
- Don't get defensive. "Good point, here's how we're thinking about that" is always the right opener
- Acknowledge valid criticism publicly — it shows you're serious
- Thank people who take time to write detailed feedback even if it stings
- HN users respect genuine builders who engage honestly

**Remember:** When Dropbox launched on HN, it was mocked. It became a billion-dollar company. HN is often wrong, but it's also the most honest feedback you'll get anywhere.

---

## Server Prep (Non-Negotiable)

HN traffic is unforgiving. If your server goes down, your post slides off the front page and you lose the window.

**Quick static HTML trick:**
```bash
php index.php > index.html
```
This renders your dynamic page to a static HTML file. NGINX serves static files with almost zero CPU. When the traffic surge passes, restore dynamic rendering.

**Minimum prep:**
- Enable caching on every page
- Cloudflare free tier in front of your server
- UptimeRobot alert so you know within 1 minute if you go down
- Have a recovery plan (know your SSH login by heart)

---

## If It Doesn't Work

- Wait a week, try a different title, different time of day
- Try a different angle on the same product
- If it consistently doesn't land after 2–3 attempts: HN's audience isn't the right early adopter for your product, and that's fine. Reddit, specific subreddits, or Twitter may be better fits.
- Don't spam. HN bans IPs for aggressive submissions.

---

## When to Submit

**Best times:** Tuesday–Thursday, 8–11am PST (morning in San Francisco, still afternoon in Europe, catching maximum active users)

**Worst times:** Friday afternoon, weekends, US holidays

---

## Traffic Expectations

| Result | Visitors | Concurrent | Notes |
|---|---|---|---|
| Front page #1–3 | 80,000–150,000 | 2,000–5,000 | Server must handle this |
| Front page #4–10 | 30,000–60,000 | 500–1,500 | Most common for good launches |
| Page 2–3 | 5,000–15,000 | 100–300 | Still valuable for niche products |

HN traffic converts better than Product Hunt because the audience is searching for specific things, not just browsing. A developer who needs what you built will sign up immediately.

---

## Do This Today

Write 5 different Show HN titles for your product. Send them to someone who knows nothing about your product and ask them to rank which one makes them most want to click. Use the winner.
