---
# Title, summary, and page position.
linktitle: Google Ads Conversion Tracking - Shopify Checkout Tag 
summary: Solutions to a broken Google Ads Conversion Tracking tag with Shopify.
weight: 1
icon: ads
icon_pack: fas

# Page metadata.
title: Google Ads Conversion Tracking - Shopify Checkout Tag
date: "2022-01-15T00:00:00Z"
type: book  # Do not modify.
---

## Task Overview

The client has just created a new Google Ads account, and their Ecommerce platform is Shopify. Below is a broken Google Ads Conversion Tracking Tag. The value parameter should be Order Subtotal (which should not include a currency symbol or any commas), and we will also be including a new parameter, **transaction_id** which will be the Order Number. Revenue is only showing up for orders less than $1,000, and orders are being duplicated. Please help!

## Bonus: 

Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you
add that as well? 

## Implicit Subtasks

Below is a list of tasks derived from the prompt, the relevant text from the prompt, and links to the solutions:

1. Make `value` parameter **Order Subtotal** and remove currency symbol and commas.

> The value parameter should be Order Subtotal (which should not include a currency symbol or any commas).

{{< cta cta_text="Jump to Subtask 1 Solution" cta_link="task1-1" >}}

2. Set `transaction_id` parameter to **Order Number**.   

> we will also be including a new parameter, **transaction_id** which will be the Order Number

{{< cta cta_text="Jump to Subtask 2 Solution" cta_link="task1-2" >}}

3. Ensure all revenue amounts are showing.

> Revenue is only showing up for orders less than $1,000

{{< cta cta_text="Jump to Subtask 3 Solution" cta_link="task1-3" >}}

4. Prevent collection of duplicate orders. 

> orders are being duplicated.

{{< cta cta_text="Jump to Subtask 4 Solution" cta_link="task1-4" >}}

5. Add code to ensure script only fires the first time a page is accessed.

> **Bonus** Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you
add that as well?

{{< cta cta_text="Jump to Subtask 5 (Bonus) Solution" cta_link="task1-5-bonus" >}}

## Code

For reference, here is the original code snippet included with the task with some additional formatting to make it pretty. :smile:

```javascript
!-- Global site tag (gtag.js) - Google Ads: 123456789 -->  
<script async src="https://www.googletagmanager.com/gtag/js?id=AW-123456789"></script>  
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}  
  gtag('js', new Date());
  gtag('config', 'AW-123456789'); 
</script>  
<!-- Event snippet for Test conversion page -->  
<script>
  gtag('event', 'conversion', {  
      'send_to': 'AW-123456789/AbC-D_efG-h12_34-567',  
      'value': {{ subtotal_price | money_without_currency }},  
      'currency': '{{ currency }}',  
      'transaction_id': '{{ transaction_id }}'  
    });  
</script> 
```