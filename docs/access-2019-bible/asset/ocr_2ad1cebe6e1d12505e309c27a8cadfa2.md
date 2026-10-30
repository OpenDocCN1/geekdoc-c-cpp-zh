```
Dim cReturn As Currency

Const dDISCOUNT_THRESHOLD As Double = 10000
Const dDEFAULT_DISCOUNT As Double = 0.1

cReturn = 0

If cInvoiceTotal >= dDISCOUNT_THRESHOLD Then
    cReturn = cInvoiceTotal * dDEFAULT_DISCOUNT
ElseIf IsDiscountCustomer(sCustomerID) Then
    cReturn = cInvoiceTotal * dDEFAULT_DISCOUNT
ElseIf IsLastDayOfMonth(dtInvoice) Then
    cReturn = cInvoiceTotal * dDEFAULT_DISCOUNT
End If

InvoiceDiscountAmount = cReturn

End Function
```

There are three situations that will result in a discount. If the invoice is over a certain amount, if the customer is flagged as getting a discount, or if it’s the last day of the month, the default discount is applied to the invoice. Comparing the invoice total to the threshold is fairly straightforward. In order to make the code clean and readable, the other two conditions were moved to their own functions. Those functions are shown here:

```
Private Function IsDiscountCustomer(sCustomerID As String) As Boolean

Dim rsCustomer As ADODB.Recordset
Dim conn As ADODB.Connection
Dim sSql As String

Set conn = CurrentProject.Connection
sSql = "SELECT GetsDiscount FROM Customers " & _
    "WHERE CustomerID = '" & sCustomerID & "'"

Set rsCustomer = conn.Execute(sSql)

If Not rsCustomer.EOF Then
    IsDiscountCustomer = rsCustomer.Fields(0).Value
End If

End Function
```

```
Private Function IsLastDayOfMonth(dtDate As Date) As Boolean

'The zeroth day of the next month is the last
'day of the current month
IsLastDayOfMonth = (dtDate = DateSerial(Year(dtDate), Month(dtDate), 0))

End Function
```