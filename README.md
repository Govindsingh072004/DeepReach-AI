<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DeepReach-AI — B2B Outreach Automation</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=DM+Sans:wght@300;400;500;600&family=Fraunces:ital,wght@0,300;0,700;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #0f0f0f;
    --ink2: #3a3a3a;
    --ink3: #777;
    --bg: #fafaf8;
    --surface: #f2f1ee;
    --border: #e2e1dd;
    --accent: #1a472a;
    --accent-light: #e8f0eb;
    --amber: #b45309;
    --amber-light: #fef3c7;
    --mono: 'DM Mono', monospace;
    --sans: 'DM Sans', sans-serif;
    --serif: 'Fraunces', serif;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg);
    color: var(--ink);
    font-family: var(--sans);
    font-size: 15px;
    line-height: 1.75;
    padding: 0 1rem;
  }
  .page { max-width: 860px; margin: 0 auto; padding: 4rem 0 6rem; }

  /* ── HERO ── */
  .hero { border-bottom: 1px solid var(--border); padding-bottom: 2.5rem; margin-bottom: 3rem; }
  .badge-row { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 1.5rem; }
  .badge {
    font-family: var(--mono); font-size: 11px;
    padding: 3px 10px; border-radius: 20px; font-weight: 500;
    border: 1px solid var(--border);
    color: var(--ink2); background: var(--surface);
  }
  .badge.green { background: var(--accent-light); color: var(--accent); border-color: #b6d4bc; }
  .badge.amber { background: var(--amber-light); color: var(--amber); border-color: #fcd34d; }
  h1 {
    font-family: var(--serif); font-size: 3rem; font-weight: 700;
    line-height: 1.1; letter-spacing: -0.02em;
    color: var(--ink); margin-bottom: 0.6rem;
  }
  h1 span { font-style: italic; color: var(--accent); }
  .tagline {
    font-size: 1.05rem; color: var(--ink2); font-weight: 300;
    margin-bottom: 1.5rem; max-width: 560px;
  }
  .demo-link {
    display: inline-flex; align-items: center; gap: 8px;
    background: var(--ink); color: #fff;
    padding: 10px 20px; border-radius: 6px;
    font-family: var(--mono); font-size: 12px;
    text-decoration: none; font-weight: 500;
    transition: background 0.15s;
  }
  .demo-link:hover { background: var(--accent); }
  .demo-link .dot {
    width: 7px; height: 7px; border-radius: 50%;
    background: #4ade80; animation: pulse 2s infinite;
  }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.4} }

  /* ── SECTIONS ── */
  section { margin-bottom: 3.5rem; }
  h2 {
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    color: var(--ink3); text-transform: uppercase; letter-spacing: 0.12em;
    margin-bottom: 1.2rem;
    display: flex; align-items: center; gap: 10px;
  }
  h2::after { content: ''; flex: 1; height: 1px; background: var(--border); }

  h3 { font-family: var(--serif); font-size: 1.5rem; font-weight: 700; margin-bottom: 0.75rem; color: var(--ink); }
  p { color: var(--ink2); margin-bottom: 1rem; }
  p:last-child { margin-bottom: 0; }

  /* ── CALLOUT ── */
  .callout {
    background: var(--surface); border-left: 3px solid var(--accent);
    padding: 1.1rem 1.4rem; border-radius: 0 8px 8px 0;
    margin: 1.5rem 0;
    font-family: var(--serif); font-size: 1.05rem; font-style: italic;
    color: var(--ink); line-height: 1.6;
  }

  /* ── PIPELINE ── */
  .pipeline { display: flex; flex-direction: column; gap: 0; margin: 1.5rem 0; }
  .pipe-step {
    display: flex; gap: 1rem; align-items: flex-start;
    padding: 1.1rem 1.2rem;
    border: 1px solid var(--border);
    border-bottom: none;
    background: #fff;
    transition: background 0.15s;
  }
  .pipe-step:first-child { border-radius: 8px 8px 0 0; }
  .pipe-step:last-child { border-bottom: 1px solid var(--border); border-radius: 0 0 8px 8px; }
  .pipe-step:hover { background: var(--surface); }
  .step-num {
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    color: var(--accent); background: var(--accent-light);
    padding: 2px 8px; border-radius: 4px; white-space: nowrap;
    margin-top: 2px; flex-shrink: 0;
  }
  .step-body { flex: 1; }
  .step-title { font-weight: 600; font-size: 14px; color: var(--ink); margin-bottom: 3px; }
  .step-desc { font-size: 13px; color: var(--ink3); line-height: 1.55; }
  .step-tags { display: flex; flex-wrap: wrap; gap: 5px; margin-top: 7px; }
  .tag {
    font-family: var(--mono); font-size: 10px;
    padding: 1px 7px; border-radius: 4px;
    background: var(--surface); color: var(--ink3);
    border: 1px solid var(--border);
  }

  /* ── DATA FLOW TABLE ── */
  .data-flow { display: flex; flex-direction: column; gap: 1.2rem; margin-top: 1.5rem; }
  .df-block { border: 1px solid var(--border); border-radius: 8px; overflow: hidden; }
  .df-header {
    padding: 8px 14px;
    background: var(--surface);
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    color: var(--ink2); border-bottom: 1px solid var(--border);
    display: flex; justify-content: space-between; align-items: center;
  }
  .df-header .src { color: var(--ink3); font-weight: 400; }
  .df-table { width: 100%; border-collapse: collapse; font-size: 12px; }
  .df-table th {
    text-align: left; padding: 7px 12px;
    background: var(--surface); font-weight: 500;
    color: var(--ink3); font-family: var(--mono);
    border-bottom: 1px solid var(--border); font-size: 11px;
  }
  .df-table td {
    padding: 7px 12px; color: var(--ink2);
    border-bottom: 1px solid var(--border); font-family: var(--mono); font-size: 11px;
  }
  .df-table tr:last-child td { border-bottom: none; }
  .df-table tr:hover td { background: var(--surface); }

  /* ── IMPACT TABLE ── */
  .impact-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    border: 1px solid var(--border); border-radius: 8px; overflow: hidden;
    margin-top: 1.2rem;
  }
  .impact-col { padding: 0; }
  .impact-col-head {
    padding: 10px 16px; font-family: var(--mono);
    font-size: 11px; font-weight: 500;
    border-bottom: 1px solid var(--border);
  }
  .impact-col:first-child .impact-col-head {
    background: #fff5f5; color: #991b1b; border-right: 1px solid var(--border);
  }
  .impact-col:last-child .impact-col-head {
    background: var(--accent-light); color: var(--accent);
  }
  .impact-item {
    padding: 9px 16px; font-size: 13px; color: var(--ink2);
    border-bottom: 1px solid var(--border); line-height: 1.45;
  }
  .impact-item:last-child { border-bottom: none; }
  .impact-col:first-child .impact-item { border-right: 1px solid var(--border); }

  /* ── FILE TABLE ── */
  .file-table { width: 100%; border-collapse: collapse; margin-top: 1.2rem; font-size: 13px; }
  .file-table th {
    text-align: left; padding: 8px 12px;
    background: var(--surface); color: var(--ink3);
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    border: 1px solid var(--border);
  }
  .file-table td {
    padding: 8px 12px; border: 1px solid var(--border);
    color: var(--ink2); vertical-align: top;
  }
  .file-table tr:hover td { background: var(--surface); }
  .fname { font-family: var(--mono); font-size: 12px; color: var(--ink); white-space: nowrap; }
  .fstage { font-family: var(--mono); font-size: 11px; color: var(--accent); white-space: nowrap; }

  /* ── EMAIL EXAMPLE ── */
  .email-box {
    border: 1px solid var(--border); border-radius: 8px;
    overflow: hidden; margin-top: 1.2rem;
  }
  .email-chrome {
    background: var(--surface); padding: 10px 14px;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 10px;
  }
  .email-chrome .dot-r { width:10px;height:10px;border-radius:50%;background:#ff5f57; }
  .email-chrome .dot-y { width:10px;height:10px;border-radius:50%;background:#febc2e; }
  .email-chrome .dot-g { width:10px;height:10px;border-radius:50%;background:#28c840; }
  .email-meta { padding: 12px 16px; background: #fff; border-bottom: 1px solid var(--border); }
  .email-meta .subj { font-weight: 600; font-size: 13px; color: var(--ink); margin-bottom: 4px; }
  .email-meta .from { font-size: 11px; color: var(--ink3); font-family: var(--mono); }
  .email-body {
    padding: 16px; font-size: 13px; color: var(--ink2);
    line-height: 1.7; background: #fff; white-space: pre-wrap;
    font-family: var(--sans);
  }

  /* ── SETUP ── */
  .setup-steps { display: flex; flex-direction: column; gap: 1rem; margin-top: 1.2rem; }
  .setup-step { display: flex; gap: 1rem; align-items: flex-start; }
  .setup-num {
    width: 26px; height: 26px; border-radius: 50%;
    background: var(--ink); color: #fff;
    display: flex; align-items: center; justify-content: center;
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    flex-shrink: 0; margin-top: 1px;
  }
  .setup-text { flex: 1; }
  .setup-text strong { font-weight: 600; font-size: 14px; color: var(--ink); display: block; margin-bottom: 3px; }
  .setup-text p { font-size: 13px; color: var(--ink3); margin: 0; }
  pre {
    background: var(--ink); color: #d4d4d4;
    padding: 1rem 1.2rem; border-radius: 6px;
    font-family: var(--mono); font-size: 12px;
    line-height: 1.6; overflow-x: auto; margin-top: 0.6rem;
  }
  pre .comment { color: #6a9955; }
  pre .key { color: #9cdcfe; }
  pre .val { color: #ce9178; }

  /* ── FOOTER ── */
  .footer {
    border-top: 1px solid var(--border); padding-top: 2rem;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 1rem;
  }
  .footer-name { font-family: var(--serif); font-size: 1.1rem; font-weight: 700; }
  .footer-links { display: flex; gap: 16px; }
  .footer-links a {
    font-family: var(--mono); font-size: 12px;
    color: var(--ink3); text-decoration: none;
  }
  .footer-links a:hover { color: var(--accent); }
</style>
</head>
<body>
<div class="page">

  <!-- HERO -->
  <div class="hero">
    <div class="badge-row">
      <span class="badge green">Live on Render</span>
      <span class="badge">Python</span>
      <span class="badge">Groq · LLaMA 3</span>
      <span class="badge">Tavily API</span>
      <span class="badge">SerpAPI · Adzuna</span>
      <span class="badge">Instantly.ai</span>
      <span class="badge amber">B2B Outreach Automation</span>
    </div>
    <h1>DeepReach<span>-AI</span></h1>
    <p class="tagline">Turns active job postings into hyper-personalized outreach emails — research, scoring, and writing handled entirely by AI.</p>
    <a class="demo-link" href="https://client-finder-ai.onrender.com" target="_blank">
      <span class="dot"></span>
      client-finder-ai.onrender.com
    </a>
  </div>

  <!-- THE PROBLEM -->
  <section>
    <h2>The Problem</h2>
    <p>Sales teams spend hours manually researching companies, guessing who might need their services, and writing outreach emails that get ignored. There's no clear signal for when a company actually has a need — so most outreach lands at the wrong time, to the wrong person, with the wrong message.</p>
    <p>The other side of the problem is personalization. Decision-makers get dozens of cold emails every day. Anything that reads like a template gets deleted. But writing a genuinely researched email for every single lead isn't possible at scale — not manually.</p>

    <div class="callout">
      A company posting a job is a company that already knows it has a gap. That's not a cold lead — that's a warm signal hiding in plain sight.
    </div>

    <p>If a company is actively hiring a Salesforce Developer or an ML Engineer, they have a confirmed, time-sensitive need. DeepReach-AI picks up that signal, researches the company in real time, and generates an email specific enough to feel like it was written by someone who actually did their homework.</p>
  </section>

  <!-- HOW IT WORKS -->
  <section>
    <h2>How It Works</h2>
    <div class="pipeline">
      <div class="pipe-step">
        <span class="step-num">01</span>
        <div class="step-body">
          <div class="step-title">Job Signal Detection</div>
          <div class="step-desc">Scrapes live job postings for roles that indicate a staffing need — Salesforce developers, ML engineers, data scientists. Tracks already-processed jobs to avoid duplicates across runs.</div>
          <div class="step-tags"><span class="tag">SerpAPI</span><span class="tag">Adzuna API</span><span class="tag">seen_jobs.json</span></div>
        </div>
      </div>
      <div class="pipe-step">
        <span class="step-num">02</span>
        <div class="step-body">
          <div class="step-title">Company Intelligence + Pain Point Research</div>
          <div class="step-desc">For every company found, runs automated internet research — pulling revenue, employee count, recent news, market activity, and business pain points in real time. No static databases. Actual live context per lead.</div>
          <div class="step-tags"><span class="tag">Tavily API</span><span class="tag">Groq LLaMA 3</span><span class="tag">structured JSON output</span></div>
        </div>
      </div>
      <div class="pipe-step">
        <span class="step-num">03</span>
        <div class="step-body">
          <div class="step-title">Lead Enrichment + AI Scoring</div>
          <div class="step-desc">Apollo CSV data is merged with live research output. CEO name, verified email, domain, and LinkedIn are extracted. Each lead gets an AI-generated score based on company size, revenue, and hiring volume — prioritizing the highest-intent targets.</div>
          <div class="step-tags"><span class="tag">Apollo.io CSV</span><span class="tag">Data_Enrichment.py</span><span class="tag">lead_scoring.py</span></div>
        </div>
      </div>
      <div class="pipe-step">
        <span class="step-num">04</span>
        <div class="step-body">
          <div class="step-title">Hyper-Personalized Email Generation</div>
          <div class="step-desc">Groq (LLaMA 3 8B) generates a unique email per lead using company-specific context. Role-aware logic picks the right positioning — Salesforce, AI/ML, or blended. A 40+ word forbidden list eliminates marketing tone. Output consistently passes AI-detection tools as human-written.</div>
          <div class="step-tags"><span class="tag">Groq LLaMA 3 8B</span><span class="tag">AsyncIO</span><span class="tag">anti-spam prompting</span><span class="tag">API key rotation</span></div>
        </div>
      </div>
      <div class="pipe-step">
        <span class="step-num">05</span>
        <div class="step-body">
          <div class="step-title">Campaign-Ready Output</div>
          <div class="step-desc">Outputs a structured CSV with generated subject lines and email bodies — formatted for direct upload to Instantly.ai. No reformatting, no copy-pasting. Upload and send.</div>
          <div class="step-tags"><span class="tag">Instantly.ai API</span><span class="tag">Google Sheets sync</span><span class="tag">Instantly_Ready_Leads.csv</span></div>
        </div>
      </div>
    </div>
  </section>

  <!-- DATA FLOW -->
  <section>
    <h2>Data Flow — What Each File Looks Like</h2>
    <div class="data-flow">

      <div class="df-block">
        <div class="df-header">
          Input — Apollo CSV export
          <span class="src">leads with company, title, email, revenue, tech stack</span>
        </div>
        <table class="df-table">
          <tr><th>First Name</th><th>Title</th><th>Company</th><th>Email</th><th>Annual Revenue</th></tr>
          <tr><td>Marc</td><td>CEO</td><td>Actian</td><td>marc@actian.com</td><td>$56.5M</td></tr>
          <tr><td>Emma</td><td>CTO</td><td>Actian</td><td>emma@actian.com</td><td>$56.5M</td></tr>
        </table>
      </div>

      <div class="df-block">
        <div class="df-header">
          After Enrichment
          <span class="src">CEO details, domain, verified LinkedIn added</span>
        </div>
        <table class="df-table">
          <tr><th>Company_Name</th><th>CEO_Full_Name</th><th>Official_Domain</th><th>LinkedIn_URL</th></tr>
          <tr><td>Actian Corporation</td><td>Marc Potter</td><td>actian.com</td><td>linkedin.com/in/pottermarc</td></tr>
        </table>
      </div>

      <div class="df-block">
        <div class="df-header">
          Final Output — Instantly Ready CSV
          <span class="src">personalized subject + body, ready to upload to Instantly.ai</span>
        </div>
        <table class="df-table">
          <tr><th>Generated_Email_Subject</th><th>First Name</th><th>Company Name</th><th>Email</th></tr>
          <tr><td>Growth and AI Engineering at Photon Group</td><td>Kushmitha</td><td>Photon Group</td><td>k@photon.com</td></tr>
        </table>
      </div>

    </div>
  </section>

  <!-- EMAIL EXAMPLE -->
  <section>
    <h2>Example Output Email</h2>
    <div class="email-box">
      <div class="email-chrome">
        <div class="dot-r"></div><div class="dot-y"></div><div class="dot-g"></div>
      </div>
      <div class="email-meta">
        <div class="subj">Growth and AI Engineering at Photon Group</div>
        <div class="from">To: kushmitha@photongroup.com · Generated by DeepReach-AI</div>
      </div>
      <div class="email-body">Hi Kushmitha,

Saw that Photon Group recently expanded its AI practice — the move toward enterprise automation makes sense given where the market is heading.

You're currently looking to bring on a few engineers with ML and data pipeline experience. Finding people who can actually deliver in that environment, not just interview well, is genuinely hard right now.

At AnavClouds, we work with teams like yours by placing pre-vetted AI and data engineers who are ready to contribute from day one — contract or direct hire, depending on what works for the team.

A few things that tend to matter in this context :

* Engineers screened specifically for production ML, not just theory

* Onboarding in days rather than weeks

* Flexible engagement — contract, contract-to-hire, or direct

* Culture fit evaluated alongside technical fit

Worth a short conversation if the timing is right.</div>
    </div>
  </section>

  <!-- BUSINESS IMPACT -->
  <section>
    <h2>Business Impact</h2>
    <div class="impact-grid">
      <div class="impact-col">
        <div class="impact-col-head">Before DeepReach-AI</div>
        <div class="impact-item">Hours of manual company research per campaign</div>
        <div class="impact-item">Generic email templates sent to everyone</div>
        <div class="impact-item">Cold leads with no timing signal</div>
        <div class="impact-item">Low reply rates from spray-and-pray blasts</div>
        <div class="impact-item">Manual copy-paste into Instantly.ai</div>
      </div>
      <div class="impact-col">
        <div class="impact-col-head">After DeepReach-AI</div>
        <div class="impact-item">Automated live intel for hundreds of companies per run</div>
        <div class="impact-item">Unique email per lead based on real company context</div>
        <div class="impact-item">Warm leads identified by active hiring signals</div>
        <div class="impact-item">Higher intent targeting = better conversion chances</div>
        <div class="impact-item">Campaign-ready CSV in minutes, direct upload</div>
      </div>
    </div>
  </section>

  <!-- FILE TABLE -->
  <section>
    <h2>File Breakdown</h2>
    <table class="file-table">
      <tr><th>File</th><th>Stage</th><th>What It Does</th></tr>
      <tr><td class="fname">project_2.py</td><td class="fstage">01 — Lead Sourcing</td><td>Scrapes job postings via SerpAPI + Adzuna. Tracks processed jobs in seen_jobs.json</td></tr>
      <tr><td class="fname">company_intel.py</td><td class="fstage">02 — Intel</td><td>Extracts company revenue + employee count. Groq parses raw data into structured JSON</td></tr>
      <tr><td class="fname">deep_company_research.py</td><td class="fstage">02 — Research</td><td>Tavily API pulls market news, pain points, and growth signals per company</td></tr>
      <tr><td class="fname">company_cleaner.py</td><td class="fstage">02 — Cleaning</td><td>Deduplicates and normalizes company names before enrichment runs</td></tr>
      <tr><td class="fname">Data_Enrichment.py</td><td class="fstage">03 — Enrichment</td><td>Merges Apollo data with research output. Extracts CEO name, domain, verified email</td></tr>
      <tr><td class="fname">lead_scoring.py</td><td class="fstage">03 — Scoring</td><td>AI scores each lead by revenue, employee count, and hiring volume</td></tr>
      <tr><td class="fname">email_generation.py</td><td class="fstage">04 — Email Gen</td><td>Async LLaMA generation with anti-spam prompting. Reads/writes Google Sheets</td></tr>
      <tr><td class="fname">API_rotation.py</td><td class="fstage">All stages</td><td>Round-robin rotation across multiple Groq API keys. Prevents rate limit failures</td></tr>
      <tr><td class="fname">instantly_mail_send.py</td><td class="fstage">05 — Delivery</td><td>Pushes finalized emails to Instantly.ai via API</td></tr>
      <tr><td class="fname">upload_to_sheets.py</td><td class="fstage">05 — Storage</td><td>Syncs all enriched data and email status to Google Sheets dashboard</td></tr>
    </table>
  </section>

  <!-- SETUP -->
  <section>
    <h2>Setup</h2>
    <div class="setup-steps">
      <div class="setup-step">
        <div class="setup-num">1</div>
        <div class="setup-text">
          <strong>Clone and install</strong>
          <pre>git clone https://github.com/g07oct2004-hash/Client_Finder_AI.git
cd Client_Finder_AI
pip install -r requirements.txt</pre>
        </div>
      </div>
      <div class="setup-step">
        <div class="setup-num">2</div>
        <div class="setup-text">
          <strong>Add your API keys to .env</strong>
          <pre><span class="comment"># Groq — add multiple for key rotation</span>
<span class="key">GROQ_API_KEY_1</span>=<span class="val">your_key_here</span>
<span class="key">GROQ_API_KEY_2</span>=<span class="val">your_key_here</span>
<span class="key">SERPAPI_KEY</span>=<span class="val">your_serpapi_key</span>
<span class="key">ADZUNA_APP_ID</span>=<span class="val">your_adzuna_id</span>
<span class="key">ADZUNA_APP_KEY</span>=<span class="val">your_adzuna_key</span>
<span class="key">TAVILY_API_KEY</span>=<span class="val">your_tavily_key</span>
<span class="key">INSTANTLY_API_KEY</span>=<span class="val">your_instantly_key</span>
<span class="key">GOOGLE_SERVICE_ACCOUNT_JSON</span>=<span class="val">{"type":"service_account",...}</span></pre>
        </div>
      </div>
      <div class="setup-step">
        <div class="setup-num">3</div>
        <div class="setup-text">
          <strong>Export your leads from Apollo.io as CSV and place in root directory</strong>
          <p>The system expects standard Apollo export format with company, title, email, and revenue columns.</p>
        </div>
      </div>
      <div class="setup-step">
        <div class="setup-num">4</div>
        <div class="setup-text">
          <strong>Run the pipeline or launch the Streamlit UI</strong>
          <pre><span class="comment"># Full pipeline</span>
python project_2.py

<span class="comment"># Or use the web interface</span>
streamlit run app.py</pre>
        </div>
      </div>
      <div class="setup-step">
        <div class="setup-num">5</div>
        <div class="setup-text">
          <strong>Upload Instantly_Ready_Leads.csv to Instantly.ai</strong>
          <p>The output CSV is pre-formatted with subject lines and email bodies. Direct upload — no reformatting needed.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <div class="footer">
    <div>
      <div class="footer-name">Govind Singh</div>
      <div style="font-size:12px;color:var(--ink3);font-family:var(--mono);margin-top:2px;">Associate Data Scientist</div>
    </div>
    <div class="footer-links">
      <a href="https://linkedin.com/in/Govindsingh" target="_blank">LinkedIn</a>
      <a href="https://github.com/Govindsingh072004" target="_blank">GitHub</a>
      <a href="https://client-finder-ai.onrender.com" target="_blank">Live Demo</a>
    </div>
  </div>

</div>
</body>
</html>
