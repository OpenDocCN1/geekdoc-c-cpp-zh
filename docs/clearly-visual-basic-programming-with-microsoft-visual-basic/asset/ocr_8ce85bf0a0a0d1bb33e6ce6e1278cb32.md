![](bbox=[0.181, 0.143, 0.826, 0.291])

**Figure 27-10:** List of properties and methods for a RectangularPool object

+   6. Click **Length** in the list, if necessary, then press **Tab**. Click **another line** in the Code Editor window.
+   
+   7. On your own, change poolSize.decWidth in the second TryParse method to **pool.Width**, and change poolSize.decDepth in the third TryParse method to **pool.Depth**.
+   
+   8. Now use the class’s GetVolume method to get the volume. Select CalcVolume(poolSize) in the statement below the last TryParse method, then type **pool.** (be sure to type the period). Click **GetVolume** in the list, then press **Tab**.
+   
+   9. Finally, use the class’s GetGallons method to get the number of gallons. On your own, change decPoolVolume * 7.48 to **pool.GetGallons**. Figure 27-11 shows the modified Click event procedure. The changes you made to the procedure are shaded in the figure.

```
```vb
Private Sub btnCalc_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCalc.Click
    'calculates volume and number of gallons
    Dim pool As New RectangularPool
    Dim decPoolVolume As Decimal
    Dim decGallons As Decimal

    Decimal.TryParse(txtLength.Text, pool.Length)
    Decimal.TryParse(txtWidth.Text, pool.Width)
    Decimal.TryParse(txtDepth.Text, pool.Depth)

    decPoolVolume = pool.GetVolume
    decGallons = pool.GetGallons

    lblVolume.Text = decPoolVolume.ToString("N0")
    lblGallons.Text = decGallons.ToString("N0")
End Sub
```
```

**Figure 27-11:** Modified Click event procedure for the btnCalc control