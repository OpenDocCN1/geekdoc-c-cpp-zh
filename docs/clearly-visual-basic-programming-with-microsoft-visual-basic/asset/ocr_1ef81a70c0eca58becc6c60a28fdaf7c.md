![](bbox=[0.13, 0.145, 0.42, 0.31])

txtType control

**Figure 12-17:** Interface for the Shady Hollow Hotel-Version 2 application

```
~~~vb
Private Sub btnDisplay_Click(ByVal sender As Object, ByVal e As System.Ev...
    ' displays a room's daily rate
    Dim strType As String
    Dim intDailyRate As Integer

    ' assign room type to a variable
    strType = txtType.Text.ToUpper

    If strType = "S" Then
        intDailyRate = 90
    ElseIf strType = "D" Then
        intDailyRate = 115
    End If

    ' display daily rate
    lblDaily.Text = intDailyRate.ToString("C0")
End Sub
~~~
```

assigns the contents of the text box, in uppercase, to the variable

test each path in this selection structure

**Figure 12-18:** Display Rate button's Click event procedure in the Shady Hollow Hotel-Version 2 application

Before testing the Shady Hollow Hotel-Version 2 application, you will create a set of test data. Recall that the first guideline in Figure 12-1 is to test the application without entering any data. This application requires the user to enter only one item of data: the room type. If the user clicks the Display Rate button without entering the room type, the procedure should display $0 in the Daily rate box. The second guideline in Figure 12-1 pertains to numbers entered in a text box. In this application, the user will be entering a string (rather than a number) in the txtType control; therefore, you can skip the second guideline. The third guideline covers selection structures. The only selection structure in the application's code is located in the Display Rate button's Click event procedure. According to the third guideline, you need to test each path in the selection structure. If the path condition compares strings, you should include uppercase and lowercase text in the test data. Begin by making a list of valid values that the user might enter as the room type. In this case, the user might enter any of the following letters: S, s, D, or d. The expected results are $90, $90, $115, and $115. Now consider values that the user