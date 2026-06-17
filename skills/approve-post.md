---
name: approve-post
description: Push an approved LinkedIn post to the Notion Content Pipeline database. Can be called after /weekly-posts or /linkedin-post. Accepts post content directly or reads it from context.
---

## STEP 1 — COLLECT POST DETAILS

If the user ran /weekly-posts or /linkedin-post just before this, use that post's content and metadata from context.

Otherwise, ask the user for:
- **Post text** (full copy, paste it in)
- **Pillar** — GTM Tools & Tech Stack | ABM | RevOps | Outbound Systems | Storytelling
- **Hook formula** — which of the 8 formulas was used
- **Post type** — TOFU | MOFU | BOFU
- **Visual** — Text-only | Single-picture | Carousel | Infographic | Video
- **Scheduled date** (optional — if known)

---

## STEP 2 — CREATE NOTION PAGE

Use `mcp__claude_ai_Notion__notion-create-pages` with:

```json
{
  "parent": {
    "type": "data_source_id",
    "data_source_id": "8077dce9-dc67-40fe-ae84-38790ee40c7c"
  },
  "properties": {
    "Name": {
      "title": [{ "text": { "content": "<first 60 chars of post>" } }]
    },
    "Post Stage": {
      "select": { "name": "Draft" }
    },
    "Pillar": {
      "select": { "name": "<pillar>" }
    },
    "Hook Formula": {
      "select": { "name": "<hook_formula>" }
    },
    "Post Type": {
      "select": { "name": "<TOFU|MOFU|BOFU>" }
    },
    "Visual": {
      "select": { "name": "<visual type>" }
    }
  },
  "content": "<full post text as page body>"
}
```

If a scheduled date was provided, add:
```json
"Publish Date": {
  "date": { "start": "<YYYY-MM-DD>" }
}
```

---

## STEP 3 — CONFIRM

After creating the page, confirm to the user:
- "Done — pushed to Notion as Draft"
- Show the page title and which database it went into
- If Notion returns a URL for the page, show it

Do not push to our_posts.json at this stage — that happens after the post is published and engagement is being tracked via /log-engagement.
