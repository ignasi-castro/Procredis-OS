---
name: weekly-posts
description: Generate 5 LinkedIn posts for the week based on brain data, competitor intelligence, and what's actually worked. Run Sunday night or Monday morning. 2 TOFU + 2 MOFU + 1 BOFU, one per pillar.
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

## STEP 1 — READ BRAIN (do all at once)

Read these files in parallel:
- `/Users/luiscastro/LinkedIn-Content-OS/brain/pillars.md`
- `/Users/luiscastro/LinkedIn-Content-OS/brain/voice.md`
- `/Users/luiscastro/LinkedIn-Content-OS/brain/icp.md`
- `/Users/luiscastro/LinkedIn-Content-OS/brain/services.md`
- `/Users/luiscastro/LinkedIn-Content-OS/brain/competitors.md`

---

## STEP 2 — READ PERFORMANCE DATA

Read `/Users/luiscastro/LinkedIn-Content-OS/data/our_posts.json`.

Extract:
- Top 3 posts by `total_likes` per pillar — note their `hook_formula` and what made them work
- Which hook formulas have the highest avg likes overall
- Which pillars are performing best
- What post types (TOFU/MOFU/BOFU) have been underused recently

Key patterns already established from data:
- **Best hook:** Observation Authority (28.7L avg) — lead with it when possible
- **Best pillars:** ABM (24.4L avg), GTM Tools (22.7L avg)
- **BOFU is underused** — must include 1 BOFU this week
- **Carousels = 0** — consider recommending one visual this week

---

## STEP 3 — READ COMPETITOR INTELLIGENCE

Read `/Users/luiscastro/LinkedIn-Content-OS/data/competitor_posts.json`.

For each pillar you're generating a post for, find the single highest-performing competitor post tagged with that pillar (sort by `likes` + `comments × 3`).

**Pull the FULL TEXT of that post.** You will be doing a close variation on it — you need every word.

If competitor_posts.json is empty, skip this step and rely on own data only.

---

## STEP 4 — CHECK NOTION PIPELINE

Use `mcp__claude_ai_Notion__notion-search` with:
- `data_source_url: "collection://8077dce9-dc67-40fe-ae84-38790ee40c7c"`

Find posts with status "Draft" or "Scheduled" created in the last 14 days.
Identify which pillars already have posts queued — avoid doubling up on the same pillar.

---

## STEP 5 — PLAN THE 5 POSTS

Assign one post per pillar (rotate through all 5 each week):
1. GTM Tools & Tech Stack
2. ABM
3. RevOps
4. Outbound Systems
5. Storytelling

Mix: 2 TOFU + 2 MOFU + 1 BOFU
- BOFU must go on whichever pillar has the best proof point available this week

For each post, identify:
- The exact competitor post you'll use as the base (competitor name, post id, likes count, full text preview)
- Which specific words to swap: their credentials → ours, their tools → our tools, their subject → our equivalent pillar
- Funnel stage — TOFU/MOFU/BOFU based on the week's mix target

Show this plan to the user and confirm before writing.

---

## STEP 6 — WRITE ALL 5 POSTS AS CLOSE VARIATIONS

**THIS IS THE MOST IMPORTANT RULE IN THIS SKILL.**

You are NOT writing new posts. You are doing close variations of proven competitor posts.

**The method:**
1. Take the exact competitor post text, word for word.
2. Identify every place that refers to the competitor's credentials, tools, company, clients, or subject.
3. Swap only those specific words/phrases for Procredis equivalents:
   - Their credentials → Ignasi's credentials ("I've built revenue systems for DHL, FC Barcelona, Microsoft")
   - Their tools → our tools (Clay, HubSpot, Instantly.ai, HeyReach.io, Parabola)
   - Their subject/niche → our equivalent pillar subject
   - Their company name → Procredis
   - Their clients → our proof points (keeping accuracy rules)
4. Keep every other sentence as close to the original as possible.
5. Target: 80%+ of the original words/flow should survive unchanged.

**What changes:**
- Credentials, tools, company name, specific clients
- Numbers that are specific to them (replace with our verified numbers)
- Any claims that would be false for us (omit or replace with what's true)

**What does NOT change:**
- The hook structure and first line format
- The flow and rhythm of the body
- The transition phrases
- The numbered sections and their order
- The CTA structure
- The tone and sentence length

**NEVER:**
- Rewrite the post from scratch using "the same theme"
- Create a new post "inspired by" the competitor post
- Change the structure because you think a different structure would work better
- Start with a different kind of hook

If you find yourself writing a post that doesn't look like the original with swapped words, stop and redo it as described above.

---

## STEP 7 — DISPLAY ALL 5 POSTS

Show each post in this format:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST [N]/5
PILLAR:        [name]
HOOK FORMULA:  [name]
TYPE:          [TOFU/MOFU/BOFU]
CHAR COUNT:    [number]
SOURCE:        [competitor name] — [their post likes]L / [their post comments]C (post id: [id])
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ORIGINAL (first 3 lines):
[first 3 lines of competitor post verbatim]

OUR VARIATION:
[full post text — ready to copy-paste]

WHAT CHANGED: [bullet list of the specific swaps made]
VISUAL: [Text-only | Single image — description | Carousel — what each slide covers]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

After all 5, show a summary table:

| # | Pillar | Source Competitor | Source Likes | Type | Char |
|---|--------|-------------------|--------------|------|------|
| 1 | ... | ... | ... | ... | ... |

---

## STEP 8 — ASK FOR ACTION

After displaying all 5, ask:

**For each post, what would you like to do?**
- **Approve** → run `/approve-post` to push to Notion
- **Revise** → describe the change and I'll rewrite it
- **Skip** → drop it from this week
- **Regenerate** → new version with different hook or angle

If the user says "approve all" or "approve [number]", push those posts to Notion using the approve-post skill logic:
- Create a page in database `8077dce9-dc67-40fe-ae84-38790ee40c7c`
- Properties: Post Stage = "Draft", Pillar, Hook Formula, Post Type, Visual Required
- Full post text in page body
