```
```vb
Public Property ProductName As String

<Required()> _
<Range(1, Integer.MaxValue)> _
Public Property SupplierID As Integer

<Required()> _
<Range(1, Integer.MaxValue)> _
Public Property CategoryID As Integer

<StringLength(20)> _
Public Property QuantityPerUnit As String

<Range(0.0, MoneyMaxValue)> _
Public Property UnitPrice As Nullable(Of Decimal)

<Range(0, Short.MaxValue)> _
Public Property UnitsInStock As Nullable(Of Short)

<Range(0, Short.MaxValue)> _
Public Property UnitsOnOrder As Nullable(Of Short)

<Range(0, Short.MaxValue)> _
Public Property ReorderLevel As Nullable(Of Short)
End Class
```
```

> *Code snippet from \\Models\\Product.vb*

Run the application, navigate to `/Admin`, and click the Edit link for one of the items. Update a field or two with values that will fail validation and click the Save button. Because we have client validation implemented, you should see the error messages without posting back to the server (see Figure 23-19). Correcting the errors and tabbing out of the fields should remove the error messages.

![](bbox=[0.146, 0.541, 0.736, 0.93])

# FIGURE 23-19