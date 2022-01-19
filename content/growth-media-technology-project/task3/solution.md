---
title: VBA Title Changes - Solution
linktitle: Final Solution
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## Summary

***

Here's what we did to address everything in Task 3:

1. Using the provided sample rules, we determined final output is `Tinuitit Men's Longsleeve Plaid Flannel, Size medium in Red And Black' and explained all operations with inline comments.

:point_right: [Subtask 1 Solution]({{< relref "/growth-media-technology-project/task3/subtask1.md" >}})

2. We added the `HandleNull()` function to assign default values to null variants. We inserted calls at the top of the `newtitle` function to check each argument before attempting to use them.

:point_right: [Subtask 2 Solution]({{< relref "/growth-media-technology-project/task3/subtask2-bonus.md" >}})

## Solution

***

The final code below includes all our additions plus the requested inline comments:

```vba
' assume the following:
title = "longsleeve flannel" 
brand = "tinuiti"
size = "medium" 
color = "dark red/black" 
gender = "male" 
ptype = "apparel > t-shirts and tops > shirts" 

Public Function HandleNull( Value As Variant, optional ValueIfNull As Variant = "" ) As Variant
    HandleNull = IIf(IsNull(Value), ValueIfNull, Value)
End Function

' a function that generates a new title using values like above as arguments
Public Function newtitle(title, brand, color, size, gender, ptype) 

    ' declare default value if null
    Dim ValueIfNull
    ' make the default value ""
    ValueIfNull = ""

    ' check each argument for null value, assign value of second argument if null
    title = HandleNull(title, ValueIfNull)
    brand = HandleNull(brand, "Tinuiti")
    size = HandleNull(size, "Unknown Size")
    color = HandleNull(color)
    gender = HandleNull(gender, ValueIfNull)
    ptype = HandleNull(ptype, ValueIfNull)

    ' Pass title to ProperCase() function in order to 
    ' convert title to proper case, then assign to newtitle
    ' ProperCase() likely contains something like ProperCase = StrConv(strText, vbProperCase)
    newtitle = ProperCase(title) ' "Longsleeve Flannel" 
    
    ' if size is not null and not "One Size"
    If IsNull(size) = False And size <> "One Size" Then
        ' add ", Size " size to the end of newtitle  
        newtitle = newtitle & ", Size " & size '"Longsleeve Flannel, Size medium" 
    End If

    ' remove "Light" from color
    color = Replace(color, "Light", "") '"dark red/black" 
    ' remove "Dark" from color
    color = Replace(color, "Dark", "") '" red/black"
    ' change "/" to " and " in color
    color = Replace(color, "/", " and ") '" red and black"

    ' add " in " to end of newtitle, make color proper case and add to end of newtitle 
    newtitle = newtitle & " in " & ProperCase(color) ' "Longsleeve Flannel, Size medium in  Red And Black"

    ' Use InStr() to check if newtitle contains "flannel" and if ptype contains "shirt"
    ' if "flannel" is in newtitle and "shirt" is in ptype 
    If InStr(newtitle, "flannel") > 0 And InStr(ptype, "shirt") > 0 Then  
        ' Replace "flannel" with "Plaid Flannel" in newtitle
        newtitle = Replace(newtitle, "Flannel", "Plaid Flannel") ' "Longsleeve Plaid Flannel, Size medium in  Red And Black" 
    End If  

    ' if gender is "male"
    If gender = "male" Then ' "male"
        ' add "Men's " to front of newtitle
        newtitle = "Men’s " & newtitle ' "Men's Longsleeve Plaid Flannel, Size medium in  Red And Black"
    Else ' if gender is not "male"
        ' add "Women's " to front of newtitle
        newtitle = "Women’s " & newtitle ' "Men's Longsleeve Plaid Flannel, Size medium in  Red And Black"
    End If  

    ' if brand is not "Default"
    If brand <> "Default" Then ' "tinuiti" 
        ' add brand followed by a space in front of newtitle
        newtitle = brand & " " & newtitle ' "Tinuitit Men's Longsleeve Plaid Flannel, Size medium in  Red And Black"  
    End If   
    
    ' use Replace() to change double spaces to single in newtitle
    ' repeat with the updated newtitle to change new double spaces that may exist to single
    ' use Trim() to remove whitespace from both ends of newtitle
    newtitle = Trim(Replace(Replace(newtitle, "  ", " "), "  ", "")) ' "Tinuitit Men's Longsleeve Plaid Flannel, Size medium in Red And Black"  

End Function
' declare variable
Dim newtitleStr As String

' call the newtitle function with our example values
newtitleStr = newtitle(title, brand, color, size, gender, ptype)

' output returned new title using either Debug.Print newtitle, MsgBox newtitle, or 
Console.WriteLine(newtitleStr)

' Output:
"Tinuitit Men's Longsleeve Plaid Flannel, Size medium in Red And Black"
```
This completes all three tasks. Thanks for following along and have a great day!

**NEXT**  
[:point_right: Jump to Project Overview]({{< relref "/growth-media-technology-project/_index.md" >}})