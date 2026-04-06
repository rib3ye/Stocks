# Ubiquiti Inc (UI) Stock Research Page — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page stock research reference for Ubiquiti Inc (UI) with financials, peer comparisons, regulatory context, and pros/cons — populated with real, publicly sourced data.

**Architecture:** Single `index.html` with Tailwind CDN. No build step, no JS. All content is static HTML populated through web research. Research tasks gather data first, then build tasks assemble the page section by section.

**Tech Stack:** HTML, Tailwind CSS (CDN)

---

## File Structure

```
/Users/noahtsutsui/Projects/Stocks/
├── index.html          # The complete research page
└── docs/
    └── superpowers/
        ├── specs/
        │   └── 2026-04-06-ubiquiti-stock-research-design.md
        └── plans/
            └── 2026-04-06-ubiquiti-research-page.md
```

Only one file is created: `index.html`. All content lives in that single file.

---

## Task 1: Research — Ubiquiti Company Overview & Business Model

**Goal:** Gather factual data about Ubiquiti's business for sections 1 (Header) and 2 (Company Overview).

**Files:**
- Create: `index.html` (scaffolding + first two sections)

- [ ] **Step 1: Research Ubiquiti company facts**

Search the web for current Ubiquiti Inc company information:
- Official description of business
- Key product lines (UniFi, UISP, AmpliFi) and what each does
- Robert Pera background, ownership stake
- Headquarters location (New York, NY)
- Employee count
- Year founded, IPO date
- Recent notable developments

Sources to check: Ubiquiti investor relations page, SEC 10-K filing, Wikipedia, recent news articles.

- [ ] **Step 2: Create index.html with page scaffolding and first two sections**

Create `index.html` with:
- Full HTML5 boilerplate
- Tailwind CDN link in `<head>`: `<script src="https://cdn.tailwindcss.com"></script>`
- Inter font from Google Fonts
- Tailwind config override for font family
- Container layout: `max-w-4xl mx-auto` with appropriate padding
- Light gray background (`bg-gray-50`), dark text (`text-gray-800`)
- **Header section:** Ticker, company name, research date, one-line description
- **Company Overview section:** Populated with researched data — business description, product lines, business model, founder info, key facts

Use semantic HTML: `<header>`, `<main>`, `<section>`, `<h2>`, `<table>`, `<ul>`.

Styling guide:
- Section headings: `text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2`
- Body text: `text-gray-700 leading-relaxed`
- Tables: `w-full text-sm` with `border-collapse`, gray header row, alternating row backgrounds
- Bullet lists: `list-disc list-inside space-y-1 text-gray-700`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UI — Ubiquiti Inc Stock Research</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-gray-50 text-gray-800 font-sans">
    <div class="max-w-4xl mx-auto px-6 py-12">

        <!-- Header -->
        <header class="mb-12">
            <div class="flex items-baseline gap-3 mb-1">
                <span class="text-3xl font-bold text-gray-900">UI</span>
                <span class="text-xl text-gray-500">Ubiquiti Inc</span>
            </div>
            <p class="text-sm text-gray-400">Stock research reference — April 6, 2026</p>
        </header>

        <main class="space-y-12">

            <!-- Company Overview -->
            <section>
                <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Company Overview</h2>
                <div class="space-y-3 text-gray-700 leading-relaxed">
                    <!-- Populated with researched content -->
                </div>
            </section>

        </main>
    </div>
</body>
</html>
```

The Company Overview `<div>` will contain `<p>` tags with the researched business description and a `<ul>` with key facts.

- [ ] **Step 3: Verify in browser**

Run: `open /Users/noahtsutsui/Projects/Stocks/index.html`

Verify: Page loads, Tailwind styles render, header and company overview display correctly. Text is readable, layout is clean.

- [ ] **Step 4: Commit**

```bash
cd /Users/noahtsutsui/Projects/Stocks
git init
git add index.html
git commit -m "feat: add page scaffolding with header and company overview"
```

---

## Task 2: Research — Ubiquiti Financials (Basic)

**Goal:** Gather financial data for section 3 (Financial Summary — Basic).

**Files:**
- Modify: `index.html` (add Financial Summary section after Company Overview)

- [ ] **Step 1: Research basic financial metrics**

Search the web for Ubiquiti's most recent financial data:
- Revenue (TTM and FY2024, FY2023, FY2022 for 3-year trend)
- Net income (TTM)
- Gross margin, operating margin, net margin
- Free cash flow
- Total debt
- Cash and equivalents
- Market cap
- P/E ratio
- P/FCF ratio
- EV/EBITDA
- PEG ratio

Sources to check: Ubiquiti most recent 10-K or 10-Q (SEC EDGAR), Yahoo Finance, Macrotrends, Wisesheets, or similar financial data aggregators.

Note: Ubiquiti's fiscal year ends June 30. FY2025 would cover July 2024–June 2025. Use the most recent available data and note the period.

- [ ] **Step 2: Add Financial Summary (Basic) section to index.html**

Add a new `<section>` after Company Overview containing:
- A table with two columns: Metric | Value
- All basic financial metrics populated with researched data
- Revenue row should include 3-year trend notation (e.g., "$1.9B → $2.1B → $2.3B")
- Include data period (e.g., "TTM ending Q2 FY2025") as a subtitle under the section heading

```html
<!-- Financial Summary -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-1 border-b border-gray-200 pb-2">Financial Summary</h2>
    <p class="text-xs text-gray-400 mb-4">Data as of [period]. Sources: SEC filings, Yahoo Finance.</p>
    <table class="w-full text-sm">
        <thead>
            <tr class="border-b border-gray-200">
                <th class="text-left py-2 text-gray-500 font-medium">Metric</th>
                <th class="text-right py-2 text-gray-500 font-medium">Value</th>
            </tr>
        </thead>
        <tbody class="divide-y divide-gray-100">
            <tr>
                <td class="py-2">Revenue (TTM)</td>
                <td class="text-right py-2 font-mono">[value]</td>
            </tr>
            <!-- ... all metrics ... -->
        </tbody>
    </table>
</section>
```

Every `[value]` placeholder must be replaced with actual researched data. No placeholders in the final HTML.

- [ ] **Step 3: Verify in browser**

Open `index.html` in browser. Verify table renders cleanly, numbers are aligned right, font-mono makes numbers easy to scan.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add basic financial summary with current data"
```

---

## Task 3: Research — Ubiquiti Financials (Advanced Metrics)

**Goal:** Calculate/gather advanced metrics for section 4.

**Files:**
- Modify: `index.html` (add Advanced Metrics subsection)

- [ ] **Step 1: Research and calculate advanced metrics**

Using the basic financials from Task 2 plus additional research, gather or calculate:

1. **Piotroski F-Score:** Score each of the 9 criteria (positive net income, positive operating CF, rising ROA, CF > net income, declining leverage, rising current ratio, no dilution, rising gross margin, rising asset turnover). Sum for 0-9 score.
2. **Altman Z-Score:** Calculate using the formula: Z = 1.2(WC/TA) + 1.4(RE/TA) + 3.3(EBIT/TA) + 0.6(MVE/TL) + 1.0(Sales/TA). Pull working capital, retained earnings, EBIT, total assets, total liabilities from latest 10-K.
3. **Rule of 40:** Revenue growth % (YoY) + FCF margin %
4. **SBC as % of Revenue:** Find stock-based compensation from cash flow statement
5. **Revenue per Employee:** Revenue / employee count
6. **ROIC:** NOPAT / Invested Capital. Search for this or calculate from financials.
7. **WACC estimate:** Search for analyst WACC estimates for UI
8. **Cash Conversion Ratio:** FCF / Net Income
9. **Debt/FCF:** Total debt / FCF
10. **Gross Margin Trend:** Compare gross margin across last 3-5 fiscal years
11. **Insider Ownership %:** Robert Pera's stake + other insiders. Check latest proxy statement.
12. **Buyback Yield:** Shares repurchased value / market cap. Check cash flow statement for treasury stock purchases.

Sources: SEC 10-K, 10-Q, DEF 14A (proxy), Yahoo Finance, GuruFocus, Finviz.

- [ ] **Step 2: Add Advanced Metrics subsection to index.html**

Add below the basic financial table, within the same section or as a labeled subsection:

```html
<!-- Advanced Metrics -->
<div class="mt-8">
    <h3 class="text-lg font-semibold text-gray-900 mb-3">Advanced Metrics</h3>
    <table class="w-full text-sm">
        <thead>
            <tr class="border-b border-gray-200">
                <th class="text-left py-2 text-gray-500 font-medium">Metric</th>
                <th class="text-right py-2 text-gray-500 font-medium">Value</th>
                <th class="text-left py-2 pl-4 text-gray-400 font-normal">What it measures</th>
            </tr>
        </thead>
        <tbody class="divide-y divide-gray-100">
            <tr>
                <td class="py-2">Piotroski F-Score</td>
                <td class="text-right py-2 font-mono">[score]/9</td>
                <td class="text-left py-2 pl-4 text-xs text-gray-400">Financial strength composite (higher = stronger)</td>
            </tr>
            <!-- ... all advanced metrics with actual values ... -->
        </tbody>
    </table>
</div>
```

Three-column table: Metric | Value | One-line explanation. All values must be populated with real data.

- [ ] **Step 3: Verify in browser**

Open page, verify advanced metrics table renders below basic financials. Check alignment and readability.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add advanced financial metrics (Piotroski, Altman Z, Rule of 40, etc.)"
```

---

## Task 4: Research — Peer Comparison Data

**Goal:** Gather comparable data for peer companies and build the comparison table (section 5).

**Files:**
- Modify: `index.html` (add Peer Comparison section)

- [ ] **Step 1: Research peer company financials**

For each peer, gather: market cap, revenue, gross margin, P/E, ROIC, Piotroski F-Score (or approximate), Rule of 40, cash conversion ratio.

Peers:
- **Cisco (CSCO):** Large cap, enterprise networking leader
- **Netgear (NTGR):** Consumer/SMB networking, closest size comp
- **Juniper Networks (JNPR):** Enterprise networking (acquired by HPE in 2024 — check if still public or use last available data)
- **HPE (Hewlett Packard Enterprise):** Aruba networking division, enterprise
- **TP-Link:** Private — note as N/A where data unavailable, include qualitative notes (market share, pricing)

Sources: Yahoo Finance, Macrotrends, GuruFocus, latest 10-K filings for each.

Note: Juniper was acquired by HPE. Research whether this closed and if Juniper still trades independently. If not, use pre-acquisition data with a note, or substitute another peer (e.g., Arista Networks ANET, or Calix CALX).

- [ ] **Step 2: Add Peer Comparison section to index.html**

Add a new `<section>` after Financial Summary:

```html
<!-- Peer Comparison -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-1 border-b border-gray-200 pb-2">Peer Comparison</h2>
    <p class="text-xs text-gray-400 mb-4">Comparable networking companies. Data as of [date].</p>
    <div class="overflow-x-auto">
        <table class="w-full text-sm">
            <thead>
                <tr class="border-b border-gray-200">
                    <th class="text-left py-2 text-gray-500 font-medium">Company</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Mkt Cap</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Revenue</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Gross Margin</th>
                    <th class="text-right py-2 text-gray-500 font-medium">P/E</th>
                    <th class="text-right py-2 text-gray-500 font-medium">ROIC</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Piotroski</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Rule of 40</th>
                    <th class="text-right py-2 text-gray-500 font-medium">Cash Conv.</th>
                </tr>
            </thead>
            <tbody class="divide-y divide-gray-100">
                <tr class="bg-blue-50/50">
                    <td class="py-2 font-medium">Ubiquiti (UI)</td>
                    <td class="text-right py-2 font-mono">[value]</td>
                    <!-- ... UI row highlighted with light blue bg ... -->
                </tr>
                <tr>
                    <td class="py-2">Cisco (CSCO)</td>
                    <!-- ... -->
                </tr>
                <!-- ... remaining peers ... -->
            </tbody>
        </table>
    </div>
</section>
```

Ubiquiti's row gets a subtle highlight (`bg-blue-50/50`) to distinguish it. All values populated with real data. TP-Link cells show "Private" where data is unavailable.

- [ ] **Step 3: Verify in browser**

Check table renders correctly, especially horizontal scroll on mobile (`overflow-x-auto`). Verify UI row is visually distinct.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add peer comparison table (CSCO, NTGR, HPE, etc.)"
```

---

## Task 5: Research — Competitive Position & Moat

**Goal:** Research and write the qualitative competitive analysis (section 6).

**Files:**
- Modify: `index.html` (add Competitive Position section)

- [ ] **Step 1: Research competitive positioning**

Search for:
- How Ubiquiti's direct-to-consumer model compares to Cisco/HPE channel model
- Ubiquiti community forums activity and role in product development
- UniFi ecosystem stickiness (controller software, adoption, migration costs)
- Margin comparison: UI gross margins vs Cisco, Netgear, HPE networking segments
- Enterprise penetration: is UniFi gaining in mid-market/enterprise? Evidence?
- Known weaknesses: enterprise support gaps, certification programs, partner ecosystem

Sources: Industry analyses, Ubiquiti community forums, product reviews, analyst notes, Reddit/forum discussions about enterprise adoption.

- [ ] **Step 2: Add Competitive Position section to index.html**

Add a new `<section>` after Peer Comparison. Use a mix of prose paragraphs and bullet points:

```html
<!-- Competitive Position & Moat -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Competitive Position & Moat</h2>
    <div class="space-y-4 text-gray-700 leading-relaxed">
        <p>[Opening paragraph about UI's unique market position]</p>
        <ul class="list-disc list-inside space-y-2">
            <li><strong>Direct-to-consumer model:</strong> [detail]</li>
            <li><strong>Community-driven development:</strong> [detail]</li>
            <li><strong>Ecosystem lock-in:</strong> [detail]</li>
            <li><strong>Margin advantage:</strong> [detail]</li>
            <li><strong>Enterprise weakness:</strong> [detail]</li>
        </ul>
    </div>
</section>
```

All `[detail]` placeholders must be replaced with actual researched content.

- [ ] **Step 3: Verify in browser**

Check section renders cleanly and reads well.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add competitive position and moat analysis"
```

---

## Task 6: Research — Regulatory & Geopolitical Context

**Goal:** Research the foreign router ban landscape and its implications for UI (section 7).

**Files:**
- Modify: `index.html` (add Regulatory section)

- [ ] **Step 1: Research regulatory and geopolitical context**

Search for recent news and developments on:
- TP-Link investigation by US government (Commerce Dept, DOJ, DOD investigations)
- Any proposed or enacted legislation restricting foreign router imports
- CISA / national security advisories on Chinese networking equipment
- Timeline of regulatory actions (when did scrutiny begin, what's the current status as of early 2026)
- Which agencies are involved and what authority they have
- Ubiquiti's manufacturing: where are products assembled? (historically Shenzhen/China, Vietnam)
- Ubiquiti's supply chain exposure to tariffs and trade restrictions
- Any statements from Ubiquiti about domestic manufacturing or supply chain diversification
- Other US networking companies that could benefit (Arista, Juniper/HPE, Calix)

Sources: Reuters, Bloomberg, The Verge, Ars Technica, Congressional records, CISA advisories, Ubiquiti 10-K risk factors section.

- [ ] **Step 2: Add Regulatory & Geopolitical Context section to index.html**

Add a new `<section>` after Competitive Position:

```html
<!-- Regulatory & Geopolitical Context -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Regulatory & Geopolitical Context</h2>
    <div class="space-y-4 text-gray-700 leading-relaxed">
        <p>[Overview of foreign router security concerns]</p>
        <p>[TP-Link specific situation and timeline]</p>
        <p>[Ubiquiti as potential beneficiary — US-headquartered alternative]</p>
        <p>[Ubiquiti's own China/Asia manufacturing exposure]</p>
        <p>[Net assessment paragraph]</p>
    </div>
</section>
```

All content must be populated with researched facts. Include approximate dates and sourcing context inline (e.g., "As of early 2026, the Commerce Department...").

- [ ] **Step 3: Verify in browser**

Check section reads well and regulatory timeline is clear.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add regulatory and geopolitical context section"
```

---

## Task 7: Research — Risks, Pros, Cons, and Summary

**Goal:** Complete the final four sections (8–11) of the page.

**Files:**
- Modify: `index.html` (add Risks, Pros, Cons, Summary sections)

- [ ] **Step 1: Research risks and compile arguments**

Compile from all prior research plus targeted searches:

**Risks (section 8):**
- Robert Pera concentration risk (% ownership, board control)
- Supply chain dependence on Asia (manufacturing locations, component sourcing)
- Transparency concerns (history of irregular earnings calls, minimal IR)
- 2021 security breach details and aftermath
- Key-person risk (management depth)
- Tariff exposure (% of COGS from imports, tariff rates)
- Competitive threats from Cisco Meraki, Aruba Instant On moving downmarket

**Pros (section 9) — with data:**
- Insider ownership % (specific number)
- FCF generation (specific numbers, FCF margin)
- Regulatory tailwind (reference section 7)
- Community metrics (forum activity, NPS if available)
- Gross margin vs peers (specific comparison)
- Buyback history (dollars repurchased, share count reduction)
- UniFi enterprise adoption evidence

**Cons (section 10) — with data:**
- Governance specifics (when was last earnings call, disclosure gaps)
- China manufacturing % if known
- Valuation: P/E and P/FCF vs growth rate, vs sector median
- Breach specifics and any ongoing trust impact
- Pera dependency (what happens to stock if he leaves)
- Analyst coverage count
- Tariff impact estimate

Search for any recent analyst reports, earnings transcripts, or news articles that provide supporting data for these arguments.

- [ ] **Step 2: Add Risks section**

```html
<!-- Risks -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Risks</h2>
    <ul class="space-y-3 text-gray-700">
        <li><strong>Founder concentration:</strong> [specific detail about Pera's control]</li>
        <li><strong>Supply chain:</strong> [specific manufacturing exposure detail]</li>
        <!-- ... all risks with real content ... -->
    </ul>
</section>
```

- [ ] **Step 3: Add Pros section**

```html
<!-- Pros -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Bullish Case</h2>
    <ul class="space-y-3 text-gray-700">
        <li><strong>Insider alignment:</strong> [ownership % and what it means]</li>
        <!-- ... all pros with supporting data ... -->
    </ul>
</section>
```

- [ ] **Step 4: Add Cons section**

```html
<!-- Cons -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Bearish Case</h2>
    <ul class="space-y-3 text-gray-700">
        <li><strong>Governance opacity:</strong> [specific disclosure concerns]</li>
        <!-- ... all cons with supporting data ... -->
    </ul>
</section>
```

- [ ] **Step 5: Add Summary section**

```html
<!-- Summary -->
<section>
    <h2 class="text-2xl font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2">Summary</h2>
    <p class="text-gray-700 leading-relaxed">
        [2-3 neutral sentences weighing both sides. No buy/sell recommendation. Note this is research reference only, not investment advice.]
    </p>
    <p class="text-xs text-gray-400 mt-4">This page is a personal research reference and does not constitute investment advice.</p>
</section>
```

- [ ] **Step 6: Verify in browser**

Open full page. Scroll through all sections. Verify:
- All sections present and populated (no leftover placeholders)
- Consistent styling throughout
- Tables render cleanly
- Responsive on narrow viewport (resize browser window)
- Peer comparison table scrolls horizontally on mobile

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: add risks, pros, cons, and summary sections — page complete"
```

---

## Task 8: Final Review and Polish

**Goal:** Review complete page for data accuracy, completeness, and presentation quality.

**Files:**
- Modify: `index.html` (any final fixes)

- [ ] **Step 1: Full page review**

Read through the entire `index.html` and check:
1. No placeholder text remaining (`[value]`, `[detail]`, `TBD`, etc.)
2. All financial numbers are internally consistent (e.g., FCF margin matches FCF / Revenue)
3. Peer comparison data aligns with individual company sources
4. Regulatory section reflects most current available information
5. Pros and cons reference specific data points, not vague claims
6. All section headings match the spec
7. Source attributions are present (date ranges, "per 10-K FY2025", etc.)

- [ ] **Step 2: Fix any issues found**

Make any necessary corrections to data, wording, or styling. If no issues found, skip this step.

- [ ] **Step 3: Final browser check**

Open page one last time. Quick visual scan. Everything looks clean and complete.

- [ ] **Step 4: Final commit (if changes were made)**

```bash
git add index.html
git commit -m "chore: final review polish and data verification"
```
