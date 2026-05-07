---
name: product-hunt-playbook
description: "Use this BEFORE advising on a Product Hunt launch, preparing a PH submission, or getting PH upvotes. Invoke before answering 'how do I launch on Product Hunt?', 'when should I launch on PH?', or 'how do I get featured?'"
metadata:
  plugin: solo-builder
---

# Product Hunt Launch Playbook

## Why Product Hunt Matters

Product Hunt is one of the most important platforms for an indie maker launch. It's a daily leaderboard where anyone can submit a product and compete — a solo builder gets the same shot as a VC-funded team. Expect **~10,000 visitors and ~300 simultaneous users** on launch day. Conversion rate is lower than search traffic (people are browsing, not searching), but the real payoff comes 1–3 days later: **tech journalists crawl PH daily**. A good PH launch leads to press articles that bring another 50,000+ visits over the following weeks. Pieter Levels was 2x Product Hunt Maker of the Year by mastering this process.

---

## Before You Launch: One Shot, Make It Count

You only get one primary submission per product. Don't waste it. Study what the top PH products of the last 6 months look like — thumbnail quality, tagline clarity, comment engagement. If you ship something, you can't pretend it was never launched.

---

## Timing: Midnight PST

Product Hunt resets at **midnight San Francisco time (PST/PDT)**. Launch at 00:00:01 or as close as possible. Submitting at 9pm PST with 3 hours left puts you at a mathematical disadvantage. Set an alarm.

---

## Submission Checklist

### Name
- First launch: just your product name
- Relaunch: `Product Name 2.0` or `3.0`
- Inform PH community managers if relaunching — they may not allow it otherwise

### Tagline
The tagline is your first impression. Most are too complex. Test it: can a stranger immediately understand what your product does?

**Bad:** "An algorithmic application for machine learning applied to photos"
**Good:** "The first 🤖 machine learning 📷 photo editor"

Rules:
- Describe what it **does**, not what it **is**
- One clear benefit, no jargon
- Add 1–2 relevant emojis at the end
- Under 60 characters

### Thumbnail / GIF
- Use an **animated GIF** — PH supports it and it stands out in the feed
- Convert a screen recording to GIF with GIPHY Capture (free)
- Square format, keep file size under 3MB
- Show your product in motion, not a static logo

### Screenshots / Gallery
- Upload **8–16 high-res screenshots**
- Zoom your browser to 150% before screenshotting — they display scaled down on PH, so crisp originals matter
- Show the core user flows, not marketing slides
- Sequence them like a story: problem → solution → result

### Video (Optional but Powerful)
- Auto-plays muted on desktop when your product page opens
- **30 seconds or shorter** — people don't watch long ones
- Cover: what problem it solves → how it works → call to action
- Use Loom or QuickTime + iMovie if you don't have video skills

---

## The Day of Launch

### Announcing (Without Begging)
Post on Twitter, Instagram, LinkedIn — "Hey, we're on Product Hunt today!" with a link.

**Do NOT ask people to upvote.** PH detects vote manipulation. If people like it, they'll upvote. Ask them to check it out, give feedback, or comment.

If you have an email list, send one email. Same rule — share the link, invite feedback, don't beg.

### Your Maker Comment (First Comment Is Critical)
Write a genuine intro immediately after launch. This is your most-read piece of copy on PH.

Template:
```
Hi Product Hunt! 👋

I'm [Name]. I built [Product] because [personal problem you experienced].

[1-2 sentences on how it works and what makes it different]

[What stage you're at: beta / paying customers / etc.]

I'd love your honest feedback — what's missing? What would make this 10x better?

Happy to answer any questions!
```

Stay in the comments **all day**. Reply to every question. Be humble, not salesy. People are testing whether there's a real human behind the product.

### What NOT to Do
- Don't fight critics in comments — thank them and ask what they'd improve
- Don't brag about traction, funding, or press ("crushing it" language)
- Don't go silent after submission and hope for the best

---

## Traffic Expectations

| Outcome | Visitors | Concurrent | Conversions |
|---|---|---|---|
| Top 5 of the day | 10,000–20,000 | 200–500 | 2–5% sign up |
| Front page (not top 5) | 3,000–8,000 | 50–200 | 1–3% sign up |
| Not front page | 500–2,000 | 10–50 | 1–2% sign up |

**The journalist multiplier:** Being on PH puts you in front of reporters from TechCrunch, TNW, Mashable etc. who monitor it daily. Even a #3 finish typically yields 3–8 press articles within 72 hours — each bringing 5,000–20,000 additional visitors. This is often more valuable than the PH traffic itself.

---

## Server Prep

Make sure your server can handle traffic before you launch. At minimum:
- Enable basic caching on your pages
- Make your static assets (images, CSS, JS) load from a CDN (Cloudflare free tier works)
- Test with a load simulator if possible
- Have your monitoring (UptimeRobot, etc.) active so you know immediately if something breaks

---

## Relaunching (2.0, 3.0)

You can relaunch when you've made **significant** improvements — not minor bug fixes. Think: rebuilt core feature, new pricing model, major new audience. Use version numbers. Communicate with PH's community team first. Each relaunch resets the clock and gives you another press cycle.

---

## What Makes a PH Launch Fail

- Launching at a bad time (9pm PST, Friday, December holidays)
- No maker comment or engagement
- Tagline nobody understands
- Static logo thumbnail (vs. GIF)
- Not telling anyone about the launch
- Expecting PH alone to grow a business — it's a spike, not a channel

---

## Do This Today

Write your PH tagline and get three people outside your industry to tell you in one sentence what they think your product does. If they're wrong, rewrite it.
