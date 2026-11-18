# Tensorust Private Credit and Counterparty

Three skills for credit, valuation and compliance work, built on the Tensorust Ontology connector. The data comes from public records: SEC filings by business development companies (BDCs), USAspending, SAM, Form 5500, FCC licensing and county property rolls.

## Skills

- **mark-cross-check**: you name a borrower and, if you have one, your own mark. Claude pulls what every BDC lender that holds the first-lien loan reported it at, shows the gap between the lowest and highest manager, and says where your mark sits.
- **counterparty-screen**: you name a company, vendor or contractor. Claude checks who it is in public records, whether its private lenders are marking its loan down, its federal contract exposure, and whether it matches the DoD 1260H, Section 889, FCC Covered List, UFLPA or BIOSECURE lists.
- **q3-markdown-watch**: Claude lists the Q3 2026 loan markdowns as BDCs file their 10-Qs, and the holders that have not filed yet and still carry the same loan higher.

## Install

From the Claude directory, or in Claude Code:

```
/plugin install tensorust-private-credit --marketplace Mattbusel/tensorust-skills
```

## Use it

Install the plugin, then connect the Tensorust connector from the plugin's Connectors tab. No account or sign-in is needed. Then ask in plain words, for example:

- "Cross-check our 92 mark on Pluralsight against the BDC lenders."
- "Screen BGI Americas before we pay this invoice."
- "Which loans did BDCs mark down in Q3, and who hasn't filed yet?"

Free answers are previews (for example the top 10 rows, or the lowest and highest lender). A Tensorust key returns full lists.

## Privacy

The plugin itself stores nothing and runs no code. The skills call one remote server, https://shop.tensorust.com/api/connector, and send it only the arguments of each tool call (a company name, an address, or vendor lines you paste). The server does not see your conversation and needs no sign-in. It keeps nothing from a call except what the privacy policy names (a ROAD Act screening stored under its id, a private workspace a user creates, a rate-limit counter, and standard server logs). Privacy policy: https://shop.tensorust.com/privacy. Terms: https://shop.tensorust.com/terms. Support: mattbusel@tensorust.com.

Answers are data from public filings, not investment, legal or compliance advice. A name that does not match is not a clearance.
