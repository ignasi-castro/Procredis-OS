---
name: scrape-competitors
description: Weekly scrape of all tracked competitors' LinkedIn posts. Filters high-performers, tags them with pillar + hook formula, pushes to Notion Competitor Posts DB. Run every Sunday before /weekly-posts.
---

## WHAT THIS DOES

Scrapes the last 30 posts from each tracked competitor, keeps only high-performers (200+ likes OR 30+ comments), tags them automatically, and adds them to the Notion Competitor Posts database so they're available for /weekly-posts.

---

## STEP 1 — READ TRACKED COMPETITORS

Read `/Users/luiscastro/LinkedIn-Content-OS/brain/competitors.md` to get the current list of tracked creators and their LinkedIn URLs.

---

## STEP 2 — SCRAPE EACH COMPETITOR

For each competitor, run the Apify actor:

```bash
curl -s -X POST 'https://api.apify.com/v2/acts/supreme_coder~linkedin-post/runs?token=$APIFY_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{"urls":["<competitor_linkedin_url>"],"resultsLimit":30,"deepScrape":false}'
```

Wait for run to complete (poll status), fetch results from the dataset.

Extract per post: `url`, `text`, `likesCount`, `commentsCount`, `publishedAt`.

---

## STEP 3 — FILTER HIGH-PERFORMERS

Keep only posts where: `likes >= 200 OR comments >= 30`

Discard the rest.

---

## STEP 4 — DEDUPLICATE

For each high-performer, check if it already exists in Notion by searching:
- `mcp__claude_ai_Notion__notion-search` with `data_source_url: "collection://14d10dfe-efd5-4cb1-b936-15e5d4e2a415"` and a query using the first 50 chars of the post text

If a match is found: skip (already in Notion).
If not found: proceed to tag and add.

---

## STEP 5 — TAG EACH NEW POST

For each new post, determine:

**pillar_match** — pick the single best match:
- "GTM Tools & Tech Stack" — Clay, Apollo, Instantly, Smartlead, AI GTM, CRM, enrichment, tech stack
- "ABM" — account-based marketing, targeting, intent signals, named accounts, multi-channel
- "RevOps" — revenue operations, CRM architecture, pipeline hygiene, forecasting, health scores
- "Outbound Systems" — cold email, deliverability, sequences, reply rates, signal-based outbound
- "Storytelling" — founder story, lessons learned, contrarian takes, milestones, personal POV

**hook_formula** — identify from the first 2 lines:
- "Observation Authority" — sharp opinionated market take
- "Bold Stat + Controversy" — number challenging a common belief
- "Number Contrast" — two numbers creating tension
- "Case Study Result" — company name + specific outcome immediately
- "Insider Stack Reveal" — "here's exactly what we use"
- "Named Person Story" — opens with a real person and their situation
- "Old vs New" — contrast between old way and new way
- "Milestone + Lesson" — real milestone + non-obvious lesson

**angle** — one sentence: what specific insight drove the engagement

---

## STEP 6 — PUSH NEW POSTS TO NOTION

For each new tagged post, create a page in the Competitor Posts database using `mcp__claude_ai_Notion__notion-create-pages`:

```
parent: { type: "data_source_id", data_source_id: "14d10dfe-efd5-4cb1-b936-15e5d4e2a415" }
properties:
  Post Text: first 97 chars of post text
  Competitor: [competitor name]
  Likes: [number]
  Comments: [number]
  Pillar: [pillar_match]
  Hook Formula: [hook_formula]
  Angle: [angle sentence]
  LinkedIn URL: [post url]
  date:Date:start: [publishedAt as YYYY-MM-DD]
  Used For Post: false
content: full post text
```

Process in batches of 20 to avoid rate limits.

---

## STEP 7 — REPORT

After completing all competitors, report:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMPETITOR SCRAPE — [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Competitor name]: X new posts added (Y scraped, Z below threshold, W duplicates)
[Competitor name]: X new posts added
...
Total new posts in Notion: [number]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOP NEW POST THIS WEEK:
[competitor] — [likes]L / [comments]C
"[first line of post]"
Pillar: [pillar] | Hook: [hook formula]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then ask: "Ready to run /weekly-posts?"
