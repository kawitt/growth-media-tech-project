---
title: Google Sheet Weekly Report Troubleshooting - Subtask 6 (Bonus)
linktitle: Subtask 6 (Bonus)
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## Description

***

{{< hl >}}**Bonus** They really want to use periods to show the dates...{{< /hl >}}
<br />

6. Alter the formulas in the Weekly section table to support dates with periods. 

## Solution

***

Change:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&$B14-6,'Raw Data Combined'!$A:$A,"<="&$B14,'Raw Data Combined'!$I:$I,"<>#N/A")
```
To:
```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&SUBSTITUTE($B14,".","/")-6,'Raw Data Combined'!$A:$A,"<="&SUBSTITUTE($B14,".","/"),'Raw Data Combined'!$I:$I,"<>#N/A")
```

## Explanation

***

As mentioned in Subtask 3, valid date formats include `-` or `/`. Dates using `.` aren't interpreted by Sheets as a date, but rather text. Attempting to pass text to our `SUMIFS()` formula when the expected value is a valid date causes the function to fail. 

To ensure the dates used in the formula are valid, apply the [`SUBSTITUTE`](https://support.google.com/docs/answer/3094215?hl=en) function to replace `.` with `/`.

Alternatively, we can accomplish the same thing using the[`REGEXREPLACE`](https://support.google.com/docs/answer/3098245) function:

```swift
# replaces all . with /
=REGEXREPLACE(TO_TEXT($B16), "\.+", "/")
```
For a more robust solution, we can replace all non-digit values with `/`:

```swift
# replaces all non-digit [0-9] characters with /
=REGEXREPLACE(TO_TEXT($B16), "\D+", "/")
# Input
11-29.2020 or 11x29y2020 or 11*29&2020, etc.
# Output
11/29/2020
```

Inserting the code above, the final formula in C14 looks like this:

```swift
=SUMIFS('Raw Data Combined'!D:D,'Raw Data Combined'!$A:$A,">="&REGEXREPLACE(TO_TEXT($B14), "\D+", "/")-6,'Raw Data Combined'!$A:$A,"<="&REGEXREPLACE(TO_TEXT($B14), "\D+", "/"), 'Raw Data Combined'!$I:$I,"<>#N/A")
```

At this point, updating each cell of the table can be arduios. The formula for each cell in a given row contains a unique reference to that row's date. i.e. `">="&$B14-6,` and `"<="&$B14`. Manually editing every cell would be too time consuming. Slightly faster would be using Find and Replace one row at a time. 

We can use Find and replace with a regular expression and capture group to make updating the formulas even faster. From the [Google Sheets Documentation]

> You can replace parts of a regular expression with capture groups. You reference these capture groups in the "Replace" string using
> the format "$<group number>." Note: Capture groups only work with Google Sheets. 

For each row, the date column is always B and the row number changes. Using a capture group we capture the row number and re-insert it into our replace string.

The regular expression `"&(\$B\d*)` matches `"&$B` followed by any number of digits and stores it as capture group `$1`. 

We can use the regular expression `"&REGEXREPLACE(TO_TEXT($1), "\D+", "/")` as the replacement string, using `$1` as the cell address we captured in the find string. 

{{< figure src="task2-6-find-and-replace-regex.png" caption="" numbered="false" >}}

```
{{% callout note %}}
[regex101.com](https://regex101.com) is a great resource for all things regex including testing expressions.
{{% /callout %}}

Here you can see the **Executive Overview** sheet working well even with `.` in dates:

{{< gdocs src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSPCEPP1hgRuK767G4NOxXVYe2SHP1cWTZrgYouH5vbC2jBBxJCdN8qEKTtdHill4Q2CNgNpQmXGAA-/pubhtml?gid=391302551&single=true" >}}