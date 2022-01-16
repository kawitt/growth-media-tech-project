---
title: Google Ads Conversion Tracking - Subtask 2
linktitle: Subtask 2
type: book
date: "2022-01-15T00:00:00+01:00"

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## Description

***

{{< hl >}}we will also be including a new parameter, **transaction_id** which will be the Order Number.{{< /hl >}}
<br />

2. Set `transaction_id` parameter to **Order Number**.   


## Solution

***

Change:
```js
      'transaction_id': '{{ transaction_id }}'  
```
To:
```js
      'transaction_id': '{{ order.order_number }}'     
```

## Explanation

***

We can see in the provided code snippet, the `transaction_id` parameter is actually already included and set to `{{ order_number }}`.

```HTML
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

According to Shopify's documentation, **Order Number** is an attribute of both the `checkout` and `order` objects. The available documentation doesn't clarify which object `{{ order_number }}` references. One important caveat with `checkout.order_number`:

> Depending on the payment provider, the order might not have been created yet on the checkout order status page.

To ensure the **Order Number** actually exists, we'll use `order.order_number`.