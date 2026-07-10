# Getting Started

## What is PBB?

**Pay by Bank (PBB)** is a way to pay directly from your bank account — no card needed. You (the customer) get a request on your banking app asking "do you want to pay this merchant/wallet KES X?", you approve it with your PIN or biometric, and the money moves straight from your bank account to the receiver. Kenswitch is the plumbing in the middle that makes sure that request gets from the merchant to your bank, and the approval gets back, safely and instantly.

Technically, it's called a **Request-to-Pay (RtP)** framework — the payment starts with a *request* (from the merchant/wallet), not a *push* (like a card swipe) or a *pull* (like a direct debit). Nothing moves until you, the account holder, say yes.

## What problem does it solve?

Card payments in Kenya route through international card networks and cost merchants a percentage fee on every transaction. PBB moves money bank-to-bank instead, over Kenswitch's own switching rails, settled via the Central Bank of Kenya's RTGS system (KEPSS). For merchants: cheaper. For the ecosystem: less dependence on card rails, and it keeps switching revenue and payment data inside Kenya's own infrastructure rather than flowing through Visa/Mastercard.

## What's out there already

So you know where PBB sits relative to alternatives:

- **Cards** (Visa/Mastercard rails) — the incumbent, what PBB is positioned to reduce reliance on
- **M-Pesa STK Push** — similar "approve a request" UX, but wallet-to-wallet/wallet-to-till, not bank-account-to-bank-account
- **PBB** — same "approve on your phone" feel as STK Push, but it's your *bank account* talking to another *bank account* (or a wallet, in the Fund My Wallet use case), routed through Kenswitch instead of Safaricom's wallet rails

## What Kenswitch actually does (and doesn't do)

Kenswitch runs the message routing and validation in the middle — it's the switch, not a bank. It does **not** hold your money, does not guarantee your bank will approve the request, and does not take on settlement risk. Your bank (the **Issuer**) makes the actual approve/reject call and is on the hook for authenticating you. The merchant's bank or PSP (the **Acquirer**) is responsible for onboarding and vetting the merchant. Kenswitch just makes sure the request and response get where they need to go, correctly and on the record.

## Two use cases running on this same core rail today

- **Lipa na Bank** — merchant checkout (you pay a shop/biller)
- **Fund My Wallet** — wallet top-up (you fund your M-Pesa wallet from your bank account)

Same API, same rulebook, same flow underneath — just relabeled for who's on the receiving end. See [Use Cases](use-cases.md) for the full picture, including transaction types already supported but not yet built out.

!!! tip "New terms?"
    Check the [Glossary](../../glossary/index.md) for Issuer, Acquirer, RtP, and KEPSS.
