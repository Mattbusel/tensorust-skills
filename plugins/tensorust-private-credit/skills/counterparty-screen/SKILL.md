---
name: counterparty-screen
description: Screen a company, vendor, supplier, contractor or borrower before a deal, payment or onboarding. Use when the user asks for KYC or due diligence on a business, who owns or controls a company, whether a vendor is on a banned or restricted list (1260H, Section 889, FCC Covered List, UFLPA, BIOSECURE), or whether a counterparty's lenders are marking it down.
---

# Counterparty screen

Use the Tensorust connector to build a short, sourced screen of one business counterparty from public records.

## Steps

1. Get the counterparty's name. A UEI or EIN also works for `contractor_credit`.
2. Identity and control: call `lookup_organization` with the name.
   - If nothing is found, call `search_organizations` and ask the user to pick from the matches.
   - Note the sources, the control links (parents, subsidiaries, licenses) and any `obligations` (federal rules that likely apply).
3. Restricted vendors: call `exposure_screen_purchases` with one line, `{"vendor": "<name>"}`. If the user pasted invoice or purchase-order lines, pass those instead (vendor, description, amount, date, award). Report each hit with its list, rule status and severity.
4. Lender stress and federal exposure: call `contractor_credit` with the name. Report the lowest and highest lender mark, the Q3 2026 move if any, federal obligations, the top agency and the stress signals. If it is not found, say the company has no BDC first-lien loan in the filings.
5. Only if the counterparty is buying single-family homes: call `road_investor_group` with the name for its control group and ROAD Act status.

## Report

Give one table with a row per check: Identity, Restricted lists, Lender stress, Federal exposure, and ROAD Act if run. Each row has the finding, the source and the as-of date. Then one line with what needs a human look.

## Rules

- A check with no match is "no match found in these sources", never "clear" or "approved".
- This screen covers businesses only. Do not use it to look up private individuals.
- Free answers are previews. Do not call with `full=true` unless the user says they have a Tensorust key set up.
- This is public-records data, not legal or compliance advice. Final decisions stay with the user's compliance team.
