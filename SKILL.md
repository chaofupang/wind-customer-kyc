[SKILL_v1.4.0.md](https://github.com/user-attachments/files/31637000/SKILL_v1.4.0.md)
---
name: wind-customer-kyc
description: Use when researching a company before creating a Wind CRM account. Performs entity verification, fixed CRM customer-type classification, Wind competitor screening, sanctions pre-screening, AUM/scale and core-business research, QFII/Bond Connect and China-exposure checks, evidence-based asset-class mapping, Wind product-fit analysis, sales recommendations, LinkedIn search keywords, and personalized outreach templates.
license: Proprietary. Internal Wind use only.
compatibility: Requires an agent with web/browser access for current public information. Can use bundled XLSX/CSV/JSON references. If live web access is unavailable, mark dynamic checks as UNKNOWN rather than guessing.
metadata:
  author: Wind EMEA Sales
  version: "1.4.0"
---

# Wind Customer KYC

## Repository layout

All bundled resources are relative to this `SKILL.md`:

- `qfii_official_2026-07.csv`
- `competitor_reference.csv`
- `product_mapping.csv`
- `china_market_access.md`
- `bond_connect_lookup.md`
- `output_schema.json`
- `lingotto-example.md`

## Inputs

Minimum input:

`<company name>`

Examples:

- `Lingotto Investment Management LLP`
- `KYC: Squarepoint Capital`
- `Check S&P Global before CRM creation`

If the entity is clearly identifiable, begin immediately. Ask only when multiple materially different entities match.

## Required workflow

Run these research steps in order:

1. Entity verification
2. Wind competitor screening
3. Sanctions and risk screening
4. Fixed Wind CRM customer-type classification
5. Company scale / AUM
6. Core business / investment strategy verification
7. QFII and Bond Connect verification
8. China exposure analysis, including China-related AUM/share only when reliably disclosed
9. Evidence-based asset-class verification
10. Wind product / function mapping by confirmed asset class
11. Recommended sales angles
12. LinkedIn search keywords
13. First-round validation questions
14. Personalized LinkedIn and Email outreach templates

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

Read `competitor_reference.csv` for known examples and overlap areas.

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

Output exactly one primary `Customer Type`. It MUST be selected from the fixed Wind CRM taxonomy below. Do not invent, paraphrase, merge, or create new customer-type labels.

Canonical taxonomy:

| Chinese output | English output |
|---|---|
| 海外央行 | Overseas Central Bank |
| 海外商业银行 | Overseas Commercial Bank |
| 海外保险 | Overseas Insurance |
| 海外券商 | Overseas Securities Firm |
| 海外资管机构 | Overseas Asset Manager |
| 海外对冲基金 | Overseas Hedge Fund |
| 海外PEVC | Overseas PEVC |
| 海外政府机构 | Overseas Government Institution |
| 海外交易所 | Overseas Exchange |
| 海外高校 | Overseas University |
| 海外管理咨询公司 | Overseas Management Consulting Firm |
| 海外智库 | Overseas Think Tank |
| 海外媒体 | Overseas Media |
| 海外企业 | Overseas Corporate |
| 海外其它 | Overseas Other |

Rules:

1. Select only one category.
2. Use the exact Chinese label when the report is in Chinese.
3. Use the exact mapped English label when the report is in English.
4. If the entity has multiple characteristics, choose the category that best represents its principal business and intended CRM classification.
5. If it cannot reliably fit the first 14 categories, use `海外其它` / `Overseas Other`.
6. Do not output alternative labels such as `Central Bank`, `Alternative Asset Manager`, `Financial Institution`, or `Government` as the Customer Type.

Examples:

- European Central Bank → `海外央行` / `Overseas Central Bank`
- Tudor Investment Corporation → `海外对冲基金` / `Overseas Hedge Fund`
- Siemens Energy AG → `海外企业` / `Overseas Corporate`

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

Primary bundled source: `qfii_official_2026-07.csv`.

Match the researched entity against the `英文名称` field.

Lookup rules:

1. Always attempt the bundled CSV before returning `QFII = UNKNOWN`.
2. Exact legal-name match = confirmed.
3. Normalized case/punctuation differences may be accepted only when the legal entity is clearly the same.
4. A common-name, parent, subsidiary, branch, or affiliate match must be verified before treating it as the researched entity.
5. Fuzzy similarity alone is not confirmation.
6. If the official CSV is successfully read and the entity is not present, output `QFII = NO` for the July 2026 official CSRC list.
7. If the CSV cannot be accessed/read, output `QFII = UNKNOWN` and explicitly state that the bundled official QFII source could not be read.
8. Do not infer QFII status from news, parent-company status, affiliates, or similar names when the official bundled list is available.

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

Read and follow `bond_connect_lookup.md`.

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

Read `product_mapping.csv`.

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

### Language consistency

The entire report must be in one language.

- If the user asks in Chinese, output the full report in Chinese.
- If the user asks in English, output the full report in English.
- Do not mix Chinese and English except for product / technical names that are difficult or inappropriate to translate, such as `WFT`, `WDS`, `API`, `PIT`, `EDB`, and official legal entity names where appropriate.

Start with:

`# Wind Customer KYC — <Company>`

Do not add a separate screening-date line unless the date is materially needed for a dynamic risk or official-list result.

### 1. Customer Snapshot / 客户总览

Use a single-column, two-field table. Do not use a four-column layout.

Chinese format:

| 项目 | 结果 |
|---|---|
| **正式名称** | <Official Entity Name> |
| **客户类型** | <必须从固定15类中选择> |
| **总部** | <HQ> |
| **其他办公室** | <Major offices, only if confirmed> |
| **管理规模（AUM）** | <Traditional AUM or the most relevant qualified scale metric> |
| **核心业务** | <Core confirmed business / investment strategies> |
| **主要市场** | <Main confirmed geographic / financial markets> |
| **中国敞口** | <China market access and, when reliably available, China-related AUM and share of total AUM> |
| **是否为Wind竞品** | <是 / 部分 / 否> |
| **制裁风险** | <简洁状态> |

English format:

| Item | Result |
|---|---|
| **Official Name** | <Official Entity Name> |
| **Customer Type** | <exact mapped English label from the fixed taxonomy> |
| **Headquarters** | <HQ> |
| **Other Offices** | <Major offices, only if confirmed> |
| **AUM / Relevant Scale** | <Traditional AUM or the most relevant qualified scale metric> |
| **Core Business** | <Core confirmed business / investment strategies> |
| **Main Markets** | <Main confirmed geographic / financial markets> |
| **China Exposure** | <China market access and, when reliably available, China-related AUM and share of total AUM> |
| **Is a Wind Competitor** | <Yes / Partial / No> |
| **Sanctions Risk** | <concise status> |

Snapshot rules:

- Do NOT include regulator, QFII approval date, AUM date as a separate row, sales priority, CRM recommendation, or overall judgment.
- Do NOT add a prose paragraph immediately below the snapshot that repeats the table.
- Do not output QFII and Bond Connect as separate snapshot rows.
- Integrate QFII / Bond Connect into `China Exposure`.
- When reliable China-related AUM is available, include both amount and share of total AUM where possible.
  Example: `QFII; Bond Connect; China-related AUM approx. USD 10bn, ~12% of total AUM.`
- When market access is confirmed but China AUM is not publicly disclosed:
  `QFII; China-related AUM not publicly disclosed.`
- When no reliable amount can be established, never estimate a China AUM percentage.

### 2. Confirmed Asset Classes & Wind Opportunities / 已确认资产类别与 Wind 机会

This is the core analytical section.

Only include an asset class or business area when reliable evidence confirms that the company actually conducts that activity. Prefer omission over speculation.

Actively verify relevant coverage across, where applicable:

- Equities
- Fixed Income / Bonds
- Funds
- FX
- Commodities
- Macroeconomics
- Private Markets / PEVC
- Quantitative / Systematic Research
- other materially relevant asset classes or research areas

Do NOT add an asset class merely because the institution is described as `multi-strategy`, `asset manager`, `bank`, `hedge fund`, or another broad category.

Output:

| Asset Class / Business Area | Confirmed Activity | Potential Data Needs | Relevant Wind Products / Functions | Fit |
|---|---|---|---|---|
| <asset class> | <concise evidence-backed activity> | <needs logically arising from confirmed activity> | <specific Wind products/functions> | <Very High / High / Medium / Low> |

Chinese reports must use Chinese headers and Chinese fit labels.

Rules:

1. `Confirmed Activity` must be evidence-backed.
2. `Potential Data Needs` may infer reasonable needs from confirmed activity, but phrase them as potential needs rather than confirmed procurement pain points.
3. Product mapping must be selective and specific.
4. Integrate China-related opportunities into the relevant asset class rather than creating a separate `China Opportunity` section.
5. QFII should strengthen the fit of China equity / onshore-market datasets only when consistent with the client's confirmed business.
6. Bond Connect should strengthen the fit of China fixed-income / rates / credit datasets only when consistent with the client's confirmed business.
7. Do not create an Opportunity Score section.
8. Do not create a separate Key Business Details section; relevant details belong in the Snapshot.

### 3. Risk Screening / 风险检查

Output only these two checks:

| Check | Result | Why |
|---|---|---|
| **Is a Wind Competitor** | <Yes / Partial / No> | <one concise sentence explaining why> |
| **Sanctions Risk** | <status> | <one concise sentence explaining why> |

Chinese reports must use:

| 检查项 | 结果 | 原因 |
|---|---|---|
| **是否为Wind竞品** | <是 / 部分 / 否> | <一句话说明原因> |
| **制裁风险** | <结果> | <一句话说明原因> |

Do not include customer type, data-demand authenticity, China-business evidence, or CRM eligibility in this section.

### 4. Recommended Sales Angles / 推荐销售切入

List only the 2–4 strongest sales angles supported by the KYC.

For each angle include:

- short opportunity title
- fit level
- priority Wind products / functions
- concise explanation of the potential need and why Wind may be relevant

Do not repeat long company-background descriptions.

### LinkedIn Recommended Keywords / LinkedIn推荐关键词

Provide practical search strings based on the client's confirmed businesses, functions, locations, and relevant China / Asia exposure.

Example:

```text
Company Portfolio Manager
Company Global Macro
Company Quantitative Research
Company Data
Company Investment Technology
Company Asia
```

Do not output a generic `Recommended Contacts` list. Output LinkedIn search keywords instead.

### Recommended First-Round Validation Questions / 建议首轮确认

Provide 3–4 specific questions that could materially change the qualification or product-fit conclusion.

Avoid generic discovery questions.

## 16. Outreach Templates

At the end of every standard KYC output, generate both:

1. LinkedIn outreach template
2. Email outreach template

The templates must be personalized from:

- the current user's professional identity, when known;
- the customer's fixed Customer Type;
- confirmed Core Business;
- confirmed asset classes;
- China Exposure;
- confirmed QFII / Bond Connect status;
- the strongest evidence-backed Wind product fit.

### Current-user identity rule

Use the current user's known professional identity when it is available in the host agent's context, including:

- Name
- Company
- Role / responsibility
- Region

Never hardcode another user's name, region, title, or responsibility into the Skill.

For example, only use a sentence such as:

`I’m Chaofu from Wind Information, responsible for our business in the UK and Europe.`

when the current user is actually known to be Chaofu with that responsibility.

If the current user's identity is unavailable or uncertain, use placeholders rather than guessing:

`I’m [Name] from Wind Information, responsible for [Region / Role].`

If the user's company is also unknown, use `[Company]`.

### Outreach structure

Generate the outreach in this order:

1. Introduce the sender.
2. Give a one-sentence, highly concise introduction to Wind.
3. Explain why the sender is reaching out to this specific client, based on confirmed business.
4. Explain how Wind may help the client's work.
5. Mention 1–3 plausible pain points that Wind can address, phrased cautiously as potential/common challenges rather than claims about the client.
6. Ask for a short meeting / visit and ask what time is convenient.

### QFII / Bond Connect outreach logic

If QFII is confirmed:

- it may be explicitly mentioned;
- prioritize relevant China equity, fundamental, PIT, historical-market-data, API/WDS use cases when supported by the client's business;
- do not imply that QFII proves material China holdings.

If Bond Connect is confirmed:

- it may be explicitly mentioned;
- prioritize relevant China fixed income, rates, yield curves, credit, valuation, macro, API/WDS use cases when supported by the client's business.

If both are confirmed:

- `onshore China market access` may be highlighted;
- specific pitch areas must still follow confirmed asset classes.

If neither is confirmed:

- do not imply China market-access status;
- China data may still be pitched only where the client's confirmed global / Asia / research activities make it relevant.

### LinkedIn template

Requirements:

- typically 120–180 words;
- professional, concise and natural;
- for English output, use `Hi [Name],` and preferably `Thanks for connecting.` when appropriate;
- do not turn it into a long product catalogue;
- close by asking for a short meeting and what time works.

Output under:

`## LinkedIn`

inside a plain text code block.

### Email template

Requirements:

- typically 180–300 words;
- include a subject linked directly to the client's confirmed core business;
- concise sender introduction;
- one-sentence Wind introduction;
- explain why this client is being contacted;
- include 2–5 relevant Wind capabilities;
- mention a plausible customer pain point without presenting it as confirmed fact;
- end with a meeting / visit CTA asking what time is convenient.

Output under:

`## Email`

inside a plain text code block.

### Outreach prohibitions

Never:

- pitch an unverified asset class;
- fabricate a customer pain point;
- claim the customer uses Bloomberg, LSEG, FactSet, CEIC, or another vendor without evidence;
- equate QFII / Bond Connect with actual China AUM;
- hardcode the Skill author's identity into another user's outreach;
- mix Chinese and English in the outreach unless required for product names such as WFT, WDS, API, PIT, or EDB.

