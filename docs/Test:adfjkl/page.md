---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
With Belvo's Open Finance Payment Initiation (OFPI), you can collect payments from your customers and optimize their payment experience. In this guide, we’ll show you:

* the general flow of data
* how to create a payment intent to collect payments
* track the status of your payment requests

<HTMLBlock>{`<div style="border-left: 4px solid #FFEB3B; background-color: #fff8e1; padding: 10px; margin: 10px 0; border-radius: 5px;">
  <strong>Prerequisites:</strong> Please make sure you have completed all the steps in our dedicated <a href="https://developers.belvo.com/docs/ofpi-prerequisites" target="_blank">prerequisites</a> article before continuing this guide.
</div>`}</HTMLBlock>

# Data flow overview

As you can see in the diagram below, the data flow for creating a payment using Pix via Open Finance involves:

1. Creating a payment intent (containing the required information for the payment to be processed in the Open Finance Network).
2. Listening for the `OBJECT_CREATED` webhook from the transactions resource.
3. Getting the transaction details.

![](https://files.readme.io/4502548fd198d8fa320f7a588141bef543ac8e1b3de9c397a12cc49abcdd830d-CleanShot_2024-09-10_at_16.43.292x.png)

<br />

# Create a Payment Intent

The Payment Intent contains all the information necessary to register and process the payment in the Open Finance Network. To reduce friction for your customer, we recommend that you create your payment screen so that you can send all the information in just one POST call.

<Image align="center" src="https://files.readme.io/05ff611cd29be3028f68f4165ecd3558e35bcfec2fdca9b515ecf33cde8385d5-Pix_Automatico_-_One_Screen.png" />

To create a Payment Intent, check out the recipe below which guides you through all the required parameters:

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="66ded1f5128b550019f811ea" link="https://developers.belvo.com/v1.0/recipes/create-a-payment-intent" slug="create-a-payment-intent" title="Create a Payment Intent" />

Once you successfully create a Payment Intent, you will need to use the URL in the `payment_method_information.open_finance.redirect_url` parameter to redirect your user to their financial institution to confirm the payment. After confirming the payment, your user is redirected back to the `callback_url` you provided in the Payment Intent request.

For details regarding the response from the Payment Intent request, please see our dedicated <a href="https://developers.belvo.com/docs/payment-intent-model-and-states-ofpi#payment-intent-model" target="_blank">Payment Intent (OFPI) Model and States</a> article.

# Payment Intents, Charges, and Transactions

For each payment, Belvo generates a **Charge** object within the Payment Intent response body. Once a Charge is processed successfully, Belvo generates a **Transaction** associated with that Charge.

<Image align="center" width="50% " src="https://files.readme.io/5e155442aa07614aefddb4b89138c5b4108db6e8cdaef501a075ef2814dbc3fe-image.png" />

# Payment statuses and notifications

Once you create an immediate payment, you will receive webhook updates for the associated Payment Intent, Charge, and Transaction.

Below you can see an example of an immediate payment and the associated statuses the payment will go through. You will receive `STATUS_UPDATE` webhook notifications for each status that is marked with a red dot (🔴).

![](https://files.readme.io/f48a52d1d7a15d5413a3480fade1edf177c995d3024f7955e7c91865516574fe-image.png)

When you receive the `OBJECT_CREATED` Transaction webhook event, this indicates that the given scheduled payment was settled.

# Listen for payment status updates

Once you create the Payment Intent, Belvo will provide you updates regarding the payment via webhooks. As you can see in the image in the [Data flow overview](https://developers.belvo.com/docs/direct-api-pix-via-open-finance#data-flow-overview) section, you will receive the following webhooks during the payment process:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Event
      </th>

      <th style={{ textAlign: "left" }}>
        Resource
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        `STATUS_UPDATE`
      </td>

      <td style={{ textAlign: "left" }}>
        Payment Intents
      </td>

      <td style={{ textAlign: "left" }}>
        The `STATUS_UPDATE` events for Payment Intents indicate the stage of the Pix via Open Finance payment process. You will receive the following status updates: `REQUIRES_ACTION`, `PROCESSING`, and `SUCCEEDED`.  

        > **Note**: Apart from responding to the event with a `200 OK`, no further action is required.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `STATUS_UPDATE`
      </td>

      <td style={{ textAlign: "left" }}>
        Charges
      </td>

      <td style={{ textAlign: "left" }}>
        The `STATUS_UPDATE` events for Charges indicates the stage of the Pix via Open Finance payment process. You will receive the following status updates:  `SUCCEEDED`.  

        > **Note**: Apart from responding to the event with a `200 OK`, no further action is required.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `OBJECT_CREATED`
      </td>

      <td style={{ textAlign: "left" }}>
        Transactions
      </td>

      <td style={{ textAlign: "left" }}>
        The `OBJECT_CREATED` event for Transactions indicates that the payment funds were transferred from one account to another.  

        > **Note**: Apart from responding to the event with a `200 OK`, we recommend you also make a [Get Transaction Details](https://developers.belvo.com/docs/direct-api-pix-via-open-finance#get-details-for-successful-transactions) request to get the transaction information.
      </td>
    </tr>
  </tbody>
</Table>

# Get details for successful transactions.

The `OBJECT_CREATED` webhook from the Transactions resource that indicates that the **payment succeeded and funds were transferred** from one account to another. This means that every time money has been successfully transferred to your account, you’ll receive the following notification:

```json OBJECT_CREATED transactions webhook payload
{
  "webhook_id": "3b9a69f7-0f0a-455b-832d-49ad6fd4905c",
  "webhook_type": "TRANSACTIONS",
  "webhook_code": "OBJECT_CREATED",
  "object_id": "d2e40773-19f6-48d1-93c3-3590ec0c74df",
  "data": {}, //For OBJECT_CREATED webhooks, the data field returns an empty object.
}
```

You can get the details about the transaction by making a [GET details](https://developers.belvo.com/reference/detailpaymenttransactionsbrazil) call using the `object_id` of the transaction (which you receive in the webhook event).

```curl Get Transaction Details request
curl --request GET \
     --url https://api.belvo.com/payments/br/transactions/{id}/ \
     --header 'accept: application/json'
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
        `id`
      </td>

      <td style={{ textAlign: "left" }}>
        string\
        (uuid)
      </td>

      <td style={{ textAlign: "left" }}>
        The `transaction.id` that you want to get detailed information about. You can retrieve this ID from the `object_id` field that you received in the `OBJECT_CREATED` transactions webhook.
      </td>

      <td style={{ textAlign: "left" }}>
        a3b92311-1888-449f-acaa-49ae28d68fcd
      </td>
    </tr>
  </tbody>
</Table>

You will receive the following information regarding the transaction:

```json Transactions response payload
{
  "id": "fd0f3303-cafb-47ea-9753-21155cb144ab",
  "created_at": "2020-04-23T21:30:20.336854+00:00",
  "created_by": "1c83ead8-6665-429c-a17a-ddc76cb3a95e",
  "amount": "500",
  "currency": "BRA",
  "description": "Awesome training Sneaker",
  "transaction_type": "INFLOW",
  "beneficiary": "a80d5a9d-20ae-479a-8dd7-ff3443bcbbfc",
  "payer": {},
  "payment_intent": "1c83ead8-6665-429c-a17a-ddc76cb3a95e",
  "customer": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

<br />

> 👍 And that's it! By following this guide you can make payments using Belvo's Pix via Open Finance product.