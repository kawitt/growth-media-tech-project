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

5. Extend the Weekly section table in the **Executive Overview** sheet to 15 weeks.

## Solution

***

Add the two missing rows for `10/31/2020` and `9/12/2020` to the **Executive Overview**. Alternatively, add two rows to the bottom of the table.

## Explanation

***

The original table contains 12 rows starting on 8/22/2020 and ending on 11/28/2020. We already noted in Subtask 4 that rows for `10/31/2020` and `9/12/2020` are missing in the **Executive Overview** table. Likely the preferred solution is to add these missing rows following these steps:

1. Insert an empty row, one each, between `11/7/2020` and `10/24/2020` and between `9/19/2020` and `9/2/2020`.
2. For each new row, select the cells in the above row from the B to N columns.
3. Drag the fill handle (blue square in the bottom right corner) down to fill the empty row.
4. Unfortunately, Sheets isn't quite as smart as Excel, so we need to manually correct the two new dates to `10/31/2020` and `9/12/2020`.

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRWrRGnoU7BA2TuysnAJMGBqAmhKaOQ7Lo9f2FLx4-3P00xVLx1rPUN5k68tZK295FAhQjzs6ZAfMpx/pubhtml?gid=391302551&single=true" >}}
[Click here to view the full sheet](https://docs.google.com/spreadsheets/d/14EzeN-8yZDYyZlXtBgIAXJq3gjbTAL4BMejvUZ4jkV0/edit?usp=sharing)

Alternatively, given the date range provided in **Executive Overview** is 8/2/2020 through 12/1/2020 (cells H8 and H9), we see `8/15/2020` and `8/8/2020` are also missing. In this case we add two rows for the two weeks preceding 8/22/2020 following these steps:

1. Insert two empty rows at the bottom of the table.
2. Select cells B26 to N26.
3. Drag the fill handle (blue square in the bottom right corner) down two rows.
4. Unfortunately, Sheets isn't quite as smart as Excel, so we need to manually correct the two new dates to `8/15/2020` and `8/8/2020`.

Here you can see the completed sheet with the two new rows for a total of 17 weeks:

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vS4ov_cwPuvw6sRquHg2QaXR1mIqpvB9QTZQSYiIoFLuUPlN6lrKxI1BsE3t8i45eUJ6A14UVtboa84/pubhtml?gid=391302551&single=true" >}}
[Click here to view the full sheet](https://docs.google.com/spreadsheets/d/1K9p0SnE4wwdlY5NlMFn7ckW3qKDqKml74wpuZ8BIY44/edit?usp=sharing)
