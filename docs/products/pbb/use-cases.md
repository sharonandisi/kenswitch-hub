# Use Cases

PBB is one core rail, powered by a single API endpoint (`POST /api/v1/pbb/request`). A single field — `payee.tranType` — determines which use case a given request represents. Everything below is the same request → route → approve → settle flow; only the labels and the receiving end change.

## 1. Lipa na Bank — merchant checkout
`tranType: MERCHANT_PAYMENT`

You're paying a shop, biller, or online merchant directly from your bank account instead of tapping a card. The merchant's Acquirer submits the request with merchant metadata (MCC, display name, location); your Issuer presents it as "Pay [Merchant Name] KES X."

## 2. Fund My Wallet — wallet top-up
`tranType: WALLET_FUNDING`

You're moving money from your bank account into your M-Pesa wallet. Same flow, but the "payee" side is M-Pesa's wallet system rather than a merchant, and the request reads as "Fund your M-Pesa wallet with KES X" on your banking app.

## 3–5. Supported by the API, not yet built out

- `BILL_PAYMENT` — paying a biller (utility, school fees, etc.) directly from your bank
- `ACCOUNT_TRANSFER` — bank-to-bank transfer initiated via request-to-pay
- `SACCO_CONTRIBUTION` — paying into a SACCO account

!!! question "Open question"
    These three transaction types are already accepted by the API but have no integration guide or partner-facing documentation yet. Worth a roadmap conversation — intentionally dormant, planned, or simply unbuilt?
