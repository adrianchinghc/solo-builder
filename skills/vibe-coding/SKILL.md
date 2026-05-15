---
name: vibe-coding
description: "Use this BEFORE advising on building faster with AI tools, using Cursor, Bolt, or Replit, or shipping an MVP without a technical co-founder. Invoke before answering 'how do I build this faster?', 'which AI coding tool should I use?', or 'can I build this without a developer?'"
metadata:
  plugin: solo-builder
---

# Vibe Coding: Building Apps Without a CS Degree

## The Evidence

Founders with zero or minimal coding background have built production apps generating real revenue using AI coding tools.

## The Default Stack (2025-2026)

| Layer | Tool | Cost | Why |
|-------|------|------|-----|
| AI Coding | Cursor ($20-200/mo) or Claude Code ($200/mo) | $20-200/mo | Most AI-friendly coding tools |
| Frontend | Next.js + TypeScript | Free | Most supported by AI, huge community |
| Backend/DB | Supabase | $0-30/mo | Auth, database, storage in one |
| Hosting | Vercel | $0-20/mo | Deploy directly from code editor |
| Payments | Stripe (web) or RevenueCat (mobile) | Transaction fees | Industry standard |
| Email | Resend | $0-20/mo | Developer-friendly |
| AI Inference | OpenAI or Anthropic API | $40-100/mo | For AI features in your app |
| Mobile (optional) | Rork or Expo | $25-30/mo | Cross-platform mobile apps |

**Total infrastructure**: ~$100-400/month to run a $10K+ MRR business.

## The 48-Hour Sprint

| Hours | Activity |
|-------|----------|
| 1-4 | Map existing systems, SOPs, workflows of target users |
| 5-12 | Build core features with Cursor (functional, not perfect) |
| 13-20 | Test, fix bugs, iterate with Cursor |
| 21-30 | Polish UI and branding ("branding is everything") |
| 31-40 | Edge case testing, ensuring stability |
| 41-48 | Final polish, prep demo, record video |

## A Non-Technical Founder's Learning Path

Evolution from zero coding knowledge to a shipped product:

1. **Started**: Described idea to ChatGPT voice mode, got code
2. **First tool**: Copy-pasted code into Notepad (yes, Notepad)
3. **Upgrade 1**: Discovered VS Code, still copy-pasting from ChatGPT
4. **Upgrade 2**: Switched to Cursor (raw dogging it in VS Code is dumb when Cursor exists)
5. **First MVP**: Built in one week with Cursor, deployed on Heroku
6. **First user**: Got an "application error" screen... but still used the core features
7. **Lesson**: As long as what you're trying to solve works, you can ship anything

## Key Principles

### 1. Domain knowledge > coding skill
Every vibe coder who succeeded had deep understanding of their target user's pain. The code was the easy part.

### 2. Ship broken, fix fast
First users getting error screens, APIs going down at launch — these happen and you recover. Shipping > perfection.

### 3. Know when to hire
The greatest ROI often comes from hiring a developer for $250 on Fiverr for payments and auth integration. Vibe code the 80%, hire for the 20% you can't figure out.

### 4. Use AI as your advisor
When you hit an issue, copy the error logs and throw them into ChatGPT or Claude. Use AI as your on-demand technical advisor throughout the build.

### 5. Expand past vibe coding at $5K MRR
Vibe coding is great to release quickly and validate ideas, but once you start moving past $5K a month, you should start investing in product quality.

## Common Vibe Coding Mistakes

- Spending months "learning to code" before building (just start prompting)
- Not using the right tool (Cursor > VS Code for AI-assisted coding)
- Over-engineering the MVP (functional > perfect)
- Not hiring for things outside your ability (payments, auth, complex integrations)
- Building features nobody asked for (talk to users first)

## Timeline: Zero to Revenue

| Week | Activity |
|------|----------|
| 1 | Choose idea based on domain knowledge, start prompting in Cursor/Claude Code |
| 2 | Core functionality working, deployed somewhere (even if buggy) |
| 3 | First users testing, collecting feedback daily |
| 4 | Iterating based on feedback, fixing critical bugs |
| 5-6 | Launch publicly, start distribution (see distribution playbooks) |
| 8-12 | If traction exists, $1K-5K MRR |
