---
title: Bancontact
deprecated: false
hidden: false
metadata:
  robots: index
---
### Bancontact Deferred Sales

Bancontact Deferred Sales is a combined service that allows the card acceptor to perform an authorization for a temporary amount (reservation/pre-authorization) and a completion for the final amount within a limited time frame. This service is offered for use in the context of:

* Automated Fuel Dispensers
* Parking
* Electric Car Charging Stations
* Mass Transit, allowing Public Transport Operators to accept Bancontact payments through their ticket validators
* Click and Collect, allowing shops to process payments for pre-orders followed by collect or delivery services, where the final amount of the purchase can vary.

#### Maximum Interval Between Authorization and Completion Messages Based on MCC Code

| Timer Values                       | MCC Code                                                                                                                                                        | Duration       |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| MCC \= 5542                         | Automated Fuel Dispensers                                                                                                                                       | Max 15 minutes |
| MCC \= 5552                         | Electric Car Charging Stations                                                                                                                                  | Max 8 hours    |
| MCC \= 4011, 4111, 4112, 4131, 4784 | Mass Transit related (Railroads, Local and suburban commuter passenger transportation, including ferries, Passenger railways, Bus lines, Tolls and bridge fees) | Max 24 hours   |
| MCC \= 7523                         | Parking Lots and Garages                                                                                                                                        | Max 7 days     |
| MCC \= 5411, 5432, 5499             | Groceries and Supermarkets, Click and Collect services, Miscellaneous Food Shops-Convenience Shops and Specialty retail outlets                                 | Max 8 days     |
| All other MCCs, except 6011        | Other categories                                                                                                                                                | Max 24 hours   |

<br />

#### Call Types

There are 3 different calls:

* Authorize
* CancelAuthorize
* Capture

The minimum transaction amount is 0.02 EUR.

#### Service and Transaction Details

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Service
      </th>

      <th style={{ textAlign: "left" }}>
        Mode
      </th>

      <th style={{ textAlign: "left" }}>
        Allowed MCC
      </th>

      <th style={{ textAlign: "left" }}>
        Amount, Transaction
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        DeferredSales
      </td>

      <td style={{ textAlign: "left" }}>
        Contact CVM
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        If MCC \= 5411, 5432 or 5499 then must be \> 0.00 EUR and \<\= 325.00 EUR  
        Else If MCC \= 5542 then must be \> 0.00 EUR and \<\=375.00 EUR
        Else If MCC \= 5552 then must be \> 0.00 EUR and \<\=60.00 EUR
        Else If MCC \= 7523 then must be \> 0.00 EUR and \<\=170.00 EUR
        Else If MCC \= 4011, 4111, 4112, 4131 or 4784 then must be \> 0.00 EUR and \<\= 30.00 EUR
        Else must be > 0.00 EUR and \<\= 100.00 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        Contact No CVM
      </td>

      <td style={{ textAlign: "left" }}>
        4011, 4111, 4112, 4131, 4784, 7523
      </td>

      <td style={{ textAlign: "left" }}>
        If MCC \= 4011, 4111, 4112, 4131 or 4784 then must be \> 0.00 EUR and \<\= 30.00 EUR  
        Else must be \> 0.00 EUR and \<\= 50.00 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        Contactless CVM
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        Same as for Contact CVM
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        Contactless no CVM
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        If MCC \= 4011, 4111, 4112, 4131 or 4784 then must be \> 0.00 EUR and \<\= 30.00 EUR  
        Else must be \> 0.00 EUR and \<\= 50.00 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        E-Commerce QR Code
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        If MCC \= 5411, 5432 or 5499 then must be \> 0.00 EUR and\<\= 325.00 EUR  
        Else If MCC \= 5542 then must be \> 0.00 EUR and \<\=375.00 EUR
        Else If MCC \= 5552 then must be \> 0.00 EUR and \<\=60.00 EUR
        Else If MCC \= 7523 then must be \> 0.00 EUR and \<\=170.00 EUR
        Else If MCC \= 4011, 4111, 4112, 4131 or 4784 be \> 0.00 EUR and \<\= 30.00 EUR
        Else must be > 0.00 EUR and \<\= 100.00 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        E-Commerce URL-Intent
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        Same as for E-Commerce QR Code
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        (RFU)E-Commerce NFC/RF/Tel
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        Same as for E-Commerce QR Code
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        E-Commerce Manual PAN Entry
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        If MCC \= 5411, 5432 or 5499 then must be \> 0.00 EUR and\<\= 325.00 EUR  
        Else If MCC \= 5552 then must be \> 0.00 EUR and \<\=60.00 EUR
        Else If MCC \= 5542 then must be \> 0.00 EUR and \<\=375.00 EUR
        Else If MCC \= 7523 then must be \> 0.00 EUR and \<\=170.00 EUR
        Else If MCC \= 4011, 4111, 4112, 4131 or 4784 be \> 0.00 EUR and \<\= 30.00 EUR
        Else must be \> 0.00 EUR and \<\= 100.00 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        E-Commerce PAN From Server
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        Same as for E-Commerce Manual PAN Entry
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        E-Commerce Wallet Initiated
      </td>

      <td style={{ textAlign: "left" }}>
        All, excluding 6011
      </td>

      <td style={{ textAlign: "left" }}>
        Same as for E-Commerce QR Code
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />

#### MCC Values Defined

* **Mass Transit related**
  * 4011: Railroads
  * 4111: Local and suburban commuter passenger transportation, including ferries
  * 4112: Passenger railways
  * 4131: Bus lines
  * 4784: Tolls and bridge fees

* **Click and Collect related**
  * 5411: Groceries and Supermarkets
  * 5432: Click and Collect services
  * 5499: Miscellaneous Food Shops-Convenience Shops and Specialty retail outlets

* **Automated Fuel Dispenser related**
  * 5542: Automated Fuel Dispensers

* **Electric Car Charging Station related**
  * 5552: Electric Car Charging Stations

* **Parking related**
  * 7523: Parking Lots and Garages