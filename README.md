# US business texting rules by state (2026): quiet hours, consent, opt-outs

Open data (CSV + JSON) on the state rules that can apply to business texts, especially **missed call text back** (an automatic text to someone whose call you didn't answer). 50 states + DC, with statute links for every verified row.

**Not legal advice.** Last verified **October 9, 2026**. Only 9 states are marked `verified` (we read the statute or official agency page). `not_verified` does **not** mean the state has no law; it means we didn't verify a texting-specific rule. Federal rules apply everywhere.

Human-readable version with search, filters and explanations: [Missed call text back laws by state (Peace Call)](https://getpeacecall.com/missed-call-text-back-laws-by-state/?utm_source=github&utm_medium=dataset&utm_campaign=quiet_hours_data)

## Files

| File | What it is |
|---|---|
| `us_business_texting_rules_by_state.csv` | One row per state + DC |
| `us_business_texting_rules_by_state.json` | Same data, `sources` as an array of URLs |

### Fields

- `state`
- `status`: `verified` or `not_verified`
- `stricter_than_federal`: `True` if at least one state hours rule is narrower than the federal 8 a.m.–9 p.m.
- `covers_texts`: whether (and how) the state law reaches text messages
- `quiet_hours`, `quiet_hours_notes`: recipient's local time
- `consent_limits_optout`: consent, frequency caps, opt-out rules
- `reply_or_inquiry_carveout`: exceptions for replies to a request or inquiry (relevant to missed call text back)
- `sources`: statute / official agency URLs
- `last_verified`: date we read the sources

## Federal baseline (all states)

- No telephone solicitations before 8 a.m. or after 9 p.m. recipient local time ([47 CFR 64.1200(c)(1)](https://www.law.cornell.edu/cfr/text/47/64.1200)).
- STOP, QUIT, END, REVOKE, OPT OUT, CANCEL, UNSUBSCRIBE always revoke consent; honor within 10 business days ([47 CFR 64.1200(a)(10)](https://www.law.cornell.edu/cfr/text/47/64.1200)).
- Autodialed marketing texts need prior express written consent ([47 CFR 64.1200(a)(2)](https://www.law.cornell.edu/cfr/text/47/64.1200)).
- The FCC one-to-one consent rule was vacated (11th Cir., Jan 2025) and removed effective Aug 29, 2025 ([FCC](https://www.fcc.gov/document/fcc-removes-one-one-consent-rule-nullified-court-decision)).

A window that fits every hours rule we verified: **Monday–Saturday, 9 a.m.–7 p.m.** recipient local time (Pennsylvania also bans Sundays and legal holidays from mid-October 2026).

## Using it in code

```python
import csv
rows = list(csv.DictReader(open("us_business_texting_rules_by_state.csv")))
stricter = [r["state"] for r in rows if r["stricter_than_federal"] == "True"]
print(stricter)
```

## Corrections

Found a law we missed or a change? Open an issue with the statute link. We'd rather be corrected than wrong.

## License and disclosure

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Credit "Peace Call (getpeacecall.com)".

This repo is maintained by an AI agent (Grok Bot) for Peace Call, a small site with free tools for service businesses. Peace Call earns affiliate commissions from HighLevel; nothing in this dataset depends on that, and no income claims are made.
