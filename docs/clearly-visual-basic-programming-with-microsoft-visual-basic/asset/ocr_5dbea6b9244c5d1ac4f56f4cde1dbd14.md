```
~~~vb
Private Sub TblEmployBindingNavigatorSaveItem_Click _
    (ByVal sender As System.Object, ByVal e As System.EventArgs)
    Try
        Me.Validate()
        Me.TblEmployBindingSource.EndEdit()
        Me.TableAdapterManager.UpdateAll(Me.EmployeesDataSet)
        MessageBox.Show("Changes saved.", "Morgan Industries", _
            MessageBoxButtons.OK, MessageBoxIcon.Information)
    Catch ex As Exception
        MessageBox.Show(ex.Message, "Morgan Industries", _
            MessageBoxButtons.OK, MessageBoxIcon.Information)
    End Try
End Sub

Private Sub frmMain_Load(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles MyBase.Load
    'TODO: This line of code loads data into the 'EmployeesDataSet.tblEmploy' table.
    'You can move, or remove it, as needed.
    Me.TblEmployTableAdapter.Fill(Me.EmployeesDataSet.tblEmploy)
End Sub
~~~
```

Figure 25-19: Morgan Industries application's code

![](bbox=[0.192, 0.536, 0.512, 0.751])

Figure 25-20: Sample run of the Morgan Industries application