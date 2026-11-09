2. See Figure 19-22.

```
```vb
Private Sub btnCount_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCount.Click
    ' searches the array for a letter grade, then displays the
    ' number of times the letter grade appears in the array

    Dim strGrades() As String = {"C", "B", "C", "A", "B", "A", _
                                "F", "A", "B", "B", "C"}

    Dim strSearchFor As String
    Dim intCounter As Integer   ' counter

    strSearchFor = txtLetterGrade.Text.ToUpper
    intCounter = 0

    For intSubscript As Integer = 0 To strGrades.Length - 1
        If strGrades(intSubscript) = strSearchFor Then
            intCounter = intCounter + 1
        End If
    Next intSubscript

    MessageBox.Show(strSearchFor & ": " & intCounter.ToString, _
                    "Grades", MessageBoxButtons.OK, _
                    MessageBoxIcon.Information)
End Sub
```
```

**Figure 19-22**