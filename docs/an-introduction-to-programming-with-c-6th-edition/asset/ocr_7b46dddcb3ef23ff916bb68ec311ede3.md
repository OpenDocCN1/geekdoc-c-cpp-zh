# Step 5—Desk-check the Program

is the cout << "Enter the bill: " statement. The statement displays a prompt on the computer screen; it does not make any changes to the variables; therefore, no entry is necessary in the desk-check table. The next statement, cin >> totalBill11; allows the user to enter the total bill, and stores the user's response in the totalBill11 variable. If the user enters the number 45, the statement stores 45.0 in the variable, which is the double type. Then record 45 in the totalBill11 column in the desk-check table. As you learned in Chapter 2, programmers help it to lightly cross the previous value in a column before recording a new value; this is not a requirement. Next, the cout << "Enter the liquor charge:" statement prompts the user to enter the liquor charge. The cin >> liquor; statement waits and stores the response in the liquor variable. If the user enters the number 10, the desk-check table shows 10. The cout << "Enter the tip percentage in decimal format:" statement prompts the user to enter the percentage. cin >> tipPercent; stores the response in the tipPercent variable. If the user enters the number 2, record 2 in the desk-check table. Figure 4-15 shows the input values recorded in the program's desk-check table.

| totalBill | liquor | percent | totalNoLiquor | tip |
| :--- | :--- | :--- | :--- | :--- |
| 45.0 | 10.0 | 2 | 0.0 | 0.0 |

Figure 4-15 Input values in the program's desk-check table

The totalNoLiquor = totalBill - liquor; statement subtracts the contents of the liquor (10.0) from the contents of the totalBill11 (45.0) and stores the result (35.0) in the totalNoLiquor variable. Notice that the expression appears on the right side of the assignment operator is evaluated, and then the result is stored in the variable whose name on the left side of the assignment operator. As a result of this statement, record 35.0 in the totalNoLiquor column in the desk-check table, as shown in Figure 4-16.

| totalBill | liquor | tipPercent | totalNoLiquor | tip |
| :--- | :--- | :--- | :--- | :--- |
| 45.0 | 10.0 | 2 | 35.0 | 0.0 |

Figure 4-16 Desk-check showing the result of the total bill without liquor charge calculation

The next statement, tip = totalNoLiquor * tipPercent; multiplies the contents of the totalNoLiquor variable (35.0) by the contents of the tipPercent variable (2) and stores the result (7.0) in the tip variable. In the desk-check table, you record the number 7.0 in the tip column, as shown in Figure 4-17.