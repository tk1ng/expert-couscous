---
title: Blank page
deprecated: false
hidden: true
metadata:
  robots: index
---
# Institutions

![](https://files.readme.io/065cff3-small-Links_-_with_employment.png)

An *institution* is an entity that Belvo can access information from. It can be a:

* bank institution, such as Banamex retail banking or HSBC business banking.
* fiscal institution, such as the Servicio de Administración Tributaria (SAT) in Mexico.
* employment institution, such as Instituto Mexicano del Seguro Social (IMSS) in Mexico.

> ✅ Belvo resources and institutions
>
> Not all institutions support the same Belvo resources. For example, the Accounts resource (used with banking institutions) won't be supported in fiscal institutions. To know which resources you can use for each institution, look at the `resources` array when you use one of the methods in the table below.

You can see a complete list of banking institutions by either consulting our Institutions page, or querying the following resources:

| Endpoint                                                           | Method | Description                                         |
| :----------------------------------------------------------------- | :----- | :-------------------------------------------------- |
| [List](https://developers.belvo.com/reference/listinstitutions)    | `GET`  | List all institutions currently supported by Belvo. |
| [Detail](https://developers.belvo.com/reference/detailinstitution) | `GET`  | Get the details for a specific institution.         |

# Links

Whenever a user connects to their institution using the Belvo API, we create a *Link*. A Link is a set of encrypted credentials, for example the username and password, that is associated with the user. You will always need to first register a Link before being able to access information specific to that end user. 

You can perform the following operations with our Links resource:

| Endpoint                                                        | Method   | Description                                                                                                          |
| :-------------------------------------------------------------- | :------- | :------------------------------------------------------------------------------------------------------------------- |
| [Register](https://developers.belvo.com/reference/registerlink) | `POST`   | Register a new link from a financial institution to your Belvo account.                                              |
| [List](https://developers.belvo.com/reference/listlinks)        | `GET`    | List all links currently associated with your Belvo account.                                                         |
| [Resume](https://developers.belvo.com/reference/patchlinks)     | `PATCH`  | Resume a link registering session that was paused because an MFA token was required by the institution.              |
| [Detail](https://developers.belvo.com/reference/detaillink)     | `GET`    | Get the details of a specific link.                                                                                  |
| [Update](https://developers.belvo.com/reference/updatelink)     | `PUT`    | Update the password of a specific link.                                                                              |
| [Destroy](https://developers.belvo.com/reference/destroylink)   | `DELETE` | Delete permanently a link and all associated accounts, transactions, and owners information from your Belvo account. |

> ✅ Use your own identifier 🤩
>
> We really recommend you make use of the `external_id` parameter when creating links as this will allow you to have your own unique identifier for a link in your own database. Check out our [Link creation best practices article](https://developers.belvo.com/docs/link-creation-best-practices#adding-your-own-identifier) for more information.

## Recurrent links

With recurrent links, Belvo automatically refreshes information weekly and notifies you via [webhook](https://developers.belvo.com/docs/webhooks) so you always have up-to-date data. Then, when you receive the webhook, you can use GET requests to the List or Detail endpoints to instantly access up-to-date information, without needing to connect to the institution.

<Image title="Recurrent Link FLow.png" alt={1918} align="center" src="https://files.readme.io/eb96451-BANKING_DATA_-_Recurrent_Link_Asynchronous.png">
  Recurrent link flow
</Image>

When you create a recurrent link, Belvo automatically retrieves key information about the Link ID. Once we have the information, we'll send you a historical webhook event indicating that you can make a GET request for that information. 

We recommend you don't make POST calls immediately after a link is created. Instead, wait for a [historical update webhook](https://developers.belvo.com/docs/webhooks#webhook-events) which indicates that Belvo has scraped the data and then you can make a GET request to retrieve the information (the webhook is sent soon after a link is created). If you make a GET request before you receive a historical webhook, you will receive responses with empty data fields or duplicated information. 

> 🛑 Use of user credentials
>
> When using recurrent links, you must ensure that you comply with the data privacy regulation of the country you operate in. Additionally, we recommend that you inform users that their credentials will be used daily in order to cyclically retrieve up-to-date data.

### Refresh rates

By default, recurrent links are automatically **refreshed once every seven days**. However, you can change the update frequency of your recurrent links to every:

* 6 hours (four times per day)
* 12 hours (twice a day)
* 24 hours (once a day)
* 30 days (once a month)\
  Note: with the 30-day refresh rate, we distribute the link updates between day 1 and day 20 of the given month. The refresh date for each monthly recurrent link is initially assigned randomly between the 1st and the 20th of the month. If the following link updates are successful then the subsequent refreshes for this link will occur on the same day each month. Links are not scheduled to be updated after the 20th of the month to reserve some time for potential re-tries. For more information, check out our [Help Center article](https://support.belvo.com/hc/en-us/articles/9438194912541) on Monthly recurrent links.

{/*Recurrent links are scheduled to be refreshed within a time frame from the moment they are created.
For example, if a recurrent link is created at 12:00 with a refresh rate of six hours, the system will schedule the first refresh between 12:00 and 18:00. If the system does the first refresh at 16:00, all following refreshes will be based on this time (so the next refresh will be at 22:00, then at 04:00, and then again at 10:00).\\\\\\\\\*/}

> ✅ Refresh rate pricing
>
> To change your refresh rate or discuss refresh rate pricing, just email our sales team at <a href="mailto:sales@belvo.com">sales\@belvo.com</a>, and they'll get right to it.

With recurrent links, we update the following information according to your chosen frequency:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Institution
      </th>

      <th style={{ textAlign: "left" }}>
        Initial information
      </th>

      <th style={{ textAlign: "left" }}>
        Refreshed information
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Banking
      </td>

      <td style={{ textAlign: "left" }}>
        All account, transaction, and owner information
      </td>

      <td style={{ textAlign: "left" }}>
        \- Account information, including current balance and credit data.<br/><br/>\- New transactions (added since the last recurrent link update).<br/><br/>\- Personal information of the link owner.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Fiscal
      </td>

      <td style={{ textAlign: "left" }}>
        All invoices, the tax compliance statuses, tax returns, and the tax status.
      </td>

      <td style={{ textAlign: "left" }}>
        \- New invoices sent or received within the last five years.<br/><br/>\- New tax returns added within the last five years.
      </td>
    </tr>
  </tbody>
</Table>

## Single links

Single links are used to perform ad hoc data access to accounts, owners,  transactions, and so on. For example, you can use it when you want to do an underwriting process to assess risk before lending money.

For single links, you need to pass the `fetch_resources` parameter when creating and then listen for webhooks once the historical data has been asynchronously extracted. 

<Image align="center" src="https://files.readme.io/2558317-BANKING_DATA_-_Single_Link_Asynchronous_1.png" />

# Link statuses

A link can have different statuses, which reflect if the link is operational or if an action is needed to restore the link.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Status
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>

      <th style={{ textAlign: "left" }}>
        Action
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        `valid`
      </td>

      <td style={{ textAlign: "left" }}>
        A `valid` link is a fully working link.
      </td>

      <td style={{ textAlign: "left" }}>
        None 🎉
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `invalid`
      </td>

      <td style={{ textAlign: "left" }}>
        An `invalid` link means that the credentials are no longer valid.
      </td>

      <td style={{ textAlign: "left" }}>
        You need to ask your user to update their credentials in order for the link to be valid again.  

        💡Use the Connect widget in update mode to ask your user to provide a new password.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `unconfirmed`
      </td>

      <td style={{ textAlign: "left" }}>
        An `unconfirmed` link means that the link was never created successfully. A common situation where this can occur is when a user was prompted to for an MFA token but never provided it. 
      </td>

      <td style={{ textAlign: "left" }}>
        You need to [resume](https://developers.belvo.com/reference/patchlinks) the link creation process with a token to complete the link creation.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `token_required`
      </td>

      <td style={{ textAlign: "left" }}>
        A `token_required` link means that a previously `valid` link now requires a new token.
      </td>

      <td style={{ textAlign: "left" }}>
        You need to [resume](https://developers.belvo.com/reference/patchlinks) the link update process with a token.  

        💡Use the Connect widget in update mode to ask your user to provide a new password.
      </td>
    </tr>
  </tbody>
</Table>

# Checking the status of a link

You can find the status of a link by making one of the following queries and checking the value of the status field in the JSON response:

## List all current links

Use the [List all links method](https://developers.belvo.com/reference/listlinks) to get all the links you currently have access to. You can perform filtering on the responses to return just the links that have a certain status. In the example below, we filter the response to just have invalid links.

```shell List (filtered)
curl -- request POST 'https://sandbox.belvo.co/api/links/?status=invalid'\
  -u [Secret Key ID]:[Secret Key PASSWORD]
```
```shell List (unfiltered)
curl -- request POST 'https://sandbox.belvo.co/api/links/'\
  -u [Secret Key ID]:[Secret Key PASSWORD]
```

If you want to know about applying filters in your queries, see our [Filtering responses](https://developers.belvo.com/docs/searching-and-filtering) article.  

## Get details for a specific link

Use the [Get a link's details method](https://developers.belvo.com/reference/detaillink) to get the details for a specific Link. 

```curl Link detail request
curl -- request GET 'https://sandbox.belvo.co/api/links/{id}' \
  -u [Secret Key ID]:[Secret Key PASSWORD]
```
```json Link detail response
...
{
    “id”: “c70a25d4-d8ad-9999-b59e-b8f57f0e7123",
    “institution”: “liverpool_mx_retail”,
    “access_mode”: “recurrent”,
    “last_accessed_at”: “2019-10-04T10:58:20.374432Z”,
    “status”: “valid”, // Status of the link. In this case it's valid - perfect!
    “created_by”: “b18626ab-74aa-45fd-a66d-babf1461f962"
}
...
```

Where:

* `{id}` is the ID of the link. For example: `c70a25d4-d8ad-9999-b59e-b8f57f0e7123`.