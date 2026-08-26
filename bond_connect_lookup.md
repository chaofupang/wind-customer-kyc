# Bond Connect Northbound Verification Protocol

Official source:
https://www.chinabondconnect.com/sc/Northbound/Onboarding/Approved-Investors.html

## Mandatory lookup rule

Bond Connect verification is mandatory for every KYC when China market access is relevant.

Use the official China Bond Connect Northbound Approved Investors page as the primary source. Do not rely on general web snippets, news articles, or third-party lists for a YES/NO decision.

## Lookup sequence

1. Open the official Approved Investors page.
2. Confirm the list's stated reference date/month.
3. Search the page for the exact legal English name of the researched entity.
4. If no exact match:
   - try normalized punctuation/case;
   - try a verified current legal/common name;
   - check whether the page lists a branch/subsidiary instead of the parent.
5. A parent, subsidiary, branch, or affiliate match must NOT be transferred to another group entity without verifying that the researched legal entity itself is the approved investor.
6. If an exact/verified entity match is found on the official page:
   - Bond Connect Northbound = YES
   - record the exact listed entity name
   - record the official list reference date
   - cite the official page
7. If the official page was successfully loaded and searched but the entity was not present:
   - Bond Connect Northbound = NO
8. If the official page could not be accessed or searched:
   - Bond Connect Northbound = UNKNOWN
   - do not convert a technical lookup failure into NO.

## Confidence

- CONFIRMED YES: exact or legally verified entity match on official list.
- CONFIRMED NO: official current list successfully searched and no entity match.
- UNKNOWN: official current list not accessible/searchable.
- RELATED ENTITY ONLY: affiliate/branch/parent/subsidiary found, but not the researched entity.

## China relevance

A confirmed Bond Connect Northbound match is Tier 1 evidence of China fixed-income market access and should materially increase:
- China Relevance Score
- China Bond Data fit
- issuer/credit data fit
- valuation/yield/curve fit
- EDB/macroeconomic fit
- API/WDS fit when appropriate

Do not assume actual portfolio size or current bond holdings merely from market access.
