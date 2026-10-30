CalcTax() creates a recordset that sums the quantities and prices for the taxable items in tblSalesLineItems for the current sale. The function receives two parameters: the tax rate (dTaxPercent) and the invoice number (lInvoiceNum). The code checks to see whether the recordset returned a record. If the recordset is at the end of the file (EOF), the recordset did not find any line items for the current sale—and CalcTax returns 0. If the recordset does contain a record, the return value for CalcTax is set to the recordset’s Subtotal field times the tax rate (dTaxPercent).

At the end of a procedure that calls CalcTax, shown in Figure 28.11, txtTaxAmount is set to the cTaxAmount value.

When the Buyer, Tax Location, or Tax Rate controls are changed in frmSales, you use the AfterUpdate event for the individual control to recalculate the tax amount. Figure 28.11 shows the code for the txtTaxRate_AfterUpdate event.

# FIGURE 28.11

Recalculating a control after a control is updated.

![](bbox=[0.2, 0.53, 0.7, 0.8])

The logic implemented in txtTaxRate_AfterUpdate is identical to the logic in fsubSalesLineItems_AfterUpdate. In fact, you can use the same code for the Buyer and Tax Location controls as well. The only difference between the code in Figure 28.9 and the code in Figure 28.11 is that the procedure in Figure 28.9 runs whenever a change occurs in the sales line items subform, whereas the code in Figure 28.11 runs whenever a change is made to txtTaxRate on the main form.

# Checking the status of a record deletion

Use the form’s AfterDelConfirm event to recalculate the txtTaxAmount control when deleting a line item. The form’s AfterDelConfirm event (shown in Figure 28.12) is similar to the code for the subform’s AfterUpdate event. Notice, however, that txtTaxAmount on the main sales form is set by this procedure, even though this code runs in fsubSalesLineItems subform embedded on frmSales.