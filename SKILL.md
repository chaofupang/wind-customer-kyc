---
name: wind-customer-kyc
description: Use when researching a company before creating a Wind CRM account. Performs entity verification, Wind competitor screening, sanctions pre-screening, AUM/scale and strategy research, QFII/Bond Connect China-market-access checks, China relevance scoring, Wind product-fit analysis, lead scoring, and a CRM-ready recommendation.
license: Proprietary. Internal Wind use only.
compatibility: Requires an agent with web/browser access for current public information. Can use bundled XLSX/CSV/JSON references. If live web access is unavailable, mark dynamic checks as UNKNOWN rather than guessing.
metadata:
  author: Wind EMEA Sales
  version: "1.3.3-team"
---

# Wind Customer KYC

## Repository layout

All bundled resources are relative to this `SKILL.md`:

- `references/qfii_emea_reference.csv`
- `references/qfii_emea_reference.xlsx` (optional backup)
- `references/competitor_reference.csv`
- `references/product_mapping.csv`
- `references/china_market_access.md`
- `references/bond_connect_lookup.md`
- `schemas/output_schema.json`
- `examples/lingotto-example.md`

## Inputs

Minimum input:

`<company name>`

Examples:

- `Lingotto Investment Management LLP`
- `KYC: Squarepoint Capital`
- `Check S&P Global before CRM creation`

If the entity is clearly identifiable, begin immediately. Ask only when multiple materially different entities match.

## Required workflow

Run these steps in order:

1. Entity verification
2. Wind competitor screening
3. Sanctions and risk screening
4. Customer classification
5. Company scale / AUM
6. Business or investment strategy
7. China market access screening
8. China exposure analysis
9. Wind product fit
10. China relevance score
11. Commercial lead score
12. Evidence summary
13. CRM recommendation
14. CRM-ready summary
15. Next sales validation question

If a direct Wind competitor is confirmed, clearly flag `DO NOT CREATE / WIND COMPETITOR`.

If a material sanctions issue is identified, compliance status takes priority over commercial attractiveness.

## 1. Entity verification

Verify:

- Official company name
- Common/trading name
- Official website
- Headquarters
- Major offices
- Parent company
- Relevant subsidiaries
- Ownership type
- Public / Private / Government / Sovereign / Subsidiary
- Short business description

Do not mix information from similarly named legal entities.

## 2. Wind competitor screening

Classify:

- `YES — Direct`
- `PARTIAL`
- `NO`

A direct competitor materially overlaps with Wind in one or more of:

- financial terminals
- market data
- company fundamentals
- equity/bond/fund data
- macroeconomic databases
- financial APIs / bulk data
- research platforms
- index data / index services
- China financial data

Read `references/competitor_reference.csv` for known examples and overlap areas.

The reference list is not exhaustive. Independently assess any company not listed.

Never classify an institution as a competitor merely because it operates in financial services.

Output:

- Wind Competitor
- Competitor Level
- Overlapping Business
- Evidence / reason

## 3. Sanctions and risk screening

Prefer current authoritative sources:

1. US OFAC
2. European Union sanctions sources
3. UK sanctions / OFSI
4. United Nations
5. Relevant national regulators/governments

Always state the screening date.

Use these statuses:

- `CLEAR`
- `SANCTIONS-LINKED`
- `POTENTIAL MATCH`
- `CONFIRMED MATCH`
- `UNKNOWN`

`SANCTIONS-LINKED` means the entity itself may not be directly listed but a material connection exists, such as a sanctioned controlling shareholder, parent, important subsidiary, sectoral restriction, or restricted products/services.

Do not declare a company sanctioned merely because of nationality, geography, media language, or a similar name.

This is a sales pre-screening and does not replace formal Wind compliance approval.

## 4. Customer classification

Choose one primary type and optional secondary type.

Examples:

- Hedge Fund
- Asset Manager
- Mutual Fund Manager
- Pension Fund
- Sovereign Wealth Fund
- Private Equity
- Venture Capital
- Bank
- Investment Bank
- Broker
- Insurance
- Corporate
- Commodity Trader
- Energy Company
- University
- Research Institution
- Government
- Central Bank
- Exchange
- Index Provider
- Financial Data Provider
- Fintech
- Consulting
- Other

## 5. Company scale / AUM

Use the most relevant metric for the customer type.

For investment managers, distinguish:

- Traditional AUM
- Regulatory AUM / RAUM
- NAV
- Gross Asset Value
- Firmwide assets
- Commitments

Never label RAUM, NAV, GAV, or commitments as conventional AUM without qualification.

Always state the reference date/year and source.

For banks use total assets/revenue/employees as relevant.

For corporates use revenue/market cap/employees/geographic scale.

For universities/research institutions use potential user base and relevant finance/economics/business research scale rather than corporate revenue.

## 6. Business / investment strategy

For investment managers identify, when evidence exists:

- Long Only
- Long/Short
- Market Neutral
- Quantitative/Systematic
- Fundamental
- Multi-Strategy
- Global Macro
- CTA
- Equity
- Fixed Income
- Credit
- Multi-Asset
- Private Markets
- Emerging Markets
- Asia
- China
- Event Driven
- Arbitrage

Also assess data intensity.

For non-investment customers, analyze relevant use cases such as treasury, trading, research, commodity exposure, FX, economic research, benchmarking, or risk advisory.

## 7. China market access screening

This is a mandatory high-value check.

### QFII

QFII verification is MANDATORY.

Primary bundled source: `references/qfii_emea_reference.csv`.

Optional backup: `references/qfii_emea_reference.xlsx`.

Match the researched entity against the `英文名称` field.

Lookup rules:

1. Always attempt the bundled CSV before returning `QFII = UNKNOWN`.
2. Exact legal-name match = confirmed.
3. Normalized case/punctuation differences may be accepted only when the legal entity is clearly the same.
4. A common-name, parent, subsidiary, branch, or affiliate match must be verified before treating it as the researched entity.
5. Fuzzy similarity alone is not confirmation.
6. If the CSV is successfully read and the entity is not present, output `QFII = NO` for this EMEA reference.
7. If the CSV cannot be accessed/read, try the XLSX backup if available.
8. Only after both bundled sources fail technically may output be `QFII = UNKNOWN`.

If matched, output:

- QFII: YES
- QFII entity name
- Approval date
- Registration place
- Primary custodian

A confirmed QFII match is Tier 1 evidence of China market access and should materially increase China relevance.

Do not assume a historic QFII approval is still commercially active if there is evidence of exit or closure.

### Bond Connect Northbound

Bond Connect verification is MANDATORY when assessing China market access.

Read and follow `references/bond_connect_lookup.md`.

Primary official source:

`https://www.chinabondconnect.com/sc/Northbound/Onboarding/Approved-Investors.html`

Required behavior:

1. Open the official Approved Investors page.
2. Confirm the list's stated reference date/month.
3. Search the page for the exact legal English name of the researched entity.
4. If needed, try normalized punctuation/case and a verified current legal/common name.
5. Do NOT transfer a parent/subsidiary/branch/affiliate match to the researched entity without verifying the legal entity.
6. If exact/verified match exists on the official page:
   - Bond Connect Northbound = YES
   - record exact listed entity
   - record official list reference date
7. If the official page loads successfully, is searched, and the entity is absent:
   - Bond Connect Northbound = NO
8. If the official page cannot be accessed or searched:
   - Bond Connect Northbound = UNKNOWN
   - never convert a technical lookup failure into NO

A confirmed Bond Connect match is Tier 1 evidence of China fixed-income access.

### Other market-access evidence

Where reliable sources exist, also consider:

- Swap Connect
- Stock Connect-related institutional activity
- CIBM access
- other formal China market-access programs

Do not invent eligibility.

## 8. China exposure analysis

Assess four dimensions separately:

### A. Investment Exposure
Examples: A-shares, H-shares, China bonds, Chinese companies, China/Greater China funds, EM portfolios, disclosed holdings.

Rating: High / Medium / Low / Unknown.

### B. Operating Exposure
Examples: Mainland/HK offices, China revenue, local subsidiaries, China clients, manufacturing/sales operations.

Rating: High / Medium / Low / Unknown.

### C. Research / Data Exposure
Examples: China PMs, analysts, economists, China research, quant China roles, China-data recruitment.

Rating: High / Medium / Low / Unknown.

### D. Physical Presence
Mainland China / Hong Kong / Greater China / Asia hub.

Rating: High / Medium / Low / None / Unknown.

Also output trend:

- `↑ Expanding`
- `→ Stable`
- `↓ Contracting`
- `? Unknown`

Use recent material changes where available.

## 9. China evidence hierarchy

Use this priority:

### Tier 1 — Direct market access
Very strong evidence:
- QFII
- Bond Connect Northbound
- equivalent formal onshore market access

### Tier 2 — Confirmed activity
Strong evidence:
- disclosed China/A-share/bond holdings
- China/Greater China fund
- dedicated China PM/team
- substantial China operating business

### Tier 3 — Indirect signal
Supporting evidence:
- Asia strategy
- HK office
- China recruitment
- China research/publications
- general global mandate

Do not elevate Tier 3 evidence to Tier 1 strength.

## 10. Wind product fit

Read `references/product_mapping.csv`.

Recommend only products supported by the customer's actual profile.

Potential areas include:

- Wind Financial Terminal
- China Equity Data
- China Bond Data
- China Fund Data
- Private Fund Data
- EDB / Macroeconomic Data
- Quantitative Factors
- PIT Fundamentals
- Historical Market Data
- API
- WDS / Bulk Data
- Research
- ESG
- Index Data / Index Services

Use `HIGH FIT`, `MEDIUM FIT`, `LOW FIT`.

QFII should increase relevance of China equity, PIT, market data, terminal and API/WDS use cases when consistent with the customer's strategy.

Bond Connect should increase relevance of China bond, issuer/credit, valuation/yield/curve, macro and API/WDS use cases.

Do not recommend every Wind product.

## 11. China relevance score

Score 0–10.

- 8–10: Very High
- 5–7: High
- 2–4: Medium
- 0–1: Low

A confirmed QFII or Bond Connect match is a strong upward factor.

If both QFII and Bond Connect are confirmed, China relevance should normally be at least 8/10 unless reliable evidence shows the access is inactive or the relevant business has been exited.

Explain the score in 1–3 sentences.

## 12. Commercial lead score

Score 0–100:

- Data Intensity: 25
- China Relevance: 25
- Wind Product Fit: 25
- Commercial Scale / Institutional Potential: 15
- Accessibility / Geographic Fit: 10

Classification:

- 80–100: Priority A
- 60–79: Priority B
- 40–59: Priority C
- 0–39: Low Priority

### Guardrails

For a normal corporate without a confirmed treasury/trading/research/commodity/economic-data use case, Data Intensity should normally not exceed 15/25.

For universities/research institutions, use `Institutional Potential / Potential User Base` instead of corporate scale.

A direct competitor must not receive a normal sales priority.

A compliance-risk entity may still have commercial fit, but the CRM recommendation must reflect the risk status.

Show the component scores, not only the total.

## 13. Evidence rules

Use:

### ✅ Confirmed
Reliable direct or authoritative evidence.

### ⚠️ Inferred / Likely
Strong indirect evidence, but not explicitly confirmed.

### ❓ Unknown
Reliable public information could not be found.

Never invent:

- AUM
- China AUM
- strategy
- portfolio exposure
- Bloomberg/FactSet/LSEG/CEIC usage
- Wind usage
- sanctions status
- ownership
- China team
- user count
- procurement budget

If unverified, write `UNKNOWN`.

## 14. Source priority

Prefer:

1. Government / regulatory / sanctions authority
2. Official company website
3. Annual report / filing
4. Regulatory disclosure
5. Official fund report
6. Reputable financial media
7. Established industry source
8. Recruitment/job pages
9. Other credible public sources

For important facts include the source and reference date.

## 15. Required output format

Start with:

# Wind Customer KYC — <Company>

**Screening date:** <date>

## 1. CRM Decision
One-line recommendation and Lead Score.

## 2. Entity Verification
Concise table.

## 3. Wind Competitor Screening
YES / PARTIAL / NO plus evidence.

## 4. Sanctions / Risk Screening
Status plus caveat.

## 5. Customer Type & Scale
Include AUM definition/date if relevant.

## 6. Strategy / Business Model
Only relevant strategy/use-case information.

## 7. China Market Access
QFII / Bond Connect / other access.

## 8. China Exposure
Investment / Operating / Research-Data / Presence / Trend.

## 9. China Relevance Score
X/10 with reason.

## 10. Wind Product Fit
Prioritized product table.

## 11. Commercial Lead Score
Show all five components and total.

## 12. Why Wind?
2–5 specific sales reasons.

## 13. Evidence Summary
Confirmed / Inferred / Unknown.

## 14. CRM Summary
Provide this exact field block:

**Company:**  
**Official Entity:**  
**Primary Customer Type:**  
**HQ:**  
**Scale:**  
**AUM Type:**  
**Main Strategy / Business:**  
**QFII:** YES / NO / UNKNOWN  
**QFII Approval Date / Custodian:**  
**Bond Connect:** YES / NO / UNKNOWN  
**Bond Connect Official List Date:**  
**Investment China Exposure:**  
**Operating China Exposure:**  
**Research/Data China Exposure:**  
**China Presence:**  
**China Trend:**  
**China Relevance:** X/10  
**Wind Competitor:**  
**Sanctions Status:**  
**Potential Wind Needs:**  
**Lead Score:** XX/100  
**CRM Recommendation:**  

Then provide a 3–5 sentence CRM-ready narrative.

## 15. Next Sales Validation Question

End with 1–3 high-value questions that would most change the qualification or product-fit conclusion.

Prefer specific questions over generic discovery questions.

Example for a newly approved QFII:

`Are you currently building out your onshore China investment and data infrastructure following the QFII approval, and which teams will consume China market/fundamental data?`
