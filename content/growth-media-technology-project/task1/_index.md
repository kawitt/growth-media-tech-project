---
# Title, summary, and page position.
linktitle: Task 1 Overview
summary: Solutions to a broken Google Ads Conversion Tracking tag with Shopify.
weight: 1
icon: tags
icon_pack: fas

# Page metadata.
title: Google Ads Conversion Tracking - Shopify Checkout Tag
date: "2022-01-15T00:00:00Z"
type: book  # Do not modify.
---

## Task 1

***

### Prompt

The client has just created a new Google Ads account, and their Ecommerce platform is Shopify. Below is a broken Google Ads Conversion Tracking Tag. The value parameter should be Order Subtotal (which should not include a currency symbol or any commas), and we will also be including a new parameter, **transaction_id** which will be the Order Number. Revenue is only showing up for orders less than $1,000, and orders are being duplicated. Please help!

### Bonus

Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you add that as well? 

### Code 

For reference, here is the original code snippets included with the task with some additional formatting to make it pretty. :smile:

{{< spoiler text="Click to view the code" >}}
```html
<!-- Global site tag (gtag.js) - Google Ads: 123456789 -->  
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
{{< /spoiler >}}

## Inferred Subtasks

***

Below is a list of tasks derived from the prompt, the relevant text from the prompt, and links to the solutions:

{{< hl >}}The value parameter should be Order Subtotal (which should not include a currency symbol or any commas).{{< /hl >}}
<br />

1. Make `value` parameter **Order Subtotal** and remove currency symbol and commas.

:point_right: [Subtask 1 Solution]({{< relref "/growth-media-technology-project/task1/subtask1.md" >}})

{{< hl >}}we will also be including a new parameter, **transaction_id** which will be the Order Number.{{< /hl >}}
<br />

2. Set `transaction_id` parameter to **Order Number**.   

:point_right: [Subtask 2 Solution]({{< relref "/growth-media-technology-project/task1/subtask2.md" >}})

{{< hl >}}Revenue is only showing up for orders less than $1,000{{< /hl >}}
<br />

3. Ensure all revenue amounts are showing.

:point_right: [Subtask 3 Solution]({{< relref "/growth-media-technology-project/task1/subtask3.md" >}})

{{< hl >}}orders are being duplicated.{{< /hl >}}
<br />

4. Prevent collection of duplicate orders. 

:point_right: [Subtask 4 Solution]({{< relref "/growth-media-technology-project/task1/subtask4.md" >}})

{{< hl >}}**Bonus** Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you
add that as well?{{< /hl >}}
<br />

5. Add code to ensure script only fires the first time a page is accessed.

:point_right: [Subtask 5 Solution]({{< relref "/growth-media-technology-project/task1/subtask5-bonus.md" >}})

## Final Solution

***

Don't want to wade through the subtasks?

{{< cta cta_text=":point_right: Jump to Task 1 Solution" cta_link="/growth-media-technology-project/task1/solution" >}}

**NEXT**  
[Google Ads Conversion Tracking - Subtask 1]({{< relref "/growth-media-technology-project/task1/subtask1.md" >}})