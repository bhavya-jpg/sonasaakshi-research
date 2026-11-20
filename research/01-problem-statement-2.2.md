# Problem 2.2: the 9-part schema, with our notes

Source: Tech4Bharat 2026 Problem Statements brochure, Theme 2 Jeweltech, statement 2.2, tagged **Agentic AI**. The organisers' points are summarised in the left column. Our working notes are on the right; anything marked *to validate* is a hypothesis for field research.

| Part | Organisers' framing (summarised) | Our notes |
| --- | --- | --- |
| 1. The problem | Jewellers issue gold to karigars by weight and get finished pieces back with agreed wastage. Tracking issue, return, wastage, deadlines and payment across many karigars and custom orders is manual. That causes losses, disputes, missed delivery dates and late pay. | Jewellery ERPs already digitise the jeweller's side (see 03). The unsolved part is a record **both** sides trust, plus deadline planning and fair settlement. |
| 2. Who lives with this | Karigars working from small workshops or home for several jewellers at once, and jewellers juggling custom orders across many karigars. | Many karigars in southern hubs are Bengali migrants (see 04), so jeweller and karigar often don't share a first language. *To validate: share of Bengali karigars in Bengaluru clusters.* |
| 3. How it's handled today | A notebook or slip for each issue, wastage agreed verbally, deadlines chased by phone, accounts squared at month end. | Each side keeps its own notebook. *To validate: how often the two notebooks disagree at month end.* |
| 4. What it costs | Unexplained gold losses, soured relationships, missed wedding dates, artisans waiting weeks for pay. | At Rs 12,615/g (22K, Bengaluru, 15 Nov 2026), every unexplained gram costs about Rs 12,600. *To validate: grams unexplained per shop per month.* |
| 5. Who else is in the picture | Jewellers and counter staff; karigars and helpers; customers with fixed occasion dates; refiners recovering gold from workshop scrap. | The refiner is the neutral party for scrap weight. The JanAI Cafe can be the neutral re-weigh point. |
| 6. What makes it hard | Accuracy must hold at weight level, both parties must accept the audit trail, and fairness matters most to the artisan, who has less power. | Our design: instrument readings only, co-signed hash-chained events, and a karigar-owned view. |
| 7. Boundaries | Settlements go to both parties for approval; each karigar has full access to his own account. | These become HITL gates 4 and 5 and the karigar ledger (see design/architecture.md). |
| 8. Field questions | How gold is issued and recorded and who holds the record; how wastage is agreed and disputed; what happens when a piece is late for a wedding; how long karigars wait for pay; what a karigar does when numbers differ; how many karigars and open orders a shop handles. | Expanded into scripts in field-research/interview-guide.md. |
| 9. Following the money | A karigar with a clean record of work delivered looks very different to anyone deciding whether to trust him. | Revenue order: jeweller subscription first; lender referral fees on the karigar Work Passport later. |

## Why this is an Agentic AI problem, not a ledger app

| Agentic requirement (brochure) | Where it shows up in 2.2 |
| --- | --- |
| Pursues a multi-step goal | Each job card runs for days or weeks: issue, accept, make, return, reconcile, settle, pay |
| Acts in external systems | Scale reading, WhatsApp/SMS/IVR notifications, payout, PDF slip, refiner log, lender share |
| Keeps memory of the case | Open loads per karigar across jewellers, deadlines, disputes, payment history |
| Recovers when something fails | Scale disagreement, unreachable karigar, missed deadline, offline phone, payout failure |
| Human approval before money, legal commitment or personal data | Gold issue, return acceptance, two-party settlement, payout, consent to share the Passport |
