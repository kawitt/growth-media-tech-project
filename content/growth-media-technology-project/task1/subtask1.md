---
title: Google Ads Conversion Tracking - Subtask 1
linktitle: Subtask 1
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## Description

***

{{< hl >}}The value parameter should be Order Subtotal (which should not include a currency symbol or any commas).{{< /hl >}}
<br />

1. Make `value` parameter **Order Subtotal** and remove currency symbol and commas.

## Solution

***

Change:
```js
      'value': {{ subtotal_price | money_without_currency }},
```
To:
```js
      'value': {{ order.subtotal_price | money_without_currency | remove:',' }},    
```

## Explanation

***

From the provided code snippet, we see the `value` parameter is currently the **subtotal price** formatted with the `money_without_currency` [money filter](https://shopify.dev/api/liquid/filters/money-filters):

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

According to [Shopify documentation](https://shopify.dev/api/liquid/objects/order), the `order` object provides access to the **order subtotal** through the `subtotal_price` attribute which gives us `'value': {{ order.subtotal_price }}`.

{{% callout warning %}}
Various sources reference `checkout.subtotal_price` or just `{{ subtotal_price }}`, often divided by 100. However, Shopify's current [`checkout` object documentation](https://shopify.dev/api/liquid/objects/checkout) does not include the `subtotal_price` attribute. My assumption is at some point `subtotal_price` was moved from `checkout` to `order`. It's not clear which `{{ subtotal_price }}` references or if `checkout.subtotal_price` is still available. The need to divide by 100 suggests checkout.subtotal_price provides the price as a number in cents i.e. $1.45 as 145. 
{{% /callout %}}

As shown below, the addition of `money_without_currency` filter divides the price by 100, negating the need to do it manually, and returns it without the currency symbol. 

```
# Input:
{{ 145 | money_without_currency }}
# Output:
1.45
```

Since the conversion value must be numeric, we use the [Liquid String Filter](https://shopify.dev/api/liquid/filters/string-filters#remove) `remove:','` to ensure commas are removed for price values over 1,000. 

{{% callout note %}}
On a related note, we provide the currency ISO code separately since we stripped it from the subtotal. While `'currency': {{ currency }}` may work, explicitly using the `checkout.currency` is likely more reliable in the long term: `'currency': '{{ checkout.currency }}',`
{{% /callout %}}