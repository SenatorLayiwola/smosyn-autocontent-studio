# AutoContent Studio & Dispatch
### AI-Powered Content Automation System for UK SMEs
**Built by [SMOSYN Digitals](https://smosyn.co.uk) — Wales, UK**

---

## The Story Behind This Build

This is not my first attempt at content automation.

Version 1 was a single n8n workflow — two parallel schedule triggers running side by side. One handled text generation and posting (Twin A). One handled image generation and posting (Twin B). It worked, but it had real problems:

- Topics were entered manually — no discovery, no intelligence
- No approval gates — content could post without review
- No hashtag generation
- No scheduling logic — bumper posting was a real issue
- No error handling — failures were silent
- Generic node names — impossible to debug or hand over to a client

It was functional. It was not production-ready.

**Version 1.1 is the rebuild.** Every weakness in v1 became a design requirement for v1.1. The result is what you see in this repository.


---

---

## What Is AutoContent Studio?

A production-grade AI content automation system built on n8n. It manages the complete content lifecycle — from live signal discovery and topic qualification, through AI content and image generation, to controlled scheduling and platform publishing — with human approval gates at every critical stage.

> Automation without control is chaos. Control without automation is inefficient. This system balances both.


---


## v1 vs v1.1 — What Changed

| Area | v1 (Twin A & B) | v1.1 (Current) |
|------|----------------|----------------|
| Topic sourcing | Manual entry only | 7 live sources + AI scoring |
| Architecture | 1 combined workflow | 5 separate modular workflows |
| Hashtags | None | Auto-generated per post |
| Approval gates | None | Telegram at every critical stage |
| Scheduling | Basic time triggers | AI-assigned + time distribution logic |
| Error handling | None — silent failures | Centralised error handler + Telegram alerts |
| Deduplication | None | Built into topic pipeline |
| Performance tracking | None | WF-04B built — pending API activation |
| Node naming | Generic (If, Switch1) | Descriptive and client-safe |
| Documentation | None | Full Master + Client docs |



## System Architecture
```
[ WF-01: Topic Discovery & AI Qualifier ]
              |
    (Telegram Approval Gate)
              |
              ▼
[ Google Sheets — Content Control Layer ]
              |
              ▼
[ WF-02: Auto Content Generator ]
   (Text + Hashtags + Image via DALL-E)
              |
              ▼
[ WF-03: Auto Content Publisher ]
   (LinkedIn | Facebook | Instagram | X)
              |
              ▼
[ WF-04B: Performance Tracker ] ← coming soon
```

---

## Workflows

| File | Workflow | Purpose |
|------|----------|---------|
| `WF01_Topic_Discovery_CLEAN.json` | Topic Discovery & AI Qualifier | Scans 7 live sources. AI scores topics. Telegram approval gate. |
| `WF02_Content_Generator_CLEAN.json` | Auto Content Generator | Generates platform-specific text, hashtags, and AI images. |
| `WF03_Publisher_CLEAN.json` | Auto Content Publisher | Posts to LinkedIn, Facebook, Instagram at scheduled time. |
| WF04B — coming soon | Performance Tracker | Fetches engagement metrics. Scores content. Identifies top performers. |

---

## Tech Stack

- **Automation:** n8n (self-hosted)
- **AI:** OpenAI GPT-4o + DALL-E 3
- **Image Hosting:** Cloudinary
- **Data Layer:** Google Sheets
- **Notifications & Approval:** Telegram Bot
- **Platforms:** LinkedIn · Facebook · Instagram · X

---

## Key Features

- 7 live signal sources scanned daily (RSS + Reddit + Google Trends)
- AI scores and ranks every topic before it enters production
- Platform-aware copy — LinkedIn posts are never the same as Instagram posts
- Hashtag generation integrated into content workflow
- Human approval gate at every critical stage
- One post per platform per run — no spam, no bulk posting
- Full audit trail via Google Sheets
- Centralised error handler with Telegram alerts
- Minimal cost architecture — every component is replaceable

---

## How to Use

### Prerequisites
- n8n instance (self-hosted or cloud)
- OpenAI API key
- Google Sheets + Google Drive OAuth2
- Telegram Bot token
- Cloudinary account
- LinkedIn, Facebook, Instagram credentials

### Import a Workflow
1. Open your n8n instance
2. Click **Add Workflow** → **Import from file**
3. Select the `.json` file
4. Update all placeholder values (see below)
5. Connect your credentials
6. Activate

### Placeholders to Replace

| Placeholder | What to Replace With |
|-------------|----------------------|
| `YOUR_GOOGLE_SHEET_ID` | Your Google Sheet ID from the URL |
| `YOUR_CONTENT_TOPIC_TAB_GID` | Tab GID for Content Topic sheet |
| `YOUR_CONTENT_PLAN_TAB_GID` | Tab GID for Content Plan sheet |
| `YOUR_TELEGRAM_CHAT_ID` | Your Telegram Chat ID |
| `YOUR_FACEBOOK_PAGE_ID` | Your Facebook Page ID |
| `YOUR_LINKEDIN_ORG_ID` | Your LinkedIn Organisation ID |
| `YOUR_SERPAPI_CREDENTIAL_ID` | Your SerpAPI credential ID in n8n |

---

## Cost Optimisation

This system was built using direct API integrations to keep running costs minimal. Every component is replaceable without rebuilding the architecture:

| Component | Current | Alternative |
|-----------|---------|-------------|
| Social Posting | Native platform nodes | Blotato, Buffer API, Publer |
| Image Hosting | Cloudinary | AWS S3, Bunny CDN |
| AI Generation | OpenAI | Claude, Gemini |
| Data Layer | Google Sheets | Airtable, Supabase |

---

## Documentation

Full Master Technical Documentation and Client Overview available on request.
Contact: [smosyn.co.uk](https://smosyn.co.uk)

---

## License

MIT — free to use and adapt. Attribution appreciated.

---

*Built with purpose. Documented with care. Designed to scale.*
