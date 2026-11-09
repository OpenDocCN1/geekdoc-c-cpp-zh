To format the area output to include only two decimal places:

+   1. Change the last assignment statement from lblArea.Text = dblArea to **lblArea.Text = dblArea.ToString("N2")**. Figure 7-14 shows the btnCalc control's Click event procedure.

```
```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays the area of a circle

    ' declare named constant
    Const dblPI As Double = 3.141593

    ' declare variables
    Dim dblArea As Double
    Dim dblRadius As Double

    ' assign radius to a variable
    Double.TryParse(txtRadius.Text, dblRadius)

    ' calculate area
    dblArea = dblRadius * dblRadius * dblPI

    ' display area
    lblArea.Text = dblArea.ToString("N2")
End Sub
```
```

Figure 7-14: Completed btnCalc Click event procedure

+   2. Save and then start the application. Type **2** in the Radius text box, then click the **Calculate** button. The interface shows that the circle's area is 12.57.

+   3. Click the **Exit** button to stop the application. Close the Code Editor window, then close the solution.

# MINI-QUIZ 2

+   1. Write the TryParse method to assign the value entered in the txtIncome control to the decIncome variable.

+   2. Write the statement to declare the intMINIMUM named constant whose value is 55.

+   3. The decSales variable contains the number 56.78. Write the assignment statement to display the value with a dollar sign and no decimal places in the lblSales control. ________