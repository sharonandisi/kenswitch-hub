# Glossary

Shared terms that show up across multiple Kenswitch products. Defined once here, linked everywhere else — so the definition never drifts between product pages.

**Issuer**
: Your bank. Approves or declines a payment request, and owns the authentication of you as the customer (PIN, biometric, OTP, etc.).

**Acquirer**
: The merchant's or wallet's bank or PSP. Onboards and vets the merchant, and submits payment requests on the merchant's behalf.

**RtP (Request-to-Pay)**
: A payment model where the transaction starts as a *request* that the payer must actively approve — as opposed to a *push* (like a card swipe) or a *pull* (like a direct debit).

**KEPSS**
: The Central Bank of Kenya's Electronic Payment and Settlement System — Kenya's real-time gross settlement rail. This is where money actually moves between banks; Kenswitch's products route and validate the messages that trigger it.

**ISO 20022**
: An international standard format for financial messaging. Kenswitch's Issuer-facing integrations (e.g. PBB) use this; Acquirer-facing integrations typically use REST/JSON instead, with Kenswitch translating between the two.

**Switching / Switch**
: The core function Kenswitch performs — routing and validating payment messages between financial institutions so they don't need one-off bilateral integrations with each other.

**Settlement**
: The actual discharge of financial obligations between institutions — as opposed to *messaging*, which is just the request/response traffic. Kenswitch handles messaging; KEPSS handles settlement.

*(This glossary grows as new products are added to the hub — if a term shows up on more than one product page, it belongs here, not repeated on each page.)*
