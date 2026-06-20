---
name: add-competitor
description: Add a new competitor to the system. Given their LinkedIn URL, scrapes the last 6 months of posts, pushes high-performers to Notion, and adds them to the weekly scrape list. Usage: /add-competitor https://linkedin.com/in/username
---

## WHAT THIS DOES

Onboards a new competitor in one shot: scrapes their history, filters and tags high-performing posts, pushes them to the Notion Competitor Posts database, and adds the competitor to `competitors.md` so they're included in every future `/scrape-competitors` run.

---

## STEP 1 — CONFIRM THE COMPETITOR

Ask the user:
1. **LinkedIn profile URL** (if not already provided)
2. **Name** — how they're known (e.g. "Dan Rosenthal")
3. **Why track them?** — one sentence on their angle/niche (e.g. "GTM workflows and AI automation")

If already in `competitors.md`: "This competitor is already tracked. Run /scrape-competitors to get their latest posts."

---

## STEP 2 — SCRAPE LAST 6 MONTHS

Run the Apify actor with a higher results limit to get 6 months of posts:

```bash
curl -s -X POST 'https://api.apify.com/v2/acts/supreme_coder~linkedin-post/runs?token=$APIFY_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{"urls":["<linkedin_url>"],"resultsLimit":100,"deepScrape":false}'
```

Wait for run to complete (poll status every 10 seconds), fetch results from dataset.

Filter to posts from the last 6 months (published after today minus 180 days).

---

## STEP 3 — FILTER HIGH-PERFORMERS

Keep only posts where: `likes >= 200 OR comments >= 30`

Report how many total posts were scraped and how many passed the threshold.

---

## STEP 4 — TAG EACH POST

For each high-performer, determine:

**pillar_match:**
- "GTM Tools & Tech Stack" — Clay, Apollo, Instantly, Smartlead, AI GTM, CRM, enrichment, tech stack
- "ABM" — account-based marketing, targeting, intent signals, named accounts
- "RevOps" — revenue ops, CRM architecture, pipeline hygiene, forecasting
- "Outbound Systems" — cold email, deliverability, sequences, reply rates, signal-based outbound
- "Storytelling" — founder story, lessons, contrarian takes, milestones, personal POV

**hook_formula:**
- "Observation Authority" | "Bold Stat + Controversy" | "Number Contrast" | "Case Study Result"
- "Insider Stack Reveal" | "Named Person Story" | "Old vs New" | "Milestone + Lesson"

**angle** — one sentence: what insight drove this post's engagement

---

## STEP 5 — PUSH TO NOTION

Create a page in the Competitor Posts database for each new post:

```
parent: { type: "data_source_id", data_source_id: "14d10dfe-efd5-4cb1-b936-15e5d4e2a415" }
properties:
  Post Text: first 97 chars
  Competitor: [name]
  Likes: [number]
  Comments: [number]
  Pillar: [pillar_match]
  Hook Formula: [hook_formula]
  Angle: [angle]
  LinkedIn URL: [post url]
  date:Date:start: [YYYY-MM-DD]
  Used For Post: false
content: full post text
```

Process in batches of 20.

---

## STEP 6 — ADD TO COMPETITORS BRAIN

Read `/Users/luiscastro/LinkedIn-Content-OS/brain/competitors.md`.

Append a new entry at the bottom:

```markdown
## [Name]
- **LinkedIn:** [profile URL]
- **Why track:** [reason from Step 1]
- **Their angle:** [what topics they post about]
- **Added:** [today YYYY-MM-DD]
```

Save the file.

---

## STEP 7 — REPORT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
NEW COMPETITOR ADDED: [Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Posts scraped (6 months):  [total]
High-performers added:     [number pushed to Notion]
Top pillars:               [pillar breakdown]
Best post:                 [likes]L / [comments]C — "[first line]"

They will be included in every future /scrape-competitors run.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
