---
title: Google Ads Conversion Tracking - Final Solution
linktitle: Final Solution
type: book
date: "2022-01-15T00:00:00+01:00"

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 6
---

## Summary

***

Here's what we did to address everything in Task 1:

1. Made `value` parameter `order.subtotal_price | money_without_currency | remove:','` which removed currency symbol and commas.

:point_right: [Subtask 1 Solution]({{< relref "/growth-media-technology-project/task1/subtask1.md" >}})

2. Set `transaction_id` parameter to `order.order_number`. 

:point_right: [Subtask 2 Solution]({{< relref "/growth-media-technology-project/task1/subtask2.md" >}})

3. Ensured order subtotals over $999.99 are captured by removing commas in Subtask 1.

:point_right: [Subtask 3 Solution]({{< relref "/growth-media-technology-project/task1/subtask3.md" >}})

4. Prevented collection of duplicate orders by setting `transaction_id` to the unique value `order.order_number`.

:point_right: [Subtask 4 Solution]({{< relref "/growth-media-technology-project/task1/subtask4.md" >}})

5.  Encapsulating the conversion script with `{% if first_time_accessed %} {% endif %}` to ensure the script only executes once.

:point_right: [Subtask 5 Solution]({{< relref "/growth-media-technology-project/task1/subtask5-bonus.md" >}})

Putting it all together, the final updated code looks like this:

```html
<!-- Global site tag (gtag.js) - Google Ads: 123456789 -->  
<script async src="https://www.googletagmanager.com/gtag/js?id=AW-123456789"></script>  
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}  
  gtag('js', new Date());
  gtag('config', 'AW-123456789'); 
</script>
{% if first_time_accessed %}  
    <!-- Event snippet for Test conversion page -->  
    <script>
    gtag('event', 'conversion', {  
        'send_to': 'AW-123456789/AbC-D_efG-h12_34-567',  
        'value': {{ order.subtotal_price | money_without_currency | remove:',' }},
        'currency': '{{ checkout.currency }}',
        'transaction_id': '{{ order.order_number }}'  
        });  
    </script> 
{% endif %}
```
For reference, included below is the original Task 1 information:

{{< spoiler text="Click to expand" >}}
## Task 1

***

### Prompt

The client has just created a new Google Ads account, and their Ecommerce platform is Shopify. Below is a broken Google Ads Conversion Tracking Tag. The value parameter should be Order Subtotal (which should not include a currency symbol or any commas), and we will also be including a new parameter, **transaction_id** which will be the Order Number. Revenue is only showing up for orders less than $1,000, and orders are being duplicated. Please help!

### Bonus

Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you
add that as well? 

### Code 

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
{{< /spoiler >}}

Next:
<br />
[Jump to Task 2]({{< relref "/growth-media-technology-project/task2/_index.md" >}})