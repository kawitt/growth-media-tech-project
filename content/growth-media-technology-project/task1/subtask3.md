---
title: Google Ads Conversion Tracking - Subtask 3
linktitle: Subtask 3
type: book
date: "2022-01-15T00:00:00+01:00"

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## Description

***

{{< hl >}}Revenue is only showing up for orders less than $1,000{{< /hl >}}
<br />

3. Ensure all revenue amounts are showing.

## Solution

***

Use the [Liquid string filter](https://shopify.dev/api/liquid/filters/string-filters#remove) `remove:','` with the `value` parameter to ensure commas are removed for price values over 1,000. 

Example:
```js
# Input:
123456

'value': {{ subtotal_price | money_without_currency }},
# Output:
1,234.56

'value': {{ order.subtotal_price | money_without_currency | remove:',' }},    
# Output:
1234.56

```

## Explanation

***

Revenue only showing for orders less than $1,000 was likely due to the inclusion of commas in the submitted `value` parameter. Remember Google expects the conversion value to be a number. Luck for us, this issue was already resolved in Subtask 1 with the addition of `remove:','` which removes all commas i.e. 1,000.00 becomes 1000  

{{% callout note %}}
[The Shopify Cheat Sheet](https://www.shopify.com/partners/shopify-cheat-sheet) is an excellent resource for building Shopify Themes with Liquid including available Tags, Filters, and Objects.
{{% /callout %}}