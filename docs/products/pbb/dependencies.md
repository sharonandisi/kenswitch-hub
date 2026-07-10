# Dependencies

PBB doesn't stand alone — it's built on top of several other pieces of infrastructure, some of them other Kenswitch products, some external.

| Dependency | What it provides | Why PBB needs it |
|---|---|---|
| **KEPSS** (Central Bank of Kenya) | Real-time gross settlement between banks | This is where money *actually* moves. PBB only carries messages; KEPSS does the settlement. |
| **ISO 20022 messaging standard** | The message formats (pain.013/014/017) | The common language every bank must speak to plug into PBB — this is what makes it interoperable rather than bilateral, one-off integrations per bank. |
| **Bank/Issuer core banking + digital channels** | The actual approve/decline screen the customer sees | PBB has no UI of its own for the payer — it depends entirely on each bank's app or USSD channel to present the request. |
| **mTLS/PKI certificate infrastructure** | Mutual authentication between Kenswitch and each participant | Every institution needs a registered client certificate before they can send or receive a single message — this is the "onboarding" gate. |
| **Acquirer/PSP systems (merchant-facing)** | The REST/JSON layer merchants integrate against | Notice: **Issuers talk ISO 20022/XML to Kenswitch; Acquirers talk REST/JSON.** Kenswitch translates between the two — a genuinely important architectural fact. |
| **HMAC-SHA256 shared secrets** | Callback authentication | Prevents a fake "payment approved" webhook from being injected by anyone who isn't the actual bank. |

## Debugging heuristic

If something's broken, first ask *which side* it's broken on:

- Kenswitch routing/validation problem?
- Issuer-side authentication/channel problem?
- Acquirer-side integration problem?
- KEPSS settlement problem?

Those are four different teams to escalate to — PBB itself only really owns the middle bit.
