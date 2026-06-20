---
name: monitor-posts
description: Weekly monitor of Ignasi's published posts. Scrapes current engagement from LinkedIn, surfaces what's resonating with ICP, and generates insights to improve future posts. Run every Monday.
---

## WHAT THIS DOES

Pulls the latest engagement data on Ignasi's recent posts, identifies which topics and hooks are connecting with the ICP, and produces a short brief that informs the week's content decisions.

---

## STEP 1 — SCRAPE IGNASI'S RECENT POSTS

Use Apify to pull the latest posts from Ignasi's LinkedIn profile.

Run the actor via Bash:
```bash
curl -s -X POST 'https://api.apify.com/v2/acts/supreme_coder~linkedin-post/runs?token=$APIFY_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{"urls":["https://www.linkedin.com/in/ignasicastro1/"],"resultsLimit":30,"deepScrape":false}'
```

Wait for the run to complete (poll the run status), then fetch results from the dataset.

Extract for each post: `url`, `text` (first 80 chars as title), `likesCount`, `commentsCount`, `publishedAt`.

---

## STEP 2 — LOAD OUR POSTS DATA

Read `/Users/luiscastro/LinkedIn-Content-OS/data/our_posts.json`.

For each scraped post, match to our_posts.json by:
1. LinkedIn URL (exact match)
2. Or first 60 chars of text (fuzzy match)

If a match is found: update `total_likes` and `total_comments` with the fresh scraped values.
If no match is found: note it as a new untracked post (ask user if they want to add it).

Save the updated `our_posts.json`.

---

## STEP 3 — CALCULATE ICP ENGAGEMENT

ICP engagement cannot be scraped automatically — it requires manually checking who liked/commented.

Ask the user: "Do you want to log ICP engagement for any posts this week? If yes, which posts and what are the ICP like/comment counts?"

ICP = VP Sales, VP RevOps, CRO, Head of Marketing/Growth, Founders/CEOs at B2B companies (20–300 employees or $2M+ raised).

If they provide ICP data, update those posts in our_posts.json:
- `icp_likes` → new value
- `icp_comments` → new value
- `fluff_engagements` → (total_likes - icp_likes) + (total_comments - icp_comments)

If they skip: proceed with total engagement only.

---

## STEP 4 — GENERATE THE WEEKLY PERFORMANCE BRIEF

Analyze the data and produce a brief covering:

**Top performers this week** (by total likes):
- Post title | Pillar | Hook formula | Likes | Comments
- What made it work (hook type + angle)

**ICP signal** (if data available):
- Which posts had the highest ICP ratio (icp_likes / total_likes)?
- What pillar/topic was the ICP responding to?
- Flag any post where ICP engagement is unusually high: "buyers are paying attention to [topic]"

**Pillar performance** (rolling avg):
- Avg likes per pillar for last 30 days
- Which pillar is trending up or down?

**Hook formula ranking** (rolling avg):
- Which hook formulas are getting the most likes right now?

**Content gap:**
- Which pillar hasn't had a post in 7+ days?
- Which TOFU/MOFU/BOFU type is underrepresented?

**Voice insights:**
- Are shorter or longer posts performing better lately?
- Any hook pattern showing up in multiple top performers?

---

## STEP 5 — RECOMMENDATIONS

Based on the analysis, give 3 specific recommendations for the coming week:

1. **Pillar to double down on** — highest ICP signal
2. **Hook formula to use** — best performing in last 30 days
3. **Topic gap to fill** — what the ICP is not seeing yet but would respond to

Format as:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WEEKLY PERFORMANCE BRIEF — [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOP POST THIS WEEK:   [title] — [likes]L / [comments]C
BEST PILLAR (30d):   [pillar] — [avg]L avg
BEST HOOK (30d):     [hook formula]
ICP SIGNAL:          [what topic ICP engaged with most]

RECOMMENDATIONS FOR THIS WEEK:
1. [pillar + why]
2. [hook formula + why]
3. [topic gap + why]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Ask at the end: "Ready to run /weekly-posts with this data in mind?"
