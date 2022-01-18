---
title: Google Sheet Weekly Report Troubleshooting - Subtask 5
linktitle: Subtask 5
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## Description

***

{{< hl >}}...there should be 15 weeks shown{{< /hl >}}
<br />

5. Extend the Weekly section table in the Executive Overview to 15 weeks.

## Solution

***

Add two rows to the bottom of the table in **Executive Overview**.

## Explanation

***

The table as is contains 12 rows starting on 8/22/2020 and ending on 11/28/2020. Given the date range provided in **Executive Overview** cells H8 and H9 is 8/2/2020 through 12/1/2020, it doesn't make sense to add rows for dates after 11/28/2020. Instead, we add two rows for the two weeks preceding 8/22/2020 following these steps:

1. Insert two empty rows at the bottom of the table.
2. Select cells B26 to N26.
3. Drag the fill handle (blue square in the bottom right corner) down two rows.
4. Unfortunately, Sheets isn't quite as smart as Excel, so we need to manually correct the two new dates to 8/15/2020 and 8/8/2020.

Here you can see the completed sheet with the two new rows:

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vS4ov_cwPuvw6sRquHg2QaXR1mIqpvB9QTZQSYiIoFLuUPlN6lrKxI1BsE3t8i45eUJ6A14UVtboa84/pubhtml?gid=391302551&single=true" >}}

