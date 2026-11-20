# Architecture (draft)

## Components

| Component | What it does | AI? |
| --- | --- | --- |
| Jeweller app (PWA) | Voice order intake, scale capture, approvals, open-orders board | Voice |
| Karigar channel | WhatsApp voice notes, IVR for feature phones, PWA for smartphones; his own cross-jeweller ledger | Voice |
| Case agent | One case per job card. Plans steps, calls tools, holds memory, retries and escalates | Yes |
| Deadline planner | Compares each karigar's open load and history with the customer's occasion date, then proposes a split or reassignment | Yes |
| Reconciliation engine | Deterministic: issued = finished + scrap + loss; compares loss to agreed allowance | No (exact maths) |
| Dispute handler | Freezes settlement, logs both readings, books a neutral re-weigh, generates a cafe handoff QR | Yes |
| Co-signed ledger | Append-only events, each signed by the acting device; SHA-256 chain per job card | No |
| JanAI Cafe console | Operator picks up a case by QR: onboarding, eKYC when needed, neutral re-weigh, printed slips | No |
| Sandbox adapters | `[SIMULATED SANDBOX API]` UPI payout, NBFC share, gold-rate feed | Labelled mocks |

## Job-card state machine

```
DRAFT
  -> ISSUE_PENDING        jeweller approves issue (HITL 1) + karigar accepts (HITL 2)
  -> ISSUED
  -> IN_PROGRESS          planner monitors the deadline
       -> AT_RISK         proposes split or reassignment; jeweller approves (HITL 3)
  -> RETURN_WEIGHED       scale readings of finished pieces + scrap
  -> RECONCILED           loss <= allowance and both scales agree within tolerance
     | DISPUTED           scales disagree or loss > allowance
          -> REWEIGH_BOOKED (JanAI Cafe or refiner) -> RECONCILED
  -> SETTLEMENT_PENDING   jeweller approves + karigar approves (HITL 4)
  -> PAYOUT_PENDING       payout approved (HITL 5) -> [SIMULATED UPI]
  -> PAID -> CLOSED
```

## Reconciliation rule

```
loss_g       = issued_g - (finished_g + scrap_g)
allowance_g  = issued_g * wastage_pct / 100
status       = RECONCILED if loss_g <= allowance_g and |jeweller_scale - karigar_scale| <= tolerance_g
               else DISPUTED
```

Worked example (demo values): issued 52.340 g, finished 50.920 g, scrap 0.610 g gives a loss of 0.810 g (1.55%). The allowance at 2% is 1.047 g, so the job is RECONCILED.

## HITL gates

| Gate | Trigger | Who approves |
| --- | --- | --- |
| 1 | Gold issue | Jeweller |
| 2 | Accepting the issued gold | Karigar |
| 3 | Reassigning or splitting a job | Jeweller (karigar informed) |
| 4 | Settlement | Both parties |
| 5 | Payout, and any share of the Work Passport | Payer for the payout; karigar for the share (spoken consent) |

## Failure recovery

| Failure | Recovery |
| --- | --- |
| Scale read fails | OCR fallback, then manual entry flagged for two-party confirmation |
| Karigar unreachable | WhatsApp, then SMS, then IVR call, then a cafe visit task; the case waits, it never auto-approves |
| Phone offline | Events queue locally with idempotent IDs and sync on reconnect; no duplicates |
| Deadline at risk | Planner alert, with proposals ranked by capacity and past on-time rate |
| Payout fails | Retry with backoff, then notify both parties; settlement stays approved |
| Speech misheard | Numbers never come from speech; every record is read back and confirmed |

## Data minimisation

- Karigar profile: name, phone, preferred language. Nothing else until payout or a lender share needs it.
- Jeweller sees only his own jobs with a karigar.
- The Work Passport shows aggregates (jobs, on-time rate, average loss %, value delivered), never other jewellers' names.
