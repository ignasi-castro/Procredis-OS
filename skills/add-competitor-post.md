---
name: add-competitor-post
description: Add a single high-performing competitor post to the brain (competitor_posts.json). Use when you spot a great post manually. Claude tags it with pillar + hook formula automatically — no API needed.
---

## STEP 1 — COLLECT POST DATA

Ask the user for:
1. **LinkedIn URL** of the post (required)
2. **Post text** — paste the full copy
3. **Likes** count
4. **Comments** count
5. **Competitor name** — if not obvious from URL, ask which tracked creator this is

Tracked creators for reference:
- Dan Rosenthal (linkedin.com/in/dan-m-rosenthal)
- Fivos Aresti (linkedin.com/in/fivosaresti)
- Michel Lieben (linkedin.com/in/michel-lieben)
- Janis Zech (linkedin.com/in/janiszech)
- Nathan Merzvinskis (linkedin.com/in/nathan-merzvinskis)

If the post is from someone not on this list, still add it — just note the name.

---

## STEP 2 — CHECK THRESHOLD

If likes < 200 AND comments < 30, warn the user:
"This post is below the tracking threshold (200+ likes or 30+ comments). Add anyway?"
Proceed if they confirm.

---

## STEP 3 — TAG THE POST (no API — done here)

Read the post text and determine:

**pillar_match** — pick one:
- "GTM Tools & Tech Stack" — tools: Clay, Apollo, Instantly, Smartlead, AI GTM, CRM, enrichment, sequencing
- "ABM" — account-based marketing, targeting, intent signals, multi-channel, named accounts
- "RevOps" — revenue operations, CRM architecture, pipeline hygiene, speed to lead, health scores
- "Outbound Systems" — cold email, deliverability, sequences, reply rates, signal-based outbound
- "Storytelling" — founder story, lessons learned, contrarian takes, milestones, personal POV

**hook_formula** — identify from the first 2 lines:
- "Bold Stat + Controversy" — opens with a number challenging a common belief
- "Number Contrast" — two numbers side by side creating tension
- "Case Study Result" — names a company + specific outcome immediately
- "Insider Stack Reveal" — "here's exactly what we use / what's inside"
- "Observation Authority" — sharp opinionated market observation
- "Named Person Story" — opens with a real person and their situation
- "Old vs New" — contrast between old way vs new way
- "Milestone + Lesson" — real milestone + the non-obvious lesson

**angle** — one sentence: what specific insight, tension, or data point drove the engagement on this post

---

## STEP 4 — DEDUPLICATE AND SAVE

Read `/Users/luiscastro/LinkedIn-Content-OS/data/competitor_posts.json`.

Generate id = first 12 chars of md5(post_text).

Check if id already exists in posts array. If yes: "Already in brain — skipping."

If new, append:

```json
{
  "id": "<md5 first 12 chars>",
  "competitor": "<name>",
  "linkedin_url": "<post URL>",
  "text": "<full post text>",
  "date": "<YYYY-MM-DD if known, else today>",
  "likes": <number>,
  "comments": <number>,
  "pillar_match": "<pillar>",
  "hook_formula": "<hook formula>",
  "angle": "<one sentence>",
  "used_for_post": false,
  "our_post_id": "",
  "added_at": "<today YYYY-MM-DD>"
}
```

Save the file.

---

## STEP 5 — CONFIRM AND SUGGEST

After saving:
- Confirm: "Added to brain — [competitor] | [pillar] | [hook_formula]"
- Show the angle in one sentence
- If this is the highest-performing post in its pillar so far, flag it: "Best [pillar] post in the brain — strong angle for next /weekly-posts"
