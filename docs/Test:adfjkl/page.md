---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
Errors are annoying - we know. That's why we have dedicated articles for each error in our DevPortal to help you solve them. Have a look at the error below, or just search for the error code you are encountering to go straight to the causes as well as solutions. 

# Response Codes

We use the following HTTP status code in the response depending on the success or failure:

| Status Code | Description                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------- |
| `200`       | ✅ **Success** - The content is available in the response body.                              |
| `201`       | ✅ **Success** - The content was created successfully on Belvo.                              |
| `204`       | ✅ **Success** - No content to return.                                                       |
| `400`       | ❌ **Bad Request Error** - Request returned an error, detail in content.                     |
| `401`       | ❌ **Unauthorized** - The Belvo credentials provided are not valid.                          |
| `403`       | ❌ **Forbidden** - You don’t have the required permissions to perform this action.           |
| `404`       | ❌ **Not Found** - The resource you try to access cannot be found.                           |
| `405`       | ❌ **Method Not Allowed** - The HTTP method you are using is not accepted for this resource. |
| `408`       | ❌ **Request Timeout** - The request timed out and was terminated by the server.             |
| `428`       | ❌ **MFA Token Required** - MFA token was required by the institution to connect.            |
| `500`       | ❌ **Internal Server Error** - The detail of the error is available in the response body.    |

Belvo API errors are returned in JSON format. For example, an error might look like this:

```json
[
  {
    "request_id": "a6e1c493d7a29d91aed4338e6fcf077d",
    "message": "This field is required.",
    "code": "required",
    "field": "link"
  }
]
```

Typically, an error response will have the following parameters:

* `request_id`: a unique ID for the request, you should share it with the Belvo support team for investigations.
* `message`: human-readable description of the error.
* `code`: a unique code for the error. Check the table below to see how to handle each error code.
* `field` *(optional)*: The specific field in the request body that has an issue.

# General error handling notes

Here is our recommendation in terms of retry on errors: 

### 50x errors

Implement an automated exponential backoff of up to five retries. We recommend that you use a base interval of three seconds with a factor of two. For example, the first retry should be after three seconds, the second retry is after 6 seconds (2\*3), the third retry is after 12 seconds (2\*6), the fourth retry is after 24 seconds (2\*12), and the fifth retry is after 48 seconds (2\*24).

### 40x errors

You should not retry making requests if you get 40x response as this is a client error. 

The only exception is the “Too Many Sessions” error, as it means that your end-user is accessing the account from another browser at the same time. In this case, please implement the same retry policy as with 50x errors.

> 🚧 Store the request\_id
>
> When implementing your Belvo integration, make sure that you account for storing the `request_id` when you receive an error. This way, when you provide our engineers the ID, they can troubleshoot the issue quickly and get you back up and running.

# 400 activation\_failed

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | Institution |         No\*         |
|     Enrichment     | Institution |         No\*         |
| Payment Initiation | N/A         |          N/A         |

> 📘
>
> \* This error is not normally displayed in the widget. However, there are exceptions where it does reflect in the widget for some institutions such as BBVA in Mexico. Reach out to us at [support@belvo.com](mailto:support@belvo.com) if you have any questions.

```json
[
  {
    "code": "activation_failed",
    "message": "The credentials provided were not accepted by the institution.",
    "request_id": "3e7b283c6efa449c9c028a16b5c249gg"
  }
]
```

**Cause**

This error occurs when Belvo was unable to automatically activate the internet banking access for the user due to missing information (for example, the 🇲🇽 CVV or 🇲🇽 NIP were missing or incorrectly provided).

**Solution**

Ask the user to first activate their internet banking access (either by contacting the bank directly or attempting to log in to their internet banking account) and then ask them to connect their account again.

***

# 400 already\_exists

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | N/A        |          N/A         |
|     Enrichment     | N/A        |          N/A         |
| Payment Initiation | Request    |          No          |

```json
[
    {
        "field": "details",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "pix_key": {
            "value": {
                "message": "This `pix_key__value` already exists. It is linked to BankAccount: d5c8cb5f-7845-4a23-a1fa-76c7ae7e5e36",
                "code": "already_exists"
            }
        }
    }
]
```

**Cause**

You are trying to register a bank account providing a value that is already linked to a bank account registered in Belvo. This could include: 

* The PIX key identifier of the bank account
* The bank account number

```json Bank account request payload using PIX Keys
{
  "institution": "f512d996-583a-4a91-8b5b-eba2e103b068",
  "holder": {
    "type": "BUSINESS",
    "information": {
        "identifier_type": "CNPJ",
        "name": "Caetano Veloso Entertainment Universe",
        "identifier": "231.002.990-00"
          }
     },
   "details": {
        "country": "BRA",
                "pix_key": "RANDOM://6c1c236c-a035-4b80-ab12-e38f88ce82ab", // Pix key already registerted in Belvo.
     }
}
```
```json Bank account request payload using account information
{
  "institution": "f512d996-583a-4a91-8b5b-eba2e103b068",
  "holder": {
    "type": "BUSINESS",
    "information": {
        "identifier_type": "CNPJ",
        "name": "Caetano Veloso Entertainment Universe",
        "identifier": "231.002.990-00"
          }
     },
   "details": {
        "country": "BRA",
        "account_type": "CHECKINGS",
        "agency": "0444",
        "number": "45722-01" // Account number already registred in Belvo.
     }
}
```

**Solution**

Make a [Get all bank accounts](https://belvo-payments-api.readme.io/reference/listbankaccounts) request to receive a list of all the bank accounts you have registered, filtering the results by the last four bank account digits to get the details.

***

# 400 blank

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json
[
    {
        "field": "institution",
        "request_id": "b9abda13c9afbbc64a265c6d4f937d06",
        "message": "This field may not be blank.",
        "code": "null"
    }
]
```

**Cause**

You sent a request with an empty string for a required field. For example:

```json
{
    "institution": "", // This field is required and cannot be an empty string.
    "username": "bnk100",
    "password": "full",
}
```

**Solution**

* Check the error message to see which field you need to provide. If you're not sure what information to provide or the format, just check our API reference documentation.

***

<br />

# 400 cancellation\_error

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
| Payment Initiation | Request    |          No          |

```json Not a scheduled payment
[
    {
        "request_id": "b9abda13c9afbbc64a265c6d4f937d06",
        "message": "Payment Intent cannot be canceled because it is not SCHEDULED",
        "code": "cancellation_error"
    }
]
```
```json Cancelling past cutoff time
[
    {
        "request_id": "b9abda13c9afbbc64a265c6d4f937d06",
        "message": "Payment Intent cannot be canceled as the cutoff time (23:59:00) has passed.",
        "code": "cancellation_error"
    }
]
```

**Cause**

This error can occur when:

* You attempted to [cancel a payment intent](https://developers.belvo.com/reference/cancelpaymentintentbrazil) that was not scheduled.
* You sent through your cancellation request past the 23:59:00 (GMT-3) cutoff time the day before the scheduled settlement date.

***

# 400 does\_not\_exist

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          No          |
|  Enrichment | Request    |          No          |

```json
[
    {
        "field": "institution",
        "request_id": "744da6621cb09b3cbb8271d89fe09060",
        "message": "Object with name=narnia does not exist.",
        "code": "does_not_exist"
    }
]
```

**Cause**

You sent a request where you provided a value that doesn't exist in the Belvo database. For example:

```json
{
    "institution": "narnia", // This institution does not exist in the Belvo database.
    "username": "bnk100",
    "password": "full"
}
```

**Solution**

Check the error message to see in which field you provided an incorrect value. Then:

* Make sure that you haven't made any typos.
* Check if the value you are providing should be present in our database (for example, if you make a request for a link that wasn't registered yet, you will receive an error).

***

# 400 duplicated

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          Yes         |
|  Enrichment | Request    |          No          |

```json
[
    {
        "request_id": "744da6621cb09b3cbb8271d89fe09060",
        "message": "Link already exists",
        "code": "duplicated",
        "institution_user_id": "4jlgn6vL7yifxMlhwFwTjbbzYxYoEEkJqK_CJhhZetI="
    }
]
```

**Cause**

This error can occur when:

* You tried to create a link that has already been associated with your account.
* Your user tried to create a link with an account they have already connected.

<Image alt="Error message displayed to the user in the widget" align="center" width="300px" src="https://files.readme.io/1356fb7-WgErrorCode_1.png">
  Error message displayed to the user in the widget
</Image>

**Solution**

You can either:

* Query your database to find the `institution_user_id` and check whether the link associated link `id` is still valid using the [Get a link's details](https://developers.belvo.com/reference/detaillink) request. If the `status` is not `valid`, then prompt your user to update their credentials by using the the [Belvo widget in update mode](https://developers.belvo.com/docs/connect-widget-update-mode).
* Query your database to find the `institution_user_id` and use the associated link `id` to delete the link from the Belvo database using the [Delete a link request](https://developers.belvo.com/reference/destroylink). Once you have deleted the link, you can ask your user to connect their account again.

***

# 400 null

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          No          |
|  Enrichment | Request    |          No          |

```json
[
    {
        "field": "institution",
        "request_id": "b9abda13c9afbbc64a265c6d4f937d06",
        "message": "This field may not be null.",
        "code": "null"
    }
]
```

**Cause**

You made a request without providing data in a required field.  For example:

```json
{
    "institution": , // This field is required.
    "username": "bnk100",
    "password": "full",
}
```

**Solution**

Check the error message to see which field you need to provide. If you're not sure what information to provide or the format, just check our API reference documentation.

***

# 400 required

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json Missing required username field
[
    {
        "field": "username",
        "request_id": "b9abda13c9afbbc64a265c6d4f937d06",
        "message": "This field is required.",
        "code": "required"
    }
]
```
```json Missing required amount field
[
    {
        "field": "amount",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "message": "This field is required.",
        "code": "required"
    }
]
```

**Cause**\
You sent a request without a required field. For example:

```json Registering a new link request
{
    "institution": "erebor_mx_retails",
            // When you are registering a new link, you must provide a username.
    "password": "full"
}
```
```json Creating a payment link request
{
     "allowed_payment_method_types": [
          "pse"
     ],
     "payment_method_details": {
          "pse": {
               "beneficiary_bank_account": "a80d5a9d-20ae-479a-8dd7-ff3443bcbbfc"
          }
     },
     "callback_urls": {
          "cancel": "https://www.acmecorp.com/checkout/3487548/cancel",
          "success": "https://www.acmecorp.com/checkout/3487548/success"
     },
           // When you are creating a payment link, you must provide an payment amount.
     "customer": "06dc2f14-1217-4480-9b36-550a944a39d1",
     "description": "Awesome training Sneaker",
     "provider": "payments_way"
}
```

**Solution**

* Check the error message to see which field you need to provide. If you're not sure what information to provide or the format, just check our API reference documentation.

***

# 400 institution\_down

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | Institution |          Yes         |
|     Enrichment     | Institution |          Yes         |
| Payment Initiation | N/A         |          N/A         |

```json
[
  {
    "code": "institution_down",
    "message": "The financial institution is down, try again later",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error occurs when the institution's website that you're trying to access is down due to maintenance or other issues, which means Belvo is unable to create new links or retrieve new data. 

**Solution**

You can retry accessing the institution later. Make sure to subscribe to our [Institutions Status Page](https://institutions.belvo.com/) to know as soon as an institution is unavailable.

You can remove an institution that is currently not available by using the [`institutions` parameter in the startup configuration](https://developers.belvo.com/docs/widget-startup-configuration#select-one-or-more-institutions-to-display) and omitting the institution from the list. 

**Widget error message**

| Language            | Error title          | Error description                                                                                                                     |
| ------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | Something went wrong | The institution you tried to access is temporarily unavailable. Please come back in a bit and we will be able to process your request |
| 🇧🇷 <br/>Portuguese | Ocorreu um erro      | Esta instituição está temporariamente inacessível. Tente novamente mais tarde e poderemos processar sua solicitação                   |
| 🇪🇸 <br/>Spanish    | Ha habido un error   | Esta institución está temporalmente inaccesible. Por favor, inténtalo de nuevo más tarde y podremos procesar tu petición              |

***

# 400 institution\_inactive

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | Institution |          Yes         |
|     Enrichment     | Institution |          Yes         |
| Payment Initiation | N/A         |          N/A         |

```json
[
  {
    "code": "institution_inactive",
    "message": "The institution has been temporarily deactivated",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error occurs when we (Belvo) have deactivated the institution in our API. 

**Solution**

You can retry later, once Belvo has reactivated the institution.

***

# 400 institution\_unavailable

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | Institution |          Yes         |
|     Enrichment     | Institution |          Yes         |
| Payment Initiation | N/A         |          N/A         |

```json
[
  {
    "code": "institution_unavailable",
    "message": "The financial institution is unavailable",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error occurs when the institution's website that you're trying to access is down due to maintenance or other issues, which means Belvo is unable to create new links or retrieve new data. 

**Solution**

You can retry accessing the institution later. Make sure to subscribe to our [Institutions Status Page](https://institutions.belvo.com/) to know as soon as an institution is unavailable.

You can remove an institution that is currently not available by using the [`institutions` parameter in the startup configuration](https://developers.belvo.com/docs/widget-startup-configuration#select-one-or-more-institutions-to-display) and omitting the institution from the list. 

**Widget error message**

| Language            | Error title          | Error description                                                                                                                      |
| ------------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | Something went wrong | The institution you tried to access is temporarily unavailable. Please come back in a bit and we will be able to process your request. |
| 🇧🇷 <br/>Portuguese | Ocorreu um erro      | O serviço está temporariamente inacessível. Tente novamente mais tarde e poderemos processar sua solicitação                           |
| 🇪🇸 <br/>Spanish    | Ha habido un error   | Esta institución está temporalmente inaccesible. Por favor, inténtalo de nuevo más tarde y podremos procesar tu petición               |

***

# 400 invalid

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json Wrong date format example
[
    {
        "field": "date_to",
        "request_id": "a7ad9a4ad8b13f8f800f8f5b69c7856f",
        "message": "Date has wrong format. Use one of these formats instead: YYYY-MM-DD.",
        "code": "invalid"
    }
]
```
```json Wrong UUID format example
[
    {
        "field": "link",
        "request_id": "448f2b58fc88b2c5a9db6c9175494950",
        "message": "“YTZjMDA3YjktZTk5Yy00MDczLTgzNGItOGM3NzA1MTMyZGU3” is not a valid UUID.",
        "code": "invalid"
    }
]
```
```json Wrong terminal_id format example
[
    {
        "field": "payments_way",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "terminal_id": [
            {
                "message": "The terminal_id is invalid, try again or contact Belvo's support.",
                "code": "invalid"
            }
        ]
    }
]
```
```json Wrong form_id format example
[
    {
        "field": "payments_way",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "form_id": [
            {
                "message": "The form_id is invalid, try again or contact Belvo's support.",
                "code": "invalid"
            }
        ]
    }
]
```
```json Incorrect resources for fetch_resources
[
    {
        "field": "resources",
        "request_id": "a7ad9a4ad8b13f8f800f8f5b69c7856f",
        "message": "The institution only supports the following resources: {1}, {2}",
        "code": "invalid"
    }
]
```

**Cause**

You sent a request where you provided a value in an invalid format. This could include:

* The format of the login credentials is incorrect.
* The date format is incorrect.
* The UUID is not valid.
* The terminal\_id is not valid.
* The form\_id is not valid.
* The resources you've included in `fetch_resources` are not supported by the institution.

For example:

```json Wrong date format request example
{
    "link": "a6c007b9-e99c-4073-834b-8c7705132de7",
    "date_from": "2020-01-01",
    "date_to": "2020-02" // Here, the date format must be YYYY-MM-DD
}
```
```json Wrong UUID format request example
{
    "link": "a6c007b9-e99c" // Here, the link ID is not a valid UUID.
}
```
```json Wrong terminal_id and form_id format example
{
     "holder": {
          "type": "BUSINESS",
          "information": {
               "name": "Trusty documentation services"
          }
     },
     "providers": {
          "payments_way": {
               "terminal_id": "1200", // Belvo provides you with the correct terminal_id you need to create a bank accont.
               "form_id": "3211", // Belvo provides you with the correct form_id you need to create a bank accont.
          }
     },
}
```

**Solution**

Check the error message to see which field is invalid and why. Then, if you need more information, check our API docs to know what the valid format for the field is.

***

# 400 invalid\_choice

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          No          |
|  Enrichment | Request    |          No          |

```json
[
    {
        "field": "access_mode",
        "request_id": "ce49b6af6710bb0c7a2a456c223dde21",
        "message": "\"Dominik\" is not a valid choice.",
        "code": "invalid_choice"
    }
]
```

**Cause**\
You made a request where in one of the fields you provided a value that wasn't valid (for example, it may only accept certain strings, much like an enum). For example:

```json
{
    "institution": "erebor_mx_retail",
    "username": "bnk100",
    "password": "full",
    "access_mode": "Australia" // This is not a valid choice, as in the documentation it states that it is an enum: single or recurrent
}
```

**Solution**

* Check the error message to see in which field you provided an incorrect value. Then check our documentation to see what value you should provide for this field.

***

# 400 invalid\_credentials\_storage

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          No          |
|  Enrichment | Request    |          No          |

```json
[
    {
        "request_id": "ce49b6af6710bb0c7a2a456c223dde21",
        "message": "Recurrent links must store the credentials",
        "code": "invalid_credentials_storage"
    }
]
```

**Cause**\
You made a request where for a recurrent link you set the `credentials_storage` parameter to `nostore` or to a date range between `1d` to `365d`.

```json
{
    "institution": "tatooine_mx_fiscal",
    "username": "PFIS010101000",
    "password": "individual",
    "access_mode": "recurrent",
    "credentials_storage": "nostore" // For recurrent links, this must be set to store
}
```

**Solution**

* If you want to create a recurrent link, change the value of `credentials_storage` to `store`.
* If you want to create a single link and not store credentials, change the `access_mode` to `single`.

***

# 400 invalid\_fetch\_resources

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          No          |
|  Enrichment | Request    |          No          |

```json
[
    {
        "request_id": "ce49b6af6710bb0c7a2a456c223dde21",
        "message": "Single links without stored credentials must fetch resources",
        "code": "invalid_fetch_resources"
    }
]
```

**Cause**\
You attempted to create a link where you set the`credentials_storage` parameter to `nostore`  and did not pass any resources in the `fetch_resources` parameter. For links where we don't store credentials, you must pass at least one resource in`fetch_resources`. 

```json
{
    "institution": "tatooine_mx_fiscal",
    "username": "PFIS010101000",
    "password": "individual",
    "access_mode": "recurrent",
    "credentials_storage": "nostore",
  	"fetch_resources": []
}
```

**Solution**

List the resources you want to retrieve in the `fetch_resources` parameter. For example: `"fetch_resources": ["ACCOUNTS", "OWNERS", "TRANSACTIONS"]` .

***

# 400 invalid\_link

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Link       |          No          |
|     Enrichment     | Link       |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
  {
    "code": "invalid_link",
    "message": "The link has been invalidated. You may need to update link credentials",
    "request_id": "9b7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error when you try to access an account but the user credentials are no longer valid, prompting an error from the institution.

> 📘
>
> A Link's status changes from `valid` to `invalid` after six unsuccessful POST requests.

**Solution**

Ask your user to provide their updated credentials. To make things easier, we highly recommend you use our [Widget in Update Mode](https://developers.belvo.com/docs/connect-widget-update-mode).

***

# 400 invalid\_period

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "The number of days between date_from and date_to must be at least 90 days",
        "code": "invalid_period",
        "request_id": "a66a4fdae4ab8cfc1ed9ee9246aa6890"
    }
]
```

**Cause**

This error occurs when you request incomes for a link within a given date range, however, the period between `date_from` and `date_to` is less than 90 days.

**Solution**

Make sure that the period between `date_from` and `date_to` is equal to or greater than 90 days.

***

# 400 login\_error

> ❗️We are currently refining our `login_error` messages to provide greater granularity and improve troubleshooting. 

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Link       |          Yes         |
|  Enrichment | Link       |          Yes         |

```json Invalid credentials
[
  {
    "code": "login_error",
    "message": "Invalid credentials provided to login to the institution",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Unsupported MFA token
[
  {
    "code": "login_error",
    "message": "A MFA token is required by the institution, but it’s not supported yet by Belvo.",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Unexpected error while logging in
[
  {
    "code": "login_error",
    "message": "Impossible to login, something unexpected happened while logging into the institution. Try again later.",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Invalid credentials
[
  {
    "code": "login_error",
    "message": "Login not attempted due to invalid credentials",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Missing credentials
[
  {
    "code": "login_error",
    "message": "Missing credentials to login to the institution",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Institution login error
[
  {
    "code": "login_error",
    "message": "The user account access was forbidden by the institution",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json User access forbidden
[
  {
    "code": "login_error",
    "message": "The user account access was forbidden by the institution",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```
```json Account locked
[
  {
    "code": "login_error",
    "message": "The user account is locked, user needs to contact the institution to unlock it",
    "request_id": "3e7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error can occur when:

* the credentials that your user provides are incorrect or missing. 
* the MFA token your user provides is not supported by Belvo
* there is an issue with the institution that prevents logins.
* the user's account is either locked or the user does not have permission to access their internet banking.

**Solution**

* Ask your user to provide their correct credentials or MFA token. Use our widget to make it even easier (we do all the heavy lifting for you).
* Ask your user to confirm with their bank that their account is active and that it isn't blocked.
* If there is an issue with the institution, try logging in at a later time.

***

# 400 max\_digits

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | N/A        |          N/A         |
|     Enrichment     | N/A        |          N/A         |
| Payment Initiation | Request    |          No          |

```json Wrong amount format
[
    {
        "field": "amount",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "message": "Ensure that there are no more than 12 digits in total.",
        "code": "max_digits"
    }
]
```

**Cause**\
You sent a request with the wrong amount format. For example:

```json Create payment link with wrong amount format
{
     "allowed_payment_method_types": [
          "pse"
     ],
     "payment_method_details": {
          "pse": {
               "beneficiary_bank_account": "a80d5a9d-20ae-479a-8dd7-ff3443bcbbfc"
          }
     },
     "callback_urls": {
          "cancel": "https://www.acmecorp.com/checkout/3487548/cancel",
          "success": "https://www.acmecorp.com/checkout/3487548/success"
     },
     "amount": 10000000000000000000,
     "customer": "06dc2f14-1217-4480-9b36-550a944a39d1",
     "description": "Awesome training Sneaker",
     "provider": "payments_way"
}
```

**Solution**

Check the error message to see why the amount format is invalid. If you're not sure what information to provide or the format, just check our API reference documentation to know what the valid format for the field is.

***

# 400 max\_decimal\_places

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | N/A        |          N/A         |
|     Enrichment     | N/A        |          N/A         |
| Payment Initiation | Request    |          No          |

```json Wrong amount format
[
    {
        "field": "amount",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "message": "Ensure that there are no more than 2 decimal places.",
        "code": "max_decimal_places"
    }
]
```

**Cause**\
You sent a request with the wrong amount format. For example:

```json Create payment link with wrong amount format
{
     "allowed_payment_method_types": [
          "pse"
     ],
     "payment_method_details": {
          "pse": {
               "beneficiary_bank_account": "a80d5a9d-20ae-479a-8dd7-ff3443bcbbfc"
          }
     },
     "callback_urls": {
          "cancel": "https://www.acmecorp.com/checkout/3487548/cancel",
          "success": "https://www.acmecorp.com/checkout/3487548/success"
     },
     "amount": 10.123,
     "customer": "06dc2f14-1217-4480-9b36-550a944a39d1",
     "description": "Awesome training Sneaker",
     "provider": "payments_way"
}
```

**Solution**

Check the error message to see why the amount format is invalid. If you're not sure what information to provide or the format, just check our API reference documentation to know what the valid format for the field is.

***

# 400 min\_value

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | N/A        |          N/A         |
|     Enrichment     | N/A        |          N/A         |
| Payment Initiation | Request    |          No          |

```json Wrong amount format
[
    {
        "field": "amount",
        "request_id": "a0c3b0e58e58409d9b1d49de9be35a3d",
        "message": "Ensure this value is greater than or equal to 0.01.",
        "code": "min_value"
    }
]
```

**Cause**\
You sent a request with the wrong amount format. For example:

```json Create payment link with wrong amount format
{
     "allowed_payment_method_types": [
          "pse"
     ],
     "payment_method_details": {
          "pse": {
               "beneficiary_bank_account": "a80d5a9d-20ae-479a-8dd7-ff3443bcbbfc"
          }
     },
     "callback_urls": {
          "cancel": "https://www.acmecorp.com/checkout/3487548/cancel",
          "success": "https://www.acmecorp.com/checkout/3487548/success"
     },
     "amount": 0.12,
     "customer": "06dc2f14-1217-4480-9b36-550a944a39d1",
     "description": "Awesome training Sneaker",
     "provider": "payments_way"
}
```

**Solution**

Check the error message to see why the amount format is invalid. If you're not sure what information to provide or the format, just check our API reference documentation to know what the valid format for the field is.

***

# 400 not\_a\_list

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json
[
    {
        "message": 'Expected a list but got type "str".',
        "code": "not_a_list",
        "request_id": "d5af76cc66e0231e2be7f7be5c41170a"
    }
]
```

**Cause**\
You sent a request where instead of sending an array of data, you sent through just a list. For example:

```json Incorrect Example
{
    "fetch_resources": "ACCOUNTS,OWNERS", // Here, fetch_resources has to be an array of values
}
```
```json Correct Example
{
    "fetch_resources": ["ACCOUNTS","OWNERS"],
}
```

**Solution**

Check your JSON request and consult our documentation to see which field should be an array. 

***

# 400 parse\_error

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json
[
    {
        "message": "JSON parse error - Expecting property name enclosed in double quotes: line 3 column 1 (char 54)",
        "code": "parse_error",
        "request_id": "d5af76cc66e0231e2be7f7be5c41170a"
    }
]
```

**Cause**\
You sent a request with invalid JSON. For example:

```json
{
    "link": "a6c007b9-e99c-4073-834b-8c7705132de7", // Here, you should not have a trailing comma in your request
}
```

**Solution**

Check the JSON payload (perhaps you're just missing a comma or quotation mark) and try again.

***

# 400 session\_expired

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          Yes         |
|  Enrichment | Request    |          Yes         |

```json
[
  {
    "code": "session_expired",
    "message": "The session you are trying to resume has expired, please start again from register/retrieve endpoint",
    "request_id": "6e7b283c6efa449c9c028a16b5c249fa"
  }
]
```

**Cause**

This error occurs when you try to resume a request session that has already expired. This is usually because the user took too long to provide their authentication token.

> For requests that require a token, there is a period of time where the user can provide their token. The period varies from institution to institution. You can check how much time the user has to enter their token by using the `expiry` parameter in the 428 `token_required` response.

**Solution**

Unfortunately, you'll need to start the entire login process with your user again.

**Widget error message**

| Language            | Error title                     | Error description                                                                              |
| ------------------- | ------------------------------- | ---------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | Please try again!               | Please try again to link your account as the session with this institution just expired        |
| 🇧🇷 <br/>Portuguese | Por favor, faça login novamente | A sessão com essa instituição expirou. Por favor, digite suas credenciais novamente            |
| 🇪🇸 <br/>Spanish    | Por favor, ingresa de nuevo     | Por favor, ingresa de nuevo tus credenciales ya que la sesión con esta institución ha expirado |

***

# 400 session\_expired\_ob

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Request    |          Yes         |

```json
[
  {
    "code": "session_expired_ob",
    "request_id": "6e7b283c6efa449c9c028a16b5c249fa"
  }
]
```

**Cause**

You can receive this error due to the following reasons:

1. The `access_token` you generated was not used within the 10 minute expiration period.
2. Instead of generating a new `access_token` for the widget for the given user, you used an `access_token` generated for another user that already created a link using the widget.
3. Your user did not click on the **Ir para a instituição** (Go to the institution) button in the widget within 60 seconds of the screen appearing.

**Solution**

Unfortunately, you'll need to start the widget process with your user again. Please make sure that you:

1. Ensure that you use the `access_token` to generate the widget as soon as it is created. If 10 minutes or more pass, you will need to create a new `access_token`.
2. Ensure that you always create a new `access_token` for every user.
3. Our UX team is improving the flow so as to prompt the user to continue the flow within the allotted 60 seconds.

**Widget error message**

| Language            | Error title     | Error description                                                                          |
| ------------------- | --------------- | ------------------------------------------------------------------------------------------ |
| 🇬🇧 <br/>English    | Session expired | Your connection session expired, please refresh the page to try again to link your account |
| 🇧🇷 <br/>Portuguese | Sessão expirada | Sua sessão expirou, atualize a página e tente vincular sua conta novamente.                |

***

# 400 too\_many\_sessions

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Link       |          Yes         |
|     Enrichment     | Link       |          Yes         |
| Payment Initiation | Link       |          Yes         |

```json
[
	{
		"code": "too_many_sessions",
		"message": "Impossible to login, a session is already opened with the institution for these credentials",
		"request_id": "3e7b283c6efa449c9c028a16b5c249fd"
	}
]
```

**Cause**

This error occurs when:

* a user is attempting to log in to their institution via Belvo while also already being logged in to their institution on a web browser or mobile app.
* you make a request for information while Belvo is scraping data from the institution for that user.

**Solution**

Try:

* Informing your user to close their web and app sessions for the given institution.
* Waiting 120 seconds and retrying your request, ensuring that Belvo has finished the data scraping process.  

**Widget error message**

| Language            | Error title                  | Error description                                                                                                                                                         |
| ------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | A session is already open    | It seems you are logged in to your account with another device. This institution only allows one logged in session at a time. Log out and try linking your account again. |
| 🇧🇷 <br/>Portuguese | Muitas sessões abertas       | Parece que já existe uma sessão aberta nesta instituição com seu usuário. Esta instituição permite apenas uma sessão aberta por vez                                       |
| 🇪🇸 <br/>Spanish    | Demasiadas sesiones abiertas | Parece que ya hay una sesión abierta en esta institución con tu usuario. Esta institución solo permite una sesión abierta a la vez.                                       |

***

# 400 unavailable\_data

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | N/A        |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "The institution did not return any data for the request.",
        "code": "unavailable_data",
        "request_id": "c76f4d0320b923eb3068f5e2c0fab18f"
    }
]
```

**Cause**

This error occurs when your request was correctly formed and sent, however, the institution did not return any data for your request.

**Solution**

We recommend first checking our <a href="https://institutions.belvo.com/" target="_blank">Institution Status Page</a> to see if there is any incident with the institution that is prohibiting data extraction. If no incidents are active for the institution, you can retry the request.  If you keep getting this error, <a href="https://support.belvo.com/hc/en-us/requests/new" target="_blank">contact our support team</a>, making sure to include the `request_id` that you receive in the message.

***

# 400 unconfirmed\_link

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Link       |          No          |
|     Enrichment     | Link       |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "The link creation has not been completed yet",
        "code": "unconfirmed_link",
        "request_id": "c76f4d0320b923eb3068f5e2c0fab18f"
    }
]
```

**Cause**

This error occurs when you try to access a link that was paused previously (and as such is not active now).

> 📘
>
> A Link's status is set to `unconfirmed_link` when your user has not completed the Link creation process successfully (for example, they might not provide a valid MFA token).

**Solution**

Ask your user to provide an MFA token through our [widget in update mode](https://developers.belvo.com/docs/connect-widget-update-mode) to complete a first login. After the user successfully completes the process, you will be able to retrieve data.

***

# 400 unsupported\_operation

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | N/A        |          N/A         |

```json Resource not supported
[
    {
        "message": "The resource you are trying to access is not supported by this institution",
        "code": "unsupported_operation",
        "request_id": "a66a4fdae4ab8cfc1ed9ee9246aa6890"
    }
]
```
```json fetch_historical required
[
    {
        "message": "For single links, you must set fetch_historical to true when using the resources request parameter.",
        "code": "unsupported_operation",
        "request_id": "a66a4fdae4ab8cfc1ed9ee9246aa6890"
    }
]
```

**Cause**

This error occurs when:

* You try to access some data operation that Belvo does not support for an institution. For example, trying to access the **Transactions** resource for Fiscal institutions.
* You make a request that requires some business logic to be completed. For example, when using the `fetch_resources` parameter on single link creation, you must also set `fetch_historical` to true

**Solution**

Make sure that:

* The resource operation (for example requesting Transactions) is supported for that institution (check our [institutions](https://developers.belvo.com/docs/institution) guide).
* Your request fulfills all the required business logic.

**Widget error message**

| Language            | Error title          | Error description                                                                                                                     |
| ------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | Something went wrong | There was an error with your request. Please try again, and if the problem persists, we will try to fix it as soon as possible        |
| 🇧🇷 <br/>Portuguese | Ocorreu um erro      | Ocorreu um erro com a sua solicitação. Tente novamente e, se o problema persistir, o corrigiremos o mais breve possível               |
| 🇪🇸 <br/>Spanish    | Ha habido un error   | Hemos tenido un error con tu petición. Por favor, inténtalo de nuevo y si el problema persiste, lo arreglaremos lo más pronto posible |

***

# 400 validation\_error

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "Bad request",
        "code": "validation_error",
        "request_id": "e912d014d7976c3172bb8e65c7a22194"
    }
]
```

**Cause**

You sent a request where:

* The credentials provided did not match the expected fields, leading to a field validation error from the institution.

For example:

```json Period exceeds 365 days example
{
    "link": "a6c007b9-e99c-4073-834b-8c7705132de7",
    "date_from": "2020-01-01",
    "date_to": "2021-03-30" // Between date_from and date_to there are more than 365 days
}
```

**Solution**

Get the details for the institution using our [Institutions endpoint](https://docs.belvo.com/#operation/DetailInstitution) and check the `form_fields` object for information on what fields need to be provided and their format.

***

# 401 authentication\_failed

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "Invalid Secret Keys",
        "code": "authentication_failed",
        "request_id": "5c09677ecf78e1d4501547252a0c4e77"
    }
]
```

**Cause**

This error occurs when you try to make an API call using incorrect Belvo API credentials (either your secret key or secret password, or both, are incorrect).

**Solution**

Check the credentials that you are using against the ones in your dashboard. Perhaps you're using your sandbox credentials to access production data (or vice versa).  Note: If you're unsure about your secretPassword, check the confirmation email that you received from Belvo. 

***

# 401 consent\_without\_accounts

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | N/A        |          N/A         |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "Information cannot be retrieved as the consent has no associated accounts",
        "code": "consent_without_accounts",
        "request_id": "5c09677ecf78e1d4501547252a0c4e77"
    }
]
```

**Cause**

This error occurs when your user has removed accounts associated with the consent they provided. For example, when your user first generated their consent, they had a checking and a loan account at the institution but has closed those accounts since then.

**Solution**

Reach out to your user to confirm whether they have removed their account and ask them to generate a new consent at their current institution.

***

# 403 access\_to\_production\_denied

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | Belvo      |          No          |

```json
[
    {
        "message": "You don’t have access to production API.",
        "code": "access_to_production_denied",
        "request_id": "d5af76cc66e0231e2be7f7be5c41170a"
    }
]
```

**Cause**

This error occurs when you try to access Belvo's production environment without the correct permissions.

**Solution**\ <a href="https://belvo.com/contact/?utm_source=documentation" target="_blank">Contact our sales team</a> to request access to production environment.

***

# 403 access\_to\_resource\_denied

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "You don't have access to this resource.",
        "code": "access_to_resource_denied",
        "request_id": "d5af76cc66e0231e2be7f7be5c41170a"
    }
]
```

**Cause**

This error occurs when you try to access a Belvo's resource without the correct permissions.

**Solution**\ <a href="https://belvo.com/contact/?utm_source=documentation" target="_blank">Contact our sales team</a> to request access to this resource.

***

# 403 Forbidden

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Belvo      |          No          |
|  Enrichment | Belvo      |          No          |

```html
<html><head><title>403 Forbidden</title></head><body>

<center><h1>403 Forbidden</h1></center>

<hr><center>openresty/1.15.8.2</center>

</body></html>
```

**Cause**

This error occurs when you make a large volume of requests (over 80 requests in 30 seconds) in quick succession from the same IP address.

**Solution**

If you expect to consistently have large volumes of calls from the same IP address, please reach our to our Customer Success team. 

***

# 403 permission\_denied

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | Belvo      |          No          |

**Cause**

This error occurs when we (Belvo) are forbidden to access a certain resource in the institution, or you have exceeded your request limit.

**Solution**\
If you were able to access this resource previously, retry later. We (Belvo) actively monitor these errors and assign engineers to correct the situation as soon as possible.

***

# 403 quota\_limit\_reached

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | N/A        |          N/A         |

```json
[
    {
        "message": "The quota limit has been reached.",
        "code": "quota_limit_reached",
        "request_id": "1d1c4f427dac394a96c3fa49568f2a38"
    }
]
```

> 📘
>
> The `quota_limit_reached` is only applicable for the development environment.

**Cause**

This error occurs when you have exceeded the Link limit in the development environment.

**Solution**

To keep using the development environment, you need to delete enough Links to be below the environment's limit.

***

# 404 not\_found

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Request    |          No          |
|     Enrichment     | Request    |          No          |
| Payment Initiation | Request    |          No          |

```json Object not found
[
    {
        "message": "Not found.",
        "code": "not_found",
        "request_id": "1d1c4f427dac394a96c3fa49568f2a38"
    }
]
```
```json Credential not found
[
    {
        "message": "The credentials of this link have expired",
        "code": "expired_credentials",
        "request_id": "4d3de3930431496799eafc5c91e5bcfe"
    }
]
```

**Cause**

You made a request where you:

* provided the wrong URL.
* used an ID (for a link, account, transaction, and so on) that is not associated with your Belvo account.
* made a request for a link where the `credentials_storage` was set to `no_store` or to `30d`, and Belvo no longer has these credentials stored to retrieve information.

**Solution**

Make sure that:

* You are using the correct URL (check for typos and our API reference documentation).
* You are using an ID that is associated with your Belvo account.

In the case where the link was created with the `credentials_storage` was set to `no_store` or `30d`, you'll need to ask the user to re-connect their account.

***

# 405 method\_not\_allowed

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | Belvo      |          No          |

```json
[
    {
        "message": "Method \"PATCH\" not allowed.",
        "code": "method_not_allowed",
        "request_id": "8ea4cd36ad39db3823b89b31aea74581"
    }
]
```

**Cause**

This error occurs when you try to use an API method that is not allowed for the given resource (for example, a PATCH request for Fiscal endpoints).

**Solution**

Double check what methods are allowed for the given resource in our API Reference Documentation.

***

# 408 request\_timeout

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          No          |
|     Enrichment     | Belvo      |          No          |
| Payment Initiation | Belvo      |          No          |

```json
[
  {
    "code": "request_timeout",
    "message": "The request timed out, you can retry asking for less data by changing your query parameters",
    "request_id": "5c7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

Belvo has a limit regarding the time it takes to log in, retrieve account data, and log out, which is set to five (5) minutes. A timeout occurs when there is a very large amount of data and everything could not be obtained within the allotted time.

> For example, if an account has more than 2000 transactions per account per month, you may receive a `request_timeout` error.

**Solution**

When a timeout occurs, our API still saves as much data as it could retrieve. So, you can try making the same request again and recover all the data successfully. 

If you keep receiving timeout errors for several links, or three timeouts for the same link, report it to Belvo and provide the `request_id`s.

**Widget error message**

| Language            | Error title                      | Error description                                                                                                                            |
| ------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 🇬🇧 <br/>English    | The connection has timed out     | The response took too long and the connection could not be established successfully. Please try again in a few minutes.                      |
| 🇧🇷 <br/>Portuguese | Tempo limite de conexão atingido | O tempo de resposta está demorando mais do que o normal e a conexão não pode ser estabelecida. Por favor, tente novamente em alguns minutos. |
| 🇪🇸 <br/>Spanish    | La conexión ha expirado          | El tiempo de respuesta ha sido demasiado largo y la conexión no se ha podido establecer. Por favor, inténtalo de nuevo en unos minutos.      |

***

# 428 activation\_required

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | Institution |          No          |
|     Enrichment     | Institution |          No          |
| Payment Initiation | N/A         |          N/A         |

```json
[
  {
    "code": "activation_required",
    "message": "This user doesn't have web access activated yet.",
    "request_id": "3e7b283c6efa449c9c028a16b5c249jk"
  }
]
```

**Cause**

This error occurs when the user has not activated their internet banking access.

**Solution**

Ask the user to first activate their internet banking access and then ask them to connect their account again.

***

# 428 token\_required

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Link       |          Yes         |
|  Enrichment | Link       |          Yes         |

```json
[
  {
    "code": "token_required",
    "message": "A MFA token is required by the institution to login",
    "request_id": "8c7b283c6efa449c9c028a16b5c249fa",
    "session": "2675b703b9d4451f8d4861a3eee54449",
    "expiry": 9600,
    "link": "30cb4806-6e00-48a4-91c9-ca55968576c8",
    "token_generation_data": {
      "instructions": "Use this code to generate the token",
      "type": "numeric",
      "value": "12345"
    }
  }
]
```

**Cause**

This error occurs when the institution requires MFA to log in. 

**Solution**

See our article on how to handle MFA. However, we highly recommend you use our Connect Widget as we'll handle these types of errors for you and walk your user through the steps to provide their authentication token.

**Widget error message**

In the case that your user incorrectly enters their token (or the token they enter is expired) while using the widget, the following error messages are displayed:

| Language            | Error title    | Error description                                                              |
| ------------------- | -------------- | ------------------------------------------------------------------------------ |
| 🇬🇧 <br/>English    | Invalid token  | It looks like the token has expired, generate a new one and try again.         |
| 🇧🇷 <br/>Portuguese | Token inválido | É provável que o token tenha expirado, gere um novo e tente novamente          |
| 🇪🇸 <br/>Spanish    | Token inválido | Es probable que el token haya caducado, genera uno nuevo y vuelve a intentarlo |

***

# 500 service\_unavailable

|     API     | Error type | Reflected in widget? |
| :---------: | :--------- | :------------------: |
| Aggregation | Belvo      |          No          |
|  Enrichment | Belvo      |          No          |

```json
[
  {
    "code": "service_unavailable",
    "message": "Belvo is unable to process the request due to an internal system issue or to an unsupported response from an institution",
    "request_id": "4a7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error occurs when we (Belvo) have encountered an internal system error (sorry about that).

**Solution**

You can retry later. If you keep getting this error, <a href="https://support.belvo.com/hc/en-us/requests/new" target="_blank">contact our support team</a>, making sure to include the `request_id` that you receive in the message. 

***

# 500 unexpected\_error

|         API        | Error type | Reflected in widget? |
| :----------------: | :--------- | :------------------: |
|     Aggregation    | Belvo      |          Yes         |
|     Enrichment     | Belvo      |          Yes         |
| Payment Initiation | Belvo      |          Yes         |

```json
[
  {
    "code": "unexpected_error",
    "message": "Belvo is unable to process the request due to an internal system issue or to an unsupported response from an institution",
    "request_id": "4a7b283c6efa449c9c028a16b5c249fd"
  }
]
```

**Cause**

This error occurs when we (Belvo) have encountered an internal system error (sorry about that) or due to an unsupported response from the institution.

This type of error can be intermittent or persistent. 

**Solution**

We recommend that you retry making your original request a **maximum of three times**, in case that the issue is intermittent. 

If the error keeps occurring with the same request, <a href="https://support.belvo.com/hc/en-us/requests/new" target="_blank">contact our support team</a>, making sure to include the `request_id` that you receive in the error message.

**Widget error message**

| Language            | Error title          | Error description                                                                                                                          |
| ------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 🇬🇧 <br/>English    | Something went wrong | There was an error linking your account. Please try again, and if the problem persists, we will try to fix it as soon as possible.         |
| 🇧🇷 <br/>Portuguese | Ocorreu um erro      | Ocorreu um erro ao vincular sua conta. Tente novamente e, se o problema persistir, o corrigiremos o mais breve possível                    |
| 🇪🇸 <br/>Spanish    | Ha habido un error   | Hemos tenido un error vinculando tu cuenta. Por favor, inténtalo de nuevo y si el problema persiste, lo arreglaremos lo más pronto posible |

***

# Payment Initiation API last encountered errors

|         API        | Error type  | Reflected in widget? |
| :----------------: | :---------- | :------------------: |
|     Aggregation    | N/A         |          N/A         |
|     Enrichment     | N/A         |          N/A         |
| Payment Initiation | last\_error |          Yes         |

In addition to the standard list of errors, our Payments Initiation API also returns additional errors called `last_error`s that are specific to the payment flow. When a payment intent fails or encounters an error at some point along the payment flow, a `last_error` message is returned in the response to give you information about what went wrong. Depending on the specific error, you might need to prompt your customer to correct their payment information or start the payment flow again.

1. `invalid_credentials`
2. `invalid_token`
3. `login_error`
4. `login_two_factor_error`
5. `missing_token_registration`
6. `payment_error`
7. `session_expired`
8. `unauthorized_credentials`

Below we provide you with example messages, causes for the error, and how to troubleshoot them.

## invalid\_credentials

```json
[
    {
      "error_code": "invalid_credentials",
      "error_message": "The credentials sent are incorrect, please try again."
    }
]
```

**Cause**

This error can occur when the credentials that your customer provides are incorrect.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## invalid\_token

```json
[
    {
      "error_code": "invalid_token",
      "error_message": "The token sent is incorrect or has expired, please try again."
    }
]
```

**Cause**

This error can occur when the MFA token your customer provides is invalid.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## login\_error

```json
[
    {
      "error_code": "login_error",
      "error_message": "Provider login error"
    }
]
```

**Cause**

This error can occur when something unexpected happened in the `display_credentials_required` next step.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## login\_two\_factor\_error

```json
[
    {
      "error_code": "login_two_factor_error",
      "error_message": "Provider login two factor error"
    }
]
```

**Cause**

This error can occur when something unexpected happened in the `display_token_required` next step.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## missing\_token\_registration

```json
[
    {
      "error_code": "missing_token_registration",
      "error_message": "The user has no token configured in the bank."
    }
]
```

**Cause**

This error can occur when your user has not registered an MFA token with their bank. 

> 📘
>
> At present, this error only occurs for our PSE product with the following institutions:
>
> * Bancolombia
> * Banco de Bogota

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## payment\_error

```json
[
    {
      "error_code": "payment_error",
      "error_message": "Unexpected error to confirm the payment"
    }
]
```

**Cause**

This error can occur when something unexpected happens during the payment confirmation process.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## session\_expired

```json
[
    {
      "error_code": "session_expired",
      "error_message": "Bank session was not found"
    }
]
```

**Cause**

This error occurs when you try to send a PATCH request after the session has already expired (the session expires after 10 minutes).

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.

***

## unauthorized\_credentials

```json
[
    {
      "error_code": "unauthorized_credentials",
      "error_message": "Your credentials are not authorized. Please, contact the bank."
    }
]
```

**Cause**

This error occurs when your user has not provided the correct *authorized* credentials to log in to their institution.

**Solution**

Please check what the next step is in the payment intent process to complete the transaction. You can do this by making a [Get details about a payment link](https://developers.belvo.com/reference/detailcreatepaymentlink) request and checking the `next_step` field.