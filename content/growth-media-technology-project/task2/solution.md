---
title: Google Sheet Weekly Report Troubleshooting - Final Solution
linktitle: Final Solution
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 7
---

## Summary

***

Here's what was done to address everything in Task 2:

1. Corrected the data cells referenced in each formula in the **Executive Overview** sheet so that they point to the relevant column in the **Weekly Overview** sheet.

:point_right: [Subtask 1 Solution]({{< relref "/growth-media-technology-project/task2/subtask1.md" >}})

2. Changed the date cell referenced in each formula to from A to match the date column B in **Executive Overview** table.

:point_right: [Subtask 2 Solution]({{< relref "/growth-media-technology-project/task2/subtask2.md" >}})

3. Updated the dates in Column B so that they are properly formatted with either `-` or `/`.

:point_right: [Subtask 3 Solution]({{< relref "/growth-media-technology-project/task2/subtask3.md" >}})

4. Visually verified the values in the Weekly section in the **Executive Overview** match the **Weekly Overview** sheet.

:point_right: [Subtask 4 Solution]({{< relref "/growth-media-technology-project/task2/subtask4.md" >}})

5. Extended the Weekly section table in the Executive Overview to 15 weeks using the fill handle.

:point_right: [Subtask 5 Solution]({{< relref "/growth-media-technology-project/task2/subtask5.md" >}})

6. Bonus. Allowed dates to include `.` by inserting `SUBSTITUTE` or `REGEXREPLACE` in the `SUMIFS()` formula to replace `.` in dates with `/` during execution. 

:point_right: [Subtask 6 Solution]({{< relref "/growth-media-technology-project/task2/subtask6-bonus.md" >}})

Putting it all together, the final updated formula looks like this:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&REGEXREPLACE(TO_TEXT($B14), "\D+", "/")-6,'Raw Data Combined'!$A:$A,"<="&REGEXREPLACE(TO_TEXT($B14), "\D+", "/"), 'Raw Data Combined'!$I:$I,"<>#N/A")
```
And here we see the final Sheet:

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSOar_-xkKkpsRxkMgFZnOUBPN5XBia0Vih2L6jmOJhlp_4y3y8wIcJGU-h1RePHd-hpYeJCeDNFrZb/pubhtml?gid=391302551&single=true" >}}

For reference, included below is the original Task 2 information:

{{< spoiler text="Click to expand" >}}

## Task 2

***

### Prompt

A fellow account manager has been working on their weekly report for a client, but can’t quite seem to get it working. The individual sheets work, but the Weekly section in the Executive Overview isn’t pulling in any data, even though they copied the formulas over and dragged them across. It looks like the formulas in range B14 to N27 aren’t reading properly, but the dates in Column B look different too. Once you’re able to figure that out, the data needs to match the Weekly sheet, and there should be 15 weeks shown. Please help, and explain your findings. 

### Bonus

They really want to use periods to show the dates, maybe there’s a way to make it work? 

### File Link

Here is their report (File > Make A Copy): 
https://docs.google.com/spreadsheets/d/1nAediTxPONsJwQoWwFwjqSadE51r0LT3_Wv_GGCLo7c/ edit 

{{< /spoiler >}}

***


Next:
<br />
[Jump to Task 3]({{< relref "/growth-media-technology-project/task3/_index.md" >}})