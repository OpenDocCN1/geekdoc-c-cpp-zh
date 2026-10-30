```
```vb
vaWords = Split("Now is the title.", Space(1))

For i = LBound(vaWords) To UBound(vaWords)
    Debug.Print vaWords(i)
Next i

End Sub
```
```

The vaWords variable will be a variant array containing four elements: Now, is, the, and time. The delimiter—in this case, a single space—is not included in the elements. The period at the end is included, making the last element time. (with a period) rather than time (without a period).

# NOTE

Several VBA functions, including Split, have a compare argument that dictates whether text comparisons are case sensitive. It's always an optional argument and is omitted in the example in this section. Valid choices for a compare argument are vbBinaryCompare (case sensitive), vbDatabaseCompare (uses the default compare for your database), and vbTextCompare (not case sensitive).

# The Join function

The Join function is the opposite of Split. Join takes an array and returns a string. The syntax for Join is:

```
```vb
Join(source_array, [delimiter])
```
```

The first argument is the one-dimensional array to be converted into a String. The source_array can be any data type that VBA can convert into a String, even numbers and dates. The delimiter is the character or characters to be inserted between the elements of the array:

```
```vb
Sub TheJoinFunction()

    Dim sResult As String
    Dim aWords(1 To 5) As String

    aWords(1) = "The"
    aWords(2) = "quick"
    aWords(3) = "brown"
    aWords(4) = "fox"
    aWords(5) = "jumped"

    sResult = Join(aWords, Space(1))

    Debug.Print sResult

End Sub
```
```