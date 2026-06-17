---
name: linkedin-post
description: Generate a single LinkedIn post for Procredis on demand. Usage examples: /linkedin-post revops observation-authority mofu | /linkedin-post abm case-study | /linkedin-post (auto-detects gap in pipeline)
---

## ACCURACY RULES — READ BEFORE ANYTHING ELSE

**Proof point accuracy:**
- DHL / FC Barcelona / Microsoft / Factorial / Lidl / Shopify = "calls booked" or "opportunities booked" — NEVER "clients," "customers," or "case studies"
- SugarCRM = the only confirmed client where result ($100M → $125M ARR) can be stated — "case study," not "client reference"
- Saint-Gobain Spain = confirmed ABM deployment — OK as "deployment," not "result"
- Clay / Parabola / Userpilot = "the same ABM approach behind their growth" — NOT "our clients"
- Scale stats you MAY use: "200k+ emails/month" | "900+ opportunities generated" | "25.4% reply rate" | "30+ databases tested"

**Numbers policy:** Only use numbers from the brain files. Never invent or round up. If uncertain, omit.

**Positioning:** Procredis is an "AI-native revenue architecture firm." We DO it at scale. Competitors TEACH it.

**Forbidden phrases:** end-to-end, holistic, synergy, best-in-class, AI-powered platform, game-changer, seamless, robust, leverage, utilize, cutting-edge, innovative, transformative, scalable solution

---

## STEP 1 — PARSE THE REQUEST

Parse the user's input for:
- **Pillar:** outbound / gtm-tools / revops / abm / storytelling / mcp (if not specified → auto-detect)
- **Hook formula:** bold-stat / number-contrast / case-study / insider-stack / observation-authority / named-person / old-vs-new / milestone (if not specified → auto-pick)
- **Type:** tofu / mofu / bofu (if not specified → default tofu)

If no arguments: use `mcp__claude_ai_Notion__notion-search` with `data_source_url: "collection://8077dce9-dc67-40fe-ae84-38790ee40c7c"` to find which pillar has the fewest drafts this week. Generate for that pillar.

---

## STEP 2 — READ BRAIN FILES

Read in parallel:
1. `/Users/luiscastro/LinkedIn-Content-OS/brain/voice.md` — tone, 8 hook formulas, post structure
2. `/Users/luiscastro/LinkedIn-Content-OS/brain/pillars.md` — read the section for the requested pillar
3. `/Users/luiscastro/LinkedIn-Content-OS/brain/services.md` — proof points and positioning
4. `/Users/luiscastro/LinkedIn-Content-OS/brain/icp.md` — who we're writing for

Then read for data signals:
5. `/Users/luiscastro/LinkedIn-Content-OS/data/our_posts.json` — find top 2 posts for this pillar by total_likes, note their hook_formula and what worked
6. `/Users/luiscastro/LinkedIn-Content-OS/data/competitor_posts.json` — find top 2 competitor posts for this pillar by likes, note the angle field

---

## STEP 3 — WRITE THE POST

Apply all writing rules:

**Structure:**
```
LINE 1-3:   HOOK — Bold claim, specific number, or tension. Stop the scroll.
LINE 4-5:   BRIDGE — "Here's why." / "Here's how." / "Here's what we found."
LINE 6-50:  BODY — Numbered framework. 5–8 points. Proof embedded in body.
LAST 2-3:   CTA
OPTIONAL:   P.S.
```

**Rules:**
- Lead with a result. Never with context.
- 3 types of numbers: volume + metric + contrast.
- Short sentences. Line break after every 1–2 sentences.
- Proof embedded in body, not appended at the end.
- No forbidden phrases.
- Character count: educational 1,900–2,700 | story 1,400–2,100 | comment-gated 1,200–1,800

**Internal checklist (fix before showing):**
- [ ] Hook stops scroll in under 2 seconds?
- [ ] 3 specific numbers?
- [ ] Proof in lines 1–3?
- [ ] Numbered structure in body?
- [ ] Short sentences, line breaks?
- [ ] CTA at end?
- [ ] No false claims?
- [ ] No forbidden phrases?
- [ ] Character count in range?

If post fails more than 2 items, rewrite before showing.

---

## STEP 4 — SHOW TO USER

Display with clear formatting:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PILLAR:        [name]
HOOK FORMULA:  [name]
TYPE:          [TOFU/MOFU/BOFU]
CHAR COUNT:    [number]
CTA TYPE:      [comment keyword / question / DM / repost]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[full post text — ready to copy-paste]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VISUAL BRIEF:
[specific description of what the image/infographic should show]

AGENT NOTES:
[accuracy checks run + why this hook was chosen]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## STEP 5 — ASK FOR ACTION

After displaying the post, ask:

**What would you like to do?**
1. Save to Notion as Draft
2. Revise — [describe the change you want]
3. Generate a different version with [different hook / pillar / type]
4. Nothing — just showing me

**If option 1:** Create a page in the Content Pipeline database:
- `parent`: `{"type": "data_source_id", "data_source_id": "8077dce9-dc67-40fe-ae84-38790ee40c7c"}`
- Properties: Post Stage = "Draft", Source = "On-Demand", Pillar, Hook Formula, Post Type, Visual Required = true, Hook Used, Agent Notes
- Full post text in page body.

**If option 2:** Apply the revision and re-display (start at Step 3).

**If option 3:** Re-run with the new parameters (start at Step 1).
