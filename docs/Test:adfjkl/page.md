---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
In Brazil’s Open Finance network, there are monthly limits regarding how often you can retrieve data for a specific person or business. These limits are linked to a combination of:

* the user’s CPF or CNPJ
* the API resource you request data for
* the Open Finance network certificate

Once the monthly limit of API calls is reached, no more information can be retrieved for the CPF/CNPJ until the start of the next calendar month.

The limits are outlined in the table below:

| Belvo API Resource (POST calls)                                | Open Finance Operation Limit                                                                                                   |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Owners                                                         | 4 API calls per CPF/CNPJ                                                                                                       |
| Accounts                                                       | 4 API calls per CPF/CNPJ <br/><br/>**Note**: Balance and overdraft limit information can be updated up to 240 times per CPF/CNPJ |
| Transactions (up to 365 days from the moment of the request)   | 4 API calls per CPF/CNPJ                                                                                                       |
| Transactions (less than 6 days from the moment of the request) | 240 API calls per CPF/CNPJ                                                                                                     |

> 📘
>
> **Note**: The monthly data retrieval limits are shared across all applications using the same open finance certificate.

In this article, we provide you with guidelines on how these limits may impact your data retrieval flows and, based on your data frequency needs, offer recommendations to mitigate disruptions.

# Asynchronous workflow (single links)

> 👍
>
> **Data frequency needs:** Low
>
> You only need to retrieve historical information once (or once a week). For example, credit lenders or ID verification.

When you create a single link using our [asynchronous workflow (which uses our `fetch_resources` parameter),](https://developers.belvo.com/docs/asynchronous-requests#asynchronous-historical-data-workflow-single-links) Belvo will asynchronously retrieve the historical information for your user (up to 365 days). After you receive the webhook notification that the historical data is available, you can retrieve it using GET calls.

For any subsequent POST calls you make after link creation, the information that you retrieve will depend on the API resource (see the table below).

| Belvo API Resource | Information updated on each POST call              | Recommended frequency |
| ------------------ | -------------------------------------------------- | --------------------- |
| Accounts           | Balances, overdraft limits, and credit card limits | Daily or weekly       |
| Owners             | User personal details                              | Monthly               |
| Transactions       | Transactions within the last six days.             | Weekly                |

> 🚧
>
> **Avoid duplicate links**: For each link that you create, a new consent is generated in Brazil’s Open Finance network and Belvo retrieves historical data for that CPF/CNPJ, consuming the operational limits.

# Asynchronous workflow (recurrent links)

> 👍
>
> **Data frequency needs:** High
>
> You need balance, overdraft, and transaction information on a daily basis. For example, PFMs or ERPs.

When you create a recurrent link, Belvo will asynchronously retrieve the historical information for your user (up to 365 days). After you receive the webhook notification that the historical data is available, you can retrieve it using GET calls as usual. Depending on your refresh rate, you will receive webhooks indicating whether a new account, owner, or transaction has been retrieved from the institution, which you can also retrieve using GET calls.

Any individual POST call you make will retrieve the following information:

| Belvo API Resource | Information updated on each POST call              | Recommended frequency |
| ------------------ | -------------------------------------------------- | --------------------- |
| Accounts           | Balances, overdraft limits, and credit card limits | Daily or weekly       |
| Owners             | User personal details                              | Monthly               |
| Transactions       | Transactions within the last six days.             | Weekly                |

# Single links

> 👍
>
> **Data frequency needs:** Very low
>
> You only need to retrieve historical information once. For example, one-off credit analysis.

When you create a single link without historical data, you will need to make individual POST calls to retrieve data for your user.

| Belvo API Resource | Information updated on the first POST call |
| ------------------ | ------------------------------------------ |
| Accounts           | Historical account information             |
| Owners             | Historical owner details                   |
| Transactions       | Up to 365 days of transactional data       |

Any subsequent individual POST call you make will retrieve the following information:

| Belvo API Resource | Information updated on each POST call              | Recommended frequency |
| ------------------ | -------------------------------------------------- | --------------------- |
| Accounts           | Balances, overdraft limits, and credit card limits | Daily or weekly       |
| Owners             | User personal details                              | Monthly               |
| Transactions       | Transactions within the last six days.             | Weekly                |

# FAQ

#### Given the limits, is it possible that account and owner data for a recurrent link will not be updated for an entire month?

Yes, in the situation where the operational limit has been reached for a CPF/CNPJ, the recurrent link will not be updated (and new accounts or owners will not be identified). This can occur for three reasons:

1. The user has created a link four times within the month.
2. Clients not using asynchronous workflows have used up the operational limits for the CPF/CNPJ using POST calls.

> 📘
>
> Information regarding account balance and overdrafts limits have a higher limit (minimum of 240 API calls). As such, this information will be updated for existing accounts until the limit for those resource has been reached.

#### Do I still receive transaction webhooks for daily or weekly refreshes?

Yes, as the limits for transactional information within the last six days are larger (240 requests), you will still receive webhooks for new transactions that occur.

#### What API error will I receive when the limit is reached?

When the limit is reached you will ll receive a `400` HTTP error (`operational_limits_reached`), indicating that Belvo could not retrieve information for the link due to the limits being reached.

```json Example error
[
  {
    "code": "operational_limits_reached",
    "message": "The institution has reached its operational limits",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```

#### Will my user be aware that they have reached the limit when creating their link?

As the API calls occur **after** the user has created their link, they will not receive any error which indicates that the application they’re granting consent to won’t be able to retrieve data.