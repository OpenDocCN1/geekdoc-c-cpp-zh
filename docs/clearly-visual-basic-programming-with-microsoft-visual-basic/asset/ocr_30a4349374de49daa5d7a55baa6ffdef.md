```
```vb
Private Sub btnCalc_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCalc.Click
    ' prompts the user to enter two sale amounts, then totals both amounts,
    ' then calls a function to calculate the bonus, then displays the bonus

    Dim strInputSale1 As String
    Dim strInputSale2 As String
    Dim decSale1 As Decimal
    Dim decSale2 As Decimal
    Dim decSum As Decimal
    Dim decBonus As Decimal

    strInputSale1 = InputBox("First sale amount", "Bonus Solution")
    strInputSale2 = InputBox("Second sale amount", "Bonus Solution")

    Decimal.TryParse(strInputSale1, decSale1)
    Decimal.TryParse(strInputSale2, decSale2)
    decSum = decSale1 + decSale2
    decBonus = GetBonus(decSum)
    lblBonus.Text = decBonus.ToString("C2")
End Sub
```
```

**Figure 18-14** *(continued from previous page)*

2. Figure 18-15 shows the code for the GetSum function. In the btnCalc control's Click event procedure, change the decSum = decSale1 + decSale2 statement to decSum = GetSum(decSale1, decSale2).

```
```vb
Private Function GetSum(ByVal decS1 As Decimal, _
    ByVal decS2 As Decimal) As Decimal
    ' totals the sales amounts

    Return decS1 + decS2
End Function
```
```

**Figure 18-15**