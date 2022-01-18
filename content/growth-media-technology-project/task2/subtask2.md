---
title: Google Sheet Weekly Report Troubleshooting - Subtask 2
linktitle: Subtask 2
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## Description

***

{{< hl >}}...the formulas in range B14 to N27 aren’t reading properly...{{< /hl >}}
<br />

2. Correct the formula(s) in the Weekly section in the Executive Overview to ensure proper output.  

## Solution

***

Update the date cell referenced in each formula. For example, C14 in **Executive Overview**:  
<br />

Change:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&$A14-6,'Raw Data Combined'!$A:$A,"<="&$A14,'Raw Data Combined'!$I:$I,"<>#N/A")
```
To:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&$B14-6,'Raw Data Combined'!$A:$A,"<="&$B14,'Raw Data Combined'!$I:$I,"<>#N/A")
```

## Explanation

***

Looking at the syntax again:

```swift
SUMIFS(sum_range, criteria_range1, criterion1, [criteria_range2, criterion2, ...])
```
1. sum_range - The range to be summed. 
2. criteria_range1 - The range to check against criterion1.
3. criterion1 - The pattern or test to apply to criteria_range1.
4. criteria_range2, criterion2, ... - [ OPTIONAL ] - Additional ranges and criteria to check.

The two remaining `SUMIFS()` arguments to review are `criterion1` and `criterion2`. From our formula, we see `criterion1= ">="&$A14-6` and `criterion2= "<="&$A14`. Given the desired formula output is bound by a date range (weekly) for each row, it makes sense that these criterion should reference dates.

In plain terms, `criterion1= ">="&$A14-6` tells the formula to ignore rows with a date before the date six days prior to the value referenced in cell A14 of the  **Executive Overview** sheet. Similarly, `criterion2= "<="&$A14` tells the formula to ignore rows with a date after the date referenced in cell A14.  

An undesired consequence of {{< hl >}}copying the formulas over [from **Weekly Overview**] and dragging them across{{< /hl >}}, all the formulas incorrectly reference date values from cells in column A. Unlike in **Weekly Overview**, the dates in **Executive Overview** are in column B, not A. As in the example above, to correct the reference we simply change `A` to `B` everywhere the formulas reference the date.
<br />

{{< figure src="task2-2-dates-column-b.png" caption="Dates column is B not A" numbered="false" >}}

Of course, we'll need to do this for all formulas in the table, not just cell C14. Rather than change each cell manually, we can use **Find & Replace** to do it much quicker.

{{< figure src="task2-2-replace-date-reference-1.png" caption="Use `ctrl+h` to get there faster." numbered="false" >}}

Below we can see the correct date cell references being used in the table formulas. Unfortunately, we're still not seeing any values. It seems there must be another issue.

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTPrh4r8q7UkoAbsL9podtCBEfBrXAeHdoj2GH4aAw5CzKwsYAFdTPhTIoC4YOoF3KVJoGzKT7lTDnk/pubhtml?gid=391302551&single=true" >}}

