---
layout: post
title: "Understanding Credit Card Product Types in Braintree"
description: ""
category: articles
modified: 2014-12-23
---

Every time you retrieve a transaction in Braintree, you'll get a credit card object with the attribute `product_id`. It tends to be pretty cryptic and only a few characters long.

    credit_card: {
        bin: "000000", 
        card_type: "Visa", 
        cardholder_name: "Chariot Customer", 
        commercial: "No",
        prepaid: "Yes",
        debit: "Yes",
        product_id: "MPX"
    }

As of this post, `product_id` isn't described anywhere in the Braintree documentation, but it effectively tells you which credit product the customer is using (e.g. a classic Visa card vs. a Signature Preferred, Student Card, Corporate Fleet, etc.). Each has a corresponding code.

There are lots of really useful ways to apply this info. You could use the product id to display a visual representation of the customer's card, or to figure out who your corporate buyers are and target them differently from the marketing side.

At [Chariot](https://www.chariotsf.com), we wanted to encourage our riders to take advantage of pre-tax transit benefits, usually via a prepaid debit card. These cards are issued by the employer and valid for any transit-related expense. The percentage of transactions made with this type of card is a great data point for us, because it's a proxy for how many of our customers use their benefits. Knowing whether a card's type is flex benefits can also help us provide better customer support. If a Chariot rider contacts us about a failed transaction, and the declined card was an MPX (employer-issued transit benefits), we'll give the customer a different set of advice than if they were trying to buy with a C (personal credit card).

The only problem? The `product_id` codes are useless if you don't know what they mean. I didn't see a full list available online, so I called up a couple of major payment processors and asked them for a description of each product code. The following codes are flex benefits cards: J3, MPV, and MPX. This list will be updated if I see anything missing:

- **A** Visa Traditional
- **AX1** American Express
- **B** Visa Traditional Rewards
- **C** Visa Signature
- **D** Visa Signature Preferred
- **D1** Discover
- **E–F** Reserved
- **G** Visa Business
- **G1** Visa Signature Business
- **G2** Visa Business Check Card
- **G3** Visa Business Enhanced
- **H** Visa Check Card
- **I** Reserved
- **J** Reserved
- **J1** Visa General Prepaid
- **J2** Visa Prepaid Gift
- **J3** Visa Prepaid Benefits
- **J4** Visa Prepaid Commercial
- **K** Visa Corporate
- **K1** Visa GSA Corporate T&E
- **L** Reserved
- **M** MasterCard/EuroCard
- **N–P** Reserved
- **Q** Private Label
- **Q1** Private Label Prepaid
- **R** Proprietary
- **S** Visa Purchasing
- **S1** Visa Purchasing with Fleet
- **S2** Visa GSA Purchasing
- **S3** Visa GSA Purchasing with Fleet
- **T** Reserved
- **U** Visa TravelMoney
- **V1** Reserved
- **W–Z** Reserved
- **O–9** Reserved
- **ACQ** Acquiring Only
- **CIR** Cirrus
- **DLG** Debit MasterCard Gold—Delayed Debit
- **DLH** Debit MasterCard World Embossed—Delayed Debit
- **DLI** Debit MasterCard Standard ISIC Student Card—Delayed Debit
- **DLS** Debit MasterCard Card—Delayed Debit
- **MAB** World Elite MasterCard Business
- **MAC** MasterCard Corporate World Elite
- **MBD** MasterCard Professional Debit Business Card
- **MBE** MasterCard Electronic Business Card
- **MBK** MasterCard Black
- **MCA** MasterCard Electronic Basic Card
- **MCB** MasterCard BusinessCard Card MasterCard Corporate Card
- **MCE** MasterCard Electronic Card
- **MCF** MasterCard Corporate Fleet Card
- **MCG** Gold MasterCard Card
- **MCH** MasterCard Premium Charge
- **MCM** MasterCard Corporate Meeting Card
- **MCO** MasterCard Corporate
- **MCP** MasterCard Corporate Purchasing Card
- **MCS** MasterCard Standard Card
- **MCT** Titanium MasterCard
- **MCU** MasterCard Unembossed
- **MCV** Merchant-Branded Program
- **MCW** World MasterCard Card
- **MDB** Debit MasterCard BusinessCard Card
- **MDG** Debit Gold MasterCard
- **MDH** World Debit Embossed
- **MDJ** Debit- Debit Other 2 Embossed
- **MDL** Business Debit Other Embossed
- **MDM** Middle Market Fleet Card
- **MDN** Middle Market Purchasing Card
- **MDO** Debit MasterCard Other
- **MDP** Debit MasterCard Platinum
- **MDQ** Middle Market Corporate Card
- **MDS** Debit MasterCard
- **MDT** MasterCard Business Debit
- **MDU** Debit MasterCard Unembossed
- **MEB** MasterCard Executive BusinessCard Card
- **MEC** MasterCard Electronic Commercial
- **MED** Debit MasterCard Electronic
- **MEF** MasterCard Electronic Payment Account
- **MEO** MasterCard Corporate Executive Card
- **MEP** Premium Debit MasterCard
- **MFB** Flex World Elite
- **MFD** Flex Platinum
- **MFE** Flex charge World Elite
- **MFH** Flex World
- **MFL** Flex Charge Platinum
- **MFW** Flex Charge World
- **MGF** MasterCard Government Commercial Card
- **MHA** MasterCard Healthcare Prepaid Non-tax
- **MHB** MasterCard HAS Substantiated
- **NHC** MasterCard Healthcare Credit Non-substantiated
- **MHH** MasterCard Unembossed Prepaid Student card
- **MIB** MasterCard Credit Electronic Student Card
- **MIC** MasterCard Credit Standard Student Card
- **MID** MasterCard Debit Unembossed Student Card
- **MIG** MasterCard Credit Umembossed Student Card
- **MIH** MasterCard Electronic Consumer Non U.S. Student Card
- **MIJ** MasterCard Debit Unembossed Non U.S. Student Card
- **MIK** MasterCard Electronic Consumer Prepaid Non U.S Student Card
- **MIL** MasterCard Unembossed Prepaid Non U.S Student Card
- **MIP** MasterCard Debit Prepaid Student Card
- **MIS** MasterCard Debit Standard Student Card
- **MIU** Debit MasterCard Unembossed Outside US
- **MLA** MasterCard Central Travel Solutions Air
- **MLC** MasterCard Micro-Business Card
- **MLD** MasterCard Distribution Card
- **MLL** MasterCard Central Travel Solutions Land
- **MNF** MasterCard Public Sector Commercial Card
- **MNW** World MasterCard Card (Europe)
- **MOW** World Maestro
- **MPA** Prepaid MasterCard Payroll Card
- **MPB** MasterCard Preferred BusinessCard
- **MPC** MasterCard Professional Card
- **MPF** Prepaid MasterCard Gift Card
- **MPG** Prepaid MasterCard Consumer Reloadable Card
- **MPJ** Prepaid Debit MasterCard Card Gold
- **MPK** Prepaid MasterCard Government Commercial Card
- **MPL** Platinum MasterCard Card
- **MPM** Prepaid MasterCard Consumer Promotion Card
- **MPN** Prepaid MasterCard Insurance Card
- **MPO** Prepaid MasterCard Other Card
- **MPR** Prepaid MasterCard Travel Card
- **MPT** Prepaid MasterCard Teen Card
- **MPV** Prepaid MasterCard Government Benefit Card
- **MPW** Prepaid MasterCard Corporate Card
- **MPX** Prepaid MasterCard Flex Benefit Card
- **MPY** Prepaid MasterCard Employee Incentive Card
- **MPZ** Prepaid MasterCard Emergency Assistance Card
- **MRB** Prepaid MasterCard Electronic BusinessCard
- **MRC** Prepaid MasterCard Electronic Card
- **MRF** Standard Deferred
- **MRG** Prepaid MasterCard Card Outside US
- **MRH** MasterCard Platinum Prepaid Travel Card
- **MRJ** Prepaid MasterCard Gold Card
- **MRL** Prepaid MasterCard Electronic Commercial
- **MRK** Prepaid MasterCard Public Sector Commercial Card
- **MRO** MasterCard Rewards Only
- **MRP** Standard Retailer Centric Payments
- **MRS** Prepaid MasterCard ISIC Student Card
- **MRW** Prepaid MasterCard BusinessCard Credit Outside US
- **MSD** Deferred Debit MasterCard
- **MUP** Premium Debit MasterCard Unembossed
- **MUS** Prepaid MasterCard Unembossed US
- **MUW** MasterCard World Domestic Affluent
- **MWB** World MasterCard for Business
- **MWD** World Deferred
- **MWE** MasterCard World Elite
- **MWO** MasterCard Corporate World
- **MWR** World Retailer Centric Payment
- **PVA** Private Label 1
- **PVB** Private Label 2
- **PVC** Private Label 3
- **PVD** Private Label 4
- **PVE** Private Label 5
- **PVF** Private Label 6
- **PVG** Private Label 7
- **PVH** Private Label 8
- **PVI** Private Label 9
- **PVJ** Private Label 10
- **SUR** Prepaid MasterCard Unembossed Outside US
- **TBE** Business—Immediate Debit
- **TCB** MasterCard Business Card — Immediate Debit
- **TCC** MasterCard (Mixed BIN) — Immediate Debit
- **TCE** MasterCard Electronic — Immediate Debit
- **TCF** MasterCard Fleet Card — Immediate Debit
- **TCG** Gold MasterCard Card — Immediate Debit
- **TCO** MasterCard Corporate — Immediate Debit
- **TCP** MasterCard Purchasing Card — Immediate Debit
- **TCS** MasterCard Standard Card — Immediate Debit
- **TCW** World Signia MasterCard Card — Immediate Debit
- **TDN** Middle Market MasterCard Purchasing Card — Immediate Debit
- **TEB** MasterCard Executive BusinessCard Card — Immediate Debit
- **TEC** MasterCard Electronic Commercial — Immediate Debit
- **TEO** MasterCard Corporate Executive Card — Immediate Debit
- **TIB** ISIC MasterCard Electronic Student Card — Immediate Debit
- **TIC** ISIC MasterCard Standard Student Card — Immediate Debit
- **TIU** MasterCard Unembossed — Immediate Debit
- **TLA** MasterCard Central Travel Solutions Air — Immediate Debit
- **TNF** MasterCard Public Sector Commercial Card — Immediate Debit
- **TNW** MasterCard New World — Immediate Debit
- **TPB** MasterCard Preferred Business Card — Immediate Debit
- **TPC** MasterCard Professional Card — Immediate Debit
- **TPL** Platinum MasterCard — Immediate Debit
- **VISA DEBIT** Visa Debit