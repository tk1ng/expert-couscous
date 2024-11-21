---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
Belvo - Developer Hub

v1.0

View

Edit

My Developers



Guides
Recipes
API Reference
Changelog
Custom Pages
Pages with invalid MDX (24)

New Category
Extract Employment Information in Mexico (API)
So, want to get employment data about your users in Mexico? Well, you've come to the right place 😎
Error Rendering Page: Check MDX for JSX syntax errors. Need help? Ask support
In this guide, we walk you through everything you need to extract employment data about your users using our API. This includes:

* A general overview of the data flow
* Generating your API keys
* Providing a webhook URL (to receive events from Belvo)
* Creating a link
* Getting employment record information

> 📘 What data can I get about my users?
>
> For a detailed list of data that our Employment Record API returns for your users, see our:
>
> * Dedicated <a href="https://developers.belvo.com/docs/employment-records-data-mexico" target="_blank">Employment Records Data (Mexico) guide</a>
> * <a href="https://developers.belvo.com/reference/listemploymentrecords" target="_blank">API Reference</a>

# General flow of data

> 👍 Average time to retrieve employment data
>
> The average time it takes for Belvo to retrieve employment data from an employment institution and send you a webhook event is 15 seconds. However, this can vary depending on the institution's responsiveness and their current request load.

Belvo uses *asynchronous workflows* to improve your data flow (check the diagram below). 

Whenever you create a link, Belvo automatically extracts all the Employment Record data for you in the background, and once we have all the data, we notify you via a webhook that the data is ready to be retrieved. So that we can notify you once the data is ready, you'll need to provide a URL where we can send events to.

<Image alt="Employment Records Asynchronous Workflow" align="center" src="https://files.readme.io/8052084-EMPLOYMENT_DATA_MEXICO_-_Asynchronous.png">
  Employment Records Asynchronous Workflow
</Image>

# Generate API Keys

To use our API, you will need to generate some API keys to authenticate all your request.

To generate your API keys:

1. Sign in to your <a href="https://dashboard.belvo.com" target="_blank">Belvo Dashboard</a>.
2. Choose the environment you want to create API keys for (<a href="https://dashboard.belvo.com/sandbox/api-keys/" target="_blank">Sandbox</a> or <a href="https://dashboard.belvo.com/production/api-keys/" target="_blank">Production</a>). If you're just starting to use the Belvo API, we recommend using the **Sandbox** environment.
3. Go to **Developers** -> **API Keys**.
4. Click on **Generate API Keys**, which will automatically generate your API keys.
5. In the pop-up, copy and securely save the values for **Secret ID** and **Secret Password**.\
   **Note**: In the pop-up, you also have the option of forking Belvo's API collection. For more information on how to use Postman and Belvo's collection, see our Getting started in 10 minutes guide.

✳️ **Done**! You've just generated your API keys! But before you can start making API calls, you just need to set up a webhook where we can send events to.

# Add a webhook URL

> 📘 Just testing out?
>
> If you're just starting your integration and aren't sure how to get a URL for a webhook, you can use a service like Pipedream. Check out our <a href="https://developers.belvo.com/docs/get-started-in-10-minutes" target="_blank">Getting started in 10ish minutes</a> to see how it's done!

To set up a new webhook:

1. Sign in to your <a href="https://dashboard.belvo.com" target="_blank">Belvo Dashboard</a>.
2. Choose the environment you want to receive webhook events for (<a href="https://dashboard.belvo.com/sandbox/webhooks/" target="_blank">Sandbox</a> or <a href="https://dashboard.belvo.com/production/webhooks/" target="_blank">Production</a>).
3. Go to **Developers** -> **Webhooks**.
4. Click **+New webhook**.
5. Fill in the **New webhook** form with the required information.
   1. **URL**: the URL to receive the webhook notifications.
   2. **Authorization**: an optional bearer token to use if your URL is protected.
6. Click **Create webhook**.

✳️ **Done**! You've now created a webhook and can start creating links and receiving events!

### Whitelisting Belvo IP addresses

Belvo will send events to your webhook URL from the IP addresses listed below. Your security team may want to add these to their list of IP addresses that they allow events from (otherwise, your system may block events from reaching your system).

* `3.130.254.46`
* `18.220.61.186`
* `18.223.45.212`

# Create a link

> 👍 What's a link?
>
> A link is Belvo's term for a connection between your user (CURP) and the employment institution (IMSS). Whenever you want to extract information from a new user, you'll need to create a link.

To create a link, you just need to make the following **POST Register a new link** request:

```curl Sandbox
curl --location 'https://sandbox.belvo.com/api/links/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic BASE64(SECRET_ID:SECRET_PASSWORD)' \
--data '{see examples below}'
```
```curl Production
curl --location 'https://api.belvo.com/api/links/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic BASE64(SECRET_ID:SECRET_PASSWORD)' \
--data '{see examples below}'
```

```json Sandbox Payload
{
  "institution": "planet_mx_employment",
  "username": "BLPM951331IONVGR54",
  "fetch_resources": ["EMPLOYMENT_RECORDS","OWNERS"],
  "access_mode": "single",
  "external_id":"COHORT_32_User_6790023X5"
}
```
```json Production Payload
{
  "institution": "imss_mx_employment",
  "username": "valid_curp",
  "fetch_resources": ["EMPLOYMENT_RECORDS","OWNERS"],
  "access_mode": "single",
  "external_id":"COHORT_32_User_6790023X5"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Parameter
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>

      <th>
        Example
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `institution`
      </td>

      <td>
        string
      </td>

      <td>
        true
      </td>

      <td>
        The institution where you want to create the link
      </td>

      <td>
        - `planet_mx_employment` for Sandbox  

        * `imss_mx_employment` or `issste_mx_employment` for Production
      </td>
    </tr>

    <tr>
      <td>
        `username`
      </td>

      <td>
        string
      </td>

      <td>
        true
      </td>

      <td>
        The CURP of the individual.<br/><br/>Note: Belvo uses industry-standard AES-256 symmetric encryption to encrypt credentials.
      </td>

      <td>
        `BLPM951331IONVGR54`
      </td>
    </tr>

    <tr>
      <td>
        `fetch_resources`
      </td>

      <td>
        array
      </td>

      <td>
        true
      </td>

      <td>
        The resources you want Belvo to retrieve. For employment records in Mexico, you must send through at least `EMPLOYMENT_RECORDS`
      </td>

      <td>
        `["EMPLOYMENT_RECORDS","OWNERS"]`
      </td>
    </tr>

    <tr>
      <td>
        `access_mode`
      </td>

      <td>
        string
      </td>

      <td>
        true
      </td>

      <td>
        The type of link to create. For employment data, we recommend using `single` links. For more information about a link's access\_mode, see our dedication section [here](https://developers.belvo.com/edit/links-and-institutions).
      </td>

      <td>
        `single`
      </td>
    </tr>

    <tr>
      <td>
        `external_id`
      </td>

      <td>
        string
      </td>

      <td>
        recommended
      </td>

      <td>
        Your internal reference for this user. This is extremely useful for you as you'll be able to relate the data that Belvo retrieves for this user in your system.
      </td>

      <td>
        `COHORT_32_User_6790023X5`
      </td>
    </tr>
  </tbody>
</Table>

```json Example Response
{
    "id": "74c01cb4-edf1-44d6-8876-b1dc2aebcb14",
    "institution": "planet_mx_employment",
    "access_mode": "single",
    "status": "valid",
    "refresh_rate": null,
    "created_by": "6e9be884-4781-4143-b673-aca02475ee8c",
    "last_accessed_at": "2024-06-26T16:25:54.344113Z",
    "external_id": "COHORT_32",
    "created_at": "2024-06-26T16:25:54.334413Z",
    "institution_user_id": "BidIxnZkKvQx0_F0oSYVx6Jnsh4Zmoat2ot2iOoG018=",
    "credentials_storage": "365d",
    "stale_in": null,
    "fetch_resources": [
        "EMPLOYMENT_RECORDS",
        "OWNERS"
    ]
}
```

<br />

✳️ **Done**! Belvo will now connect to the institution and validate that the provided CURP is correct. Once validated and your link is created, Belvo will asynchronously load the employment data. We will send you a webhook once we have retrieved the data for the given link, and you can then extract it with a get request.

### Common errors when creating a link

When you create a link with IMSS Mexico, you might receive specific errors due to the CURP you provide. Below you can see a couple of common errors along with the explanations as to why they occur:

| Belvo error\_code         | Error Message                                                                                                                                                         | Reason                                                                                                                                                         |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400 invalid_credentials` | El NSS capturado no coincide con la CURP                                                                                                                              | The associated NSS does not match the CURP number.                                                                                                             |
| `400 login_error`         | El NSS no fue localizado en el IMSS                                                                                                                                   | The NSS number is not present in the IMSS system.                                                                                                              |
| `400 login_error`         | El CURP proporcionado no fue localizado en la entidad externa RENAPO                                                                                                  | The CURP was not found in the RENAPO system.                                                                                                                   |
| `400 login_error`         | CURP es incorrecto                                                                                                                                                    | The CURP is incorrect (might have a typo, not enough characters, or poorly formatted)                                                                          |
| `400 login_error`         | Por favor, ingresa un CURP válido. Debe contener 18 caracteres                                                                                                        | The CURP provided has more or less than 18 characters.                                                                                                         |
| `400 login_error`         | La persona no cuenta con NSS                                                                                                                                          | The individual does not have a *Número de Seguridad Social* (NSS) number.                                                                                      |
| `400 login_error`         | Los datos registrados en el IMSS asociados a la CURP, presentan alguna inconsistencia, por favor acude a tu Subdelegación para obtener tu Número de Seguridad Social. | There is an inconsistency with the information provided to login and what the institution has.                                                                 |
| `400 login_error`         | Es necesario que acudas a la subdelegación más cercana a tu domicilio a presentar tu trámite                                                                          | The user associated with the CURP needs to go to their nearest IMSS office in order to submit additional paperwork for the operation to be carried out.        |
| `400 login_error`         | El correo ya está registrado con otro CURP                                                                                                                            | The email address is already registered with another CURP.                                                                                                     |
| `403 forbidden_by_host`   | Has agotado el número de solicitudes permitidas por día.                                                                                                              | The user's CURP has been used more than three times to log in to the institution within a 24-hour period. We recommend you retry retrieving data the next day. |

# Wait for a webhook and get employment data

`<Employmentsmexicohistoricalwebhook />`

# Wait for a webhook and get owner data

`<Webhookownersguide />`
What’s Next
Tell your users what they should do after they've finished this page

Save
Copyright © 2020-2023 Belvo. All rights reserved

Legal notice Privacy policy Terms of service Cookie policy

Feedback


