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

For each pillar you're generating a post for, find the highest-performing competitor post tagged with that pillar.
Note: `angle` (what made it work), `hook_formula` used, `likes` count.

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

For each post, select:
- **Hook formula** — default to Observation Authority or Insider Stack Reveal (best performers). Use competitor data to validate angle.
- **Angle** — the specific insight, tension, or data point that drives engagement. Taken from: competitor post angle, our own top-performer pattern, or a proof point from services.md
- **Funnel stage** — TOFU/MOFU/BOFU based on the week's mix target

---

## STEP 6 — WRITE ALL 5 POSTS

For each post, follow this exact structure:

```
HOOK (lines 1–2):
  - Under 140 chars
  - Never start with "I"
  - Specific number, name, or sharp observation — never vague
  - Must stop scroll before "see more"

BRIDGE (lines 3–4):
  - "Here's why." / "Here's how." / "Here's what we found." / "Most teams get this wrong."

BODY:
  - Short paragraphs — max 2–3 lines per block
  - One idea per paragraph
  - Clear line breaks between every block
  - Numbered or bulleted framework where applicable
  - Embed proof points naturally in body, never appended at end
  - 3 types of numbers where possible: volume + metric + contrast

CLOSE:
  - Punchy takeaway, question that invites comments, or soft CTA
  - No "comment YES if you agree" or hollow engagement bait

OPTIONAL P.S.:
  - Only if it adds a genuinely useful second insight or CTA
```

Character count targets:
- Educational / framework: 1,900–2,700
- Story / personal: 1,400–2,100
- Comment-gated / list: 1,200–1,800

**Internal checklist before showing each post (fix silently if failing):**
- [ ] Hook stops scroll in under 2 seconds?
- [ ] No false claims?
- [ ] 3 specific numbers in body?
- [ ] Proof in lines 1–3?
- [ ] Short sentences + line breaks throughout?
- [ ] CTA at end?
- [ ] No forbidden phrases?
- [ ] Character count in range?

If a post fails more than 2 checklist items, rewrite before showing.

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
INSPIRED BY:   [competitor name + their post angle, or "own data"]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[full post text — ready to copy-paste]

VISUAL: [Text-only | Single image — description | Carousel — what each slide covers]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

After all 5, show a summary table:

| # | Pillar | Hook | Type | Char |
|---|--------|------|------|------|
| 1 | ... | ... | ... | ... |

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
