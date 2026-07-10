# Legal, Risk & Compliance

## What Kenswitch Is (and Isn't), Legally

Kenswitch is classified as a **messaging and switching infrastructure provider** — not an e-money issuer, not a merchant acquirer, not a deposit-taker, and not a party (principal) to any transaction. In plain terms: Kenswitch never touches, holds, or guarantees anyone's money. It routes and validates payment messages between banks and PSPs, full stop.

## Regulatory Framework

Governed primarily by the National Payment Systems Act and CBK directives, POCAMLA (AML/CFT law), and the Data Protection Act. Each participating institution remains independently responsible for its own regulatory compliance — Kenswitch doesn't absorb anyone's regulatory obligations by routing their messages.

## Risk Allocation — Who Owns What

| Risk | Who's responsible |
|---|---|
| Customer authentication (was it really you approving?) | **Issuer** (your bank) |
| Merchant fraud | **Acquirer/PSP** |
| Duplicate submission | **Acquirer** (though Kenswitch's idempotency controls catch most of this automatically) |
| Wrong amount submitted | **Acquirer** |
| System outage | Whichever participant's system went down |
| AML breach | The institution that originated the transaction |
| Settlement shortfall | The bank that owes the net obligation |

Kenswitch never assumes credit, fraud, or settlement risk on anyone's behalf — it facilitates the message flow and clearing coordination, nothing more.

## Finality & Disputes — the part people will actually ask about

**Core rule: once you approve a PBB request, it's final. There is no chargeback.** This isn't a gap — it's deliberate. PBB isn't a card scheme and doesn't carry card-style reversal rights. Here's what actually happens instead, by scenario:

| If this happens... | Who handles it | How |
|---|---|---|
| Customer says "I never approved that" | **Issuer** | Bank investigates its own authentication logs (OTP, biometric, device, session data). If fraud is confirmed, the *bank* refunds the customer under its own fraud policy — not Kenswitch. |
| Same request submitted twice by mistake | **Kenswitch (automatically)** | Idempotency controls reject the duplicate outright — no manual dispute needed. |
| Wrong amount charged | **Acquirer/Merchant** | Merchant issues a refund as a new, separate transaction. The original can't be edited or reversed. |
| Customer paid but merchant didn't deliver | **Merchant, off-platform** | Commercial dispute between customer and merchant — Kenswitch has no role and no liability. |
| A PSP is submitting fraudulent/abusive requests | **Kenswitch escalation** | Immediate suspension of that PSP's access, escalation to the AML/Compliance Committee, CBK notification if warranted. |

!!! note "The one-line answer for frontline/support staff"
    Once you've approved a PBB payment, Kenswitch can't reverse it — any fix has to come from a fresh refund initiated by the merchant, or a fraud investigation by your bank if you didn't actually approve it.

## KYC / AML Obligations

- **Issuer** does customer KYC and ongoing due diligence.
- **Acquirer** does merchant KYC and monitors for lawful merchant activity.
- Each institution independently handles suspicious transaction reporting (STR) and sanctions screening — Kenswitch doesn't do KYC on anyone.

## Suspension Triggers

An institution can be suspended from the scheme for: repeated fraudulent claims, systemic duplicate submissions, AML breaches, regulatory violations, or settlement default.

## Settlement Legal Status

Settlement runs once daily through KEPSS on a **multilateral net basis** (positions are netted across all participants, not settled transaction-by-transaction). Once KEPSS settles a cycle, that's final and irrevocable — there's no undo at that layer either.

## Data Protection

Governed by Kenya's Data Protection Act.

!!! question "Open question — needs Legal"
    What specific data crosses the switch (full payer details? just identifiers?), and under what lawful basis? Not addressed in the current rulebook.

## Open Questions / Needs Legal Review

- [ ] Data protection basis for data flowing through the switch
- [ ] Has a suspension ever actually been triggered? Any case study worth documenting?
- [ ] Finance Act 2026 WHT exposure question (cross-reference KRA workstream)
