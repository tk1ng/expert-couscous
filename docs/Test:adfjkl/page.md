---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
With Belvo's Open Finance Data Aggregation (OFDA) product for Brazil, you can retrieve the account information for a link.

`<Ofdaaccountsdataimage />`

For each account that the user has, you receive:

* Core information about the account (category, type, number, currency).
* Balance and overdraft information
* In the case that the account is a credit card account, detailed information regarding the credit limits and cards.
* In the case that the account is a loan-type account, detailed information regarding the loan amount, repayment schedule, interest rates, and more. 

# Core information

```json Account (OFDA) Core Information
{
  "id": "0d3ffb69-f83b-456e-ad8e-208d0998d71d",
  "link": "30cb4806-6e00-48a4-91c9-ca55968576c8",
  "created_at": "2022-02-09T08:45:50.406032Z",
  "collected_at": "2019-09-27T13:01:41.941Z",
  "last_accessed_at": "2021-03-09T10:28:40.000Z",
  "category": "CHECKING_ACCOUNT",
  "balance_type": "ASSET",
  "currency": "BRL",
  "name": null,
  "type": "CONTA_DEPOSITO_A_VISTA",
  "subtype": "INDIVIDUAL",
  "number": "11188222",
  "agency": "6272",
  "check_digit": "4",
  "public_identification_name": "AGENCY/NUMBER",
  "public_identification_value": "6272/11188222",
  "internal_identification": "92792126019929279212650822221989319252576",
  "institution": {
    "name": "ofmockbank_br_retail",
    "type": "bank"
  },
  "balance": {}, // See the specific balance section below
  "overdraft": {}, // See the specific overdraft section below
  "credit_data": {}, // See the specific credit_data section below
  "loan_data": {} // See the specific loan_data section below
}

```

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        id
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Belvo's unique identifier for the current item.
      </td>

      <td style={{ textAlign: "left" }}>
        0d3ffb69-f83b-456e-ad8e-208d0998d71d
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        link
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The `link.id` the data belongs to.
      </td>

      <td style={{ textAlign: "left" }}>
        30cb4806-6e00-48a4-91c9-ca55968576c8
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        created\_at
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date-time)
      </td>

      <td style={{ textAlign: "left" }}>
        The ISO-8601 timestamp of when the data point was created in Belvo's database.
      </td>

      <td style={{ textAlign: "left" }}>
        2022-02-09T08:45:50.406032Z
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        collected\_at
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date-time)
      </td>

      <td style={{ textAlign: "left" }}>
        The ISO-8601 timestamp when the data point was collected.
      </td>

      <td style={{ textAlign: "left" }}>
        2019-09-27T13:01:41.941Z
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        last\_accessed\_at
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date-time)
      </td>

      <td style={{ textAlign: "left" }}>
        The ISO-8601 timestamp when Belvo last accessed the account.
      </td>

      <td style={{ textAlign: "left" }}>
        2021-03-09T10:28:40.000Z
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        category
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of account.\
        We return one of the following enum values: `ADVANCE_DEPOSIT_ACCOUNT`, `CHECKING_ACCOUNT`, `CREDIT_CARD`, `FINANCING_ACCOUNT`, `INVESTMENT_ACCOUNT`, `INVOICE_FINANCING_ACCOUNT`, `LOAN_ACCOUNT`, `PENSION_FUND_ACCOUNT`, `SAVINGS_ACCOUNT`, or `UNCATEGORIZED`
      </td>

      <td style={{ textAlign: "left" }}>
        CHECKING\_ACCOUNT
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The account type, as designated by the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        CONTA\_DEPOSITO\_A\_VISTA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subtype
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The account subtype, as designated by the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        INDIVIDUAL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The account name, as given by the institution.
      </td>

      <td style={{ textAlign: "left" }}>
        CONTA\_DEPOSITO\_A\_VISTA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The account number, as designated by the institution.
      </td>

      <td style={{ textAlign: "left" }}>
        4057068115181
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        agency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The branch code where the product was opened.
      </td>

      <td style={{ textAlign: "left" }}>
        6272
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        check\_digit
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The check digit of the product's number, if applicable.
      </td>

      <td style={{ textAlign: "left" }}>
        7
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        clearing\_code
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The clearing code for the account.
      </td>

      <td style={{ textAlign: "left" }}>
        1
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        currency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The three-letter currency code (ISO-4217).  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `balances` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        BRL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        public\_identification\_name
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The public name for the type of identification. For 🇧🇷 Brazilian savings and checking accounts, this field will be `AGENCY/ACCOUNT`.
      </td>

      <td style={{ textAlign: "left" }}>
        AGENCY/ACCOUNT
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        public\_identification\_vale
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The value for the `public_identification_name`.  

        For 🇧🇷 OFDA Brazilian savings and checking accounts, this field will be the agency and bank account number, separated by a slash. For example: `0444/45722-0`.  

        For 🇧🇷 OFDA Brazilian credit card accounts, we will return a string of concatenated credit card numbers associated with the account. For example: "8763,9076,5522"
      </td>

      <td style={{ textAlign: "left" }}>
        6272/24550245
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        internal\_identification
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The institution's internal identification for the account.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `balances` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        92792126019929279212650822221989319252576
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        balance\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Indicates whether this account is either an `ASSET` or a `LIABILITY`. You can consider the balance of an `ASSET` as being positive, while the balance of a `LIABILITY` as negative.
      </td>

      <td style={{ textAlign: "left" }}>
        ASSET
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        balance
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding the current and available balances for the account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [balance section for details](https://developers.belvo.com/docs/accounts-ofda-data#balance).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        overdraft
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding any overdraft limits the user has with the institution for this account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [overdraft section for details](https://developers.belvo.com/docs/accounts-ofda-data#overdraft).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        credit\_data
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding the credit cards associated with this account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [credit\_data section for details](https://developers.belvo.com/docs/accounts-ofda-data#credit_data).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        loan\_data
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>

      <td style={{ textAlign: "left" }}>
        The loan options associated with this account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [loan\_data section for details](https://developers.belvo.com/docs/accounts-ofda-data#loan_data).
      </td>
    </tr>
  </tbody>
</Table>

# balance

In the `balance` object, we provide you with the information regarding the account's balances. 

```json balance
{
  "balance": {
    "current": 5874.13,
    "available": 5621.12,
    "blocked": 60.32,
    "automatically_invested": 131.5
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        current
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The current balance is calculated differently according to the type of account.\*
      </td>

      <td style={{ textAlign: "left" }}>
        5874.13
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        available
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The balance that the account owner can use. \*
      </td>

      <td style={{ textAlign: "left" }}>
        5621.12
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        blocked
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The amount that is currently blocked due to pending transactions.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `balances` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        60.32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        automatically\_invested
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The amount that is automatically invested (as agreed upon with the institution).  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `balances` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        131.5
      </td>
    </tr>
  </tbody>
</Table>

\* Please note that for the `current` and `available` fields, the values returned for checking, credit card, or loan accounts depend on the account type:

| Parameter | Checking or Savings                                                                          | Credit Cards                                                           | Loan Account                                                                                                                                               |
| :-------- | :------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| current   | The user's account balances as of the `collected_at` timestamp.                              | The amount the user has spent in the current card billing period.      | The amount remaining to pay on the users's loan.                                                                                                           |
| available | The available balance may be different to the `current` balance due to pending transactions. | The credit amount the user still has available for the current period. | The present value required to pay off the loan, as provided by the institution.**Note:** If the institution does not provide this value, we return `null`. |

<br />

# overdraft

In the `overdraft` object, you can see what limits have been agreed with the bank (`arranged`), how much the user has already used (`used`), and whether or not the user has gone over their limit without agreeing with the bank (`unarranged`).

```json overdraft
{
  "overdraft": {
    "arranged": 5000.5,
    "used": 1000.5,
    "unarranged": 300.1
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        arranged
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The agreed upon overdraft limit between the account holder and the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `overdraft` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        5000.5
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        used
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The overdraft value used.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `overdraft` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        1000.5
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        unarranged
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The overdraft used that was not arranged between the account holder and the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `overdraft` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        300.1
      </td>
    </tr>
  </tbody>
</Table>

<br />

# credit\_data

<div style={{ backgroundColor: "#FCF8F2", borderLeft: "5px solid #F0AD4E", padding: "20px", borderRadius: "10px", fontFamily: "Arial, sans-serif", lineHeight: "1", margin: "20px 0" }}><strong>Only applicable for credit card accounts.</strong><br/></div>

In the `credit_data` object, we provide you with the details of the credit card account, including:

* detailed information regarding the type of limit the credit card has (`limits`)
* the network that the card belongs to (`network` and `network_additional_info`)
* whether or not there are multiple cards associated with the credit card account (`cards`)

```json credit_data
{
  "credit_data": {
    "credit_limit": 192000.9,
    "cutting_date": "2019-12-11",
    "minimum_payment": 2400.3,
    "network": "MASTERCARD",
    "network_additional_info": "AURA CARD",
    "limits": [
      {
        "identification_number": "4453",
        "credit_limit": 1000.04,
        "used_amount": 400.04,
        "available_amount": 600,
        "is_limit_flexible": false,
        "type": "TOTAL_LIMIT",
        "consolidation_type": "INDIVIDUAL",
        "line_name": "CREDITO_A_VISTA",
        "line_name_additional_info": "Informações adicionais e complementares"
      }
    ],
    "cards": [
      {
        "is_multiple": false,
        "identification_number": "4453"
      }
    ]
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        credit\_limit
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The upper credit limit of the card.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        192000.9
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        cutting\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date when the credit card's bill is due.
      </td>

      <td style={{ textAlign: "left" }}>
        2019-12-11
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        minimum\_payment
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The minimum amount that the account owner needs to pay in the current credit period.
      </td>

      <td style={{ textAlign: "left" }}>
        2400.3
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        network
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The credit network that the card is associated with. We return one of the following values: `VISA`, `MASTERCARD`, `AMERICAN_EXPRESS`, `DINERS_CLUB`, `HIPERCARD`, `BANDEIRA_PROPRIA`, `CHEQUE_ELETRONICO`, `ELO`, or `OTHER`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        VISA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        network\_additional\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information about the credit card network.
      </td>

      <td style={{ textAlign: "left" }}>
        AURA CARD
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        limits
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding the credit limits for each credit card associated with the account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [limits section for details](https://developers.belvo.com/docs/accounts-ofda-data#limits).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        cards
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding the cards associated with the account.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [cards section for details](https://developers.belvo.com/docs/accounts-ofda-data#cards).
      </td>
    </tr>
  </tbody>
</Table>

## limits

For each card associated with the account, you receive a separate `limits` object detailing the credit limits and usage for the given card.

```json credit_data.limits
{
  "credit_data": {
    "limits": [
      {
        "identification_number": "4453",
        "credit_limit": 1000.04,
        "used_amount": 400.04,
        "available_amount": 600,
        "is_limit_flexible": false,
        "type": "TOTAL_LIMIT",
        "consolidation_type": "INDIVIDUAL",
        "line_name": "CREDITO_A_VISTA",
        "line_name_additional_info": "Informações adicionais e complementares"
      }
    ]
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        identification\_number
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The credit card number.  

        * \*Note:\*\* Often, this is just the last four digit of the credit card.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        4453
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        credit\_limit
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The limit of the credit card.
      </td>

      <td style={{ textAlign: "left" }}>
        1000.04
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        used\_amount
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The amount used.
      </td>

      <td style={{ textAlign: "left" }}>
        400.04
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        available\_amount
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The amount still available.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        600
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        is\_limit\_flexible
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>

      <td style={{ textAlign: "left" }}>
        Boolean to indicate if the `credit_limit` is flexible.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        false
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of limit. We return one of the following values: `TOTAL_LIMIT` or `MODAL_LIMIT`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        TOTAL\_LIMIT
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        consolidation\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Indicates whether or not the credit limit is consolidated or individual.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        CONSOLIDADO
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        line\_name
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The credit limit line name.
      </td>

      <td style={{ textAlign: "left" }}>
        CREDITO\_A\_VISTA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        line\_name\_additional\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information about the line name.
      </td>

      <td style={{ textAlign: "left" }}>
        Informações adicionais e complementares
      </td>
    </tr>
  </tbody>
</Table>

## cards

For each credit card associated with the account, you receive a `cards` object detailing the the identification number of the card.

```json credit_data.cards
{
  "credit_data": {
    "cards": [
      {
        "is_multiple": false,
        "identification_number": "4453"
      }
    ]
  }
}
```

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        is\_multiple
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>

      <td style={{ textAlign: "left" }}>
        Boolean to indicate if this account has multiple credit cards.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        false
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        identification\_number
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The credit card number.  

        * \*Note:\*\* Often, this is just the last four digit of the credit card.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        4453
      </td>
    </tr>
  </tbody>
</Table>

# loan\_data

In the `loan_data` object, we provide you with the details of the loan account, including:

* The type of loan (`loan_type`)
* The start and end dates of the loan (`contract_start_date` and `contract_end_date`)
* A detailed breakdown of the interest rates applied to the loan (`interest_rates.interest_rate_data`)
* The collateral provided for the loan (`collaterals`)
* Whether any balloon payments have been made (`balloon_payments`)

```json loan_data
{
  "loan_data": {
    "loan_type": "HOME_EQUITY",
    "loan_code": "92792126019929279212650822221989319252576",
    "contract_number": "1324926521496",
    "contract_amount": 202000,
    "total_effective_cost": 209000,
    "outstanding_balance": 182000,

    "contract_start_date": "2020-03-01",
    "disbursement_dates": ["2021-09-23"],
    "settlement_date": "2021-09-23",
    "contract_end_date": "2027-10-01",

    "installments_contract_term_frequency": "MONTH",
    "installment_frequency": "MONTHLY",
    "installment_frequency_info": "Sem informações adicionais",
    "first_installment_due_date": "2020-03-01",
    "number_of_installments_total": 60,
    "number_of_installments_outstanding": 48,
    "number_of_installments_paid": 32,
    "number_of_installments_past_due": 2,
    "contract_remaining_frequency": "MONTH",
    "contract_remaining_total": 20,
    "amortization_schedule": "SEM_SISTEMA_AMORTIZACAO",
    "amortization_schedule_info": "Sem informações adicionais",
    "consignee_id": "60500998000135",
    "interest_rates": [
      {
        "name": "NOMINAL",
        "type": "MONTHLY",
        "value": 7.85,
        "interest_rate_data":
          {
            "tax_type": "NOMINAL",
            "rate_type": "SIMPLE",
            "type": "MONTHLY",
            "calculation_base": "30/360",
            "reference_index_type": "FLOATING",
            "reference_index_subtype": "TR_TBF",
            "reference_index_info": "Informações adicionais sobre o TJLP",
            "pre_fixed_rate": 0.062,
            "post_fixed_rate": 0.062,
            "additional_info": "Informações adicionais sobre a taxa"
          }
      }
    ],
    "fees": [
      {
        "name": "Renovação de cadastro",
        "code": "CADASTRO",
        "fee_charge_type": "SINGLE",
        "fee_charge": "FIXED",
        "value": 5.6,
        "rate": 0.062
      }
    ],
    "contracted_charges": [
      {
        "type": "LATE_PAYMENT_INTEREST_FEE",
        "info": "Late fee",
        "rate": 0.062
      }
    ],
    "collaterals": [
      {
        "type": "HIPOTECA",
        "subtype": "IMOVEIS_RESIDENCIAIS",
        "currency": "BRL",
        "amount": 45391.89
      }
    ],
    "balloon_payments": [
      {
        "due_date": "2021-09-06",
        "currency": "BRL",
        "amount": 45391.89
      }
    ],
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        loan\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of the loan, according to the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        HOME\_EQUITY
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        loan\_code
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The country-specific standardized contract number.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        92792126019929279212650822221989319252576
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_number
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The contract number of the loan, as given by the institution.
      </td>

      <td style={{ textAlign: "left" }}>
        1324926521496
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_amount
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The initial total loan amount when the contract was signed, calculated by the institution. This amount includes the principal + interest + taxes + fees.
      </td>

      <td style={{ textAlign: "left" }}>
        202000
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        total\_effective\_cost
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The initial total effective cost of the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        209000
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        outstanding\_balance
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The amount remaining to pay in total, including interest.
      </td>

      <td style={{ textAlign: "left" }}>
        182000
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_start\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date when the loan contract was signed, in `YYYY-MM-DD` format.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        2020-03-01
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        disbursement\_dates
      </td>

      <td style={{ textAlign: "left" }}>
        array of strings
      </td>

      <td style={{ textAlign: "left" }}>
        An array of dates when the loan was disbursed. Each date is in `YYYY-MM-DD` format.
      </td>

      <td style={{ textAlign: "left" }}>
        ["2021-09-23"]
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        settlement\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date that the loan was settled, in `YYYY-MM-DD` format.
      </td>

      <td style={{ textAlign: "left" }}>
        2021-09-23
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_end\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date when the loan is expected to be completed, in `YYYY-MM-DD` format.
      </td>

      <td style={{ textAlign: "left" }}>
        2027-10-01
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        installments\_contract\_term\_frequency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The frequency of contracted installment payments, as defined when the contract was first signed. We return one of the following: `DAY`, `WEEK`, `MONTH`, `YEAR`, `NO_DEADLINE_REMAINING`, or `null`.
      </td>

      <td style={{ textAlign: "left" }}>
        MONTH
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        installment\_frequency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The frequency that the installments are paid. We return one of the following values: `IRREGULAR`, `WEEKLY`, `FORTNIGHTLY`, `MONTHLY`, `BIMONTHLY`, `QUARTERLY`, `BIANNUALLY`, `ANNUALLY`, or `OTHER`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        MONTHLY
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        installment\_frequency\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information regarding the `installment_frequency`.
      </td>

      <td style={{ textAlign: "left" }}>
        Sem informações adicionais
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        first\_installment\_due\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date when the first installment of the loan is to be paid, in `YYYY-MM-DD` format.
      </td>

      <td style={{ textAlign: "left" }}>
        2020-03-01
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        number\_of\_installments\_total
      </td>

      <td style={{ textAlign: "left" }}>
        integer
      </td>

      <td style={{ textAlign: "left" }}>
        The total number of installments required to pay the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        60
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        number\_of\_installments\_outstanding
      </td>

      <td style={{ textAlign: "left" }}>
        integer
      </td>

      <td style={{ textAlign: "left" }}>
        The number of installments left to pay.
      </td>

      <td style={{ textAlign: "left" }}>
        48
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        number\_of\_installments\_paid
      </td>

      <td style={{ textAlign: "left" }}>
        integer
      </td>

      <td style={{ textAlign: "left" }}>
        The number of installments already paid.
      </td>

      <td style={{ textAlign: "left" }}>
        32
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        number\_of\_installments\_past\_due
      </td>

      <td style={{ textAlign: "left" }}>
        integer
      </td>

      <td style={{ textAlign: "left" }}>
        The number of installments that are overdue.
      </td>

      <td style={{ textAlign: "left" }}>
        2
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_remaining\_frequency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The frequency of the remaining contracted installment payments, as defined when the contract was first signed. We return one of the following: `DAY`, `WEEK`, `MONTH`, `YEAR`, `NO_DEADLINE_REMAINING`, or `null`.
      </td>

      <td style={{ textAlign: "left" }}>
        MONTH
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contract\_remaining\_total
      </td>

      <td style={{ textAlign: "left" }}>

      </td>

      <td style={{ textAlign: "left" }}>
        The total number of installments remaining on the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        20
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        amortization\_schedule
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The loan amortization schedule.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        SEM\_SISTEMA\_AMORTIZACAO
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        amortization\_schedule\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information regarding the `amortization_schedule`.
      </td>

      <td style={{ textAlign: "left" }}>
        Sem informações adicionais
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        consignee\_id
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The ID of the consignee of the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        60500998000135
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        interest\_rates
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Breakdown of the interest applied to the loan. **With OF Brazil, we highly recommend using the information in`interest_rate_data` for in-depth information.**  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [interest\_rates section for details](https://developers.belvo.com/docs/accounts-ofda-data#interest_rates).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        fees
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Breakdown of the fees applied to the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [fees section for details](https://developers.belvo.com/docs/accounts-ofda-copy#fees).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        contracted\_charges
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Breakdown of the charges applied to the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [contracted\_charges section for details](https://developers.belvo.com/docs/accounts-ofda-data#contracted_charges).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        collaterals
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Details regarding any loan collaterals that the individual or business supplied.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [collaterals section for details](https://developers.belvo.com/docs/accounts-ofda-data#collaterals).
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        balloon\_payments
      </td>

      <td style={{ textAlign: "left" }}>
        array of objects
      </td>

      <td style={{ textAlign: "left" }}>
        Detailed information regarding any balloon payments for the loan, if applicable.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [balloon\_payments section for details](https://developers.belvo.com/docs/accounts-ofda-data#balloon_payments).
      </td>
    </tr>
  </tbody>
</Table>

## interest\_rates

In the `interest_rates` array we provide you information regarding the interest rates of the loan. For each interest rate applied to the load, you receive a separate object.

```json loan_data.interest_rates
{
  "loan_data": {
    "interest_rates": [
      {
        "name": "NOMINAL",
        "type": "MONTHLY",
        "value": 7.85,
        "interest_rate_data":
          {
            "tax_type": "NOMINAL",
            "rate_type": "SIMPLE",
            "type": "MONTHLY",
            "calculation_base": "30/360",
            "reference_index_type": "FLOATING",
            "reference_index_subtype": "TR_TBF",
            "reference_index_info": "Informações adicionais sobre o TJLP",
            "pre_fixed_rate": 0.062,
            "post_fixed_rate": 0.062,
            "additional_info": "Informações adicionais sobre a taxa"
          }
      }
    ]
  }
}
```

However, we **highly recommend** that you use the `interest_rate_data` array within the `interest_rates` object as it contained more detailed information regarding the loan. 

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The name of the type of interest rate applied to the loan.  

        * \*Note:\*\* For OFDA Brazil, we recommend you use the `interest_date_data.tax_type` parameter.
      </td>

      <td style={{ textAlign: "left" }}>
        NOMINAL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The period that the interest is applied to the loan.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        MONTHLY
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        value
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The interest rate (in percent or currency value).  

        * \*Note:\*\* For OFDA Brazil, we recommend you use the `interest_date_data.pre_fixed_rate` and `interest_date_data.post_fixed_rate`parameter.
      </td>

      <td style={{ textAlign: "left" }}>
        7.85
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        interest\_rate\_data
      </td>

      <td style={{ textAlign: "left" }}>
        objects
      </td>

      <td style={{ textAlign: "left" }}>
        Detailed information regarding the interest rate.
      </td>

      <td style={{ textAlign: "left" }}>
        See the [interest\_rate\_data section](https://developers.belvo.com/docs/accounts-ofda-data#interest_rate_data).
      </td>
    </tr>
  </tbody>
</Table>

## interest\_rate\_data

The `interest_rate_data` object contains detailed information regarding each interest rate applied to the loan. We highly recommend using the data within this field as it contains more specific information regarding each interest rate.

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        tax\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of interest rate tax. We return one of the following values: `NOMINAL` or `EFFECTIVE`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        NOMINAL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        rate\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of interest rate. We return one of the following values: `SIMPLE`, or `COMPOUND`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        SIMPLE
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The period that the interest is applied to the loan.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        MONTHLY
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        calculation\_base
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The base calculation for the interest rate.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        21/252
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reference\_index\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The reference index rate. We return one of the following values: `WITHOUT_INDEX_TYPE`, `PRE_FIXED`, `POST_FIXED`, `FLOATING`, `INDEXED_PRICE`, `RURAL_CREDIT`, or `OTHER_INDEX`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        PRE\_FIXED
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reference\_index\_subtype
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The subtype of the reference index rate.
      </td>

      <td style={{ textAlign: "left" }}>
        TJLP
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        reference\_index\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information regarding the reference index rate.
      </td>

      <td style={{ textAlign: "left" }}>
        Informações adicionais sobre o TJLP
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        pre\_fixed\_rate
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The pre-fixed percentage rate of the interest rate.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        0.6
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        post\_fixed\_rate
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The post-fixed percentage rate of the interest rate.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network.
      </td>

      <td style={{ textAlign: "left" }}>
        0.55
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        additional\_info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information regarding the interest rate.
      </td>

      <td style={{ textAlign: "left" }}>
        Informações adicionais sobre a taxa
      </td>
    </tr>
  </tbody>
</Table>

## fees

In the `fees` array, we provide you detailed information regarding each fee applied to the loan.

```json loan_data.fees
{
  "loan_data": {
    "fees": [
      {
        "name": "Renovação de cadastro",
        "code": "CADASTRO",
        "fee_charge_type": "SINGLE",
        "fee_charge": "FIXED",
        "value": 5.6,
        "rate": 0.062
      }
    ]
  }
}
```

<br />

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        name
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The fee name.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `fees` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        Renovação de cadastro
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        code
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The fee code.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `fees` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        CADASTRO
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        fee\_charge\_type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Indicates the type of charge. We return one of the following values: `SINGLE` or `PER_INSTALLMENT`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `fees` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        SINGLE
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        fee\_charge
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Billing method, as agreed upon with the institution. We return one of the following values: `MINIMUM`, `MAXIMUM`, `FIXED`, or `PERCENTAGE`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `fees` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        PERCENTAGE
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        value
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The total value of the fee. Same currency as the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        5.6
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        rate
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The percentage rate of the fee. Required when `fee_charge` is set to `PERCENTAGE`.
      </td>

      <td style={{ textAlign: "left" }}>
        0.062
      </td>
    </tr>
  </tbody>
</Table>

## contracted\_charges

In the `contracted_charges` array. we provide you with detailed information regarding all the charges that the loan has incurred.

```json loan_data.contracted_charges
{
  "loan_data": {
    "contracted_charges": [
      {
        "type": "LATE_PAYMENT_INTEREST_FEE",
        "info": "Late fee",
        "rate": 0.062
      }
    ]
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of contracted charge. We return one of the following values: `LATE_PAYMENT_INTEREST_FEE`, `LATE_PAYMENT_PENALTY_FEE`, `DEFAULT_INTEREST_FEE`, `LOAN_CONTRACT_TAX`, `LATE_PAYMENT_TAX`, `NO_CHARGE`, or `OTHER`.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `contracted_charges` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        LATE\_PAYMENT\_INTEREST\_FEE
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        info
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        Additional information regarding the contracted charge.
      </td>

      <td style={{ textAlign: "left" }}>
        Informações adicionais sobre encargos.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        rate
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The percentage rate of the charge, calculated based on the amount of the loan.
      </td>

      <td style={{ textAlign: "left" }}>
        0.07
      </td>
    </tr>
  </tbody>
</Table>

## collaterals

In the `collaterals` array, we provide you with detailed information regarding any collateral that was provided for the loan.

```json loan_data.collaterals
{
  "loan_data": {
    "collaterals": [
      {
        "type": "HIPOTECA",
        "subtype": "IMOVEIS_RESIDENCIAIS",
        "currency": "BRL",
        "amount": 45391.89
      }
    ]
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        type
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The type of collateral, as defined by the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `collaterals` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        HIPOTECA
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        subtype
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The subtype of the collateral, as defined by the institution.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `collaterals` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        IMOVEIS\_RESIDENCIAIS
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        currency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The three-letter currency code (ISO-4217).  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `collaterals` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        BRL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        amount
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The total amount of the bill.  

        > **Non-nullable:** A value must be returned by Brazil's open finance network if the `collaterals` field is available.
      </td>

      <td style={{ textAlign: "left" }}>
        45391.89
      </td>
    </tr>
  </tbody>
</Table>

## balloon\_payments

In the `balloon_payments` array, we provide you with detailed information regarding any balloon payments for the loan, if applicable.

```json loan_data.balloon_payments
{
  "loan_data": {
    "balloon_payments": [
      {
        "due_date": "2021-09-06",
        "currency": "BRL",
        "amount": 45391.89
      }
    ]
  }
}
```

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Parameter
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        due\_date
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (date)
      </td>

      <td style={{ textAlign: "left" }}>
        The date that the balloon payment is to be paid, in `YYYY-MM-DD` format.
      </td>

      <td style={{ textAlign: "left" }}>
        2021-09-06
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        currency
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>

      <td style={{ textAlign: "left" }}>
        The three-letter currency code (ISO-4217).
      </td>

      <td style={{ textAlign: "left" }}>
        BRL
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        amount
      </td>

      <td style={{ textAlign: "left" }}>
        number
      </td>

      <td style={{ textAlign: "left" }}>
        The total amount of the balloon payment.
      </td>

      <td style={{ textAlign: "left" }}>
        1000.037
      </td>
    </tr>
  </tbody>
</Table>