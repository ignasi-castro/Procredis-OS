---
name: log-engagement
description: Log daily engagement for a published LinkedIn post. Updates engagement_log.json with a snapshot and updates our_posts.json totals. Run daily for the first 7 days after publishing, then weekly.
---

## STEP 1 — IDENTIFY THE POST

Ask the user:
1. **Which post?** — paste the LinkedIn URL, or describe it (I'll look it up in our_posts.json by title/date)
2. **Today's numbers:**
   - Total likes so far
   - Total comments so far
   - ICP likes (likes from VP Sales, RevOps, CRO, Head of Marketing/Growth, Founders/CEOs at B2B companies)
   - ICP comments (same criteria)

If the user doesn't know the ICP breakdown, log 0 for ICP and note "not tracked" — don't block logging.

---

## STEP 2 — LOAD FILES

Read both files:
- `/Users/luiscastro/LinkedIn-Content-OS/data/our_posts.json`
- `/Users/luiscastro/LinkedIn-Content-OS/data/engagement_log.json`

Find the post in `our_posts.json` by matching LinkedIn URL or title (fuzzy match first 60 chars).

If the post isn't in our_posts.json yet (was just published), ask the user for:
- Pillar, post type, hook formula, published date, visual type
Then create the entry first.

---

## STEP 3 — UPDATE our_posts.json

Update the matching post's fields:
- `total_likes` → new value
- `total_comments` → new value
- `icp_likes` → new value
- `icp_comments` → new value
- `fluff_engagements` → (total_likes - icp_likes) + (total_comments - icp_comments)

If `linkedin_url` was missing, set it now.

---

## STEP 4 — APPEND TO engagement_log.json

Read `/Users/luiscastro/LinkedIn-Content-OS/data/engagement_log.json`.

Append a new entry to the `log` array:

```json
{
  "post_id": "<id from our_posts.json>",
  "date": "<today YYYY-MM-DD>",
  "days_since_published": <number>,
  "total_likes": <number>,
  "total_comments": <number>,
  "icp_likes": <number>,
  "icp_comments": <number>,
  "fluff_engagements": <number>
}
```

Calculate `days_since_published` from `published_date` in our_posts.json vs today.

Save the file.

---

## STEP 5 — SURFACE INSIGHTS

After saving, tell the user:
- Current totals vs the avg for this pillar (from our_posts.json data)
- Whether ICP engagement is above or below their historical rate
- If it's day 7+: summarise the post's final performance and whether it beat the pillar average
- Flag if ICP engagement is unusually high → "this post resonated with buyers, consider a follow-up"
