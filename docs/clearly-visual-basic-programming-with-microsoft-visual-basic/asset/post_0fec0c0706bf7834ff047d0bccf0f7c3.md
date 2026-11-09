
Sam wants an application in which he can enter the quantity of an item that a customer purchases and the item's price. Customers who work at Sam's company are entitled to a 10% employee discount. The application should both calculate and display the total amount the customer owes.

- *Output:* total due
- *Input:* quantity ordered, item price, employee?
- *Algorithm:*

![](img/cf88270932e011575089da06b940a1d9_198_0.png)

**Figure 9-17:** Total Due problem specification along with a different algorithm

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' calculates and displays the total amount due

    Const decDISC_RATE As Decimal = 0.1
    Dim intQuantity As Integer
    Dim decPrice As Decimal
    Dim decTotal As Decimal

    ' assign quantity and price to variables
    Integer.TryParse(txtQuantity.Text, intQuantity)
    Decimal.TryParse(txtPrice.Text, decPrice)

    ' calculate total due
    decTotal = intQuantity * decPrice
    If chkEmployee.Checked = True Then
        decTotal = decTotal * (1 - decDISC_RATE)
    End If

    ' display total due
    lblTotal.Text = decTotal.ToString("C2")
End Sub
```

calculates the total due before any discount

multiplies the total due by 90%

**Figure 9-18:** Code corresponding to Figure 9-17's algorithm

## To code the Total Due—Version 2 application, and then test it:

- 1. Open the **Total Due Solution (Total Due Solution.sln)** file, which is contained in the ClearlyVB\Chap09\Total Due Solution—Version 2 folder. If necessary, open the designer window.
- 2. Open the Code Editor window, which contains the code for the btnExit control's Click event procedure. Open the btnCalc control's Click event procedure, then enter the code shown in Figure 9-18.
- 3. Save the solution, then start the application. Use the quantity, price, and check box information shown earlier in Figure 9-16, as well as your own data, to test the application.
- 4. When you are finished testing the application, click the **Exit** button. Close the Code Editor window, then close the solution.

Figure 9-19 shows still a different way of solving the Total Due problem, and Figure 9-20 shows the corresponding code.

Sam wants an application in which he can enter the quantity of an item that a customer purchases and the item's price. Customers who work at Sam's company are entitled to a 10% employee discount. The application should both calculate and display the total amount the customer owes.

- **Output:** total due
- **Processing:** discount
- **Input:** quantity ordered, item price, employee?
- Algorithm:
  - 1. enter the quantity ordered, item price, and employee? items
  - 2. calculate the total due by multiplying the quantity ordered by the item price
  - 3. if employee?, do this:
    - calculate the discount by multiplying the total due by 10%
    - subtract the discount from the total due
    - end if
  - 4. display the total due

Figure 9-19: A different way of solving the Total Due problem

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' calculates and displays the total amount due

    Const decDISC_RATE As Decimal = 0.1
    Dim intQuantity As Integer
    Dim decPrice As Decimal
    Dim decTotal As Decimal

    ' assign quantity and price to variables
    Integer.TryParse(txtQuantity.Text, intQuantity)
    Decimal.TryParse(txtPrice.Text, decPrice)

    ' calculate total due
    decTotal = intQuantity * decPrice
    If chkEmployee.Checked = True Then
        Dim decDiscount As Decimal
        decDiscount = decTotal * decDISC_RATE
        decTotal = decTotal - decDiscount
    End If

    ' display total due
    lblTotal.Text = decTotal.ToString("C2")
End Sub
```

block variable

Figure 9-20: Code corresponding to Figure 9-19's algorithm

Study closely the instructions in the selection structure's true path shown in Figure 9-20. The first instruction, Dim decDiscount As Decimal, declares a variable named decDiscount. Like the variables declared at the beginning of a procedure, variables declared within a statement block in a selection structure remain in memory until the procedure ends. However, unlike variables declared at the beginning of a procedure, variables declared within a statement block have block scope rather than procedure scope. A variable that has procedure scope can be used anywhere within the procedure, whereas a variable that has **block scope** can be used only within the statement block in which it is declared. In this case, for example, the intQuantity, decPrice, and decTotal variables (and also the decDISC_RATE named constant) can be used anywhere within the btnCalc control's Click event procedure, but the decDiscount variable can be used only within the If...Then...Else statement's true path. You may be wondering why the decDiscount variable was not declared at the beginning of the procedure, along with the other variables. Although there is nothing wrong with declaring all variables at the beginning of a procedure, the decDiscount variable is necessary only when the discount needs to be calculated, so many programmers would prefer to create the variable only if it is necessary to do so. This is because fewer unintentional errors occur in applications when the variables are declared using the minimum scope needed. In this case, the minimum scope for the decDiscount variable is block scope, because only the selection structure's true path uses the variable. A variable declared within a statement block is called a **block variable**.

## To code the Total Due—Version 3 application, and then test it:

- 1. Open the **Total Due Solution (Total Due Solution.sln)** file, which is contained in the ClearlyVB\Chap09\Total Due Solution—Version 3 folder. If necessary, open the designer window.
- 2. Open the Code Editor window, which contains the code for the btnExit control's Click event procedure. Open the btnCalc control's Click event procedure, then enter the code shown in Figure 9-20.
- 3. Save the solution, then start the application. Use the quantity, price, and check box information shown earlier in Figure 9-16, as well as your own data, to test the application.
- 4. When you are finished testing the application, click the **Exit** button. Close the Code Editor window, then close the solution.

## MINI-QUIZ 2

- 1. Write an If...Then...Else statement that displays the string "Overtime pay" in the lblMsg control when the number of hours contained in the decHours variable is greater than 40.
- 2. Modify the If...Then...Else statement from Question 1 so that it displays the string "Regular pay only" when the selection structure's condition evaluates to False.
- 3. What is the scope of a variable declared in a selection structure's false path?
  - a. the entire application
  - b. the procedure containing the selection structure
  - c. the entire selection structure
  - d. only the selection structure's false path

![](img/cf88270932e011575089da06b940a1d9_202_0.png)

For more examples of selection structures, see the Selection Structure section in the Ch9WantMore.pdf file.

It's time to view the Ch09-Selection Structure video.

## SUMMARY

- The selection structure is one of the three control structures. It is used when you need the computer to make a decision and then take an appropriate action.
- Studying the problem specification will help you determine whether a solution requires a selection structure.
- You should indent the instructions in a selection structure's true path and in its false path. The set of instructions in each path is called a statement block.
- You can use the If...Then...Else statement to code the selection structure in Visual Basic. The statement's condition must contain an expression that evaluates to a Boolean value, either True or False. You will find comparison operators in most conditions.
