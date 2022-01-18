---
# Title, summary, and page position.
linktitle: Task 3 Overview
summary: Walking through a VBA script that changes titles.
weight: 2
icon: microsoft
icon_pack: fab

# Page metadata.
title: VBA Title Changes  
date: "2022-01-15T00:00:00Z"
type: book  # Do not modify.
---

## Task 3

***

### Prompt

The account manager is ready to update their titles. We have several variables, including Title, Brand, Color, Size, Gender, and Product Type. Given the rules below, what will be the outcome? Please explain the order of operations, and include a variable-worded output (e.g. <title> with <size> in <color>)

### Bonus

These functions often break if there is a null field. How could the script be revised to account for nulls in all fields? 

### Sample Rules

Title = longsleeve flannel 
Brand = tinuiti 
Size = medium 
Color = dark red/black 
Gender = male 
Product Type = apparel > t-shirts and tops > shirts 

### Code 

For reference, here is the original code snippets included with the task with some additional formatting to make it pretty. :smile:

{{< spoiler text="Click to view the code" >}}
```vb
Public Function newtitle(title, brand, color, size, gender, ptype)  

    newtitle = ProperCase(title)  

    If IsNull(size) = False And size <> "One Size" Then  
        newtitle = newtitle & ", Size " & size  
    End If

    color = Replace(color, "Light", "")  
    color = Replace(color, "Dark", "")  
    color = Replace(color, "/", " and ")  
    newtitle = newtitle & " in " & ProperCase(color)  
  
    If InStr(newtitle, "flannel") > 0 And InStr(ptype, "shirt") > 0 Then  
        newtitle = Replace(newtitle, "Flannel", "Plaid Flannel")  
    End If  
  
    If gender = "male" Then  
        newtitle = "Men’s " & newtitle  
    Else 
        newtitle = "Women’s " & newtitle  
    End If  
  
    If brand <> "Default" Then  
        newtitle = brand & " " & newtitle  
    End If   
    
    newtitle = Trim(Replace(Replace(newtitle, "  ", " "), "  ", ""))   

End Function 
```
{{< /spoiler >}}

## Inferred Subtasks

***

Below is a list of tasks derived from the prompt, the relevant text from the prompt, and links to the solutions:

{{< hl >}}Given the rules below, what will be the outcome? Please explain the order of operations, and include a variable-worded output (e.g. <title> with <size> in <color>) {{< /hl >}}
<br />

1. Using the provided sample rules, provide the output and explain the operations line by line. 

:point_right: [Subtask 1 Solution]({{< relref "/growth-media-technology-project/task3/subtask1.md" >}})

{{< hl >}}**Bonus**...How could the script be revised to account for nulls in all fields?{{< /hl >}}
<br />

2. Alter the formulas in the Weekly section table to support dates with periods. 

:point_right: [Subtask 2 Solution]({{< relref "/growth-media-technology-project/task2/subtask2-bonus.md" >}})


## Final Solution

***

Don't want to wade through the subtasks?
<br />

point_right: [Jump to Solution]({{< relref "/growth-media-technology-project/task3/solution.md" >}})
