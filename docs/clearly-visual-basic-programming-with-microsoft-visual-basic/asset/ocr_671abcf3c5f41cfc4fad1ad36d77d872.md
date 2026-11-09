# Example 2

```
    Dim decOwed As Decimal
    Dim decPaid As Decimal
    Dim decDifference As Decimal
    Decimal.TryParse(txtOwed.Text, decOwed)
    Decimal.TryParse(txtPaid.Text, decPaid)
    decDifference = decPaid - decOwed
    If decDifference < 0 Then
        lblMessage.Text = “You still owe money”
    End If
    lblDifference.Text = decDifference.ToString(“C2”)
```

If the decDifference variable contains a number that is less than zero, the instruction in the true path assigns the string “You still owe money” to the lblMessage control.

**Figure 9-8:** *If…Then…Else statement and comparison operators (continued from previous page)*

The selection structure in Example 1 in Figure 9-8 tells the computer to perform one set of tasks when the condition evaluates to True, but a different set of tasks when the condition evaluates to False. In Example 2, the selection structure tells the computer to perform the one task only when the condition evaluates to True. Keep in mind that comparison operators are evaluated after any arithmetic operators in an expression. When processing the expression 7 > 3 + 5, for example, the computer first will add the number 3 to the number 5, giving 8. It then will compare the number 7 to the number 8. Because 7 is not greater than 8, the expression will evaluate to False.

# **To complete the btnCalc control’s Click event procedure:**

+   1. According to Step 2 in the algorithm from Figure 9-6, the selection structure’s *condition* needs to compare Mary’s sales amount with the number 3000. The “at least 3000” in the algorithm means that the smallest amount that qualifies for the 2% bonus is $3000. Therefore, the correct comparison operator to use in the *condition* is the >= (greater than or equal to) operator. Type **determine bonus rate** and press **Enter**, then type **if decSales >= 3000 then** and press **Enter**. Notice that the Code Editor automatically enters the End If line for you. It also automatically indents the current line.
+   2. If the value stored in the decSales variable is greater than or equal to 3000, the *condition* will evaluate to True. In that case, the bonus rate should be 2%. You will assign the bonus rate, converted to its decimal equivalent, to the decRate variable. Type **decRate = .02** and press **Enter**.