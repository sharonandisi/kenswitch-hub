# How It Works

## The plain-English version

1. A merchant (or M-Pesa, for the wallet top-up use case) wants to collect money from you. Their bank/PSP — the **Acquirer** — sends a payment *request* into Kenswitch.
2. Kenswitch validates and routes that request to **your** bank — the **Issuer**.
3. Your bank puts the request in front of you in your banking app: "Approve payment of KES X to [merchant]?"
4. You approve, decline, or ignore it. Your bank sends your decision back through Kenswitch to the Acquirer.
5. If approved, your bank actually moves the money. Kenswitch doesn't touch the funds at any point — it only carries the messages.
6. At the end of the day, all banks/PSPs on the platform settle what they owe each other through the Central Bank's real-time settlement system (**KEPSS**), and everyone gets a reconciliation report.

That's the whole shape of it. Everything below is the same flow, described the way the technical spec and rulebook describe it — useful once someone needs to actually build or debug against it.

## The technical version (same flow, formal names)

Every message in PBB is an **ISO 20022** message — an international standard format for financial messaging. Three message types carry the flow:

| Message | Plain meaning | Who sends it |
|---|---|---|
| **pain.013** | "Here's a payment request" | Acquirer → Kenswitch → Issuer |
| **pain.014** | "Here's the payer's decision" (or a later status update) | Issuer → Kenswitch → Acquirer |
| **pain.017** | "Cancel this request" (only allowed before the payer decides) | Acquirer → Kenswitch → Issuer |

Each message carries a **Business Application Header (BAH)** — think of it as the envelope: who sent it, who it's for, what type of message is inside, and when it was created. Every request also carries a transaction ID made of three fields together, which is what lets the system recognize "this is the same request being resent" rather than accidentally creating a duplicate payment if something gets retried.

### The lifecycle a request moves through

```
CREATED → ROUTED → PRESENTED → PENDING → ACCEPTED (or DECLINED / EXPIRED / CANCELLED) → EXECUTED → SETTLED
```

A few rules that matter operationally:

- **You have up to 30 seconds** to act on a request before it expires automatically.
- **Once you approve it, it's final** at the messaging layer — Kenswitch has no "undo" or chargeback mechanism from that point. Anything that needs reversing after approval is a bank-to-bank/merchant conversation, not a Kenswitch one. See [Legal & Compliance](legal-compliance.md) for exactly how that's handled.
- **Banks must acknowledge a request within 5 seconds**, or the transaction fails and the Acquirer can safely retry it using the same reference (no duplicate risk, by design).
- Status/decision updates going back to the Acquirer are authenticated using a **signed callback** (HMAC-SHA256) — this is just a cryptographic signature that proves the message genuinely came from the bank it claims to, so nobody can fake a "payment approved" notification.

## Where the money actually moves

Never through Kenswitch. Kenswitch validates and routes messages only. The actual funds move bank-to-bank at end of day through **KEPSS**, the Central Bank of Kenya's settlement system — same rail that underpins the whole national banking system's interbank transfers.
