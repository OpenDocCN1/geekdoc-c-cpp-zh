+   2. See Figure 17-29.

```
~~~vb
Public Class frmMain

    Private Sub CalcBonus(ByVal decS1 As Decimal, _
                          ByVal decS2 As Decimal, _
                          ByRef decBonusAmt As Decimal)
        ' calculates the bonus

        Dim decSum As Decimal

        decSum = decS1 + decS2
        If decSum > 1200 Then
            decBonusAmt = decSum * 0.1
        Else
            decBonusAmt = decSum * 0.08
        End If
        lblBonus.Text = decBonusAmt.ToString("C2")
    End Sub

    Private Sub btnExit_Click ...

    Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
        ' prompts the user to enter two sale amounts, then calls a
        ' sub procedure to calculate the bonus, then displays the bonus

        Dim strInputSale1 As String
        Dim strInputSale2 As String
        Dim decSale1 As Decimal
        Dim decSale2 As Decimal
        Dim decBonus As Decimal

        strInputSale1 = InputBox("First sale amount", "Bonus Solution")
        strInputSale2 = InputBox("Second sale amount", "Bonus Solution")

        Decimal.TryParse(strInputSale1, decSale1)
        Decimal.TryParse(strInputSale2, decSale2)
        Call CalcBonus(decSale1, decSale2, decBonus)
        lblBonus.Text = decBonus.ToString("C2")
    End Sub
End Class
~~~
```

**Figure 17-29**