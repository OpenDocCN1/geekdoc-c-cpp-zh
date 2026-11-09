2. See Figure 15-16.

```
```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays the odd and even numbers from one integer to another

    Dim intNum1 As Integer
    Dim intNum2 As Integer
    Dim intStep As Integer

    Integer.TryParse(txtNum1.Text, intNum1)
    Integer.TryParse(txtNum2.Text, intNum2)

    ' determine stepValue
    If intNum1 > intNum2 Then
        intStep = -1
    Else
        intStep = 1
    End If

    lblOdd.Text = String.Empty
    lblEven.Text = String.Empty

    For intNumber As Integer = intNum1 To intNum2 Step intStep
        If intNumber Mod 2 = 0 Then
            lblEven.Text = lblEven.Text & intNumber.ToString _
                & ControlChars.NewLine
        Else
            lblOdd.Text = lblOdd.Text & intNumber.ToString _
                & ControlChars.NewLine
        End If
    Next intNumber
End Sub
```
```

Figure 15-16