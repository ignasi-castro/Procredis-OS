---
name: monitor-posts
description: Monitor the last 7 days of Ignasi's posts. Track total engagement and ICP engagement per post. Classify who is engaging (ICP lead, competitor, or other). Update brain files with what's winning so future posts do more of it.
---

## WHAT THIS DOES

For each post published in the last 7 days: track total engagement, identify how much of it is ICP vs competitors vs noise, and update the brain so the content machine learns what resonates with buyers.

---

## STEP 1 — SCRAPE LAST 7 DAYS OF POSTS

Run the Apify actor to pull recent posts from Ignasi's profile:

```bash
curl -s -X POST 'https://api.apify.com/v2/acts/supreme_coder~linkedin-post/runs?token=$APIFY_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{"urls":["https://www.linkedin.com/in/ignasicastro1/"],"resultsLimit":10,"deepScrape":false}'
```

Wait for the run to complete (poll status), fetch results.

Filter to posts where `publishedAt` is within the last 7 days.

If no posts in the last 7 days: tell the user and stop.

---

## STEP 2 — FOR EACH POST: COLLECT ENGAGEMENT

For each post from the last 7 days, extract:
- Post title (first 60 chars)
- Total likes
- Total comments
- LinkedIn URL

Then ask the user:

> "I found [N] posts from the last 7 days. For each one, I need you to review who liked and commented — go to the post on LinkedIn and paste in the names + job titles of people who engaged. Focus on anyone that looks like a lead or a competitor."

For each post, the user provides a list like:
```
- John Smith — VP Sales at Acme Corp
- Maria García — RevOps Manager at SaaS Co
- Dan Rosenthal — GTM consultant (competitor)
- [etc]
```

If the user can't or won't review engagement for a post, skip ICP classification for that post and log total only.

---

## STEP 3 — CLASSIFY EACH PERSON

For each name/title the user provides, classify them as:

**ICP** — if they match any of:
- VP Sales, Head of Sales, Sales Director, CRO
- VP RevOps, Head of RevOps, Revenue Operations Manager
- VP Marketing, Head of Growth, CMO
- Founder, Co-founder, CEO at a B2B company (any size)
- Any GTM leader at a B2B SaaS company

**Competitor** — if they are:
- A GTM consultant, LinkedIn content creator, agency owner, or any of the 5 tracked competitors and their networks

**Other** — everyone else (SDRs, students, recruiters, etc.)

Count per post:
- `icp_count` — number of ICP engagements
- `competitor_count` — number of competitor engagements
- `other_count` — everyone else
- `icp_ratio` — icp_count / total_likes (as a %)

---

## STEP 4 — UPDATE our_posts.json

Read `/Users/luiscastro/LinkedIn-Content-OS/data/our_posts.json`.

For each monitored post, find it by LinkedIn URL or title and update:
- `total_likes` → fresh scraped value
- `total_comments` → fresh scraped value
- `icp_likes` → icp_count
- `icp_comments` → ICP comments count
- `fluff_engagements` → total_likes - icp_count

Save the file.

---

## STEP 5 — IDENTIFY WHAT'S WINNING WITH ICP

Look across all posts from the last 7 days. Find patterns in the posts with the highest `icp_ratio`:

- What pillar were they in?
- What hook formula did they use?
- What was the core angle or topic?
- How long was the post?
- What was the CTA?

---

## STEP 6 — UPDATE THE BRAIN

Based on what's winning with ICP, update the relevant brain files:

**Update `/Users/luiscastro/LinkedIn-Content-OS/brain/voice.md`:**
- Add a "What's working now" section (or update it if it exists) with:
  - Which hook formulas are getting ICP engagement
  - Sentence length and post length that ICP responds to
  - Any specific phrases or angles that drove ICP reactions

**Update `/Users/luiscastro/LinkedIn-Content-OS/brain/pillars.md`:**
- Under the winning pillar(s), add a note: "ICP responding to: [specific topic/angle] — [date]"
- If a pillar got zero ICP engagement this week, note it

Keep updates concise — one or two lines per insight. Don't overwrite existing content, append to it.

---

## STEP 7 — REPORT

Show a simple per-post summary:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST MONITOR — [date range]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Post title]
Total: [likes]L / [comments]C
ICP:   [icp_count] ([icp_ratio]%) | Competitors: [n] | Other: [n]
Pillar: [pillar] | Hook: [hook formula]
─────────────────────────────────────────────────
[Post title]
...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT'S WINNING WITH ICP THIS WEEK:
[2-3 lines: which pillar, hook, angle got the most ICP engagement]

Brain updated: voice.md + pillars.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
