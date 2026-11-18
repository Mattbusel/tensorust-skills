---
name: mark-cross-check
description: Cross-check the value of a private loan against what other lenders report. Use when the user asks what a private credit loan is worth, wants to check or defend a mark or fair value, reviews a valuation, or asks how BDC lenders value a borrower's first-lien loan.
---

# Mark cross-check

Use the Tensorust connector to compare a private loan's value with the marks that BDC (business development company) lenders report in their SEC filings.

## Steps

1. Get the borrower name. If the user gives their own mark, note it as a share of par (92 means 0.92).
2. Call `lender_marks` with the borrower name.
   - If `found` is false, show the `similar` names and ask which one is meant. Do not guess.
3. Call `contractor_credit` with the same name. It adds the Sep 30 2026 marks as they post, the quarter-on-quarter moves and stress signals. If it is not found, carry on with step 2's result.
4. Report, in this order:
   - Borrower, as-of date, number of funds and managers, loan par and maturity.
   - Lowest mark and manager, highest mark and manager, and the gap in points.
   - Where the user's own mark sits: above the highest, inside the range, or below the lowest, and by how many points.
   - Any Q3 2026 move or stress signal from step 3 (for example `marked_below_90` or `headcount_down_20pct`).
5. Add one line of context from the tool: when lenders sit 10 to 20 points above the lowest peer, the higher ones cut by 5+ points the next quarter about 20% of the time, against about 3% when lenders agree.

## Rules

- Quote marks exactly as returned and give the as-of date every time.
- Free answers are previews. If `access` is `preview`, say that the full fund list needs a Tensorust key. Do not call with `full=true` unless the user says they have a key set up.
- Say plainly that this is data from public filings and not a valuation opinion or investment advice.
- One table is enough. Do not paste the raw tool output.
