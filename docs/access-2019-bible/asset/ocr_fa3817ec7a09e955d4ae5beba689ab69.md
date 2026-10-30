# Part VI: Microsoft Access Programming Fundamentals

```
Next i

For i = 1 To 5
    Debug.Print Rndom(i)
Next i

End Sub
```

Because array indexes increase by one, For...Next loops are a common way to access all the elements in an array.

The arrays we’ve looked at so far are known as *one-dimensional arrays*. One-dimensional arrays are like lists—they have many rows, but only one column. You can also have two-dimensional arrays. Two-dimensional arrays are like tables—they have many rows and columns. Declare a two-dimensional array using a comma to separate the bounds of the first dimension from the bounds of the second dimension:

```
Dim aContact(1 To 10, 1 To 3) As String
```

The aContact array has 30 places to store data. This array might be used to store three pieces of data for ten contacts. Reading and writing to a two-dimensional array requires that you specify the index for both dimensions:

```
Sub TwoDArray()

    Dim aPotus(1 To 2, 1 To 3)
    Dim i As Long

    aPotus(1, 1) = "George"
    aPotus(1, 2) = "Washington"
    aPotus(1, 3) = "1789-1797"
    aPotus(2, 1) = "John"
    aPotus(2, 2) = "Adams"
    aPotus(2, 3) = "1797-1801"

    For i = 1 To 2
        Debug.Print aPotus(i, 1) & Space(1) & aPotus(i, 2) & Space(1) & _
            "was President in the years" & Space(1) & aPotus(i, 3)
    Next i

End Sub
```

> **NOTE**
> 
> You can specify dimensions beyond two, but those arrays can get very difficult to manage. If you need to store that much data, consider a user-defined type or a custom class module.