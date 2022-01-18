---
title: Google Sheet Weekly Report Troubleshooting - Subtask 3
linktitle: Subtask 3
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## Description

***

{{< hl >}}...but the dates in Column B look different too.{{< /hl >}}
<br />

3. Ensure the dates in Column B are properly formatted.

## Solution

***

Change the values in Column B to proper date format. For example, B14 in **Executive Overview** change `11.28.2020` to `11/28/2020`.

## Explanation

***

According to [Google Sheets Documentation](), valid date formats include `-` or `/`. Dates using `.` aren't interpreted by Sheets as a date, but rather text. Attempting to pass text to our `SUMIFS()` formula when the expected value is a valid date causes the function to fail. 

The simplest resolution is to use **Find & Replace** to replace all `.` with `/` or `-` in the values found in B14-26.

Below we can see the correct date format being used in Column B. Like magic, all the table cells populate once proper dates are provided.

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSsaVInWzwe7kOtZUxfX0sO7g8SD57gzmUHAVSmg7WGS9Ky7EGIJs5G4Hx4Yk81-mpf08kNcYQcFmYf/pubhtml?gid=391302551&single=true" >}}

