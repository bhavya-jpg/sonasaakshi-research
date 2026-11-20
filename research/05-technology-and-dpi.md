# Technology and digital public infrastructure

## Voice

- **Sarvam Saaras** speech-to-text covers 22 Indian languages plus English. It handles code-mixed speech and mid-sentence language switches, supports 8 kHz telephony audio, and offers REST (up to 30 s), batch and WebSocket streaming ([docs](https://docs.sarvam.ai/api/getting-started/models/saaras.md)).
- Its `codemix` output mode keeps English words in English and Indic words in native script, which suits a jeweller saying "Subrata ko 52.340 gram issue karo" or "Subrata-ge 52.340 gram issue maadi". Language codes include `kn-IN` and `bn-IN` ([API reference](https://docs.sarvam.ai/api-reference/speech-to-text/transcribe)).
- **Numbers are the risk.** Grams to three decimals must never come from speech alone. The scale reading is the source of truth; speech gives only the intent, the karigar, the item and the date. The read-back states the scale value.

## Weight capture

| Option | Pros | Cons | Plan |
| --- | --- | --- | --- |
| Scale with USB or serial output, via a bridge to the phone | Exact, no parsing errors | Needs a cable or adapter per scale model | Primary for jewellers whose scales support it |
| BLE scale | Wireless | Few jewellery-grade BLE scales | Optional |
| OCR of the scale's display from the phone camera | Works with any scale | Glare, decimal-point errors | Fallback, with mandatory read-back and confirmation |
| Manual entry | Always works | Disputable | Allowed only with a flag, and both parties must confirm |

## Hallmarking

- BIS hallmarking with a 6-digit HUID is mandatory in 380+ districts. Consumers can verify HUIDs in the BIS CARE app ([New Kerala / BIS](https://www.newkerala.com/news/a/seven-more-districts-added-6th-phase-mandatory-hallmarking-394.htm)).
- Relevance: the finished piece's HUID can be attached to the job card at return, linking karigar work to the hallmark record. *Future scope.*

## Credit rails for the Work Passport

- RBI is pushing banks to use the **Unified Lending Interface (ULI)** and the **Account Aggregator (AA)** framework for MSME credit ([Business Standard](https://www.business-standard.com/finance/news/banks-must-leverage-dpi-stack-to-deepen-msme-credit-access-rbi-governor-126062201009_1.html)).
- ULI has onboarded 64 lenders, and AA has 252 million linked users ([New Kerala](https://www.newkerala.com/news/a/ai-led-models-likely-unlock-up-170-bn-credit-405.htm)).
- In the hackathon, the lender share is `[SIMULATED NBFC]`. The Passport is a signed summary the karigar chooses to share; we never push data to a lender without his spoken consent.

## Proposed stack (draft)

| Layer | Choice |
| --- | --- |
| Client | PWA for entry-level Android (offline-first, IndexedDB event queue); WhatsApp and IVR for karigars without a smartphone |
| Agent | State-machine orchestrator (LangGraph or a custom FSM) with tool calls; one case per job card |
| Voice | Sarvam STT and TTS (Kannada, Bengali, Hindi, English) |
| Ledger | Append-only events, each signed by the acting party's device key; SHA-256 hash chain per job card |
| Backend | FastAPI, PostgreSQL, Redis queue |
| Sandbox | Mock UPI payout, mock NBFC, mock gold-rate feed, all visibly labelled |
