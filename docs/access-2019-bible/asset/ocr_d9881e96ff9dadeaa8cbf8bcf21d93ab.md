At the conclusion of a subroutine, program flow returns to the code or action that originally called the sub. The subroutine shown in Figure 25.6 may be called from a form’s Load event, so control is returned to that event.

As an example of a useful VBA subroutine, the next several paragraphs describe building an event procedure for a control on an Access form. This procedure retrieves a value from one of the cboCustomerID combo box columns and uses it to find a record. The RowSource of the cboCustomerID combo box is a SQL statement that returns the CustomerID and the Company fields. Here’s the SQL statement:

```
SELECT DISTINCT tblCustomers.CustomerID, tblCustomers.Company
FROM tblCustomers
INNER JOIN tblSales
ON tblCustomers.CustomerID = tblSales.CustomerID
ORDER BY tblCustomers.Company;
```

The tblCustomers table is inner-joined with the tblSales table so that only those customers with an invoice are displayed in the combo box. The DISTINCT keyword is used so that each customer is only returned once.

Chapter 14 covers SQL syntax in detail.

The objective of this exercise is to learn about procedures, but it also serves to teach you some additional VBA commands. The code is added to the form as the cboCustomerID_AfterUpdate event.

To create an event procedure in a form, follow these steps:

+   1. Select the cboCustomerID control in frmSales Design view.
+   2. Press F4 to display the Property Sheet for the control.
+   3. Click in the After Update event property in the Event tab of the Property Sheet and select [Event Procedure] from the event’s drop-down list.
+   4. Click the builder button (...) to open the VBA code editor.
+   5. Enter the following code into the cboCustomerID_AfterUpdate event procedure, as shown in Figure 25.7. The following code goes between Private Sub cboCustomerID_AfterUpdate() and End Sub in the VBA code editor:
+   6. Select Compile Chapter25 from the Debug menu in the code editor to check your syntax.
+   7. Close the VBA window and return to the frmSales form.

```
Me.txtCustomerID.SetFocus

If Not IsNull(Me.cboCustomerID.Value) Then
    DoCmd.FindRecord Me.cboCustomerID.Value
End If

Me.txtInvoiceDate.SetFocus
```