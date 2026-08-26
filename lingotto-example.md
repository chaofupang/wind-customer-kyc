# Example — Lingotto Investment Management LLP

This example demonstrates how a QFII hit should affect the KYC result.

## Key expected behavior

- Identify Lingotto Investment Management LLP as an investment manager, not a Wind competitor.
- Match the legal entity against `qfii_emea_reference.xlsx`.
- Surface:
  - QFII: YES
  - Approval date: 2026-07-07
  - Registration place: UK
  - Primary custodian: HSBC
- Treat QFII as Tier 1 China market-access evidence.
- Increase China relevance materially versus a profile based only on public China-office/fund evidence.
- Recommend China equity, PIT/historical fundamentals and API/WDS as high-priority validation areas when consistent with the firm's strategy.
- End with a specific sales question such as:

> Are you currently building out your onshore China investment and data infrastructure following the QFII approval, and which teams will consume China market/fundamental data?

Do not assume the existence of an active China portfolio solely from QFII approval; distinguish market access from confirmed holdings.
