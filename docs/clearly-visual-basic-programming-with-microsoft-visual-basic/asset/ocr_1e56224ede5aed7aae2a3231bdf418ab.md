# ANSWERS TO “TRY THIS”
EXERCISES

+   1. See Figure 19-21.

```
~~~vb
Private Sub btnVerify_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnVerify.Click
    ' searches the array for the name of a guest, then displays
    ' an appropriate message

    Dim strPartyList() As String = {"Jacob", "Karen", "Gregory", _
                                    "Jerome", "Susan", "Michele", _
                                    "Heather", "Jennifer", "George"}

    Dim strSearchFor As String
    Dim intSubscript As Integer
    Dim strFound As String

    strSearchFor = txtGuest.Text.ToUpper

    intSubscript = 0
    strFound = "N"
    Do While strFound <> "Y" AndAlso intSubscript < strPartyList.Length
        If strPartyList(intSubscript).ToUpper = strSearchFor Then
            strFound = "Y"
        Else
            intSubscript = intSubscript + 1
        End If
    Loop

    If strFound = "Y" Then
        MessageBox.Show(strSearchFor & " is invited.", _
                        "Party List", MessageBoxButtons.OK, _
                        MessageBoxIcon.Information)
    Else
        MessageBox.Show(strSearchFor & " is not invited.", _
                        "Party List", MessageBoxButtons.OK, _
                        MessageBoxIcon.Information)
    End If
End Sub
~~~
```

Figure 19-21