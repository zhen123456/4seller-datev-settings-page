# 4Seller DATEV Erlösexport Settings Fields

This document lists each setting field in `4seller_datev_settings_page.html` as an implementation reference.

## 1. Allgemeines

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| DATEV Beraternummer | Yes | Numeric text, max 7 digits | Tax advisor number written into the DATEV file header. | Must match the accountant's DATEV advisor number. Validate numeric length before export. |
| Mandantennummer | Yes | Numeric text, max 5 digits | DATEV client/company number. | Must match the client master data in DATEV. Validate numeric length before export. |
| Länge Sachkontennummern | Yes | Select: 4-8 | Length of ledger account numbers. | Use this to validate revenue accounts, debtor accounts and clearing accounts. |
| Export Format | Yes | Select | Technical export format. | Current scope is `DATEV Format (CSV)`. Keep extensible if more formats are added later. |
| Beginn des Wirtschaftsjahres Tag | Yes | Select | Fiscal year start day. | Used together with month to validate the export period. |
| Monat | Yes | Select | Fiscal year start month. | Used together with start day to avoid mixing bookings from different fiscal years. |

## 2. Erlöskonten Volle Umsatzsteuer

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Yes | Select or fallback row | Country rule for full VAT revenue account mapping. | `Alle anderen Länder` is the fallback if no country-specific rule matches. |
| Konto | Yes | Numeric account, max 8 digits | DATEV revenue account for sales with full VAT. | Example SKR03 account: `8400`. Validate by account length setting. |
| + | Optional | Action | Adds another country-specific account rule. | New rows should not duplicate the same country in the same section. |

## 3. Erlöskonten Ermäßigte Umsatzsteuer

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Yes | Select or fallback row | Country rule for reduced VAT revenue account mapping. | `Alle anderen Länder` is the fallback rule. |
| Konto | Yes | Numeric account, max 8 digits | DATEV revenue account for reduced-rate sales. | Used when order item tax rate is reduced. |
| + | Optional | Action | Adds another country-specific reduced VAT account. | Prevent duplicate country rows. |

## 4. Erlöskonten Digitale Artikel

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Yes | Select or fallback row | Country rule for digital goods and electronically supplied services. | Required because digital goods may follow destination-country tax logic. |
| Konto | Yes | Numeric account, max 8 digits | DATEV revenue account for digital article revenue. | Validate by account length setting. |
| Steuerschlüssel | Optional | Numeric tax key, max 3 digits | DATEV tax key for the mapped tax treatment. | Use only when tax treatment cannot be derived from the account alone or accountant requires it. |
| + | Optional | Action | Adds another country-specific digital goods rule. | Prevent duplicate country rows. |

## 5. Erlöskonten Für Im Inland Nicht Steuerbare Umsätze

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Optional | Select or fallback row | Country rule for sales that are not taxable in Germany. | Section is optional; only export with this mapping if configured. |
| Konto | Optional | Numeric account, max 8 digits | Revenue account for domestic non-taxable sales. | If empty, this specific booking case should not use this section. |
| Steuerschlüssel | Optional | Numeric tax key, max 3 digits | DATEV tax key for non-taxable case. | Accountant-dependent. |
| + | Optional | Action | Adds another country rule. | Prevent duplicate country rows. |

## 6. Erlöskonten Für Im Inland Nicht Steuerbare Umsätze, Ermäßigter Steuersatz

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Optional | Select or fallback row | Country rule for non-taxable sales with reduced-rate item logic. | Section is optional. |
| Konto | Optional | Numeric account, max 8 digits | Revenue account for reduced-rate non-taxable case. | Use only if configured. |
| Steuerschlüssel | Optional | Numeric tax key, max 3 digits | DATEV tax key for reduced-rate non-taxable case. | Accountant-dependent. |
| + | Optional | Action | Adds another country rule. | Prevent duplicate country rows. |

## 7. Erlöskonten Steuerfreie Umsätze Drittland

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Optional | Select or fallback row | Country rule for tax-free sales to third countries outside the EU. | Section is optional. |
| Konto | Optional | Numeric account, max 8 digits | DATEV revenue account for tax-free third-country sales. | Use only if configured. |
| + | Optional | Action | Adds a country-specific third-country account. | Prevent duplicate country rows. |

## 8. Erlöskonten OSS Fernverkäufe

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Optional | Select or fallback row | EU destination country for OSS distance sales. | Section is optional; relevant for OSS reporting logic. |
| Konto | Optional | Numeric account, max 8 digits | Revenue account for OSS sales at standard VAT rate. | Use when OSS rule and standard VAT rate match. |
| Steuerschlüssel | Optional | Numeric tax key, max 3 digits | DATEV tax key for destination-country VAT treatment. | Accountant-dependent. |
| + | Optional | Action | Adds another country-specific OSS rule. | Prevent duplicate country rows. |

## 9. Erlöskonten OSS Fernverkäufe, Ermäßigter Steuersatz

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Land | Optional | Select or fallback row | EU destination country for reduced-rate OSS distance sales. | Section is optional. |
| Konto | Optional | Numeric account, max 8 digits | Revenue account for OSS sales at reduced VAT rate. | Use when OSS rule and reduced VAT rate match. |
| Steuerschlüssel | Optional | Numeric tax key, max 3 digits | DATEV tax key for reduced destination-country VAT treatment. | Accountant-dependent. |
| + | Optional | Action | Adds another country-specific reduced OSS rule. | Prevent duplicate country rows. |

## 10. Sonstige Erlöskonten

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Erlöskonto Kleinunternehmer | Optional | Numeric account, max 8 digits | Revenue account used when the company is treated as a small business and invoices do not show VAT. | Use only if small-business taxation is enabled for the seller. |
| Erlöskonto keine Umsatzsteuer | Optional | Numeric account, max 8 digits | Fallback revenue account for orders where no VAT is booked and no more specific case matches. | Helps avoid export errors for zero-VAT orders. |
| Erlöskonto steuerfreie innergemeinschaftliche Umsätze | Optional | Numeric account, max 8 digits | Revenue account for tax-free intra-community B2B sales within the EU. | Requires tax logic to identify intra-community tax-free sales. |
| Erlöskonto Differenzbesteuerung | Optional | Numeric account, max 8 digits | Revenue account for margin scheme taxation. | Only used when order is marked as margin-scheme taxable. |

## 11. Debitorkonten

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Modus | Yes | Select: Sammelkonto, Kundennummer | Controls how debtor contra accounts are created. | `Sammelkonto` means all customer receivables use one account; `Kundennummer` means customer-number based debtor accounts. |
| Debitoren Sammelkonto | Conditional | Numeric account, max 8 digits | Collective debtor account used as contra account when mode is `Sammelkonto`. | Required when `Modus = Sammelkonto`. Usually appears opposite the revenue account. |

## 12. Sammelkonten Pro Zahlart

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Zahlart | Optional | Select or text | Payment method from order or payment transaction. | Examples: PayPal, Banküberweisung. |
| Konto | Optional | Numeric account, max 8 digits | Clearing account for the payment method. | Use when payment-specific collection accounts are needed. |
| + | Optional | Action | Adds another payment-method account rule. | Prevent duplicate payment method rows. |

## 13. Sonstiges / Belegtexte

| Field | Required | Input | Meaning | Development notes |
|---|---:|---|---|---|
| Umsatzkontonummern pro Shop erhöhen | Optional | Numeric offset, max 4 digits | Adds a shop-specific offset to revenue account numbers. | Example: base account `8400` plus offset `2` can separate revenue by shop. Confirm exact offset rule with accounting. |
| Debitorenkontonummern pro Shop erhöhen | Optional | Numeric offset, max 4 digits | Adds a shop-specific offset to debtor account numbers. | Use when debtor accounts must be separated by shop. |
| Eigenschaft Belegdatum | Yes | Select: Bestelldatum, Zahldatum, Rechnungsdatum, Versanddatum | Chooses which order date is exported as DATEV `Belegdatum`. | This affects the accounting period and must align with accountant expectations. |
| Belegtext | Optional | Template text with placeholders | DATEV voucher text column. | Exported as one text value built from fixed text and placeholders. |
| Belegfeld 1 | Optional | Template text with placeholders | DATEV voucher field 1. | Usually invoice number, external order number or primary document reference. |
| Belegfeld 2 | Optional | Template text with placeholders | DATEV voucher field 2. | Usually shop name, shipping date or secondary reference. |

## 14. Placeholder Variables

| Placeholder | Meaning | Typical use |
|---|---|---|
| `{BuyerName}` | Buyer name | Belegtext |
| `{CustomerNumber}` | Customer number | Debtor or voucher reference |
| `{InvoiceNumber}` | Invoice number | Belegfeld 1 |
| `{OrderDate}` | Order date | Belegtext |
| `{OrderRef}` | External order number | Belegtext or Belegfeld 1 |
| `{PaymentTransactionId}` | Payment transaction ID | Belegtext or audit reference |
| `{Platform}` | Sales platform | Belegtext |
| `{ShipDate}` | Shipping date | Belegfeld 2 |
| `{ShopName}` | Shop name | Belegfeld 2 |
| `{TotalSum}` | Gross or total order amount | Belegtext when amount should be visible in text |

## Implementation Rules

- Required fields must be validated before export.
- Optional account sections should only be used when account values are configured.
- Account inputs should respect `Länge Sachkontennummern`.
- `Steuerschlüssel` should be numeric and limited to 3 digits.
- Country-specific rules should override `Alle anderen Länder`.
- Template fields should remain plain text values; variable chips are input guidance only.
- DATEV/Billbee German field names should be preserved in the data model where they map directly to accounting concepts.
