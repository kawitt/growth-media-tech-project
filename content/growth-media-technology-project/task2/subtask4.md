---
title: Google Sheet Weekly Report Troubleshooting - Subtask 4
linktitle: Subtask 4
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## Description

***

{{< hl >}}...the data needs to match the Weekly sheet...{{< /hl >}}
<br />

4. Verify the values in the Weekly section in the **Executive Overview** match the Weekly sheet. 

## Solution

***

Visually compare the **Executive Overview** and **Weekly Overview** tables.

## Explanation

***

For larger tables, it might be necessary to implement something like conditional formatting or vlookups to identify mismatched values. Because these tables are small, it's easy to simply compare them row by row for any discrepancies. 

{{< figure src="../task2-4-verify-data.png" caption="The tables match." numbered="false" >}}

Comparing the two tables we see the date in **Executive Overview** B24 is `9/2/2020` while in the **Weekly Overview** table it's `9/5/2020`. Counting by weeks, the correct date is `9/5/2020`. In the next Subtask you'll see the date has been corrected. The values in the remaining rows appear to match.

{{% callout note %}}
It's worth noting that while the data in the tables match, compared to the **Weekly Overview** table, the **Executive Overview** table is actually missing rows for `10/31/2020` and `9/12/2020`. We'll address that in Subtask 5 as well.
{{% /callout %}}