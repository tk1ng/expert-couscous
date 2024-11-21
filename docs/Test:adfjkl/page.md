---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
In this guide, we walk you through everything you need to extract fiscal data about your users using our API. This includes:

* A general overview of the data flow
* Creating a link using our API
* Getting fiscal information:
  * Historic Updates (all links)
  * Recurrent Updates (just for recurrent links)

# Prerequisites

Before you proceed with your integration, make sure that you have:

1. <a href="https://developers.belvo.com/docs/get-started-in-10-minutes" target="_blank"><strong>Gone through our getting started guide</strong></a>\
   In the getting started guide, you'll create a Belvo account, generate some sandbox API keys, and set up a webhook URL.\
   For testing purposes and developing your integration, we highly recommend using the Sandbox environment along with the <a href="https://developers.belvo.com/docs/test-in-sandbox#banking---open-finance-brazil" target="_blank">Mockbank institution</a>. You can find example credentials to simulate different users for the Mockbank institution <a href="https://gitlab.com/raidiam-conformance/open-finance/certification/-/wikis/customer-Data" target="_blank">here</a>.

> 📘 What data can I get about my users?
>
> For a detailed list of data that our Fiscal Aggregation (Mexico) Product returns for your users, see the following resources:
>
> `<Fiscaldatareferencetable />`

# General flow of data

Belvo uses *asynchronous workflows* to improve your data flow (check the diagram below). 

Whenever you create a link, Belvo automatically extracts all the Employment Record data for you in the background, and once we have all the data, we notify you via a webhook that the data is ready to be retrieved. So that we can notify you once the data is ready, you'll need to provide a URL where we can send events to.

<Image alt="Fiscal data asynchronous flow" align="center" src="https://files.readme.io/cac4f2ed05016a84c20cd21747863a7e3f1086a6b35a367a8bd9ef06695494d2-image.png">
  Fiscal data asynchronous flow
</Image>

<br />

# Create a link

> 👍 What's a link?
>
> A link is Belvo's term for a connection between your user (RFC) and the employment institution (SAT). Whenever you want to extract information from a new user, you'll need to create a link.

To create a link, you just need to make a **POST Register a new link** request. See our step-by-step walkthrough on how to create a Fiscal Link (SAT Mexico) in the recipe below.

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="66fd3e41979a46001ffca81b" link="https://developers.belvo.com/v1.0/recipes/create-a-fiscal-link-sat-mexico" slug="create-a-fiscal-link-sat-mexico" title="Create a Fiscal Link (SAT Mexico)" />

Once you create a link, you will need to save the `id` of the link that your receive in the response:

```json Example Response
{
  "id": "74c01cb4-edf1-44d6-8876-b1dc2aebcb14", // <-- Save this ID.
  "institution": "tatooine_mx_fiscal",
  "access_mode": "single",
  "status": "valid",
  "refresh_rate": null,
  "created_by": "6e9be884-4781-4143-b673-aca02475ee8c",
  "last_accessed_at": "2024-06-26T16:25:54.344113Z",
  "external_id": "HJLSI-897809",
  "created_at": "2024-06-26T16:25:54.334413Z",
  "institution_user_id": "BidIxnZkKvQx0_F0oSYVx6Jnsh4Zmoat2ot2iOoG018=",
  "credentials_storage": "store",
  "stale_in": null,
  "fetch_resources": [
    "FINANCIAL_STATEMENTS",
    "INVOICES",
    "TAX_RETENTIONS",
    "TAX_RETURNS",
    "TAX_STATUS",
    "TAX_COMPLIANCE_STATUS"
  ]
}
```

<br />

✳️ **Done**! Belvo will now connect to the institution and asynchronously load the data for the resources your requested in `fetch_resources`. We will send you a webhook once we have retrieved the data for the given link, and you can then extract it with a **GET** request

# Wait for webhooks to get historical fiscal data

As soon as you create your fiscal link, Below will asynchronously retrieve historical data for each resource you added in the `fetch_resources` array. As soon as Belvo retrieves the data, you will receive a webhook indicating that the data is ready to be retrieved:

| Resource                | Number of Webhooks | Details                                                                                                                                          |
| :---------------------- | :----------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| `FINANCIAL_STATEMENTS`  | 1                  | See the [Financial Statements section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#financial-statements).   |
| `INVOICES`              | 4-8                | See the [Invoices section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#invoices).                           |
| `TAX_RETENTIONS`        | 1                  | See the [Tax Retentions section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#tax-retentions).               |
| `TAX_RETURNS`           | 2                  | See the [Tax Returns section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#tax-returns).                     |
| `TAX_STATUS`            | 1                  | See the [Tax Status section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#tax-status).                       |
| `TAX_COMPLIANCE_STATUS` | 1                  | See the [Tax Compliance Status section below](https://developers.belvo.com/docs/extract-fiscal-information-in-mexico-api#tax-compliance-status). |

## Financial Statements

`<Financialstatementwebhookhistoricalrequest />`

<br />

## Invoices

Due to the number of invoices an individual or business may have, and to optimize the extraction process, you will receive several different types of Invoice webhooks after you create the link.

### Last 30 days of data

`<Invoiceswebhookinitialrequests />`

### Last 3 years of data

`<Invoiceswebhookhistoricalrequests />`

<br />

## Tax Retentions

`<Taxretentionswebhookhistoricalrequest />`

## Tax Returns

`<Taxreturnswebhookhistoricalrequest />`

<br />

## Tax Status

`<Taxstatuswebhookhistoricalrequest />`

<br />

## Tax Compliance Status

`<Taxcompliancewebhookrequest />`

<br />

# Recurring updates

If you created a recurrent link (using `access_mode: recurrent`), then depending on the refresh rate you established with Belvo, you will receive webhooks for updated resource (see the diagram in the General flow of data section). 

The following webhooks are available for recurrent links:

| Resource      | Number of Webhooks | Details                            |
| :------------ | :----------------- | :--------------------------------- |
| `INVOICES`    | 2-4                | See the Invoices section below.    |
| `TAX_RETURNS` | 2                  | See the Tax Returns section below. |

## Invoices

According to your chosen refresh rate, Belvo will asynchronously retrieve data about any new or cancelled invoices that have appeared in the SAT system for a given link since the last update.

### New Invoices

`<Invoiceswebhookrecurrentrequest />`

<br />

### Cancelled Invoices

`<Invoicescancelledwebhookrecurrentrequest />`

<br />

## Tax Returns

`<Taxreturnsnewwebhookrecurrentrequest />`

<br />

# Errors while extracting Financial Statements

`<Financialstatementerrors />`