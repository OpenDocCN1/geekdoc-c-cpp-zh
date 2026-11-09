```
```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.Ev
    ' calculates and displays a gross pay amount

    Dim decHours As Decimal
    Dim decGross As Decimal

    ' calculate and display gross pay, or display an error message
    Decimal.TryParse(txtHours.Text, decHours)
    If decHours >= 0 AndAlso decHours <= 40 Then
        decGross = decHours * 8.35
        lblGross.Text = decGross.ToString("C2")
    Else
        lblGross.Text = "Incorrect hours"
    End If
End Sub
```
```

selection structure

Figure 10-17: Code corresponding to Figure 10-16's algorithm

# **To complete the Gross Pay application's code:**

+   1. Open the **Gross Pay Solution (Gross Pay Solution.sln)** file, which is contained in the ClearlyVB\\Chap10\\Gross Pay Solution folder. If necessary, open the designer window.

+   2. Open the **Code Editor** window, which contains the code for the **btnExit** control's Click event procedure. In the partially completed **btnCalc** control's Click event procedure, enter the selection structure shown in Figure 10-17.

+   3. Save the solution, then start the application. Type **20** in the Hours worked text box, then click the **Calculate** button. Because the hours are within the acceptable range, the **btnCalc** control's Click event procedure calculates the gross pay and displays the result ($167.00) in the Gross pay label.

+   4. Type **45** in the Hours worked text box, then click the **Calculate** button. In this case, the hours worked are not within the acceptable range, so the **btnCalc** control's Click event procedure displays the “Incorrect hours” message in the Gross pay label. See Figure 10-18.

![](bbox=[0.204, 0.69, 0.438, 0.797])

Figure 10-18: Error message displayed in the interface

+   5. Click the **Exit** button. Close the **Code Editor** window, then close the solution.