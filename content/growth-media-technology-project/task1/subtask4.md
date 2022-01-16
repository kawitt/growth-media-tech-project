---
title: Google Ads Conversion Tracking - Subtask 4
linktitle: Subtask 4
type: book
date: "2022-01-15T00:00:00+01:00"

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## Description

***

{{< hl >}}orders are being duplicated.{{< /hl >}}
<br />

4. Prevent collection of duplicate orders. 

## Solution

***

1. Encapsulate the event snippet with the following Liquid tags: `{% if first_time_accessed %}` and `{% endif %}`.

```HTML
{% if first_time_accessed %}
    <!-- Event snippet for Test conversion page --> 
    <script>
    gtag('event', 'conversion', {  
        'send_to': 'AW-123456789/AbC-D_efG-h12_34-567',  
        'value': {{ subtotal_price | money_without_currency }},  
        'currency': '{{ currency }}',  
        'transaction_id': '{{ transaction_id }}'  
        });  
    </script>
{% endif %}
```

2. Ensure the `transaction_id` parameter includes a unique value like **Order Number**: `'transaction_id': '{{ order.order_number }}'`

## Explanation

***

1. As we see in the [Shopify Documentation](https://help.shopify.com/en/manual/orders/status-tracking/customize-order-status/first-time-accessed):

> It is common to include scripts that track sales conversions on the order status page because it is the final page of checkout
> However, customers who return to check their order status might count as a second sale in your analytics.
>
> To prevent your analytics from counting customers more than once, you can add the first_time_accessed property around some or all of
> your additional scripts. To do this, use a Liquid if statement, and place any scripts that you only want to run once between {% if 
> first_time_accessed %} and {% endif %} tags.

Surrounding the conversion event code snippet as shown ensures duplicate conversions won't be captured on page reloads.

2. According to the [Google Ads Documentation](https://support.google.com/google-ads/answer/6386790?hl=en):

> If there are 2 conversions for the same conversion action with the same transaction ID, Google Ads will know the second conversion
> is a duplicate, you will see an error message, and the duplicate conversion won’t be counted.

We avoid capturing duplicate conversions by ensuring the `transaction_id` parameter is set to a unique value. Thanks to Subtask 2, we've already accomplished this with `'transaction_id': '{{ order.order_number }}'`.