# FAQ

*Grows organically — every real question that comes up in standup, onboarding, or Slack becomes an entry here. This is a living pulse-check list, not an exhaustive spec.*

## General

**What is PBB in one sentence?**
A way to pay directly from your bank account by approving a request on your banking app — no card involved.

**What's the difference between issuer and acquirer?**
Issuer = your bank (approves/declines the request). Acquirer = the merchant's/wallet's bank or PSP (submits the request on the merchant's behalf). See the [Glossary](../../glossary/index.md).

**Is PBB the same as M-Pesa STK Push?**
Similar UX (approve on your phone), different rails — STK Push is wallet-to-wallet/till; PBB is bank-account-to-bank-account (or bank-to-wallet, for Fund My Wallet).

## Technical

**What happens if the customer doesn't respond to a payment request?**
It expires automatically after up to 7 days and moves to a terminal `EXPR` state — no further action possible on that request; a new one must be submitted.

**Can a PBB payment be reversed once approved?**
No — not through Kenswitch. See [Legal & Compliance → Finality & Disputes](legal-compliance.md#finality-disputes-the-part-people-will-actually-ask-about).

## Commercial

_To be added once the Commercial team weighs in._

## Compliance

**What if a customer says they never approved a payment?**
Their bank investigates and resolves it — not Kenswitch. See [Legal & Compliance → Dispute Scenarios](legal-compliance.md#finality-disputes-the-part-people-will-actually-ask-about).
