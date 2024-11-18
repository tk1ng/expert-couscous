---
title: Parameters - Bancontact
deprecated: false
hidden: false
metadata:
  robots: index
---
## Request

### Service Specific Parameters: 

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Required",
    "h-3": "Description",
    "0-0": "InvoiceAmount",
    "0-1": "decimal",
    "0-2": "yes",
    "0-3": "The amount of the invoice. Note: In case of a CreateCombinedInvoice request, the InvoiceAmount may deviate from the transaction amount, e.g. if additional transactions are to be added later, such as ExternalPayments.",
    "1-0": "InvoiceAmountVat",
    "1-1": "decimal",
    "1-2": "",
    "1-3": "The VAT amount on the invoice.",
    "2-0": "InvoiceDate",
    "2-1": "",
    "2-2": "yes",
    "2-3": "The invoice date. (yyyy-mm-dd)",
    "3-0": "DueDate",
    "3-1": "",
    "3-2": "yes",
    "3-3": "The due date for the invoice. The schedule starts counting from this date. Important note: if combined with SEPA Direct Debit, the collect date should always precede the due date of the invoice, since you don't want to trigger a reminder step before debiting the customer. If however, the collect date is accidentally set after the due date, then the first reminder step will be postponed till the collect date, but only if it's set within 14 days after the due date. If it's set further than that, then our system will perform another check after 14 days and so on.",
    "4-0": "SchemeKey",
    "4-1": "String",
    "4-2": "",
    "4-3": "The key of the scheme to use. Available keys are found in the Buckaroo Payment Plaza: Configuration > Credit Management.",
    "5-0": "MaxStepIndex",
    "5-1": "integer",
    "5-2": "",
    "5-3": "If given, only this many scheme steps are taken, allowing the scheme to be cut short. (min: 1)",
    "6-0": "AllowedServices",
    "6-1": "string",
    "6-2": "",
    "6-3": "Allowed payment methods (Comma-separated list of service codes) when using a pay link in Credit Management. This acts as a whitelist. Cannot be combined with DisallowedServices. The order in which the payment methods are listed also determines the order in which they are displayed to the customer on the Buckaroo checkout page. Default: all services are allowed.",
    "7-0": "DisallowedServices",
    "7-1": "string",
    "7-2": "",
    "7-3": "Disallowed payment methods (Comma-separated list of service codes) when using a pay link in Credit Management. This acts as a blacklist. Cannot be combined with AllowedServices. Default: all services are allowed.",
    "8-0": "AllowedServicesAfterDueDate",
    "8-1": "string",
    "8-2": "",
    "8-3": "Allowed payment methods (Comma-separated list of service codes) after the due date when using a pay link in Credit Management. This acts as a whitelist. Comma-separated. Cannot be combined with DisallowedServicesAfterDueDate. The order in which the payment methods are listed also determines the order in which they are displayed to the customer on the Buckaroo checkout page. Default: all services are allowed.",
    "9-0": "DisallowedServicesAfterDueDate",
    "9-1": "string",
    "9-2": "",
    "9-3": "Disallowed payment methods (Comma-separated list of service codes) after the due date when using a pay link in Credit Management. This acts as a blacklist. Cannot be combined with AllowServicesAfterDueDate. Default: all services are allowed.",
    "10-0": "Code",
    "10-1": "string",
    "10-2": "Required",
    "10-3": "GroupType: Debtor. A unique code by which the merchant identifies the debtor. If the debtor with this code exists, any given components are overwritten.",
    "11-0": "Culture",
    "11-1": "string",
    "11-2": "",
    "11-3": "GroupType: Person. The person’s culture code. May be specific, e.g. nl-NL, en-US, or non-specific, e.g. en. Required if person information is provided.",
    "12-0": "Title",
    "12-1": "string",
    "12-2": "",
    "12-3": "GroupType: Person. The person’s title.",
    "13-0": "Initials",
    "13-1": "string",
    "13-2": "",
    "13-3": "GroupType: Person. The person’s initials.",
    "14-0": "FirstName",
    "14-1": "string",
    "14-2": "",
    "14-3": "GroupType: Person. The person’s first name.",
    "15-0": "LastNamePrefix",
    "15-1": "string",
    "15-2": "",
    "15-3": "GroupType: Person. The person’s last name prefix, e.g. ‘van der’.",
    "16-0": "LastName",
    "16-1": "string",
    "16-2": "",
    "16-3": "GroupType: Person. The person’s last name, excluding prefix. Required if person information is provided.",
    "17-0": "Gender",
    "17-1": "integer",
    "17-2": "",
    "17-3": "GroupType: Person. The person’s gender. Possible values: 1, 2, 0, 9 (Male, female, unknown, not applicable. Default: 0).",
    "18-0": "BirthDate",
    "18-1": "date",
    "18-2": "",
    "18-3": "GroupType: Person. The person’s date of birth (yyyy-mm-dd). Important: debtor has to be between 2 and 120 years old, in order to transfer his/her invoices to collection agency CIB.",
    "19-0": "PlaceOfBirth",
    "19-1": "string",
    "19-2": "",
    "19-3": "GroupType: Person. The person’s place of birth.",
    "20-0": "Culture",
    "20-1": "string",
    "20-2": "",
    "20-3": "GroupType: Company. The company’s culture code. May be specific, e.g. nl-NL, en-US, or non-specific, e.g. en. Required if company information is provided.",
    "21-0": "Name",
    "21-1": "string",
    "21-2": "",
    "21-3": "GroupType: Company. The company’s name. Required if company information is provided.",
    "22-0": "VatApplicable",
    "22-1": "boolean",
    "22-2": "",
    "22-3": "GroupType: Company. Whether VAT applies to the company.",
    "23-0": "VatNumber",
    "23-1": "string",
    "23-2": "",
    "23-3": "GroupType: Company. The company’s VAT identification number.",
    "24-0": "ChamberOfCommerce",
    "24-1": "string",
    "24-2": "",
    "24-3": "GroupType: Company. The company’s Chamber of Commerce registration number.",
    "25-0": "Street",
    "25-1": "string",
    "25-2": "",
    "25-3": "GroupType: Address. The address’ street name. Required if address is given. Required if CM scheme has a collection agency step.",
    "26-0": "HouseNumber",
    "26-1": "integer",
    "26-2": "",
    "26-3": "GroupType: Address. The address’ house number. Required if CM scheme has a collection agency step.",
    "27-0": "HouseNumberSuffix",
    "27-1": "string",
    "27-2": "",
    "27-3": "GroupType: Address. The address’ house number suffix.",
    "28-0": "Zipcode",
    "28-1": "string",
    "28-2": "",
    "28-3": "GroupType: Address. The address’ zip code. Required if address is given. Required if CM scheme has a collection agency step.",
    "29-0": "City",
    "29-1": "string",
    "29-2": "",
    "29-3": "GroupType: Address. The address’ city. Required if address is given. Required if CM scheme has a collection agency step.",
    "30-0": "State",
    "30-1": "",
    "30-2": "",
    "30-3": "GroupType: Address. The address’ state or province.",
    "31-0": "Country",
    "31-1": "string",
    "31-2": "",
    "31-3": "GroupType: Address. The address’ two-letter ISO country code, e.g. NL or US. Required if address is given. Required if CM scheme has a collection agency step.",
    "32-0": "Email",
    "32-1": "string",
    "32-2": "",
    "32-3": "GroupType: Email. The e-mail address of the person or company.",
    "33-0": "Mobile",
    "33-1": "string",
    "33-2": "",
    "33-3": "GroupType: Phone. The mobile phone number. Please note: this is the only number that can be used for SMS reminders. With regards to SMS reminders it is advised to send in the phone number formatted as either \"+31612345678\" or \"0612345678\", filtering out any dashes \"-\" and white spaces \" \".",
    "34-0": "Landline",
    "34-1": "string",
    "34-2": "",
    "34-3": "GroupType: Phone. The landline phone number.",
    "35-0": "Fax",
    "35-1": "string",
    "35-2": "",
    "35-3": "GroupType: Phone. The fax number.",
    "36-0": "ApplyStartRecurrent",
    "36-1": "string",
    "36-2": "",
    "36-3": "If True, every transaction via the Invoice paylink will have the property StartRecurrent = True.<br><br>"
  },
  "cols": 4,
  "rows": 37,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]


<br />

### Example Request:

```json
{
   "Currency": "EUR",
   "Invoice": "testinvoice123r",
   "Services": {
      "ServiceList": [
         {
            "Name": "CreditManagement3",
            "Action": "CreateInvoice",
            "Parameters": [
               {
                  "Name": "ApplyStartRecurrent",
                  "Value": "False"
               },
               {
                  "Name": "InvoiceAmount",
                  "Value": "10.00"
               },
               {
                  "Name": "InvoiceAmountVAT",
                  "Value": "1.00"
               },
               {
                  "Name": "InvoiceDate",
                  "Value": "2017-09-22"
               },
               {
                  "Name": "DueDate",
                  "Value": "2018-12-23"
               },
               {
                  "Name": "SchemeKey",
                  "Value": "xxxx"
               },
               {
                  "Name": "MaxStepIndex",
                  "Value": "2"
               },
               {
                  "Name": "AllowedServices",
                  "Value": "ideal,mastercard"
               },
               {
                  "Name": "AllowedServicesAfterDueDate",
                  "Value": "ideal,mastercard"
               },
               {
                  "Name": "Code",
                  "GroupType": "Debtor",
                  "GroupID": "",
                  "Value": "johnsmith4"
               },
               {
                  "Name": "Email",
                  "GroupType": "Email",
                  "GroupID": "",
                  "Value": "youremail@example.nl"
               },
               {
                  "Name": "Culture",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "nl-NL"
               },
               {
                  "Name": "Title",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "Msc"
               },
               {
                  "Name": "Initials",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "JS"
               },
               {
                  "Name": "FirstName",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "John"
               },
               {
                  "Name": "LastNamePrefix",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "Jones"
               },
               {
                  "Name": "LastName",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "Smith"
               },
               {
                  "Name": "Gender",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "1"
               },
               {
                  "Name": "BirthDate",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "1990-01-01"
               },
               {
                  "Name": "PlaceOfBirth",
                  "GroupType": "Person",
                  "GroupID": "",
                  "Value": "Utrecht"
               },
               {
                  "Name": "Culture",
                  "GroupType": "Company",
                  "GroupID": "",
                  "Value": "nl-NL"
               },
               {
                  "Name": "Name",
                  "GroupType": "Company",
                  "GroupID": "",
                  "Value": "My Company Corporation"
               },
               {
                  "Name": "VatApplicable",
                  "GroupType": "Company",
                  "GroupID": "",
                  "Value": "true"
               },
               {
                  "Name": "VatNumber",
                  "GroupType": "Company",
                  "GroupID": "",
                  "Value": "NL140619562B01"
               },
               {
                  "Name": "ChamberOfCommerce",
                  "GroupType": "Company",
                  "GroupID": "",
                  "Value": "20091741"
               },
               {
                  "Name": "Street",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "Hoofdstraat"
               },
               {
                  "Name": "HouseNumber",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "90"
               },
               {
                  "Name": "HouseNumberSuffix",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "A"
               },
               {
                  "Name": "Zipcode",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "8441ER"
               },
               {
                  "Name": "City",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "Heerenveen"
               },
               {
                  "Name": "State",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "Friesland"
               },
               {
                  "Name": "Country",
                  "GroupType": "Address",
                  "GroupID": "",
                  "Value": "NL"
               },
               {
                  "Name": "Mobile",
                  "GroupType": "Phone",
                  "GroupID": "",
                  "Value": "06198765432"
               }
            ]
         }
      ]
   }
}
```

<br />

## Response

### Parameters

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Description",
    "0-0": "InvoiceKey",
    "0-1": "The unique key that was created to identify the invoice.",
    "1-0": "DebotGuid",
    "1-1": "Unique identifier of the debtor",
    "2-0": "InvoicePayLink",
    "2-1": "Pay link of the invoice<br><br>"
  },
  "cols": 2,
  "rows": 3,
  "align": [
    null,
    null
  ]
}
[/block]


<br />

Example Response

```json
{
    "Key": "EAE77A1EDCCC479DA94325A4D245xxxx",
    "Status": {
        "Code": {
            "Code": 190,
            "Description": "Success"
        },
        "SubCode": {
            "Code": "S001",
            "Description": "Transaction successfully processed"
        },
        "DateTime": "2017-09-18T16:42:10"
    },
    "RequiredAction": null,
    "Services": [
        {
            "Name": "CreditManagement3",
            "Action": null,
            "Parameters": [
                {
                    "Name": "InvoiceKey",
                    "Value": "9C9D0305DE4A47178DE903FA91C1xxxx"
                },
                {
                    "Name": "DebtorGuid",
                    "Value": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
                },
                {
                    "Name": "InvoicePayLink",
                    "Value": "https://testcheckout.buckaroo.nl/html/?brq_paydirect_inv=xxxxxx"
                }
            ]
        }
    ],
    "CustomParameters": null,
    "AdditionalParameters": null,
    "RequestErrors": null,
    "ServiceCode": "CreditManagement3",
    "IsTest": true,
    "ConsumerMessage": null
}
```

<br />

## Push

### Parameters

| Parameter                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| InvoiceKey               | The unique key identifying the invoice. Was also output from the request that originally created the invoice.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| InvoiceNumber            | The invoice number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| WebsiteKey               | The unique key identifying the website that the invoice belongs to.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| DebtorCode               | The unique code identifying the debtor that the invoice is for.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| SchemeKey                | The key of the scheme that the invoice follows.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| IsTest                   | Wether the invoice was a test or not                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Type                     | The type of the invoice. Possible values: 1) RegularInvoice: the type of invoice that is normally used, 2) PartialInvoice: a partial invoice, such as those used in Payment Plans. Not applicable to most merchants, and can usually be ignored, 3) CreditNote: A credit note reducing the open amount of an existing invoice. The credit note also causes a financial change on the original invoice, which provides a clearer context. As such, the credit note push can usually be ignored.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Culture                  | The debtor’s culture, if available, or “en-US” otherwise.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| InvoiceDate              | The official date of the invoice.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| DueDate                  | The date on which payment is due.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| InvoiceStatusCode        | The current status of the invoice. Possible Status codes are: 10: Active. The invoice follows its scheme, if applicable. 20: Paused. The invoice currently does proceed on its scheme. 21: PausedByDispute. Like Paused, but specifically caused by a manually registered dispute. 22: PausedByPaymentPlan. Like Paused, but specifically caused by a payment plan. This status can only be removed through termination of the payment plan. 23: PausedDueToValidation. The invoice is paused because one or more scheme actions could not be performed due to a validation error. 70: PendingTransferToCollectionAgency. The invoice is marked for transfer to the collection agency, in accordance with its scheme. 71: TransferredToCollectionAgency. The invoice is at the collection agency, and awaiting their response. 72: AcceptedByCollectionAgency. The collection agency has accepted the invoice and will work on it. 73: ProcessedByCollecionAgency. The collection agency has finished its work on the invoice. 74: ProcessedByCollectionAgencyIncomplete. The collection agency has finished its work on the invoice but did not manage to (fully) collect the invoice. 75: PendingRecall. The recall request has yet to be confirmed by the collection agency. 76: Recalled. Collection agency has confirmed the recall. 79: RefusedByCollectionAgency. The collection agency has not accepted the invoice. 80: WrittenOff. The invoice was manually written off by the merchant. 90: Rejected. The invoice was rejected, most likely because its request was invalid. It has never been active. 91: Cancelled. The invoice has been active, but is no longer. For example, this can happen to the partial invoices created by a payment plan (see CreatePaymentPlan) if they cease to apply. 99: Emergency. This invoice was manually disabled because of an emergency. Tech support is examining it. 0: NotSet. A technical error took place. This status should never occur.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| PreviousStepIndex        | The last step that was taken on the invoice’s scheme. E.g. 0 means no steps were taken, 1 means step 1 is the last step that was taken, and so on.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| PreviousStepDateTime     | The moment the previous step was taken. DateTimes are in Buckaroo’s local time zone, CE(S)T, in ISO-8601 format, as seen in the examples. Most systems support automatic interpretation and conversion of this representation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Event                    | The name of the event that caused this push. 1) ChangedTransactionStatus: one of the invoice’s transactions changed status in a relevant way. Generally only a change to ‘successful’ is relevant, although there are exceptions, e.g. a Sepa Direct Debit moving to or away from ‘pending’ influences PendingSlowPaymentAmount, 2) ChangedStatus: the invoice changed status, e.g. to ‘active’ or ‘paused’. See below for options, 3) CreatedCreditNote: credit note was created on the invoice. Note that a push may be sent for the credit note itself, but the CreatedCreditNote event on the original invoice is the most relevant, 4) SentReminderMessage: a reminder was sent for the invoice, in accordance with its scheme, 5) SentBackupReminderMessage: a reminder was sent for the invoice using a backup method, in accordance with its scheme. E.g. the scheme may be set to send a letter if the e-mail cannot be delivered, 6) SkippedReminderBecauseNoMethodsRemain: a reminder action in the invoice’s scheme has failed to reach the debtor. This happens when all of the given communication methods bounce (e.g. incorrect e-mail address) or have been marked as unreachable by the merchant (e.g. through the Debtor screen in the Payment Plaza), 7) IncreasedAdminFee: the administration fee on the invoice has been increased, in accordance with the invoice’s scheme, 8) TransferredToCollectionAgency: the invoice has entered the collection agency process, in accordance with its scheme. Note that the ChangedStatus event provides more detailed updates as the invoice status changes throughout this process (transfer, acceptance, refusal, completion), 9) CreatedRecollect: a recollect was created for the invoice, in accordance with its scheme. This happens when Sepa Direct Debit recollection is active on the scheme, when the previous attempt fails and there is enough time for another attempt, 10) SentPaymentInvitationMessage: a payment invitation was sent for the invoice, in accordance with its scheme, 11) SentBackupPaymentInvitationMessage: A payment invitation was sent for the invoice using a backup method, in accordance with its scheme. E.g. the scheme may be set to send a letter if the e-mail cannot be delivered. 12) CmSchemeValidationError: One or more scheme actions could not be performed due to a validation error. 13) InvoicePausedDueToValidationErrors: The invoice is paused because one or more scheme actions could not be performed due to a validation error. This will only occur if 1) the payment invitation could not be performed, 2) not a single reminder message within a CM step could be performed or 3) the invoice could not be transferred to the collection agency. |
| EventCategory            | The category the event belongs to. Possible values: 1) FinancialChange: any change that relates to the invoice’s amounts, including the initial invoice creation, transaction status changes, and credit notes, 2) ValidationError: A validation error occurred, 3) Other: anything else, e.g. a reminder being sent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| EventDateTime            | The moment the event took place. Important, as earlier events should be ignored in case a later event has already been observed. See the section on “Order Of Events”. DateTimes are in Buckaroo’s local time zone, CE(S)T, in ISO-8601 format, as seen in the examples. Most systems support automatic interpretation and conversion of this representation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| EventParameters          | Any number of additional pieces of data regarding the Event, as key-value pairs. E.g. the ChangedTransactionStatus event has a TransactionKey and a TransactionStatusCode parameter. Or the CmSchemeValidationError and InvoicePausedDueToValidationErrors events have the ValidationErrorMessage parameter. Note that ValidationErrorMessage parameters are always supplemented with an index number, because there can be multiple ValidationErrorMessages in one push message. So the first ValidationErrorMessage is always ValidationErrorMessage0, a second one ValidationErrorMessages1, third one ValidationErrorMessages2, and so on.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Currency                 | The invoice’s currency.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| AmountDebit              | An invoice’s amount. 0 for credit notes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| AmountCredit             | A credit note’s amount. 0 except for credit notes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| AmountAdminCosts         | The administration costs that have been added to the invoice so far, in accordance with its scheme.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| AmountCreditNotes        | The total amount that has been credited on the invoice, by means of credit notes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| AmountPaid               | The total main amount that was paid on the invoice, i.e. excluding administration costs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| AmountAdminCostsPaid     | The total amount of the administration costs that was paid on the invoice.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| AmountPendingSlow        | The total amount that could still come in from pending “slow” payment methods. At the time of writing, this only applies to pending Sepa Direct Debits and Collection Agency Payouts. The invoice may not be paid yet, but it could very well become so when the payment succeeds, so we may not want to contact the debtor unless the payment fails.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| OpenAmount               | The main amount that is yet to be paid on the invoice, i.e. excluding administration costs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| OpenAmountAdminCosts     | The amount of the administration costs that is yet to be paid on the invoice.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| OpenAmountInclAdminCosts | The amount that is yet to be paid on the invoice, including administration costs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| IsPaid                   | s the invoice fully paid? This is the same as OpenAmount being greater than 0. We do not take administration costs into consideration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| DebtorGuid               | Unique identifier of the debtor                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| InvoicePayLink           | Pay link of the invoice                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

<br />

### Example Push

```json
{
   "Invoice": {
      "InvoiceKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "InvoiceNumber": "testinvoice_1614689513",
      "WebsiteKey": "0000",
      "DebtorCode": "JohnSmith12345",
      "DebtorGuid": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "SchemeKey": "xxxxx",
      "IsTest": true,
      "Type": "RegularInvoice",
      "Culture": "nl-NL",
      "InvoiceDate": "2021-03-02T00:00:00",
      "DueDate": "2021-03-02T00:00:00",
      "InvoiceStatusCode": 23,
      "PreviousStepIndex": 0,
      "PreviousStepDateTime": "2021-03-02T15:59:21",
      "InvoicePayLink": "http://testcheckout.local/html/?brq_paydirect_inv=xxxx",
      "Event": "InvoicePausedDueToValidationErrors",
      "EventCategory": "ValidationError",
      "EventDateTime": "2021-03-02T16:02:04.321891",
      "EventParameters": [
         {
            "Key": "ValidationErrorMessage0",
            "Value": "Required data Email missing."
         },
         {
            "Key": "ValidationErrorMessage1",
            "Value": "Required data MobilePhone missing."
         }
      ],
      "Currency": "EUR",
      "AmountDebit": 1,
      "AmountCredit": 0,
      "AmountAdminCosts": 0,
      "AmountCreditNotes": 0,
      "AmountPaid": 0,
      "AmountAdminCostsPaid": 0,
      "AmountPendingSlow": 0,
      "OpenAmount": 1,
      "OpenAmountAdminCosts": 0,
      "OpenAmountInclAdminCosts": 1,
      "IsPaid": false,
      "CustomParameters": [],
      "AdditionalParameters": []
   }
}
```