Research the stock with ticker symbol $ARGUMENTS and generate a comprehensive single-file HTML stock research page.

## Instructions

You are a stock research page generator. Given the ticker symbol above, you will research the company and produce a polished, self-contained HTML page. Follow these three phases exactly.

## Phase 1: Discovery

Use WebSearch to establish baseline facts about the company. Search for "$ARGUMENTS stock company overview" and "$ARGUMENTS investor relations".

Determine:
1. Company full legal name
2. Stock exchange (NYSE, NASDAQ, etc.)
3. Sector and industry classification
4. Current share price and market cap (approximate)
5. CEO / founder name
6. 2-5 relevant peer/competitor companies (adaptive count — more for well-covered industries like tech or banking, fewer for niche industries; use your judgment)

Store all of this as context for Phase 2.

## Phase 2: Parallel Research

Dispatch ALL 6 of the following agents simultaneously using the Agent tool with `subagent_type: "general-purpose"`. Send all 6 Agent tool calls in a single message so they run in parallel.

Each agent prompt MUST include this shared context block at the top (filled in with your Phase 1 findings):

```
Company: {COMPANY_NAME}
Ticker: {TICKER}
Exchange: {EXCHANGE}
Industry: {INDUSTRY}
Sector: {SECTOR}
CEO: {CEO_NAME}
Share Price: ~${PRICE}
Market Cap: ~{MARKET_CAP}
Peer Companies: {PEER_1} ({PEER_TICKER_1}), {PEER_2} ({PEER_TICKER_2}), ...
```

**IMPORTANT:** Tell every agent: "Flag any figures you are uncertain about or could not verify from primary sources with [verify] so the user can review them later."

### Agent 1: Company Overview

**Agent tool description:** "Research {TICKER} company overview"

**Prompt to send:**

You are researching {COMPANY} ({TICKER}) for a stock research page. Use WebSearch and WebFetch to find accurate data. Flag uncertain figures with [verify].

Provide the following sections as structured markdown:

**COMPANY DESCRIPTION** — Write exactly 2 paragraphs:
- Paragraph 1: What the company does, markets served, geographic reach, defining competitive characteristics, distribution model
- Paragraph 2: Founding story, IPO details (date, price per share, amount raised, initial market cap), controlling shareholders and ownership structure

**KEY FACTS TABLE** — Provide as a list of "Item: Detail" pairs. Include ALL of these rows:
- Ticker / Exchange
- Founded (date and when operations began if different)
- IPO Date (date, price, amount raised, initial market cap)
- Headquarters (city, state, country)
- Employees (count with note on workforce character if notable)
- Fiscal Year End (month)
- Founder / CEO (full name, birth year, notable other roles)
- Major Insider Ownership (shares held and % of outstanding)
- Market Cap (current approximate)
- Latest FY Revenue (dollar amount with YoY % change)
- Latest FY Net Income (dollar amount with YoY % change and net margin %)
- Operating Margin (latest FY %)

**PRODUCT LINES** — Bulleted list. For each major product line or business segment:
- **Product Name** — Description of what it does, target market, and relative importance to total revenue

**BUSINESS MODEL** — Write exactly 2 paragraphs:
- Paragraph 1: Go-to-market strategy, distribution channels, cost structure compared to peers (cite specific peers and their SG&A or cost ratios if available)
- Paragraph 2: Revenue composition (hardware vs software vs services vs subscriptions), geographic revenue mix, key distribution partners

**NOTABLE RECENT DEVELOPMENTS** — 5-8 bullet points covering:
- Most recent 1-2 quarterly/annual results (revenue, EPS, beats/misses vs estimates)
- Strategic moves (acquisitions, divestitures, partnerships, new products)
- Capital allocation (buybacks, dividends, debt changes)
- Stock performance context
- Management or strategic changes

Search queries to try:
- "{COMPANY} investor relations"
- "{TICKER} 10-K annual report SEC"
- "{COMPANY} products services overview"
- "{COMPANY} earnings results latest quarter"
- "{TICKER} company profile stockanalysis.com"

### Agent 2: CEO Profile

**Agent tool description:** "Research {TICKER} CEO profile"

**Prompt to send:**

You are researching {CEO_NAME}, the CEO of {COMPANY} ({TICKER}), for a stock research page. Use WebSearch and WebFetch. Flag uncertain figures with [verify].

Provide the following sections as structured markdown:

**BACKGROUND** — Write exactly 2 paragraphs:
- Paragraph 1: Birth info (date, place), education (degrees, schools, honors), career before this company
- Paragraph 2: How they came to lead the company, ownership stake (shares and %), net worth estimates (cite source like Forbes or Bloomberg), notable outside interests or roles

**PUBLIC PRESENCE TABLE** — For EACH of the following channels, provide a 1-3 sentence description of the CEO's activity level and any specific notable examples:
- Earnings Calls (style, depth, frequency)
- Media Interviews (frequency, notable appearances, conferences attended)
- Twitter/X (handle if exists, follower count, posting style, notable tweets)
- Instagram (handle if exists, activity level)
- Personal Blog/Website (URL if exists, topics, activity)
- Investor Relations (approach — active engagement vs bare minimum)
- Philanthropy / Public Life (foundations, donations, public roles)

**CONTROVERSIES** — Bulleted list with dates:
- Any legal, ethical, regulatory, or reputational issues involving the CEO
- Include context and current status for each
- If no major controversies exist, write: "No major public controversies known."

**CEO COMPARISON TABLE** — Compare {CEO_NAME} against the CEOs of the peer companies: {PEER_COMPANIES}. First, search for who the current CEO of each peer company is.

For EACH CEO (including {CEO_NAME}), provide these dimensions:
- Role (full title)
- Background (education and career path, 2-3 sentences)
- Ownership Stake (% and approximate dollar value)
- Compensation (total comp package, notable details like low/high SBC)
- Media Presence (level: none/low/moderate/high/very high, with examples)
- Earnings Calls (style and depth of commentary)
- Investor Relations (approach and activity level)
- Governance (board independence, succession planning)
- Philanthropy (known activities or "none publicly known")
- Leadership Style (2-3 descriptors with brief context)

**INVESTMENT IMPLICATIONS** — 3-5 bullet points:
- What this CEO profile means for: shareholder alignment, governance risk, key-person risk, transparency, strategic continuity

Search queries to try:
- "{CEO_NAME} biography background education"
- "{CEO_NAME} net worth Forbes Bloomberg"
- "{CEO_NAME} controversies legal"
- "{CEO_NAME} interview media appearance"
- "{PEER_COMPANY} CEO name compensation"

### Agent 3: Financials

**Agent tool description:** "Research {TICKER} financials"

**Prompt to send:**

You are researching {COMPANY} ({TICKER}) financials for a stock research page. Use WebSearch and WebFetch. Flag uncertain figures with [verify].

Provide ALL of the following as structured markdown:

**INCOME STATEMENT**
- Revenue (TTM / LTM): dollar amount
- Revenue for each of the 4 prior fiscal years: dollar amount with YoY % change (format: "$X.XXB (+XX.X% YoY)")
- Gross Margin (TTM): percentage
- Operating Margin (TTM): percentage
- Net Margin (TTM): percentage
- Net Income (TTM): dollar amount
- EBITDA (latest full FY): dollar amount

**CASH FLOW**
- Free Cash Flow (latest full FY): dollar amount
- Operating Cash Flow (most recent reported half-year or quarter): dollar amount

**BALANCE SHEET** (as of most recent quarter-end — state the date)
- Cash & Equivalents: dollar amount
- Total Debt: dollar amount
- Net Debt: dollar amount
- Net Debt / EBITDA: ratio

**VALUATION** (at current price ~${PRICE}/share)
- Market Cap: dollar amount
- P/E Trailing: ratio with "x" suffix
- P/E Forward: ratio with "x" suffix
- EV/EBITDA: ratio with "x" suffix
- P/FCF or EV/FCF: ratio with "x" suffix
- PEG Ratio: ratio, or "N/A — not widely reported" if unavailable

**ADVANCED METRICS** — For each metric below, provide: (1) the value, and (2) a detailed explanatory note of 2-4 sentences covering what it measures, how it was calculated for this company, and what it implies.

1. **Piotroski F-Score**: X / 9
   ALSO provide a 9-criterion breakdown as a table with columns: Criterion | Score | Detail
   For each criterion, show: criterion name (e.g., "F1 — Positive net income"), score (+1 or +0), and the specific numbers. Group criteria under: Profitability (F1-F4), Leverage/Liquidity (F5-F7), Operating Efficiency (F8-F9).

2. **Altman Z-Score**: value — show the component calculation (WC/TA, RE/TA, EBIT/TA, MVE/TL, Sales/TA with weights)

3. **Rule of 40**: value — revenue growth % + FCF margin %

4. **SBC as % of Revenue**: percentage — include 3-4 year trend of absolute SBC amounts

5. **Revenue per Employee**: dollar amount — include employee count and source

6. **ROIC**: percentage — show NOPAT calculation (EBIT x (1 - effective tax rate)) and invested capital (equity + debt - cash)

7. **WACC estimate**: percentage range — state assumptions for risk-free rate, equity risk premium, beta, debt/equity mix

8. **Cash Conversion Ratio**: ratio (FCF / Net Income)

9. **Debt / FCF**: ratio — note how quickly debt could be repaid at current FCF

10. **Gross Margin Trend**: list 5-6 data points (fiscal years + TTM) as "FYXXXX: XX.X%"

11. **Insider Ownership**: percentage and share count — note control implications

12. **Buyback Yield**: actual (historical repurchases / market cap) and forward authorized (if any buyback program exists, note amount and expiry)

**CHART DATA** — Provide these as exact arrays:
- Revenue trend: labels = [fiscal year labels ending with "TTM"], values = [numbers in billions, e.g., 1.682]
- Gross margin trend: labels = [fiscal year labels ending with "TTM"], values = [percentages, e.g., 39.6]

Search queries to try:
- "{TICKER} financial statements revenue net income"
- "{TICKER} 10-K SEC filing annual report"
- "{COMPANY} quarterly earnings results"
- "{TICKER} stockanalysis.com financials"
- "{TICKER} macrotrends.net revenue"
- "{TICKER} gurufocus Piotroski F-Score"
- "{TICKER} ROIC return on invested capital"
- "{TICKER} insider ownership shares outstanding"
- "{TICKER} share buyback program"

### Agent 4: Competitive Position

**Agent tool description:** "Research {TICKER} competitive moat"

**Prompt to send:**

You are analyzing {COMPANY}'s ({TICKER}) competitive position and moat in the {INDUSTRY} industry for a stock research page. Peers: {PEER_COMPANIES}. Use WebSearch and WebFetch. Flag uncertain figures with [verify].

Provide:

**COMPETITIVE ADVANTAGES** — A bulleted list of 4-6 items. For EACH:
- **Bold title:** followed by a full paragraph (4-6 sentences) explaining:
  - What the advantage is and how it works mechanically
  - Why it is durable / hard for competitors to replicate
  - How it compares to specific peers (name them)
  - Any data that quantifies the advantage (margins, cost ratios, market share)

Consider these categories (include only those that apply):
- Distribution or channel advantages
- Cost structure advantages (compare SG&A ratios, employee counts)
- Network effects or ecosystem lock-in (switching costs)
- Brand loyalty or community effects
- Technology, IP, or R&D advantages
- Scale or pricing power

**SYNTHESIS** — Write exactly 2 paragraphs:
- Paragraph 1: Overall moat characterization — what type of moat (economic, behavioral, technological, network-based), how durable it is, primary threats to the moat
- Paragraph 2: The key strategic question for the company's competitive future — what must go right for the moat to strengthen, and what could erode it

Search queries to try:
- "{COMPANY} competitive advantage analysis"
- "{COMPANY} vs {PEER_NAME} comparison"
- "{COMPANY} market share {INDUSTRY}"
- "{INDUSTRY} competitive landscape"
- "{COMPANY} moat analysis"

### Agent 5: Peer Comparison

**Agent tool description:** "Research {TICKER} peer financials"

**Prompt to send:**

You are building a peer comparison table for {COMPANY} ({TICKER}) against: {PEER_LIST_WITH_TICKERS}. Use WebSearch and WebFetch. Flag uncertain figures with [verify].

For EACH company in the list (including {COMPANY} itself), find:
- Market Cap (current, approximate)
- Revenue (latest FY or TTM)
- Gross Margin (%)
- P/E Ratio (trailing)
- ROIC (%)
- Piotroski F-Score (approximate, X / 9)
- Rule of 40 (revenue growth % + FCF margin %, or operating margin if FCF unavailable)
- Cash Conversion Ratio (operating cash flow / net income)

If a company is private or recently acquired, note that and provide "N/A" for unavailable metrics.

Output as a markdown table with companies as rows and metrics as columns. Put {COMPANY} as the first row.

After the table, provide:
**FOOTNOTES** — bullet points noting:
- Data sources and as-of dates for each company
- Methodology notes (e.g., "ROIC for X reflects post-acquisition goodwill", "Piotroski estimated from public data")
- Any company-specific caveats

**CHART DATA** — Provide as exact arrays:
- Company labels: ["{COMPANY_SHORT}", "{PEER_1_SHORT}", "{PEER_2_SHORT}", ...]
- Gross margin values: [XX, XX, XX, ...] (percentages as integers)
- P/E values: [XX, XX, XX, ...] (ratios as integers; use 0 or null for N/A)

Search queries to try:
- "{PEER_TICKER} financial summary"
- "{PEER_TICKER} stockanalysis.com"
- "{PEER_NAME} revenue gross margin market cap"
- "{PEER_TICKER} ROIC"

### Agent 6: Industry Context

**Agent tool description:** "Research {TICKER} industry context"

**Prompt to send:**

You are researching the regulatory, geopolitical, and macro context for {COMPANY} ({TICKER}) in the {INDUSTRY} industry. Use WebSearch and WebFetch. Flag uncertain figures with [verify].

Provide these sections as structured markdown prose:

**REGULATORY LANDSCAPE** — 2-3 paragraphs:
- Current and pending regulations affecting this industry (name specific laws, agencies, rulings)
- Government investigations, enforcement actions, or policy shifts in the past 1-2 years
- How these specifically affect {COMPANY} — positive (compliance advantage, competitor displacement) or negative (cost, restriction, liability)

**GEOPOLITICAL FACTORS** — 1-2 paragraphs:
- Trade policy: tariffs, export controls, trade agreements affecting {COMPANY}'s supply chain or markets
- Manufacturing and supply chain geography — where {COMPANY} makes its products and the associated risks
- International market dynamics — growth or restriction in key geographies

**INDUSTRY TAILWINDS AND HEADWINDS** — 1-2 paragraphs:
- Macro trends benefiting the industry (technology adoption, demographic shifts, policy support)
- Macro threats (commoditization, demand cycles, substitution risk, new entrants)
- How {COMPANY} is specifically positioned relative to these trends

**NET ASSESSMENT** — 1 paragraph:
- On balance, is the regulatory/geopolitical/macro environment positive, negative, or mixed for {COMPANY}?
- What are the key dependencies and uncertainties?
- What would change this assessment?

Search queries to try:
- "{INDUSTRY} regulation policy 2025 2026"
- "{INDUSTRY} market trends outlook"
- "{COMPANY} regulatory risk exposure"
- "{COMPANY} tariff supply chain impact"
- "{COMPANY} geopolitical risk"
- "{INDUSTRY} government investigation enforcement"

## Phase 3: Assembly

After ALL 6 agents have returned their results, proceed with assembly.

### Step 1: Synthesize Cross-Cutting Sections

Read through ALL agent outputs and write these 4 sections by synthesizing across the full body of research:

**RISKS** — 6-8 bullet points. Format each as:
`<strong>Bold risk title:</strong> Detailed explanation (3-5 sentences).`
Draw from governance, financial, operational, competitive, and regulatory domains. Be specific to THIS company — reference concrete facts from the research, not generic risk language.

**BULLISH CASE** — 6-8 bullet points (same format):
Structural advantages, financial strengths, catalysts, favorable positioning. Each point should cite specific data.

**BEARISH CASE** — 6-8 bullet points (same format):
Overvaluation arguments, vulnerabilities, headwinds, governance concerns. Each point should cite specific data.

**SUMMARY** — 1 paragraph (~150-200 words):
Neutral synthesis balancing bull and bear cases. End with the key tension or question investors must resolve. Close with: "This page is a personal research reference and does not constitute investment advice."

### Step 2: Generate the HTML

Create the {TICKER} directory if needed using Bash: `mkdir -p {TICKER}`

Then use the Write tool to create `{TICKER}/index.html` with a complete, self-contained HTML file following this exact design system.

**HTML Document Structure:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>{TICKER} – {COMPANY_NAME} | Stock Research</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.7/dist/chart.umd.min.js"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'ui-sans-serif', 'system-ui', 'sans-serif'],
          },
        },
      },
    }
  </script>
</head>
<body class="bg-gray-50 text-gray-800 font-sans">
  <div class="max-w-4xl mx-auto px-6 py-10">
```

**Header:**
```html
<header class="mb-10 border-b border-gray-300 pb-6">
  <h1 class="flex items-baseline gap-4">
    <span class="text-4xl font-bold text-gray-900 tracking-tight">{TICKER}</span>
    <span class="text-2xl font-medium text-gray-600">{COMPANY_NAME}</span>
  </h1>
  <p class="mt-1 text-sm text-gray-500">Stock research reference &middot; Research date: {TODAY'S DATE}</p>
</header>
```

**Section order** (all 11, always included, in `<main class="space-y-12">`):

1. Company Overview (`id="company-overview"`)
2. CEO Profile (`id="ceo-profile"`)
3. Financial Summary (`id="financials"`)
4. Advanced Financial Metrics (`id="advanced-financials"`)
5. Peer Comparison (`id="peer-comparison"`)
6. Competitive Position & Moat (`id="competitive-position"`)
7. Regulatory & Geopolitical Context (`id="regulatory-context"`)
8. Risks (`id="risks"`)
9. Bullish Case (`id="bullish-case"`)
10. Bearish Case (`id="bearish-case"`)
11. Summary (`id="summary"`)

**CSS Class Reference:**

| Element | Classes |
|---------|---------|
| Section heading (h2) | `text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2` |
| Sub-heading (h3) | `text-lg font-semibold text-gray-900 mt-6 mb-2` |
| Body paragraph | `text-gray-700 leading-relaxed` |
| Source attribution | `text-xs text-gray-400 mb-4` |
| Numeric table values | `font-mono` on the td |
| Subject company highlight | `bg-blue-50/50` on tr and highlighted td cells |
| Wide table wrapper | `<div class="overflow-x-auto">` around table |

**Table Styles:**

Key Facts table (Company Overview) — alternating row colors:
```html
<table class="w-full text-sm border-collapse">
  <thead><tr class="bg-gray-200 text-gray-700">
    <th class="text-left px-3 py-2 font-semibold w-1/3">Item</th>
    <th class="text-left px-3 py-2 font-semibold">Detail</th>
  </tr></thead>
  <tbody>
    <tr class="bg-white"><td class="px-3 py-2 font-medium text-gray-600">Item</td><td class="px-3 py-2 text-gray-700">Detail</td></tr>
    <tr class="bg-gray-50"><td class="px-3 py-2 font-medium text-gray-600">Item</td><td class="px-3 py-2 text-gray-700">Detail</td></tr>
  </tbody>
</table>
```

Financial data tables:
```html
<table class="w-full text-sm">
  <thead><tr class="border-b border-gray-200">
    <th class="text-left py-2 text-gray-500 font-medium">Metric</th>
    <th class="text-right py-2 text-gray-500 font-medium">Value</th>
  </tr></thead>
  <tbody class="divide-y divide-gray-100">
    <tr><td class="py-2">Metric</td><td class="text-right py-2 font-mono">$X.XXB</td></tr>
    <tr><td class="py-2 text-gray-500 text-xs pl-4">Prior FY</td><td class="text-right py-2 font-mono text-gray-500 text-xs">$X.XXB (+XX% YoY)</td></tr>
  </tbody>
</table>
```

Advanced metrics table (3-column):
```html
<table class="w-full text-sm">
  <thead><tr class="border-b border-gray-200">
    <th class="text-left py-2 text-gray-500 font-medium w-48">Metric</th>
    <th class="text-right py-2 text-gray-500 font-medium w-28">Value</th>
    <th class="text-left py-2 pl-4 text-gray-400 font-normal text-xs">What it measures / Notes</th>
  </tr></thead>
  <tbody class="divide-y divide-gray-100">
    <tr><td class="py-2 font-medium">Name</td><td class="text-right py-2 font-mono">Value</td><td class="text-left py-2 pl-4 text-xs text-gray-400">Note</td></tr>
  </tbody>
</table>
```

Piotroski detail table:
```html
<table class="w-full text-xs">
  <thead><tr class="border-b border-gray-200">
    <th class="text-left py-1 text-gray-500 font-medium">Criterion</th>
    <th class="text-center py-1 text-gray-500 font-medium w-12">Score</th>
    <th class="text-left py-1 pl-3 text-gray-400 font-normal">Detail</th>
  </tr></thead>
  <tbody class="divide-y divide-gray-100">
    <tr class="text-gray-600"><td class="py-1 font-medium text-gray-500 text-xs" colspan="3">Category</td></tr>
    <tr><td class="py-1">F1 — Name</td><td class="text-center py-1 font-mono text-green-600">+1</td><td class="py-1 pl-3 text-gray-400">detail</td></tr>
    <tr><td class="py-1">F4 — Name</td><td class="text-center py-1 font-mono text-red-400">+0</td><td class="py-1 pl-3 text-gray-400">detail</td></tr>
  </tbody>
</table>
```

Peer comparison table:
```html
<table class="w-full text-sm">
  <thead><tr class="border-b border-gray-200">
    <th class="text-left py-2 pr-3 text-gray-500 font-medium">Company</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">Mkt Cap</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">Revenue</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">Gross Margin</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">P/E</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">ROIC</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">Piotroski</th>
    <th class="text-right py-2 px-2 text-gray-500 font-medium">Rule of 40</th>
    <th class="text-right py-2 pl-2 text-gray-500 font-medium">Cash Conv.</th>
  </tr></thead>
  <tbody class="divide-y divide-gray-100">
    <tr class="bg-blue-50/50"><td class="py-2 pr-3 font-medium">{Company} ({TICKER})</td><td class="text-right py-2 px-2 font-mono">value</td></tr>
    <tr><td class="py-2 pr-3">{Peer}</td><td class="text-right py-2 px-2 font-mono">value</td></tr>
  </tbody>
</table>
```

CEO comparison table:
```html
<table class="w-full text-sm">
  <thead><tr class="border-b border-gray-200">
    <th class="text-left py-2 text-gray-500 font-medium">Dimension</th>
    <th class="text-left py-2 text-gray-500 font-medium bg-blue-50/50">{CEO} ({TICKER})</th>
    <th class="text-left py-2 text-gray-500 font-medium">{PeerCEO} ({PTICKER})</th>
  </tr></thead>
  <tbody class="divide-y divide-gray-100">
    <tr><td class="py-2 font-medium">Dimension</td><td class="py-2 text-xs bg-blue-50/50">Subject detail</td><td class="py-2 text-xs">Peer detail</td></tr>
  </tbody>
</table>
```

**List Styles:**

Product lines / simple lists:
```html
<ul class="list-disc list-inside space-y-1 text-gray-700">
  <li><span class="font-medium">{Name}</span> — {Description}</li>
</ul>
```

Competitive advantages (detailed):
```html
<ul class="list-disc list-inside space-y-3 ml-2">
  <li><strong>{Title}:</strong> {Detailed paragraph}</li>
</ul>
```

Risks / Bullish / Bearish:
```html
<ul class="space-y-3 text-gray-700">
  <li><strong>{Title}:</strong> {Detailed explanation}</li>
</ul>
```

**Chart.js Configuration:**

Place a `<script>` block at the end of `<body>` with all 4 charts:

```javascript
const gray400 = '#9ca3af';
const gray500 = '#6b7280';
const gray700 = '#374151';
const blue500 = '#3b82f6';
const blue300 = '#93c5fd';
const slate400 = '#94a3b8';

Chart.defaults.font.family = "'Inter', system-ui, sans-serif";
Chart.defaults.font.size = 12;
Chart.defaults.color = gray500;
Chart.defaults.plugins.legend.labels.boxWidth = 12;
```

Chart 1 — Revenue Trend (bar chart, canvas id="revenueChart", height="200"):
- Labels: fiscal year labels + "TTM" from Agent 3 chart data
- Data: revenue values in billions
- Colors: slate400 for all historical years, blue500 for the latest full FY, blue300 for TTM
- Y-axis: beginAtZero: true, tick format "$Xb"
- Tooltip: "$X.XXXB"
- Title: "Revenue Trend"
- borderRadius: 4, barPercentage: 0.6, legend: false, x grid: false, y grid: '#f3f4f6'

Chart 2 — Gross Margin Trend (line chart, canvas id="marginChart", height="200"):
- Labels and data from Agent 3 chart data
- borderColor: blue500, backgroundColor: 'rgba(59,130,246,0.08)', fill: true, tension: 0.3, pointRadius: 4, pointBackgroundColor: blue500
- Y-axis: min ~10 below lowest value, max ~10 above highest, tick format "X%"
- Title: "Gross Margin Trend (%)"
- Place in advanced-financials section after Piotroski detail table

Chart 3 — Peer Gross Margin (bar chart, canvas id="peerMarginChart", height="250"):
- Labels and data from Agent 5 chart data
- Colors: blue500 for subject company (first), slate400 for all peers
- Y-axis: beginAtZero: true, tick format "X%"
- Title: "Gross Margin vs Peers"

Chart 4 — Peer P/E (bar chart, canvas id="peerPEChart", height="250"):
- Same color scheme as Chart 3
- Y-axis: beginAtZero: true, tick format "Xx"
- Title: "P/E Ratio vs Peers"

Charts 3 and 4 in a grid:
```html
<div class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-6">
  <div><canvas id="peerMarginChart" height="250"></canvas></div>
  <div><canvas id="peerPEChart" height="250"></canvas></div>
</div>
```

Canvas placements:
- revenueChart: in financials section, after Income Statement table
- marginChart: in advanced-financials section, after Piotroski detail table
- peerMarginChart + peerPEChart: in peer-comparison section, in grid after peer table

**Footer:**
```html
<footer class="mt-16 pt-4 border-t border-gray-200 text-xs text-gray-400">
  Personal research reference only. Not investment advice. Data sourced from SEC filings, company IR, and public market data.
</footer>
```

### Step 3: Report Completion

After writing the HTML file, tell the user:
1. "Stock research page generated: `{TICKER}/index.html`"
2. List any `[verify]` flags from the agent outputs that appear in the final HTML — these need manual review
3. If any agents failed or returned insufficient data, note which sections may be incomplete
4. Suggest: "Open `{TICKER}/index.html` in a browser to review."
