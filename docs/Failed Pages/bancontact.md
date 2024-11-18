---
title: Bancontact
deprecated: false
hidden: false
metadata:
  robots: index
---
### Bancontact Deferred Sales

Bancontact Deferred Sales is a combined service that allows the card acceptor to perform an authorization for a temporary amount (reservation/pre-authorization) and a completion for the final amount within a limited time frame. This service is offered for use in the context of:

- Automated Fuel Dispensers
- Parking
- Electric Car Charging Stations
- Mass Transit, allowing Public Transport Operators to accept Bancontact payments through their ticket validators
- Click and Collect, allowing shops to process payments for pre-orders followed by collect or delivery services, where the final amount of the purchase can vary.

#### Maximum Interval Between Authorization and Completion Messages Based on MCC Code

| Timer Values                       | MCC Code                                                                                                                                                        | Duration       |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| MCC = 5542                         | Automated Fuel Dispensers                                                                                                                                       | Max 15 minutes |
| MCC = 5552                         | Electric Car Charging Stations                                                                                                                                  | Max 8 hours    |
| MCC = 4011, 4111, 4112, 4131, 4784 | Mass Transit related (Railroads, Local and suburban commuter passenger transportation, including ferries, Passenger railways, Bus lines, Tolls and bridge fees) | Max 24 hours   |
| MCC = 7523                         | Parking Lots and Garages                                                                                                                                        | Max 7 days     |
| MCC = 5411, 5432, 5499             | Groceries and Supermarkets, Click and Collect services, Miscellaneous Food Shops-Convenience Shops and Specialty retail outlets                                 | Max 8 days     |
| All other MCCs, except 6011        | Other categories                                                                                                                                                | Max 24 hours   |

<br />

#### Call Types

There are 3 different calls:

- Authorize
- CancelAuthorize
- Capture

The minimum transaction amount is 0.02 EUR.

#### Service and Transaction Details

[block:parameters]
{
  "data": {
    "h-0": "Service",
    "h-1": "Mode",
    "h-2": "Allowed MCC",
    "h-3": "Amount, Transaction",
    "0-0": "DeferredSales",
    "0-1": "Contact CVM",
    "0-2": "All, excluding 6011",
    "0-3": "If MCC = 5411, 5432 or 5499 then must be > 0.00 EUR and \\<= 325.00 EUR<br>Else If MCC = 5542 then must be > 0.00 EUR and \\<=375.00 EUR<br>Else If MCC = 5552 then must be > 0.00 EUR and \\<=60.00 EUR<br>Else If MCC = 7523 then must be > 0.00 EUR and \\<=170.00 EUR<br>Else If MCC = 4011, 4111, 4112, 4131 or 4784 then must be > 0.00 EUR and \\<= 30.00 EUR<br>Else must be > 0.00 EUR and \\<= 100.00 EUR",
    "1-0": "",
    "1-1": "Contact No CVM",
    "1-2": "4011, 4111, 4112, 4131, 4784, 7523",
    "1-3": "If MCC = 4011, 4111, 4112, 4131 or 4784 then must be > 0.00 EUR and \\<= 30.00 EUR<br>Else must be > 0.00 EUR and \\<= 50.00 EUR",
    "2-0": "",
    "2-1": "Contactless CVM",
    "2-2": "All, excluding 6011",
    "2-3": "Same as for Contact CVM",
    "3-0": "",
    "3-1": "Contactless no CVM",
    "3-2": "All, excluding 6011",
    "3-3": "If MCC = 4011, 4111, 4112, 4131 or 4784 then must be >0.00 EUR and \\<= 30.00 EUR<br>Else must be > 0.00 EUR and \\<= 50.00 EUR",
    "4-0": "",
    "4-1": "E-Commerce QR Code",
    "4-2": "All, excluding 6011",
    "4-3": "If MCC = 5411, 5432 or 5499 then must be > 0.00 EUR and\\<= 325.00 EUR<br>Else If MCC = 5542 then must be > 0.00 EUR and \\<=375.00 EUR<br>Else If MCC = 5552 then must be > 0.00 EUR and \\<=60.00 EUR<br>Else If MCC = 7523 then must be > 0.00 EUR and \\<=170.00 EUR<br>Else If MCC = 4011, 4111, 4112, 4131 or 4784 be > 0.00 EUR and \\<= 30.00 EUR<br>Else must be > 0.00 EUR and \\<= 100.00 EUR",
    "5-0": "",
    "5-1": "E-Commerce URL-Intent",
    "5-2": "All, excluding 6011",
    "5-3": "Same as for E-Commerce QR Code",
    "6-0": "",
    "6-1": "(RFU)E-Commerce NFC/RF/Tel",
    "6-2": "All, excluding 6011",
    "6-3": "Same as for E-Commerce QR Code",
    "7-0": "",
    "7-1": "E-Commerce Manual PAN Entry",
    "7-2": "All, excluding 6011",
    "7-3": "If MCC = 5411, 5432 or 5499 then must be > 0.00 EUR and\\<= 325.00 EUR<br>Else If MCC = 5552 then must be > 0.00 EUR and \\<=60.00 EUR<br>Else If MCC = 5542 then must be > 0.00 EUR and \\<=375.00 EUR<br>Else If MCC = 7523 then must be > 0.00 EUR and \\<=170.00 EUR<br>Else If MCC = 4011, 4111, 4112, 4131 or 4784 be > 0.00 EUR and \\<= 30.00 EUR<br>Else must be > 0.00 EUR and \\<= 100.00 EUR",
    "8-0": "",
    "8-1": "E-Commerce PAN From Server",
    "8-2": "All, excluding 6011",
    "8-3": "Same as for E-Commerce Manual PAN Entry",
    "9-0": "",
    "9-1": "E-Commerce Wallet Initiated",
    "9-2": "All, excluding 6011",
    "9-3": "Same as for E-Commerce QR Code"
  },
  "cols": 4,
  "rows": 10,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]


<br />

#### MCC Values Defined

- **Mass Transit related**
  - 4011: Railroads
  - 4111: Local and suburban commuter passenger transportation, including ferries
  - 4112: Passenger railways
  - 4131: Bus lines
  - 4784: Tolls and bridge fees

- **Click and Collect related**
  - 5411: Groceries and Supermarkets
  - 5432: Click and Collect services
  - 5499: Miscellaneous Food Shops-Convenience Shops and Specialty retail outlets

- **Automated Fuel Dispenser related**
  - 5542: Automated Fuel Dispensers

- **Electric Car Charging Station related**
  - 5552: Electric Car Charging Stations

- **Parking related**
  - 7523: Parking Lots and Garages