# Solo Builder Playbook

A Claude Code plugin with **25 namespaced growth skills** for solo builders and indie hackers, powered by real strategies from **19 founders** who built apps to **$10K-$200K+ MRR**. Extracted from [Starter Story](https://www.youtube.com/@starterstory) interviews (2025-2026).

Install it and get founder-tested growth strategies tailored to your specific project — Claude reads your repo, understands what you're building, and delivers actionable advice with real founder citations.

## Install

```bash
npx superpowers install github:adrianchinghc/solo-builder-playbook-skill
```

Then restart Claude Code. All 25 skills are available under the `solo-builder` namespace.

## Usage

### Use the advisor for broad questions — Claude diagnoses first

> **You**: `/solo-builder:advisor` How do I get users?
>
> **Claude**: *reads your repo, detects a Next.js SaaS with Stripe* — "It looks like you're building a B2B SaaS. Here's what I'd recommend based on your stage..."

### Call a specific playbook directly

> **You**: `/solo-builder:product-hunt-playbook`
>
> **Claude**: *delivers the full Product Hunt launch playbook with timing, taglines, GIF strategy, and journalist trickle tactics*

> **You**: `/solo-builder:reddit-playbook`
>
> **Claude**: *pulls Roman's $0 to $34K MRR Reddit system — subreddit selection, post formats, rules for not getting banned*

### Request deliverables

> **You**: `/solo-builder:reddit-playbook` Write me some posts to promote my app
>
> **Claude**: *reads your product details, drafts 3 Reddit posts tailored to relevant subreddits with the right tone*

> **You**: `/solo-builder:advisor` Give me a 30-day growth plan
>
> **Claude**: *diagnoses your stage and product type, creates a week-by-week action plan with specific milestones*

## What Makes This Different

Most growth advice is generic. This plugin is contextual.

**Without context** (typical chatbot):
> "Consider using social media marketing. Create content that resonates with your target audience. Try multiple channels and see what works."

**With Solo Builder Playbook** (inside your project):
> It looks like you're building a B2B SaaS with Next.js and Stripe. Based on your stack and stage, here's what worked for **Roman** — he grew his SaaS to **$34K MRR through Reddit alone** by posting genuine how-to content in subreddits where his target users hung out. Here's your 30-day plan...

The advisor skill reads your `README.md`, `package.json`, and other project files to auto-detect your product type, tech stack, and stage — then routes to the right sub-skill with personalized action items.

## Skills

### Entry Point
| Skill | Command | What It Does |
|---|---|---|
| **Advisor** | `/solo-builder:advisor` | Diagnoses your situation, asks smart questions, routes to the right playbook |

### Launch
| Skill | Command | Founder Benchmark |
|---|---|---|
| **Product Hunt** | `/solo-builder:product-hunt-playbook` | 10K visitors + press trickle on launch day |
| **Hacker News** | `/solo-builder:hacker-news-playbook` | 50K-100K visitors from a single Show HN |
| **Press Outreach** | `/solo-builder:press-outreach-playbook` | 2-sentence pitch format that gets replies |
| **Perpetual Launch** | `/solo-builder:perpetual-launch-playbook` | Every feature = a new launch moment |

### Growth Channels
| Skill | Command | Founder Benchmark |
|---|---|---|
| **Distribution Strategy** | `/solo-builder:distribution-strategy` | Match channel to product type before building |
| **Reddit** | `/solo-builder:reddit-playbook` | Roman: $0 → $34K MRR via Reddit alone |
| **TikTok** | `/solo-builder:tiktok-playbook` | Louis: $0 → $800K/year via organic TikTok |
| **Twitter/X** | `/solo-builder:twitter-playbook` | Tibo: $700K/month via build-in-public |
| **Influencers** | `/solo-builder:influencer-playbook` | George: $17K MRR with $500 influencer spend |
| **Partnerships** | `/solo-builder:partnership-playbook` | Hassam: $25K MRR in 48 hours via equity deals |
| **SEO & Content** | `/solo-builder:seo-content-playbook` | Bhanu: 50K monthly clicks, $0 ad spend |
| **Discord** | `/solo-builder:discord-playbook` | Sam: $14K MRR in 6 months via Discord |
| **Open Source** | `/solo-builder:open-source-playbook` | Nevo: 5M downloads, $17K MRR |

### Product & Strategy
| Skill | Command | What It Covers |
|---|---|---|
| **Idea Selection** | `/solo-builder:idea-selection` | 4-filter test for ideas that can reach $10K MRR |
| **Indie Maker Philosophy** | `/solo-builder:indie-maker-philosophy` | Pieter Levels' MAKE methodology for $1M+ solo |
| **B2B SaaS Playbook** | `/solo-builder:b2b-saas-playbook` | Full playbook: idea to $100K MRR |
| **Mobile App Playbook** | `/solo-builder:mobile-app-playbook` | Content-first strategy for iOS/Android |
| **Vibe Coding** | `/solo-builder:vibe-coding` | Ship faster with AI tools as a solo founder |
| **When to Pivot** | `/solo-builder:pivot-playbook` | Signal detection: bad product vs. bad distribution |

### Monetization
| Skill | Command | Founder Benchmark |
|---|---|---|
| **Pricing & Revenue** | `/solo-builder:pricing-revenue` | Pricing models from $0 to $200K MRR |
| **Lifetime Deals** | `/solo-builder:ltd-strategy` | Mike: $100K runway from LTDs before scaling |
| **Onboarding** | `/solo-builder:onboarding-playbook` | George & Connor's free-to-paid conversion formula |

### Scaling & Exit
| Skill | Command | What It Covers |
|---|---|---|
| **Automation** | `/solo-builder:automation-playbook` | Build robots: cron jobs, Zapier, lean contractor model |
| **Exit & Acquisition** | `/solo-builder:exit-acquisition-playbook` | Buyer types, valuation multiples, broker vs. direct |

## The Founders

| Founder | Product | MRR | Key Channel |
|---|---|---|---|
| Tibo | Tweethunter/Taplio | $700K/mo | Twitter + Content |
| Mike | 5 SaaS apps | $200K/mo | SEO + LTDs |
| Roman | QuillBot alternative | $34K/mo | Reddit |
| Louis | GlowUp AI | $67K/mo | TikTok |
| George | Wrestle AI | $17K/mo | Influencers |
| Connor | Payout | $20K/mo | Onboarding |
| Nevo | Postiz | $17K/mo | Open Source |
| Bhanu | SiteGPT | $13K/mo | SEO/Free Tools |
| Hassam | WhatsBot | $25K first 48hrs | Partnerships |
| Sam | Algrow | $14K/mo | Discord |
| + 9 more... | | | |

## How This Was Made

Forked from [@drewautomates](https://x.com/drewautomates)' [solo-builder-playbook-skill](https://github.com/drewautomates/solo-builder-playbook-skill), which compiled strategies from 19 founder interviews on [Starter Story](https://www.youtube.com/@starterstory). Content analysis powered by [Noverload](https://noverload.com).


## License

MIT
