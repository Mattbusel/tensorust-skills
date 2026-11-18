---
name: q3-markdown-watch
description: Track Q3 2026 private credit loan markdowns as BDCs file their 10-Qs. Use when the user asks which private loans were marked down this quarter, which BDC lenders cut marks, what might be marked down next, or how a portfolio of borrowers fared in Q3.
---

# Q3 markdown watch

Use the Tensorust connector to follow Q3 2026 (Sep 30) marks as each BDC files on EDGAR, and to flag the holders that have not filed yet.

## Steps

1. Call `credit_q3_cuts`. It returns the funds filed so far, the last filing date, the count of 5+ point cuts and the biggest cuts first.
2. Report the header numbers first: funds filed, last filing date, number of cuts.
3. List the cuts as a table: company, fund, Jun 30 mark, Sep 30 mark, change in points, par.
4. Flag every row where `holders_not_filed_yet_above` is above 0. Those are holders still carrying the same loan 5+ points higher that have not filed Q3. Call them "possible next markdowns", not predictions.
5. If the user names borrowers or a portfolio, call `lender_marks` for each name and say whether any of them appear in the cuts or have lenders 10+ points apart. For a wider view, call `credit_disagreements` for the loans lenders disagree on most.
6. If the user asks about federal contractors, call `contractor_credit_watch` with `signal` set to `cut_5pt_q3`.

## Rules

- Earnings season is still running. Always give the last filing date and say the list will grow.
- Free answers show the top 10. Do not call with `full=true` unless the user says they have a Tensorust key set up.
- Marks come from public SEC filings. This is data, not investment advice, and the user should not treat a pending holder as a trading signal.
