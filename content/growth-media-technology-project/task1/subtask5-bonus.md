---
title: Google Ads Conversion Tracking - Subtask 5 (Bonus)
linktitle: Subtask 5 (Bonus)
type: book
date: "2022-01-15T00:00:00+01:00"

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---


## Description

***

{{< hl >}}**Bonus** Shopify has a piece of code that only allows a script to fire the first time a page is accessed, can you
add that as well?{{< /hl >}}
<br />

5. Add code to ensure script only fires the first time a page is accessed.

## Solution

***

Encapsulate the event snippet with the following Liquid **first_time_accessed** property: `{% if first_time_accessed %}` and `{% endif %}`.

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

## Explanation

***

Actually, we already addressed this in Subtask 4 where a more detailed explanation is provided. To reiterate, surrounding the conversion event code snippet, or any code for that matter, with `{% if first_time_accessed %}` and `{% endif %}` ensures the code only runs once and prevents capture of duplicate conversions.