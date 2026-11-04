When the user clicks the OK button, copy the item name, price each, and quantity values into the public fields.

+   a. Copy the values entered by the user into the fields you created in the preceding step.

Create the main form shown on the left in Figure 13-1.

+   1. Create the ListView, Button, Label, and TextBox. Set their Anchor properties and make the TextBox read-only.
+   2. To make the ListView display its items in a list as shown:
+      a. Set its View property to Details.
+      b. Select its Columns property and click the ellipsis to the right to open the ColumnHeader Collection Editor shown in Figure 13-2. Click the Add button four times to make the four columns. Use the property editor on the right to set each column's Name and Text properties and to set TextAlign to Right for the numeric columns.

![](bbox=[0.28, 0.58, 0.78, 0.8])

FIGURE 13-2

When the user clicks the main form's Add Item button, make the program display a NewItemForm. If the user enters data and clicks OK, display the entered values in the main form's ListView control and update the grand total.

+   1. The button's Click event handler should use code similar to the following:

```
// A private field to keep track of grand total
// across multiple calls to the event handler.
private decimal GrandTotal = 0;
```