```
```vb
' assign IDs and prices to the array
gifts(0).strId = "BX35"
gifts(0).intPrice = 13
gifts(1).strId = "CR20"
gifts(1).intPrice = 10
gifts(2).strId = "FE15"
gifts(2).intPrice = 12
gifts(3).strId = "KW10"
gifts(3).intPrice = 24
gifts(4).strId = "MM67"
gifts(4).intPrice = 4

' assign the product ID to a variable
strSearchFor = txtId.Text.ToUpper

' search the array for the product ID
' continue searching until there are
' no more array elements to search or
' the product ID is found
strFound = "N"
Do Until intSubscript = gifts.Length _
    OrElse strFound = "Y"
    If gifts(intSubscript).strId = strSearchFor Then
        strFound = "Y"
    Else
        intSubscript = intSubscript + 1
    End If
Loop

' determine whether the product ID
' was found in the array
If strFound = "Y" Then
    lblPrice.Text = gifts(intSubscript).intPrice.ToString("C0")
Else
    MessageBox.Show("Invalid product ID", _
        "Treasures Gift Shop", MessageBoxButtons.OK, _
        MessageBoxIcon.Information)
End If
End Sub
```
```

**Figure 22-18** *(continued from previous page)*