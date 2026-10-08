+   c. Why does the net pay appear as $33.85 rather than $33.84? Hint: Change the cout << fixed << setprecision(2) << endl; statement to a comment, and save and run the program. Type 45.13 as the gross pay and press Enter. Study the output, and stop the program and change the comment back to a statement.

+   d. Use the comments that appear in the Advanced15.cpp file to modify your program's code. Why do you need to add .5 to the expressions that calculate the federal and state taxes?

+   e. Save, run, and test the program to verify that it is working correctly, and then stop the program.

+   16. Follow the instructions for starting C++ and using the SwatBugs16.cpp file. The program declares and initializes a double variable. It adds 1.5 to the variable before displaying the variable's value. If necessary, make the system("pause"); statement a comment, and then save the program. Run and then debug the program.

# Answers to TRY THIS Exercises

![](bbox=[0.125, 0.426, 0.355, 0.458])

+   1. See Figure 4-38.

| IPO chart information | C++ instructions |
| --- | --- |
| Input | |
| sale1 | double sale1 = 0.0; |
| sale2 | double sale2 = 0.0; |
| commission rate | double commissionRate = 0.0; |
| Processing | |
| totalSales | double totalSales = 0.0; |
| Output | |
| commission | double commission = 0.0; |
| Algorithm | |
| 1. enter sale1, sale2, and the commission rate | cout << "First sale? "; cin >> sale1;
cout << "Second sale? "; cin >> sale2;
cout << "Commission rate in decimal format? "; cin >> commissionRate; |
| 2. calculate the total sales by adding sale1 to sale2 | totalSales = sale1 + sale2; |
| 3. calculate the commission by multiplying the commission rate | commission = totalSales * commissionRate; |
| 4. display the commission | cout << "Commission: $\$" << commission << endl; |