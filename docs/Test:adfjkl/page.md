---
title: Break Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
Belvo's Fiscal product is a great resource to quickly verify and assess your customer's financial capabilities.\
In this guide, you'll learn how to:

* Retrieve key personal information to verify the ID of your customer
* See your customer's tax compliance status
* Assess your customer's financial stability

By the end, you'll have a great web application that'll look a little like this:

![](https://files.readme.io/cbcccc0-individual-guide-intro-diagram.png "individual-guide-intro-diagram.png")

> 📘 Prerequisites
>
> Before starting this guide, make sure you have:
>
> * [installed npm](https://www.npmjs.com/get-npm) on your machine.
> * gone through our [getting started guide](https://developers.belvo.com/docs/get-started-in-10-minutes) to get your Sandbox API keys and used our Postman collection.

# Setup

Before getting started with anything, we first need to make sure that we have all the necessary packages and files created, so that we don't run into issues later.

#### Environment setup

In your terminal, run the following commands in the project directory (you can just copy and paste in each "block"):

```shell 1. Directory Structure
# 1. Create the project structure
mkdir pages
mkdir pages/api
touch pages/api/invoices.js
touch pages/api/tax-compliance-status.js
touch pages/api/tax-returns.js
touch pages/api/tax-status.js
touch pages/index.js
```
```shell 2. Define dependencies
# 2. Define the dependencies
echo '{
  "name": "belvo-fiscal-guides",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "@observablehq/plot": "^0.1.0",
    "arquero": "^4.8.2",
    "belvo": "^0.14.1",
    "d3": "6",
    "luxon": "^1.27.0",
    "next": "10.2.3",
    "node-fetch": "^2.6.1",
    "plot-react": "^1.0.0",
    "react": "17.0.2",
    "react-dom": "17.0.2"
  }
}' >> package.json
```
```shell 3. Install dependencies
# 3. Install dependencies
npm install
```
```shell 4. Configure .env file
# 4. Set up Belvo with your info
echo "BELVO_SECRET_ID={your sandbox secretID}
BELVO_SECRET_PASSWORD={your sandbox secretPassword}
BELVO_ENV_URL=https://sandbox.belvo.com
SCRIPT_URL="https://cdn.belvo.io/belvo-widget-1-stable.js"
BELVO_ENV=sandbox" >> .env
```

#### Endpoint wrappers

First, let's start by creating our four API endpoint wrappers:

* tax-status.js
* tax-compliance-status.js
* invoices.js
* tax-returns.js. 

These endpoints will allow you to call Belvo's API from the server, using your API keys, and expose the data to the client so that you can visualize it. Just open the recipe below and copy the code for each endpoint into your local files.

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="6089c2cda6c46803aa55b7a5" link="https://developers.belvo.com/v1.0/recipes/assess-an-individual-endpoint-wrappers" slug="assess-an-individual-endpoint-wrappers" title="Assess an individual endpoint wrappers" />

#### Boilerplate code for index.js

Now that we have our wrappers created, the last step in our setup is to add all the boilerplate code in index.js, which we will use to parse the data we get from our endpoints and display it to the user. In the recipe, we've outlined the main blocks and functionalities of the code.

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="608a6ea660c57700617a19a6" link="https://developers.belvo.com/v1.0/recipes/individual-assessment-boilerplate-code" slug="individual-assessment-boilerplate-code" title="Individual assessment boilerplate code" />

#### Checkpoint

Let's run our project to see that it works! In your terminal:

1. In your terminal, run ` npm run dev`.
2. Go to <a href="http://localhost:3000/" target="_blank">localhost:3000</a> in your browser. 
3. Open the browser developer tools console (so that you can see the data being retrieved).
4. Enter a Fiscal link\_id (that you can create via Postman in the Sandbox environment).

<HTMLBlock>{`
<div>
  <details><summary>ℹ️ Creating a sandbox Fiscal link in Postman</summary>

	<p>To create a sandbox Fiscal link:</p>

	<ol>
		<li>Open up <a href="https://developers.belvo.com/docs/test-with-postman" target="_blank">Belvo's Postman collection</a>.</li>
		<li>Make sure that your environment is set to Sandbox.</li>
		<li>In the <b>Links</b> folder, select the <b>POST - Register</b> request.</li>
		<li>In the body of the request, enter the following:<br>
			<ul>
				<li>For institution, enter<code>"tatooine_mx_fiscal"</code></li>
				<li>For username, enter<code>"PFIS010101000"</code></li>
				<li>For password, <code>"individual"</code></li>
			</ul>
		</li>
		<li>Click <b>Send</b>.</li>
	</ol>

	<p>Done! Now just copy the generated link ID and use it in your app 💪. </p>

</details>
</div>

<style></style>
`}</HTMLBlock>

If everything is working fine, you should see some text on your page and data in the developer console:

![](https://files.readme.io/3361166-sat-guide-checkpoint-1.png "sat-guide-checkpoint-1.png")

> 🚧 Errors?
>
> If you're running into any errors, just make sure that you've:
>
> * you've completed the Setup steps exactly.
> * entered the correct credentials in the .env file (they should be your sandbox credentials).
> * the link*id you've used was created with the\_tatooine* fiscal institution in the [Sandbox environment](https://dashboard.belvo.com/signup/).
> * followed the endpoint wrapper and boilerplate code examples exactly.
>
> If you're still running into troubles, just write to us at: <a href="mailto:support@belvo.com">support\@belvo.com</a>

# Taxpayer details

To get information in the  *Taxpayer details* section, we query Belvo's [Tax Status resource](https://developers.belvo.com/reference/tax-status) to get key information about the person. This includes their:

* official name and contact details
* economic activities they are engaged
* what tax regimens apply to them

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="608917febde247003ff0f909" link="https://developers.belvo.com/v1.0/recipes/get-information-about-the-individual" slug="get-information-about-the-individual" title="Get information about the individual" />

# Risk variables and fraud

The [Tax compliance status](https://developers.belvo.com/reference/tax-compliance-status-1) indicates if a person or a company is paying their taxes correctly and on time. By checking the Tax compliance status, which is generated in real time,  you have a useful indicator for evaluating the likelihood of a person or a company paying their obligations by a given date.

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="6089206d81e8a80064c6deb6" link="https://developers.belvo.com/v1.0/recipes/get-the-tax-compliance-status" slug="get-the-tax-compliance-status" title="Get the tax compliance status" />

# Income insights - risk profile

With Belvo's [Invoices resource,](https://developers.belvo.com/reference/invoices) we can retrieve payroll invoices for an individual for the past year. Then, with this data, we can quickly assess their:

* Average salary
* Employment stability (in other words, how often they change employers)
* Monthly payroll income over the last 12 months

These data points will give you a great view of your clients' stability and fiscal liquidity.

In addition to looking at the client's payroll invoices, we can have a look at their submitted Tax returns to get a high-level view of their earnings from employers (as well as any other economic activities) over the past five years. And to get all that data, Belvo's [Tax returns endpoint](https://developers.belvo.com/reference/tax-returns) will do the trick.

<TutorialTile backgroundColor="#018FF4" emoji="🦉" id="608926ef12254600471585a3" link="https://developers.belvo.com/v1.0/recipes/get-income-insights-and-assess-risk" slug="get-income-insights-and-assess-risk" title="Get income insights and assess risk" />

# Run!

Now that we have all the code in place, let's see how our app works!

1. In your terminal, run ` npm run dev`.
2. Go to <a href="http://localhost:3000/" target="_blank">localhost:3000</a> in your browser. 
3. Enter a Fiscal link\_id (that you can create via Postman in the Sandbox environment).

And now, you should see all the data points for the link ID you've provided. Awesome right!?

<Embed url="https://www.youtube.com/watch?v=qO4uhrPnl3g&feature=youtu.be" title="Fiscal Guide Individual Finished App" favicon="https://www.youtube.com/s/desktop/3a32c481/img/favicon.ico" image="http://i.ytimg.com/vi/qO4uhrPnl3g/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=qO4uhrPnl3g&feature=youtu.be" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FqO4uhrPnl3g%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DqO4uhrPnl3g%26image%3Dhttp%253A%252F%252Fi.ytimg.com%252Fvi%252FqO4uhrPnl3g%252Fhqdefault.jpg%26key%3Df2aa6fc3595946d0afc3d76cbbd25dc3%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

# Summary

In this guide you learned how to:

* Retrieve and display key information about a person from the Tax status endpoint.
* Use the Tax compliance status endpoint to get a general indication of the person's risk.
* Calculate the average monthly salary and the number of employers a person has had in the last 365 days using data from the Invoices endpoint.
* Calculate the total income for a person over the last five years using the Tax returns endpoint.

Great job! Now if you want to test your app with production data, all you need to do is change your `.env` file as follows:

```text Values to change in .env file
BELVO_SECRET_ID={Your production secretID}
BELVO_SECRET_PASSWORD={Your production secretPassword}
BELVO_ENV_URL=https://api.belvo.com
SCRIPT_URL=https://cdn.belvo.io/belvo-widget-1-stable.js
BELVO_ENV=production
```

And done! Then when you want to test it out, just make sure you have a real-world Fiscal link ID to enter into your app.

> 👍 What to do next?
>
> Now that you've completed this guide, let us know if you liked it by clicking the thumbs up or down buttons below. If you have any ideas or suggestions for other guides you'd like to see, just leave us a comment using the feedback button!