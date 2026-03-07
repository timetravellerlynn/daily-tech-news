# Daily Tech Intelligence — Run Instructions

## Goal
Produce a fully updated `index.html` dashboard each day by:
1. Gathering today's 20 most influential tech news stories
2. Migrating yesterday's content into the Historical Timeline sidebar
3. Writing the new stories into the Today's Intelligence main area

---

## Step 1 — Search for Today's News

Search for the **top 20 most influential tech news from the past 24 hours**, prioritizing:
- TechCrunch
- The Verge
- Wired
- (Supplement with Yahoo Finance, Apple Newsroom, Tech Startups if needed)

For each story, collect:
- **Title**
- **2-sentence summary**
- **Source URL**
- **B2B / AI Industry Impact** (2–3 sentences: how does this affect B2B sales motions or the AI supply chain?)
- **Tags** — assign 1–3 from: `AI`, `B2B`, `Sales`, `Infra`, `Policy`, `Funding`

---

## Step 2 — Read & Parse the Existing `index.html`

Open `index.html` and extract:

### A. From the `<div class="timeline">` (sidebar):
- Read all existing `.timeline-entry` blocks
- **Keep only the most recent 5 entries** (drop anything older to save tokens)
- If a `.timeline-empty` placeholder is present, discard it

### B. From the `<div class="news-grid">` (main area):
- Extract the date from `.main-header-right` (e.g., "March 6, 2026")
- Extract the headline from card #01 (`.card-title` of the first card) — this becomes the sidebar summary
- Count total cards (should be 20)
- This block will become a new `.timeline-entry` in the sidebar

---

## Step 3 — Build the Updated `index.html`

Using `template.html` as the design reference:

### Sidebar — Historical Timeline:
Insert a new `.timeline-entry` at the **top** of the timeline for the date being archived:
```html
<div class="timeline-entry">
  <div class="timeline-date">[ARCHIVED DATE]</div>
  <div class="timeline-headline">[HEADLINE FROM CARD #01 OF THAT DAY]</div>
  <span class="timeline-count">20 stories</span>
</div>
```
Then append the previously kept timeline entries below it (max 5 total entries in sidebar).

### Main Area — Today's Intelligence:
Replace the `.news-grid` content entirely with 20 new `.card` blocks for today's stories.

Update:
- The `<title>` tag to today's date
- `.main-header-right` date text to today's date
- `.main-footer` compiled date to today's date

---

## Step 4 — Write & Clean Up

1. **Save** the fully updated content as `index.html` (overwrite the existing file)
2. **Delete** any stale `.md` brief files (e.g., `Daily_Brief.md`) — `index.html` is now the single source of truth
3. Do **NOT** delete `template.html` or `task_instruction.md`

---

## Tag Reference

| Tag       | Color   | Use when...                                              |
|-----------|---------|----------------------------------------------------------|
| AI        | Blue    | Story is about AI models, labs, or AI-native products    |
| B2B       | Green   | Story directly affects enterprise/business workflows     |
| Sales     | Orange  | Story has clear sales pipeline or GTM implications       |
| Infra     | Purple  | Story is about hardware, data centers, chips, networking |
| Policy    | Yellow  | Story involves regulation, government, compliance        |
| Funding   | Green   | Story is about investment rounds or M&A                  |

---

## Token Optimization Notes
- Only parse the **last 5 days** of history from `index.html` sidebar — ignore older entries
- Do not re-summarize or re-analyze archived entries; only carry them forward as-is
- The main area is always fully replaced with fresh content — never carry over old cards
