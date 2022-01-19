---
title: VBA Title Changes - Subtask 2 (Bonus)
linktitle: Subtask 2 (Bonus)
type: book
date: "2022-01-15T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

## Description

***

{{< hl >}}**Bonus**...How could the script be revised to account for nulls in all fields?{{< /hl >}}
<br />

2. Revise the script to account for nulls in all fields. 

## Solution

***

There are several ways to handle null values depending on desired actions. We can check each variable for null values using `IsNull(Variant)`. 

From the [VBA Documentation](https://docs.microsoft.com/en-us/office/vba/language/reference/user-interface-help/isnull-function):

> IsNull returns True if expression is Null; otherwise, IsNull returns False. If expression consists of more than one variable, Null
> in any constituent variable causes True to be returned for the entire expression.

When a null value is found, we can easily assign a default value or make the error known and halt execution. For instance, using multiple arguments, we can check all variables for null values and alert the user with a message box:

```vb
If IsNull(title, brand, color, size, gender, ptype) = True Then
    MsgBox "At least one of the arguments is null"
End if
```

Alternatively, we can check each argument individually like this:

```vb
' a function that generates a new title using values like above as arguments
Public Function newtitle(title, brand, color, size, gender, ptype) 

    ' set null value to zero length string
    If IsNull(title) = True Then title = ""
    If IsNull(brand) = True Then brand = ""
    If IsNull(size) = True Then size = ""
    If IsNull(color) = True Then color = "" 
    If IsNull(gender) = True Then gender = "" 
    If IsNull(ptype) = True Then ptype = "" 

...
```
A more robust implementation uses a function to handle null cases. This simplifies the code in the `newtitle` function, provides for quick modification of the default value used for null values, and makes adding checks for other undesired values easy.

```vb
Public Function HandleNull(Value As Variant) As Variant
    If IsNull(Value) Then 
        HandleNull = ""
    Else
        HandleNull = Value
    End If
End Function

' a function that generates a new title using values like above as arguments
Public Function newtitle(title, brand, color, size, gender, ptype) 

    title = HandleNull(title)
    brand = HandleNull(brand)
    size = HandleNull(size)
    color = HandleNull(color)
    gender = HandleNull(gender)
    ptype = HandleNull(ptype)
...
```

{{% callout note %}}
The Null value indicates that the Variant contains no valid data. Null is not the same as Empty, which indicates that a variable has not yet been initialized. It is also not the same as a zero-length string (""), which is sometimes referred to as a null string. In other words, if we're also concerned about initialized variables not yet assigned a value or zero-length strings, we'll need to use more than just `IsNull`.
{{% /callout %}}

Microsoft Access effectively has the above `HandleNull` built in as [`Nz()` (NullToZero)](https://support.microsoft.com/en-us/office/nz-function-8ef85549-cc9c-438b-860a-7fd9f4c69b6c):

> You can use the Nz function to return zero, a zero-length string (" "), or another specified value when a Variant is Null. For
> example, you can use this function to convert a Null value to another value and prevent it from propagating through an expression.

Syntax
```vb
Nz ( variant [, valueifnull ] )
```
For example:
```vb
color = Nz(color, 0) ' sets color to 0 if it's null
color = Nz(color, "blue") ' sets color to "blue" if null
color = Nz(color, "Not Specified") ' sets color to "Not Specified" if null 
```
We can even modify our `HandleNull()` function to mimic `Nz()` functionality outside of Access. In this case, `ValueIfNull` defaults to "" if not specified:
```vb
Public Function HandleNull( Value As Variant, optional ValueIfNull As Variant = "") As Variant
    ' using if then else shorthand
    HandleNull = IIf(IsNull(Value), ValueIfNull, Value)
End Function

color = HandleNull(color, "") ' sets color to "" if null
```
Here's how our script could look after adding the code above:
```vb
Public Function HandleNull( Value As Variant, optional ValueIfNull As Variant = "" ) As Variant
    HandleNull = IIf(IsNull(Value), ValueIfNull, Value)
End Function

Public Function newtitle(title, brand, color, size, gender, ptype)  

    Dim ValueIfNull
    ValueIfNull = ""

    title = HandleNull(title, ValueIfNull)
    brand = HandleNull(brand, "Tinuiti")
    size = HandleNull(size, "Unknown Size")
    color = HandleNull(color)
    gender = HandleNull(gender, ValueIfNull)
    ptype = HandleNull(ptype, ValueIfNull)

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