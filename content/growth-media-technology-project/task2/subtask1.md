---
title: Google Sheet Weekly Report Troubleshooting - Subtask 1
linktitle: Subtask 1
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## Description

***

{{< hl >}}...the Weekly section in the Executive Overview isn’t pulling in any data, even though they copied the formulas over and dragged them across.{{< /hl >}}
<br />

1. Correct the formula(s) in the Weekly section in the Executive Overview so they pull in the proper data.

## Solution

***

Correct the data cells referenced in each formula. For example, C14 in **Executive Overview** sheet:  

Change:
```swift
=SUMIFS('Raw Data Combined'!C:C,'Raw Data Combined'!$A:$A,">="&$A14-6,'Raw Data Combined'!$A:$A,"<="&$A14,'Raw Data Combined'!$I:$I,"<>#N/A")
```
To:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&$A14-6,'Raw Data Combined'!$A:$A,"<="&A$14,'Raw Data Combined'!$I:$I,"<>#N/A")
```

## Explanation

***

From the [Google Documentation](https://support.google.com/docs/answer/3238496?hl=en): 

> `=SUMIFS` returns the sum of a range depending on multiple criteria.

Let's take a look at the syntax:
```swift
SUMIFS(sum_range, criteria_range1, criterion1, [criteria_range2, criterion2, ...])
```
1. sum_range - The range to be summed. 
2. criteria_range1 - The range to check against criterion1.
3. criterion1 - The pattern or test to apply to criteria_range1.
4. criteria_range2, criterion2, ... - [ OPTIONAL ] - Additional ranges and criteria to check.

In the example from above, B14 is in the **Clicks** column with `sum_range='Raw Data Combined'!C:C` which references all rows in  column C of the **Raw Data Combined** sheet. Looking at the **Raw Data Combined** sheet, we see **Cicks** data is actually in column D. 

{{< figure src="../task2-1-raw-data-combined-clicks.png" caption="Clicks data is in column D not C" numbered="false" >}}

The remaining arguments that reference columns in the **Raw Data Combined** sheet appear to be correct. Given the desired formula output is weekly, it makes sense `criteria_range1` and `criteria_range2` reference the **Date** column (A) in **Raw Data Combined**. 

For the purpose of this task, we can assume `criteria_range3` is also correct. `'Raw Data Combined'!$I:$I,"<>#N/A"` essentially means ignore rows that contain potentially erroneous and/or missing values in the **Grouping** column (I).

Changing `sum_range` to `'Raw Data Combined'!D:D` now pulls in the correct data for the **Clicks** column. 

We repeat the process using the [fill handle](https://support.google.com/docs/answer/75509?hl=en&co=GENIE.Platform%3DDesktop&oco=1) for all the cells in the table to ensure they reference the correct columns in the **Raw Data Combined** sheet. 

The **Executive Overview** sheet now looks like this:

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTM6Dd8meE1-hr55oQqRHSaBsmEya2m-Xst_gqQmh0SVr_Yf_VEh7iN_0MjvxfVA7NJP0nKxWreDXkx/pubhtml?gid=391302551&single=true" >}}
[Click here to view the full sheet](https://docs.google.com/spreadsheets/d/1BRiU32HTpmm23hb4bARWFOVV7kkAaAEYdR83s8xGNIU/edit?usp=sharing)
<br />
Unfortunately, even though the formulas are now referencing the proper raw data, the table values are still not correct. Let's look at the two remaining arguments in Subtask 2.