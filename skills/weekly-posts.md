---
name: weekly-posts
description: Generate LinkedIn posts for Procredis one at a time, inspired by high-performing competitor posts. Analyze why the competitor post worked, then build our own version using the same hook/angle/CTA logic in our voice.
---

## ACCURACY RULES — NON-NEGOTIABLE

- DHL / FC Barcelona / Microsoft / Factorial / Lidl / Shopify = "calls booked" or "opportunities booked" — NEVER "clients" or "customers"
- SugarCRM = only confirmed client where result ($100M → $125M ARR) can be stated
- Saint-Gobain Spain = confirmed ABM deployment — OK as "deployment," not "result"
- Clay / Parabola / Userpilot = "the same ABM approach behind their growth" — NOT "our clients"
- Scale stats: "200k+ emails/month" | "900+ opportunities generated" | "25.4% reply rate" | "30+ databases tested"
- Never invent numbers. Never round up. If uncertain, omit.
- Forbidden phrases: end-to-end, holistic, synergy, best-in-class, AI-powered platform, game-changer, seamless, robust, leverage, utilize, cutting-edge, innovative, transformative, scalable solution

---

## STEP 1 — READ THE BRAIN

Read these files in parallel:
- `/Users/luiscastro/LinkedIn-Content-OS/brain/icp.md` — who we're writing for
- `/Users/luiscastro/LinkedIn-Content-OS/brain/services.md` — what we do, proof points
- `/Users/luiscastro/LinkedIn-Content-OS/brain/pillars.md` — the 5 content pillars and their angles
- `/Users/luiscastro/LinkedIn-Content-OS/brain/voice.md` — Ignasi's tone, sentence style, hook formulas

---

## STEP 2 — FIND A HIGH-PERFORMING COMPETITOR POST

Read `/Users/luiscastro/LinkedIn-Content-OS/data/competitor_posts.json`.

Ask the user (or auto-select if they say "just go"):
- Which pillar? (GTM Tools / ABM / RevOps / Outbound / Storytelling)
- Or pick the pillar with the best-performing competitor post not yet used (`used_for_post: false`)

From that pillar, find the post with the highest engagement score (`likes + comments × 3`).

Pull the **full text** of that post.

Then analyze it — answer these questions before writing anything:

**Hook analysis:**
- What is the exact hook (first 1–2 lines)?
- What makes it stop the scroll? (number, bold claim, controversy, authority, curiosity gap?)
- What emotion does it trigger in the reader?

**Angle analysis:**
- What is the core argument or insight?
- Is it contrarian, educational, validating, or aspirational?
- Why does this resonate with the ICP (VP Sales, RevOps, CRO, Founders)?

**Structure analysis:**
- How is the body organized? (numbered list, story, framework, before/after?)
- Where is the proof or credibility embedded?
- How long is it and why does that length work?

**CTA analysis:**
- What action does it ask for and why does that CTA fit this post?
- Is it a question, a comment trigger, a DM offer, or a repost ask?

**Why it performed well:**
- Write 2–3 sentences explaining why this post got the engagement it did. Be specific.

---

## STEP 3 — BUILD OUR VERSION

Now write our post. The goal is NOT to copy — it is to use the same strategic weapons (hook type, angle, structure, CTA mechanic) that made the competitor post work, loaded with our voice, our proof points, and our ICP.

**What to carry over from the competitor post:**
- The hook TYPE (e.g. bold contrarian claim, specific number, authority opener) — not the words
- The core angle (e.g. "everyone thinks X but actually Y") — adapted to our pillar
- The body structure (e.g. numbered framework, before/after) — rebuilt with our content
- The CTA mechanic (e.g. "comment X to get Y", question, DM offer) — if it fits us

**What to replace entirely:**
- All specific claims → our proof points and verified stats only
- Their tools → our tools (Clay, HubSpot, Instantly.ai, HeyReach.io, Parabola)
- Their credentials → Ignasi's credentials and Procredis's results
- Their clients/cases → our proof points (following accuracy rules above)

**Voice rules (from voice.md — always apply):**
- Short sentences. One idea per line.
- Lead with the result, never with context.
- Numbers: volume + metric + contrast wherever possible.
- No emojis unless they add visual structure (→ ✓ ok, 🚀 🙏 not ok)
- Tone: direct, confident, practitioner — not guru, not coach

**Post length:**
- TOFU: 150–250 words
- MOFU: 200–350 words
- BOFU: 250–400 words

Decide TOFU / MOFU / BOFU based on what the week needs (aim for 2 TOFU + 2 MOFU + 1 BOFU across the week).

---

## STEP 4 — SHOW BOTH POSTS SIDE BY SIDE

Display in this format:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMPETITOR POST
Competitor:   [name]
Likes:        [number]
Comments:     [number]
Date:         [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[full competitor post text]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHY IT WORKED
Hook:      [what made it stop the scroll]
Angle:     [the core insight and why it resonates with ICP]
Structure: [how the body is organized]
CTA:       [what it asks for and why it works]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OUR VERSION
Pillar:       [pillar]
Type:         [TOFU/MOFU/BOFU]
Hook formula: [name]
Char count:   [number]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[full post text — ready to copy-paste]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT WE BORROWED:  [hook type / angle / structure / CTA mechanic]
WHAT WE CHANGED:   [everything specific to them → our credentials, tools, proof points]
VISUAL:            [Text-only | Single image — what it shows | Carousel — slide breakdown]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## STEP 5 — ASK FOR APPROVAL

After showing both posts, ask:

**What would you like to do?**
1. **Approve** — upload to Notion and move to the next post
2. **Revise** — describe the change and I'll rewrite it
3. **Different competitor post** — pick another source for this pillar
4. **Different pillar** — skip this pillar, try another

---

## STEP 6 — WHEN APPROVED: UPLOAD + CONTINUE

When the user approves:

**1. Upload to Notion Content Pipeline** (`8077dce9-dc67-40fe-ae84-38790ee40c7c`):
- Name: first 60 chars of post text
- Post Stage: "Draft"
- Pillar: [pillar]
- Post Type: TOFU / MOFU / BOFU
- Hook Formula: [name]
- Hook Used: [first line verbatim]
- Source: "Competitor Variation"
- Visual Required: checked if visual needed
- Agent Notes: why this competitor post was chosen, what we borrowed
- Full post text in page body

**2. Mark the competitor post as used** — in `competitor_posts.json`, set `used_for_post: true` for the source post.

**3. Immediately move to the next post** — ask:
> "Done. Ready for the next post? Which pillar, or should I pick the best available?"

Keep going until the user stops or says they have enough for the week.
