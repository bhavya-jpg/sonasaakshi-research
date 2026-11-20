# SonaSaakshi: a witness for every gram

**Tech4Bharat 2026 (GAVS Hackathon) · Theme 2 Jeweltech · Problem 2.2: Gold given to karigars for job-work is tracked on trust, and disputes follow · Agentic AI**

SonaSaakshi is a voice-first AI agent that sits between a jeweller and the karigars (artisan goldsmiths) he gives gold to for job work. It records every issue, return, wastage allowance, deadline and payment as a **two-party record that both sides sign**. Each record is spoken back in each party's own language: Hindi-English or Kannada-English for the jeweller, Bengali or Hindi for most karigars. It plans deadlines against customers' wedding dates and runs a fair re-weigh protocol when two scales disagree. It settles labour only after both parties approve. Over time the karigar builds a **Work Passport**, a clean record of work delivered that he owns and can share, with consent, with a lender.

This repository holds our research, references, field-research kit and design notes. Application code will live in a separate repository.

## Status (20 Nov 2026)

| Area | Status |
| --- | --- |
| Problem framing (9-part schema) | Done, see [research/01-problem-statement-2.2.md](research/01-problem-statement-2.2.md) |
| Desk research and references | Done, see [REFERENCES.md](REFERENCES.md) |
| Field interviews (5 jewellers, 5 karigars, 1 refiner) | **In progress**, see [field-research/](field-research/) |
| Architecture and job-card state machine | Draft, see [design/architecture.md](design/architecture.md) |
| Event schema | Draft, see [design/job-card-schema.json](design/job-card-schema.json) |
| Demo script (3 minutes) | Draft, see [design/demo-script.md](design/demo-script.md) |
| Unit economics | Assumptions to validate, see [business/unit-economics.md](business/unit-economics.md) |

Every number in this repo is labelled as **sourced** (with a link) or **assumption** (to be validated in the field). We do not present assumptions as findings.

## The idea in one flow

```
Jeweller speaks the order  ->  scale reading fills weight  ->  jeweller approves (HITL)
        -> karigar hears it in Bengali and accepts (co-signed ISSUE)
        -> agent tracks deadline vs. wedding date, flags risk, proposes reassignment (HITL)
        -> karigar returns pieces + scrap -> weights reconciled against agreed wastage
        -> mismatch?  -> re-weigh on a neutral calibrated scale at a JanAI Cafe
        -> settlement drafted -> both parties approve (HITL) -> payout [SIMULATED UPI]
        -> karigar's Work Passport updates -> shared with a lender only on spoken consent [SIMULATED]
```

## Repository map

```
README.md                         this file
REFERENCES.md                     every source, grouped, with what we use it for
research/
  01-problem-statement-2.2.md     the organisers' problem, in the 9-part schema, with our notes
  02-market-and-industry.md       size of the trade, karigar share of manufacturing, gold prices
  03-competitive-landscape.md     existing jewellery ERPs and the gap they leave
  04-karigar-workforce.md         who karigars are, migration, languages, power imbalance
  05-technology-and-dpi.md        voice AI, BIS HUID, Account Aggregator and ULI
field-research/
  interview-guide.md              consent script and question sets for jeweller, karigar, refiner
  interview-log-template.csv      one row per interview
  artifact-checklist.md           what physical evidence to capture, and how to mask it
design/
  architecture.md                 components, agent loop, HITL gates, failure recovery, mock labels
  job-card-schema.json            event schema for the co-signed ledger
  demo-script.md                  3-minute live demo with demo-safe fallbacks
business/
  unit-economics.md               who pays, pricing, worked numbers, open questions
```

## Design boundaries we commit to (from the problem statement)

1. Settlements go to **both parties** for approval.
2. Each karigar has **full access to his own account**, across every jeweller he works for.
3. Weight is never inferred. It comes from an instrument reading, and any simulated reading is labelled.
4. Every integration without an open API (UPI payout, NBFC, gold-rate feed) is shown as `[SIMULATED SANDBOX API]`.
5. Consent before any personal data is shared. We collect only what the job needs.

## Team

| Name | Role |
| --- | --- |
| Prashant Bahuguna (CSE, 3rd year) | AI: voice agent, deadline planner |
| Prashant Thakur (CSE, 3rd year) | Field research, design, business model |
| Puneet Yadav (CSE, 3rd year) | Scale integration, offline sync, PWA |
| Bhavya Aggarwal (EE, 3rd year) | Agent orchestration, co-signed ledger, backend |

Institute: NIT Hamirpur

## Licence

Research notes and documentation: CC BY 4.0. Third-party sources remain the property of their owners and are linked, not copied.
