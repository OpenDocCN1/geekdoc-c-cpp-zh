+   3. Right-click the **form**, then click **Lock Controls**. Click **View** on the menu bar, then click **Tab Order**. Use the information shown in Figure 9-13 to set the tab order.

![](bbox=[0.2, 0.19, 0.47, 0.33])

Figure 9-13: Correct TabIndex values for the interface

+   4. Press **Esc** to remove the TabIndex boxes from the form, then save the solution.

+   5. Open the Code Editor window, which contains the code for the btnExit control's Click event procedure. It also contains the partially completed Click event procedure for the btnCalc control, as shown in Figure 9-14. Notice that the procedure declares a named constant for the 10% discount rate. It also declares five variables to store the quantity ordered, item price, subtotal, discount, and total due. In addition, it assigns the quantity and price information to two of the variables. The assignment statement in the procedure displays the total due in the lblTotal control.

```
~~~vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) H
    ' calculates and displays the total amount due

    Const decDISC_RATE As Decimal = 0.1
    Dim intQuantity As Integer
    Dim decPrice As Decimal
    Dim decSubtotal As Decimal
    Dim decDiscount As Decimal
    Dim decTotal As Decimal

    ' assign quantity and price to variables
    Integer.TryParse(txtQuantity.Text, intQuantity)
    Decimal.TryParse(txtPrice.Text, decPrice)

    ' calculate subtotal, discount, and total due

    ' display total due
    lblTotal.Text = decTotal.ToString("C2")
End Sub
~~~
```

Figure 9-14: Partially completed Click event procedure for the btnCalc control

+   6. Missing from the btnCalc control's Click event procedure are the instructions to calculate the subtotal, discount, and total due. According to the first processing symbol shown in Figure 9-11, you calculate the subtotal by multiplying the quantity ordered by the item price. Click the **blank line** below the `' calculate subtotal, discount, and total due` comment. Type **decSubtotal = intQuantity * decPrice** and press **Enter**.