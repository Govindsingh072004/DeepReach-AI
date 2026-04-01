# DeepReach-AI — B2B Outreach Automation

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Groq](https://img.shields.io/badge/LLM-Groq%20LLaMA%203-F54F29?style=flat-square)
![Tavily](https://img.shields.io/badge/Research-Tavily%20API-6366F1?style=flat-square)
![SerpAPI](https://img.shields.io/badge/Jobs-SerpAPI%20%2B%20Adzuna-10B981?style=flat-square)
![Instantly](https://img.shields.io/badge/Delivery-Instantly.ai-0EA5E9?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-gray?style=flat-square)

> **Turns active job postings into hyper-personalized outreach emails — research, scoring, and writing handled entirely by AI.**

---

## The Problem

Sales teams spend hours manually researching companies, guessing who might need their services, and writing outreach emails that get ignored. There's no clear signal for *when* a company actually has a need — so most outreach lands at the wrong time, to the wrong person, with the wrong message.

The other side of the problem is personalization. Decision-makers get dozens of cold emails every day. Anything that reads like a template gets deleted. But writing a genuinely researched email for every single lead isn't possible at scale — not manually.

> **A company posting a job is a company that already knows it has a gap.**
> That's not a cold lead — that's a warm signal hiding in plain sight.

If a company is actively hiring a Salesforce Developer or an ML Engineer, they have a confirmed, time-sensitive need. DeepReach-AI picks up that signal, researches the company in real time, and generates an email specific enough to feel like it was written by someone who actually did their homework.

---

## How It Works

```
┌─────────────────────────────────────────────────────┐
│  INPUT — Apollo CSV  (leads, emails, revenue, roles) │
└──────────────────────────┬──────────────────────────┘
                           ↓
          ┌────────────────────────────┐
          │  01  Job Signal Detection  │  SerpAPI · Adzuna
          └────────────────────────────┘
                           ↓
          ┌────────────────────────────┐
          │  02  Company Intelligence  │  Tavily API · Groq LLaMA
          │      + Pain Point Research │
          └────────────────────────────┘
                           ↓
          ┌────────────────────────────┐
          │  03  Lead Enrichment       │  Apollo CSV merge
          │      + AI Scoring          │  lead_scoring.py
          └────────────────────────────┘
                           ↓
          ┌────────────────────────────┐
          │  04  Email Generation      │  Groq LLaMA 3 8B
          │      (Hyper-Personalized)  │  AsyncIO · Anti-spam
          └────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────┐
│  OUTPUT — Instantly_Ready_Leads.csv                 │
│  (Subject + Body per lead → Direct Instantly upload) │
└─────────────────────────────────────────────────────┘
```

### Stage 01 — Job Signal Detection
Scrapes live job postings for roles that indicate a staffing need — Salesforce developers, ML engineers, data scientists. Deduplicates across runs via `seen_jobs.json`.

**Tools:** `SerpAPI` · `Adzuna API`

### Stage 02 — Company Intelligence + Pain Point Research
For every company found, runs automated internet research — pulling revenue, employee count, recent news, market activity, and business pain points in real time. No static databases. Actual live context per lead.

**Tools:** `Tavily API` · `Groq LLaMA 3` · structured JSON output

### Stage 03 — Lead Enrichment + AI Scoring
Apollo CSV data is merged with live research output. CEO name, verified email, domain, and LinkedIn are extracted. Each lead gets an AI-generated score based on company size, revenue, and hiring volume.

**Tools:** `Apollo.io CSV` · `Data_Enrichment.py` · `lead_scoring.py`

### Stage 04 — Hyper-Personalized Email Generation
Groq (LLaMA 3 8B) generates a unique email per lead using company-specific context. Role-aware logic picks the right positioning — Salesforce, AI/ML, or blended. A **40+ word forbidden list** eliminates marketing tone. Output consistently passes AI-detection tools as human-written.

**Tools:** `Groq LLaMA 3 8B` · `AsyncIO (Semaphore 3)` · `API key rotation`

### Stage 05 — Campaign-Ready Output
Outputs a structured CSV with generated subject lines and email bodies — formatted for direct upload to Instantly.ai.

**Tools:** `Instantly.ai API` · `Google Sheets API`

---

## Data Flow — What Each File Looks Like

**Input — Apollo CSV export**

| First Name | Title | Company | Email | Annual Revenue |
|---|---|---|---|---|
| Marc | CEO | Actian | marc@actian.com | $56.5M |
| Emma | CTO | Actian | emma@actian.com | $56.5M |

**After Enrichment**

| Company_Name | CEO_Full_Name | Official_Domain | LinkedIn_URL |
|---|---|---|---|
| Actian Corporation | Marc Potter | actian.com | linkedin.com/in/pottermarc |

**Final Output — Instantly Ready CSV**

| Generated_Email_Subject | First Name | Company Name | Email |
|---|---|---|---|
| Growth and AI Engineering at Photon Group | Kushmitha | Photon Group | k@photon.com |

---

## Example Output Email

```
Subject : Growth and AI Engineering at Photon Group
To      : kushmitha@photongroup.com

Hi Kushmitha,

Saw that Photon Group recently expanded its AI practice — the move toward
enterprise automation makes sense given where the market is heading.

You're currently looking to bring on a few engineers with ML and data
pipeline experience. Finding people who can actually deliver in that
environment, not just interview well, is genuinely hard right now.

At AnavClouds, we work with teams like yours by placing pre-vetted AI
and data engineers who are ready to contribute from day one — contract
or direct hire, depending on what works for the team.

A few things that tend to matter in this context :

  * Engineers screened specifically for production ML, not just theory
  * Onboarding in days rather than weeks
  * Flexible engagement — contract, contract-to-hire, or direct
  * Culture fit evaluated alongside technical fit

Worth a short conversation if the timing is right.
```

---

## Business Impact

| | ❌ Before DeepReach-AI | ✅ After DeepReach-AI |
|---|---|---|
| **Research** | Hours of manual company digging | Automated intel for 100s of leads |
| **Personalization** | Generic templates | Unique email per company context |
| **Lead Quality** | Cold leads, random timing | Warm leads via hiring signals |
| **Speed** | Manual copy-paste | Campaign-ready CSV in minutes |
| **Delivery** | Spreadsheet juggling | Direct Instantly.ai upload |

---

## File Breakdown

| File | Stage | What It Does |
|---|---|---|
| `project_2.py` | 01 — Sourcing | Scrapes job postings via SerpAPI + Adzuna. Deduplication via `seen_jobs.json` |
| `company_intel.py` | 02 — Intel | Extracts revenue + employee count. Groq structures raw data into JSON |
| `deep_company_research.py` | 02 — Research | Tavily API pulls market news, pain points, and growth signals |
| `company_cleaner.py` | 02 — Cleaning | Deduplicates and normalizes company names before enrichment |
| `Data_Enrichment.py` | 03 — Enrichment | Merges Apollo data with research. Extracts CEO, domain, verified email |
| `lead_scoring.py` | 03 — Scoring | AI scores each lead by revenue, employee count, hiring volume |
| `email_generation.py` | 04 — Email Gen | Async LLaMA generation with anti-spam prompting. Google Sheets sync |
| `API_rotation.py` | All stages | Round-robin Groq API key rotation. Prevents rate limit failures |
| `instantly_mail_send.py` | 05 — Delivery | Pushes finalized emails to Instantly.ai via API |
| `upload_to_sheets.py` | 05 — Storage | Syncs all enriched data to Google Sheets dashboard |

---

## Setup

**1. Clone and install**
```bash
git clone https://github.com/g07oct2004-hash/Client_Finder_AI.git
cd Client_Finder_AI
pip install -r requirements.txt
```

**2. Add your API keys to `.env`**
```env
# Groq — add multiple keys for rotation
GROQ_API_KEY_1=your_key_here
GROQ_API_KEY_2=your_key_here

SERPAPI_KEY=your_serpapi_key
ADZUNA_APP_ID=your_adzuna_id
ADZUNA_APP_KEY=your_adzuna_key
TAVILY_API_KEY=your_tavily_key
INSTANTLY_API_KEY=your_instantly_key
GOOGLE_SERVICE_ACCOUNT_JSON={"type":"service_account",...}
```

**3. Export leads from Apollo.io**

Place your Apollo CSV export in the root directory. Standard Apollo format with company, title, email, and revenue columns.

**4. Run the pipeline**
```bash
# Full pipeline
python project_2.py

# Or use the Streamlit UI
streamlit run app.py
```

**5. Upload output to Instantly.ai**

Use `Instantly_Ready_Leads.csv` — pre-formatted with subject lines and email bodies. Direct upload, no reformatting needed.

---

## Key Engineering Decisions

**Async pipeline with Semaphore** — `email_generation.py` uses `asyncio` with `Semaphore(3)`, processing 3 leads concurrently for ~3x throughput vs sequential.

**API key rotation** — `API_rotation.py` manages multiple Groq keys in round-robin. If one key fails mid-batch, system rotates automatically with zero manual intervention.

**Anti-spam prompt engineering** — 40+ forbidden words enforced directly in the LLM prompt. Emails are designed to land in Primary inbox, not Promotions.

**Resume capability** — All stages check if a company was already processed. Kill the script, restart — picks up exactly where it left off.

---

<br>

**Govind Singh** · Associate Data Scientist · [LinkedIn](https://www.linkedin.com/in/govind-singh-994a28290/) . [Live Demo](https://client-finder-ai.onrender.com/)
