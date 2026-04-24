# Digital Asset Intelligence Dashboard
**BUFN403 Capstone — Team 5 | Spring 2026 | American Bankers Association & Google**

A multi-dimensional digital asset classification and intent analysis platform for 16 major U.S. financial institutions, built on original NLP scoring of 128 earnings call Q&A transcripts (Q1 2024–Q4 2025), Gemini-assisted clustering, and live web research conducted April 2026.

---

## Table of Contents

- [Project Summary](#project-summary)
- [Methodology](#methodology)
- [Dashboard Pages](#dashboard-pages)
  - [Project Overview](#1-project-overview)
  - [Methodology](#2-methodology)
  - [Latest Developments](#3-latest-developments)
  - [Composite Leaderboard](#4-composite-leaderboard)
  - [Bank Profile](#5-bank-profile)
  - [Compare Banks](#6-compare-banks)
  - [Cluster Map](#7-cluster-map)
  - [Industry Timeline](#8-industry-timeline)
  - [Market Data](#9-market-data)
- [Scoring Framework](#scoring-framework)
- [Key Findings](#key-findings)
- [Known Limitations](#known-limitations)
- [Files](#files)

---

## Project Summary

We started with 50 major U.S. banks and applied a custom NLP scoring pipeline to the Q&A sections of their earnings call transcripts. Banks below a minimum engagement threshold were excluded, producing 16 institutions with measurable digital asset activity. We then developed a four-dimensional composite scoring model (0–100) to address the key weakness of single-metric NLP: it cannot distinguish broad narrative engagement from operational product deployment, and it systematically misranks banks that underdisclose in investor Q&A.

**Methodology validation:** Our model assigned Charles Schwab a peak NLP score of 19.81 in Q2 2025. On April 16, 2026 — 10 months later — Schwab launched *Schwab Crypto*, offering direct BTC and ETH trading at 75bps. High Q&A engagement scores are predictive leading indicators, not trailing descriptions.

---

## Methodology

### Why Q&A Sections Only
Prepared remarks are written by IR teams and may contain performative language. Q&A forces genuine engagement — an executive who cannot answer a direct stablecoin question reveals as much as one who can. Scoring only Q&A sections makes the scores more reliable signals of strategic intent.

### Four-Dimensional Composite Score (0–100)

| Dimension | Weight | What It Measures |
|-----------|--------|-----------------|
| **D1 — NLP Engagement** | 0–25 | Adjusted peak NLP score, log-normalised. False positive terms removed. |
| **D2 — Specificity & Depth** | 0–25 | Unique real terms + Custodial/Infrastructure ratio + quarter consistency. |
| **D3 — Disclosure Mode** | 0–25 | Ratio of Q&A score to full transcript score. Proactive vs. reactive disclosers. |
| **D4 — External Research** | 0–25 | Confirmed products launched + infrastructure depth + strategic trajectory. |

### NLP Scoring Formulas

Formula 1 — Term Match Score (per sub-category, per document)
score = (Σ weighted_term_hits ÷ document_length_chars) × 10,000
Formula 2 — Total DA Score (per document)
total = custodial_score + infrastructure_score + fintech_score + general_score
Formula 3 — Rating per document
≥ 8.0 AND ≥ 6 unique terms  →  4 · Advanced
≥ 4.0 AND ≥ 3 unique terms  →  3 · Developing
≥ 1.0 OR  ≥ 1 unique term   →  2 · Minimal
else                         →  1 · Silent
Formula 4 — Bank Average Score
bank_avg = Σ(all 8 quarter scores) ÷ 8
Formula 5 — Sentiment
positive_count > cautious_count + 2  →  "positive"
cautious_count > positive_count + 2  →  "cautious"
else                                  →  "neutral"

### Four Sub-Category Dictionaries

| Category | Example Terms | Signal |
|----------|--------------|--------|
| **Custodial** | custody, safekeeping, MPC, digital asset custody | Holding assets for clients |
| **Infrastructure** | blockchain, tokenized deposit, kinexys, deposit token | Building proprietary platforms |
| **Fintech** | stablecoin, cross-border, coinbase, DeFi | Partnerships and consumer-facing engagement |
| **General** | crypto, bitcoin, digital asset | Broad engagement, no specific product implied |

---

## Dashboard Pages

### 1. Project Overview
The landing page and executive summary. Sets full context before any analysis is presented.

- **Methodology validation callout** — highlights that Schwab's Q2 2025 NLP peak (19.81) predicted the April 2026 product launch 10 months in advance
- **Three-column summary cards** — explains what was analyzed, how 50 banks were narrowed to 16, and how the three-layer evidence approach works
- **Key findings list** — six auto-rendered findings from the data including the Goldman underdisclosure paradox, Q2 2025 inflection, and false positive disclosure
- **Composite score distribution chart** — bar chart of 5-tier breakdown (Tier 1: 2, Tier 2: 4, Tier 3: 5, Tier 4: 1, Tier 5: 4)
- **False positive warning** — explicitly documents the "circle back" idiom issue for Wells Fargo, Truist, BMO, and TD Bank before any analyst finds it independently

---

### 2. Methodology
Explains exactly how scores were calculated. Every formula and design choice is documented so the work is reproducible and defensible.

- **Four-dimension framework** — each dimension explained with plain-English rationale, formula, and the specific analytical problem it solves
- **Formula blocks** — exact mathematical expressions in monospace, matching the Python scoring code
- **Goldman Sachs underdisclosure case** — dedicated explanation of how a 0.23x Q&A/Full transcript ratio creates systematic misranking and how D4 corrects it
- **PNC vs. US Bancorp specificity contrast** — shows why two banks with similar NLP peaks (5.87 vs. 4.53) receive different composite scores based on specificity ratio (4.8% vs. 36.9%)
- **Limitations section** — three documented constraints: term disambiguation, Q&A-only scope, and analyst subjectivity in D4

---

### 3. Latest Developments
Bridges the data window (Q1 2024–Q4 2025) with the current state of the market (April 2026).

- **GENIUS Act explanation** — connects the July 18, 2025 signing (Senate 68–30, House 308–122) to the Q2 2025 NLP inflection visible across 9 of 16 banks
- **11-entry developments list** — color-coded by bank, covering April 2026 back to July 2025. Includes Schwab Crypto launch, WFUSD trademark, State Street platform, JPMorgan Canton rollout, BNY BSRXX fund, GS DAP spin-out, PNC BTC trading launch
- **Cross-cluster development callout** — flags the PNC/Citi/WFC joint stablecoin initiative via Early Warning Services as a cross-cluster development that individual NLP scores could not have predicted

---

### 4. Composite Leaderboard
The primary ranking table. All 16 banks ranked by composite score with every dimension visible simultaneously.

- **Composite as primary sort** — ranks by 0–100 composite, not raw NLP peak. Goldman Sachs (NLP 1.84, Composite 39.9) correctly appears in Tier 3 rather than near the bottom
- **All four dimension columns** — D1, D2, D3, D4 shown in separate columns (blue, green, purple, amber) so the score composition is visible without opening a profile
- **NLP peak retained** — raw adjusted NLP peak shown alongside composite so the gap is immediately visible
- **Tier filter pills** — five filter buttons (All 16 / Tier 1 Leader / Tier 2 Advanced / Tier 3 Building / Tier 4 Watching / Tier 5 Absent) with correct bank counts
- **False positive flags** — red "FP" badge on Wells Fargo, Truist, BMO, TD Bank
- **Cluster badges** — each row shows cluster assignment (Cl.A–Cl.E) in cluster color
- **Click-to-profile** — clicking any row opens that bank's full profile with the bank pre-selected

---

### 5. Bank Profile
Deep-dive on any individual bank. Every number traces back to either the raw CSV data or documented external research.

- **Bank selector dropdown** — all 16 banks by ticker and full name. Selecting a bank re-renders every element on the page
- **Composite score ring** — circular gauge showing composite score in the tier's color
- **Eight stat cards** — Ticker, Tier, Cluster, NLP Peak, Avg Score, Real Terms, Consistency (active quarters / 8), Disclosure Ratio
- **Auto-generated contextual explanation** — a paragraph that writes itself per bank. Explains composite score, flags underdiscloser status if disclosure ratio < 0.5, interprets specificity ratio, states dominant sentiment, and appends April 2026 research note
- **Four-dimension breakdown bars** — horizontal bars for D1–D4 with per-bank annotations explaining what drove each score specifically
- **Quarterly NLP timeline** — line chart across all 8 quarters. Green dots = Advanced, gold = Developing/Minimal, grey = zero or false positive
- **Sub-score breakdown chart** — Custodial / Infrastructure / Fintech / General for the peak quarter. Hover tooltips define each category
- **Transcript excerpts** — direct Q&A text from the peak quarter. False positive banks show the specific phrase confirming the false positive
- **Terms per quarter log** — every term detected in every quarter. False positive terms shown in red with annotation

---

### 6. Compare Banks
Side-by-side analysis of up to 4 banks. Most useful for finding strategic differences between banks with similar composite scores.

- **Ticker chip selector** — all 16 banks as clickable chips, color-coded by cluster. Toggle on/off, capped at 4
- **Selection counter** — live "N / 4 selected" with prompt to select at least 2
- **Composite vs. NLP peak bar chart** — shows both metrics side by side, making the gap immediately visible (e.g., Goldman vs. Schwab)
- **Quarter-by-quarter NLP trend** — overlaid line chart across all 8 quarters for all selected banks
- **Head-to-head metrics table** — 13-row comparison covering Composite, Tier, Cluster, D1–D4, NLP Peak, Real Terms, Specificity %, Disclosure Ratio, Consistency, and False Positive status
- **Dimension radar chart** — four-axis radar (D1/D2/D3/D4) overlaid for all selected banks. The most revealing chart: Goldman (D4-heavy) and Schwab (D1+D3-heavy) show completely different profile shapes despite both being Tier 3
- **Sub-score breakdown chart** — average Custodial / Infrastructure / Fintech / General across active quarters, side by side

---

### 7. Cluster Map
Shows the five strategic groupings and the three-layer evidence supporting each one.

| Cluster | Name | Banks | Composite Range |
|---------|------|-------|----------------|
| **A** | Custodial Infrastructure Leaders | BNY Mellon, State Street | 69–85 |
| **B** | Wholesale Blockchain Builders | JPMorgan, Citi, Goldman Sachs | 40–73 |
| **C** | Retail Digital Asset Pioneers | Charles Schwab, American Express | 53–83 |
| **D** | Strategic Movers — GENIUS Act Ready | US Bancorp, Bank of America, PNC, Morgan Stanley | 41–59 |
| **E** | Monitoring / False Positives | Capital One, Wells Fargo, Truist, BMO, TD Bank | 1–31 |

**Features:**
- **Five cluster cards** — clickable, expand on click, collapse on second click
- **Capability bars** — Custody, Payments, Capital Markets, Retail, Regulatory rated 1–10 per cluster
- **Cluster rationale** — written explanation based on what banks are doing, not how much they score. References specificity ratios, sub-score compositions, and disclosure patterns
- **Three-layer evidence** — NLP (score patterns and term vocabulary), Gemini (team-provided research on deployments and filings), Web (live April 2026 research). Every cluster has all three layers documented
- **Use cases by bank** — confirmed use cases per bank within the cluster, tagged Active / Pilot / Planned. Only the selected cluster's banks are shown

---

### 8. Industry Timeline
21 regulatory and product milestones from 2020 to April 2026, contextualizing the NLP findings.

- **Category filter pills** — All / Regulatory / Custody / Infrastructure / Capital Markets / Retail
- **Color-coded dots** — Red = Regulatory, Blue = Custody, Green = Infrastructure, Amber = Retail, Purple = Capital Markets
- **21 events** — JPM Coin (2020) through Schwab Crypto launch (April 16, 2026). GENIUS Act Senate passage (June 17, 2025) included as a separate entry from signing (July 18) because the Senate vote drove Q2 2025 analyst questions
- **Bank attribution on every entry** — each event names the institution for cross-reference with leaderboard
- **Explanatory callout** — identifies the two events most directly visible in NLP data: SAB 122 (December 2024) and the GENIUS Act (July 2025)

---

### 9. Market Data
External projections and benchmarks that contextualize the team's findings.

- **Four KPI cards** — JPM Kinexys daily volume ($5B), Citi GPS tokenization projection ($5T+ by 2030), Citi GPS stablecoin base case ($1.9T by 2030), BNY's share of crypto ETP fund services (80%+)
- **Stablecoin scenarios bar chart** — Now ($237B), Base Case 2030 ($1.9T), Bull Case 2030 ($4T) from Citi GPS, with scenario assumptions explained in the callout
- **Composite vs. NLP scatter plot** — X-axis = NLP peak, Y-axis = composite. Banks above the diagonal have composite scores higher than NLP suggests (Goldman: underdiscloser corrected upward by D4). Visually proves why multi-dimensional scoring outperforms NLP alone
- **Institutional projections table** — 8 entries from JPMorgan, Citi GPS, BNY Mellon, River Research, SVB, State Street with source badge, headline figure, and plain-English description

---

## Scoring Framework

### Composite Score Tiers

| Tier | Score Range | Count | Description |
|------|-------------|-------|-------------|
| **Tier 1 · Leader** | 80–100 | 2 | Operational live-ness confirmed, proactive disclosure, high external research score |
| **Tier 2 · Advanced** | 55–79 | 4 | Significant confirmed activity, multi-dimensional evidence across sources |
| **Tier 3 · Building** | 35–54 | 5 | Measurable engagement, some confirmed products, trajectory signals present |
| **Tier 4 · Watching** | 15–34 | 1 | Low engagement, infrastructure-preparation posture, no confirmed DA products |
| **Tier 5 · Absent** | 0–14 | 4 | Zero adjusted NLP score (false positives removed), D4 trajectory signal only |

### Full Composite Scores

| Bank | Ticker | D1 | D2 | D3 | D4 | Composite | Tier | Cluster |
|------|--------|----|----|----|----|-----------|------|---------|
| BNY Mellon | BK | 19.5 | 15.9 | 25.0 | 25 | **85.4** | Tier 1 | A |
| Charles Schwab | SCHW | 24.9 | 14.7 | 22.4 | 21 | **83.0** | Tier 1 | C |
| Citi | C | 16.9 | 10.3 | 25.0 | 21 | **73.2** | Tier 2 | B |
| State Street | STT | 11.8 | 20.1 | 16.0 | 21 | **68.9** | Tier 2 | A |
| JPMorgan | JPM | 15.6 | 12.7 | 14.2 | 24 | **66.5** | Tier 2 | B |
| US Bancorp | USB | 14.0 | 13.0 | 14.6 | 17 | **58.6** | Tier 2 | D |
| American Express | AXP | 17.5 | 8.2 | 14.2 | 13 | **52.9** | Tier 3 | C |
| Bank of America | BAC | 12.4 | 9.7 | 13.8 | 15 | **50.9** | Tier 3 | D |
| PNC | PNC | 15.8 | 6.6 | 14.2 | 13 | **49.6** | Tier 3 | D |
| Morgan Stanley | MS | 8.9 | 7.0 | 14.2 | 11 | **41.1** | Tier 3 | D |
| Goldman Sachs | GS | 8.6 | 3.5 | 5.8 | 22 | **39.9** | Tier 3 | B |
| Capital One | COF | 6.0 | 3.0 | 13.8 | 8 | **30.8** | Tier 4 | E |
| Wells Fargo ⚠ | WFC | 0.0 | 0.0 | 0.0 | 9 | **9.0** | Tier 5 | E |
| Truist ⚠ | TFC | 0.0 | 0.0 | 0.0 | 3 | **3.0** | Tier 5 | E |
| Bank of Montreal ⚠ | BMO | 0.0 | 0.0 | 0.0 | 2 | **2.0** | Tier 5 | E |
| TD Bank ⚠ | TD | 0.0 | 0.0 | 0.0 | 1 | **1.0** | Tier 5 | E |

> ⚠ Confirmed false positive — original NLP score driven by idiomatic language, not genuine digital asset engagement. Adjusted NLP score is zero.

---

## Key Findings

1. **Predictive validity confirmed** — Schwab's Q2 2025 NLP peak (19.81) preceded the April 16, 2026 Schwab Crypto product launch by 10 months. High Q&A engagement scores are leading indicators of real product deployment.

2. **The GENIUS Act explains the Q2 2025 inflection** — 9 of 16 banks peaked in Q2 2025. The GENIUS Act's Senate passage (June 17, 2025, 68–30) drove a wave of analyst stablecoin questions in Q2 earnings calls. The inflection is regulatory in origin.

3. **Single-score NLP misranks Goldman Sachs** — NLP peak rank: 11th (1.84). Composite rank: 11th but Tier 3 (39.9). Goldman's Q&A/Full transcript ratio is 0.23x — it discusses digital assets 4× more in scripted remarks than Q&A. GS DAP spin-out (mid-2026), tokenized MMF with BNY (live July 2025), and EIB digital bond justify a D4 score of 22/25.

4. **Specificity ratio separates operational banks from aspirational ones** — State Street has a specificity ratio of 1.000 (100% Custodial terms) and 8/8 quarter consistency. PNC's peak quarter is 90% General terms with near-zero Custodial/Infrastructure. Same NLP rating tier (Developing), completely different strategic postures.

5. **Four banks are confirmed false positives** — Wells Fargo, Truist, Bank of Montreal, and TD Bank passed initial NLP screening due to the phrase "circle back" and "full circle." Manual excerpt review confirmed none reference Circle Financial. TD Bank's "strategic investment" refers to its Schwab stake. All four have adjusted NLP scores of zero.

6. **No bank reached the Leader threshold in Q&A alone** — the ≥15 score AND ≥10 unique terms threshold was not reached by any bank in the Q&A-only dataset. This is itself a finding: institutional banks are consistently measured and conservative in investor-facing discussions about digital assets, regardless of how active they are operationally.

---

## Known Limitations

| Limitation | Description | Recommended Fix |
|------------|-------------|-----------------|
| **Term disambiguation** | "circle" matches Circle Financial but also "circle back." Caught via manual excerpt review. | Sentence-level embeddings (BERT/GPT) for context-aware matching |
| **Q&A-only scope** | Banks like Goldman Sachs that discuss DA primarily in prepared remarks are structurally underdiscovered by NLP alone | Score prepared remarks separately; compute a disclosure delta |
| **Quarter coverage gaps** | Capital One includes Q4 2023 instead of Q1 2025, slightly reducing cross-bank comparability | Standardize quarter windows across all banks |
| **D4 subjectivity** | External research scores involve analyst judgment. Weights are documented but two analysts may score differently | Develop a rubric with scored examples to calibrate inter-rater reliability |
| **No Phase 2 data** | Dataset ends Q4 2025. Q1 2026 transcripts (post-GENIUS Act) are not yet scored | Re-run pipeline on Q1–Q2 2026 transcripts to track post-GENIUS Act acceleration |

---

## Files

| File | Description |
|------|-------------|
| `digital_asset_intelligence_FINAL.html` | Interactive dashboard — open in any browser, no server required |
| `digital_asset_analysis_FINAL.docx` | Full research report — methodology, scoring tables, cluster rationale, five key findings, limitations |
| `QnA_Analysis_Results_Mar_10_2026.csv` | Raw NLP scoring output — 128 rows (16 banks × 8 quarters), all sub-scores, terms, excerpts, sentiment |
| `Digital_Assets_Results_Mar_4_2026.csv` | Full-transcript NLP scoring output — used for disclosure ratio (D3) calculation |
| `NLP_Scoring_Methodology_QnA_Analysis.docx` | Original methodology documentation from the NLP pipeline |

---

## Team

BUFN403 Capstone · Team 5  
Digital Assets Classification & Intent  
