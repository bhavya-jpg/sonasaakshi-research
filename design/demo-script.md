# 3-minute demo (Bangalore Palace, 27 Dec 2026)

Two phones (jeweller, karigar), one laptop (dashboard and cafe console), one jewellery scale with USB out. Every sandbox step has a keyboard trigger and a pre-recorded voice fallback.

| Time | Beat | What the room sees | HITL / label |
| --- | --- | --- | --- |
| 0:00 | Hook | A real, masked issue slip from field research: "This slip is the only record of 52.340 g of 22K gold, about Rs 6.6 lakh." | |
| 0:20 | Issue by voice | Jeweller says "Ramesh ko 52.340 gram 22 carat issue karo, do kangan, wastage do percent, delivery 5 December." Scale value fills the weight. Hindi read-back (Kannada for Bengaluru shops). | HITL 1 |
| 0:50 | Karigar accepts | Bengali voice note on the second phone; Ramesh accepts by voice. His ledger shows 3 jewellers and 140 g on hand. | HITL 2 |
| 1:15 | Agent plans | Time jump. The wedding is on 7 Dec and Ramesh's load makes 5 Dec unlikely. The agent proposes moving bangle 2 to another karigar. | HITL 3 |
| 1:45 | Return and dispute | 50.920 g finished + 0.610 g scrap gives a loss of 0.810 g (1.55%), inside the 1.047 g allowance. The counter scale reads 0.040 g lower, so settlement freezes and a cafe re-weigh QR is generated. | |
| 2:15 | Settle offline | Karigar phone goes into airplane mode; his approval queues and syncs without duplicates. Payout fires. | HITL 4, 5 · `[SIMULATED SANDBOX UPI]` |
| 2:40 | The point | Ramesh's Work Passport (14 jobs, 93% on time, 1.4% average loss); shared with a lender on spoken consent. | `[SIMULATED NBFC]` |

## Demo-safe mode

- Venue Wi-Fi fails: run on a phone hotspot. The backend runs locally on the laptop as well.
- Scale USB fails: use the cached reading and say so on screen.
- STT fails in the noise: play the pre-recorded clip; a "replayed audio" badge shows.
- Every number above is fixed in the seed data, so the demo is deterministic.
