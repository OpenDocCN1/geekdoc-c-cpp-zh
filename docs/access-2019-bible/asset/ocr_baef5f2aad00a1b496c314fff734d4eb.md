# FIGURE 19.18

Placing controls on a new form.

![](bbox=[0.15, 0.19, 0.62, 0.51])

# Creating a subform

Next, you'll add a subform so the user can enter products and quantities. The best way to add a subform is to create the form to be used as a subform on its own prior to adding it to the main form. To create the subform, follow these steps:

+   1. From the Create tab on the Ribbon, click Form Design to create a new form.

+   2. From the tblSalesLineItems table, add the SalesLineItemID, InvoiceNumber, ProductID, Quantity, DiscountPercent, and SellingPrice fields to the subform. This subform will be displayed as a datasheet on the main form, so it's not important that this form look pretty. It is important that the fields are in the order you want them to appear in the datasheet.

+   3. Right-click the ProductID text box and choose Combo Box from the Change To menu. This converts the ProductID control to a combo box so the user can select a product more easily.

+   4. Change the Row Source property of ProductID to the following SQL statement:

```
SELECT ProductID, Description FROM tblProducts ORDER BY Description;
```