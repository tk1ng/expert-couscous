---
title: Ideal QR BUCKAROO
deprecated: false
hidden: false
metadata:
  robots: index
---
# Enable Easy Payments with iDEAL QR!

<Image align="right" src="https://files.readme.io/a514308-Ideal-qr.png" />

## Overview:

An iDEAL QR is pre-registered at the QR bank. The bank will generate a QR with an iDEAL logo in the middle section. By scanning this iDEAL QR, payment can be started via another medium. Think of a (donation) banner or a webpage on another device than the one via which payment will be made, such as an iPad or an order kiosk in a shop. You can create an iDEAL QR via the wizard in the Buckaroo Plaza.

## Create iDEAL QR via Wizard:

1. Go to [plaza.buckaroo.nl](https://plaza.buckaroo.nl)
2. Services > iDEAL QR > Actions > Generate new QR

<Image align="center" src="https://files.readme.io/72b413a-ideal-qr-startscherm-en.png" />

3. Select Website
4. Fill in amount
5. Description (max 35 characters)
6. Fill in Purchase id
7. Fill in expiration date of QR
8. Set if QR is a one-off (one payer)
9. Set if amount is adjustable and for what amount
10. Size of the QR (max 5000 pixels)
11. Set if it is a test QR

<Image align="center" src="https://files.readme.io/1cd6a58-ideal-qr-aanmaakscherm-en.png" />

## Batch:

You can generate the iDEAL QR-codes via a batch file. As soon as the file is ready, it can be uploaded in the Plaza under: 

* Services > File upload > Actions. 
* Select the file and tick the “Upload the batch file as test” box if a test is desired. 
* In case the website key isn’t processed in the file, it can be selected here as well.

## Example File:
`# Example batch file content here`

# Enable Easy Payments with iDEAL QR!

## Overview:

An iDEAL QR is pre-registered at the QR bank. The bank will generate a QR with an iDEAL logo in the middle section. By scanning this iDEAL QR, payment can be started via another medium. Think of a (donation) banner or a webpage on another device than the one via which payment will be made, such as an iPad or an order kiosk in a shop. You can create an iDEAL QR via the wizard in the Buckaroo Plaza.

## Create iDEAL QR via Wizard:

1. Go to [plaza.buckaroo.nl](https://plaza.buckaroo.nl)
2. Services \> iDEAL QR > Actions > Generate new QR
3. Select Website
4. Fill in amount
5. Description (max 35 characters)
6. Fill in Purchase id
7. Fill in expiration date of QR
8. Set if QR is a one-off (one payer)
9. Set if amount is adjustable and for what amount
10. Size of the QR (max 5000 pixels)
11. Set if it is a test QR

## Batch:

You can generate the iDEAL QR-codes via a batch file. As soon as the file is ready, it can be uploaded in the Plaza under: 

* Services > File upload \> Actions. 
* Select the file and tick the “Upload the batch file as test” box if a test is desired. 
* In case the website key isn’t processed in the file, it can be selected here as well.

## Example File:

Link naar QR Batch Sample

<br />

<br />

| Column              | Description                                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WebsiteKey          | Go to My Buckaroo \> Websites \> (Select website under Filters). The website can also be specified during the uploading. In that case, it doesn’t have to be processed in the file.                                                                                                                                                                                |
| Amount              | The amount initially shown to the donor.                                                                                                                                                                                                                                                                                                                         |
| AmountisChangeable  | “TRUE” means that the donor can adjust the amount. “FALSE” means that the amount is fixed.                                                                                                                                                                                                                                                                       |
| MinAmount/MaxAmount | The minimum and maximum amount between which the donor can choose while making a payment. The minimum amount is €0,00 and the maximum amount is €50,000.00. The payer’s bank might sometimes allow a lower maximum amount due to security reasons. In the hospitality industry, the maximum amount allows the customer to give a tip during the payment process. |
| Expiration          | Date until which the QR code is valid. Date format is DD-MM-YYYY or YYYY-MM-DD.                                                                                                                                                                                                                                                                                  |
| Description         | Description is added to the transactions with the QR code. It is also displayed on the payer’s bank statement. The description consists of a maximum of 35 characters.                                                                                                                                                                                           |
| PurchaseID          | Invoice number of the transactions made with this QR code. If a different invoice number is selected for each QR code, it can be differentiated afterwards which QR code was used for a transaction. For charities, this is often the event code.                                                                                                                |
| IsOneOff            | “FALSE” means this QR code can be used unlimitedly. “TRUE” means a one-off QR code is generated.                                                                                                                                                                                                                                                                 |
| ImageSize           | The size of the iDEAL QR. The standard size is 100 x 100 pixels. The maximum size is 5,000 x 5,000 pixels.                                                                                                                                                                                                                                                       |
| IsProcessing        | When the iDEAL QR codes have to be generated for which Buckaroo has a working Merchant ID. In case “True” is displayed, the money will be processed via iDEAL Processing and paid directly into the account of the Merchant using Processing.                                                                                                                    |

<br />

### Link to iDEAL payment to use for mobile / QR hyperlink:

The link to the actual QR code will look something like this: `https://qr7.ideal.nl/ideal-qr/qr/get/72d374b7-f878-4b78-ac05-xxxxxxxx`. This can be found in the processing results. <br/><br/>When you scan the QR code you will end up with a link that looks something like this: `https://qr7.ideal.nl/72d374b7-f878-4b78-ac05-xxxxxxxx`. (The part, ideal-qr / qr / get / has been removed from the link.) <br/><br/>To ensure that consumers can initiate a payment from their mobile, it is recommended to add the above link. This can be done, for example, by linking a hyperlink to the QR code or by placing a special button for this.