assigns the text box’s value to the decPrice variable. In other words, a statement is missing from the procedure.

```
~~~vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCa
    ' calculates and displays a 10%, 20%, and
    ' 30% discount on an item's price

    ' declare variables
    Dim decPrice As Decimal
    Dim decDiscount10 As Decimal
    Dim decDiscount20 As Decimal
    Dim decDiscount30 As Decimal

    ' calculate discounts
    decDiscount10 = decPrice * 0.1
    decDiscount20 = decPrice * 0.2
    decDiscount30 = decPrice * 0.3
~~~
```

**Figure 8-10:** Value stored in decPrice before the highlighted statement is executed

+   8. Click **Debug** on the menu bar, then click **Stop Debugging** to stop the debugger. Click the blank line below the last Dim statement, then press **Enter** to insert another blank line. Type `' assign price to a variable` and press **Enter**, then type `decimal.tryparse(txtPrice.text, decPrice)` and press **Enter**.
+   9. Save the solution. Click **Debug** on the menu bar, then click **Step Into**. Type **100** in the Price text box, then click the **Calculate** button. (If the interface still appears on the screen, click the Code Editor window’s title bar.) Press **F8** to process the procedure header. The debugger highlights the `Decimal.TryParse(txtPrice.Text, decPrice)` statement and pauses execution of the code.
+   10. Before the highlighted statement is processed, the txtPrice control’s Text property should contain 100, which is the value you entered in the control. Place your mouse pointer on txtPrice.Text in the highlighted statement. The box shows that the Text property contains the expected value. The 100 is enclosed in quotation marks because it is considered a string. (As you learned in Chapter 7, a string is text enclosed in quotation marks.)
+   11. The decPrice variable should contain its initial value, 0D. Place your mouse pointer on decPrice in the highlighted statement. The box shows that the variable contains the expected value.
+   12. Press **F8** to process the TryParse method. The debugger highlights the `decDiscount10 = decPrice * 0.1` statement before pausing execution of the code. Place your mouse pointer on decPrice in the TryParse method, as shown in Figure 8-11. Notice that after the method is processed by the computer, the decPrice variable contains the number 100D.