---
title: Boost - Quote Flow
deprecated: false
hidden: false
metadata:
  robots: index
---
[block:api-header]
{
  "title": "Summary"
}
[/block]
<div>
<body>
<style>
.colorme {color: #0097A7; }
.highlightme { background-color:#E6E567; }

</style>
Once the Customer has provided the necessary information on your front end you will send a single <span class="highlightme">POST</span> request to the <span class="highlightme">/quotes</span> endpoint. That request should contain the relevant Rating Factors, limits, deductibles, Customer data, and some time-based attributes like when the Policy or Coverage should go into effect and when it should be terminated. Assuming that the request was formatted correctly, a Quote record will be created, or modified in the case of a Customer updating (via <span class="highlightme">PATCH</span>) previously submitted requests, in Boost’s system. That Quote will be returned in a quote state defined by the status field.
[block:api-header]
{
  "title": "Quote Walkthrough"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ca88104-Screen_Shot_2020-10-02_at_8.47.40_AM.png",
        "Screen Shot 2020-10-02 at 8.47.40 AM.png",
        964,
        1226,
        "#e5eaea"
      ]
    }
  ]
}
[/block]