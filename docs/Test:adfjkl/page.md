---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
With our App2App flow, you can offer your clients a more native app experience using Belvo’s Hosted Widget, enhancing their user experience and reducing friction. On this page, we’ll guide you through the new flow and provide guidelines on how to implement it.

# User flow

With the App2App flow, the key difference for the user is that after they grant their consent to share data:

1. They are redirected to a secure browser to complete the request.
2. They are redirected directly to your app.
3. The Belvo widget opens in a webview within your app.

> 📘 How does this differ from the usual flow?
>
> In the usual flow, when you implement the Hosted Widget using deep links, the user completes the entire connection process in the browser and is then prompted to be redirected to your application, which leads to friction and a suboptimal user experience. With this new flow, the user is seamlessly transferred through the different redirections.

<Embed url="https://www.youtube.com/watch?v=qJrJSKNNlrA" title="App2App Flow Example" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/qJrJSKNNlrA/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=qJrJSKNNlrA" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FqJrJSKNNlrA%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DqJrJSKNNlrA%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FqJrJSKNNlrA%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

# Implementation

To use the App2App flow, you will need to make the following changes to your current implementation:

1. Create a link to your application.
2. Use the link when generating the access token.
3. Open the Webview Widget upon being redirected to your application.

## 1. Link to your application

Before setting up the native app experience, you need to prepare a universal link (iOS) or an app link (Android). This link is used to redirect your user back to your application after they have granted their consent in their institution.

> 📘 Why not use a deep link?
>
> When using a deep link to your application, users receive a pop-up message that they need to confirm before being redirected to your app, which can lead to a poor user experience and friction.
>
> By using the `application_link`, users are automatically redirected to your application without needing to confirm the redirect.

## 2. Generating your `access_token`

When generating your `access_token`, you need to provide the following parameters in the `callback_urls` object:

* `application_link` : The link to your application that users will be redirected to after granting consent in their institution.
* `success`: The URL users are redirected to when they have successfully completed the widget flow.
* `exit`:  The URL users are redirected to when they exit the widget before completing the flow.
* `event`: The URL users are redirected to when an error occurs.

```json callback_urls for App2App flow
{
  ...
  "callback_urls": {
    "application_link": "https://your.company_name.br/belvo-widget",
    "success": "https://your.company_name.br/success",
    "exit": "https://your.company_name.br/exit",
    "event": "https://your.company_name.br/error"
  }
  ...
}

```

For complete instructions how how to generate the `access_token`, please see our dedicated <a href="https://developers.belvo.com/docs/hosted-widget-ofda#1-generating-an-access_token-ofda" target="_blank">Hosted Widget (OFDA) guide</a>.

## 3. Open Webview on redirect

Once users grant consent in their institution, they are redirected to your application using the `application_link`, along with a query string that you’ll need to use to open the Belvo widget as a webview inside your application.

```shell Redirect Example to application_link
https://mobile.your-app-name.br/belvo-widget/ # Your application_link
	?access_token={someAccessToken}&consent_id={someConsentId}&locale=pt... # Query string with details to open the Belvo widget
```

As soon as users are redirected to your application, you need to open a webview within your application and launch Belvo’s widget:

```shell Opening the widget in a webview example
https://widget.belvo.io/ # The Belvo Hosted Widget URL
	?access_token={someAccessToken}&consent_id={someConsentId}&locale=pt... # The query string you received
```

<br />

✅ Done! With these few tweaks to your implementation, users will seamlessly move from your application to the widget, grant their consent, and then return to the widget within your application.