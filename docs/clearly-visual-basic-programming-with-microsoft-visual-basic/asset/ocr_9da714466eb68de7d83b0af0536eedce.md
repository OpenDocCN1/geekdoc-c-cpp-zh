![](bbox=[0.195, 0.131, 0.461, 0.3])

**Figure 22-5: Sample run of the Willow Pools application**

```
```vb
Private Function CalcVolume(ByVal decLen As Decimal, _
                            ByVal decWid As Decimal, _
                            ByVal decDep As Decimal) As Decimal
    Dim decVol As Decimal

    If decLen > 0 AndAlso decWid > 0 AndAlso decDep > 0 Then
        decVol = decLen * decWid * decDep
    Else
        decVol = 0
    End If
    Return decVol
End Function

Private Sub btnCalc_Click(ByVal sender As Object, _
        ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates volume and number of gallons

    Dim decPoolLength As Decimal
    Dim decPoolWidth As Decimal
    Dim decPoolDepth As Decimal
    Dim decPoolVolume As Decimal
    Dim decGallons As Decimal

    Decimal.TryParse(txtLength.Text, decPoolLength)
    Decimal.TryParse(txtWidth.Text, decPoolWidth)
    Decimal.TryParse(txtDepth.Text, decPoolDepth)

    decPoolVolume = _
        CalcVolume(decPoolLength, decPoolWidth, decPoolDepth)
    decGallons = decPoolVolume * 7.48

    lblVolume.Text = decPoolVolume.ToString("N0")
    lblGallons.Text = decGallons.ToString("N0")
End Sub
```
```

receives 3 variables
*by value*

returns the volume

declares 3 variables
to store the input data

passes 3 variables to the
CalcVolume function

**Figure 22-6: Code for the Willow Pools application (without a structure)**