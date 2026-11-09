+   2. See Figure 26-7.

```
~~~vb
Private Sub btnDisplayCost_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayCost.Click
    ' displays magazines costing $4 or more

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
                  Where magazine.Cost >= 4 Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnDisplayName_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayName.Click
    ' displays magazines whose name starts with C

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
                  Where magazine.MagName Like "C*" _
                  Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnAverage_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnAverage.Click
    ' displays the average cost of a magazine

    Dim avgCost = Aggregate magazine In MagazinesDataSet.tblMagazine _
                  Select magazine.Cost Into Average()
    MessageBox.Show("Average cost of a magazine: " _
                    & avgCost.ToString("C2"), "Magazines", _
                    MessageBoxButtons.OK, MessageBoxIcon.Information)
End Sub
~~~
```

**Figure 26-7**