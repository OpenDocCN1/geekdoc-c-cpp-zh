# Chapter 28: Accessing Data with VBA

```
Exit Sub
Else
    Status = acDeleteOK
End If
```

The Status argument is provided to enable your VBA code to override the user’s decision to delete a record if conditions warrant such an override. In the case that Status is set to acDeleteCancel, the copy of the record stored in the temporary buffer is restored to the recordset, and the delete process is terminated. If, on the other hand, Status is set to acDeleteOK, the deletion proceeds and the temporary buffer is cleared after the user moves to another record in the recordset.

# Eliminating repetitive code

The examples in this section result in three procedures containing nearly identical code. If the code needs to be modified, you will have to modify it in the Form_AfterDelConfirm and Form_AfterUpdate events of the subform and the txtTaxRate_AfterUpdate event of the main form. If your modifications are not identical or if you simply forget to modify the code in one of the procedures, you can introduce errors into the project.

When you find yourself writing the same, or very similar, code in multiple event procedures, the best practice is to move the code to a standard module and call it from the event procedures. We can’t simply copy the code to a standard module because, while very similar, the code isn’t exactly the same. The differences in the code, for example how txtTaxRate is referenced, need to be handled in parameters to the new procedure:

```
Public Sub UpdateTaxRate(frmMain As Form, _
    dTaxRate As Double, _
    lInvoiceNumber As Long)

    Dim cTaxAmount As Currency

    cTaxAmount = CalcTax(dTaxRate, lInvoiceNumber)

    frmMain.txtTaxAmount.Value = cTaxAmount

End Sub
```

This procedure is placed in the modSalesFunctions module. Instead of having similar code in three event procedures, each of those event procedures calls this procedure. If any changes are necessary, only this procedure needs to be updated. The following code shows how to call this procedure from the subform’s Form_AfterUpdate event and the main form’s txtTaxRate_AfterUpdate event:

```
Private Sub txtTaxRate_AfterUpdate()

    UpdateTaxRate Me, CDbl(Nz(Me.txtTaxRate.Value, 0)), _
        Me.InvoiceNumber.Value

End Sub
```