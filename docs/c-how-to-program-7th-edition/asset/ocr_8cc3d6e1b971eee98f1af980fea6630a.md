```
   8    int y; // declare y
    9    int x = 1; // initialize x
   10    int total = 0; // initialize total
   11
   12    while ( x <= 10 ) // loop 10 times
   13    {
   14        y = x * x; // perform calculation
   15        cout << y << endl; // output result
   16        total += y; // add y to total
   17        x++; // increment counter x
   18    } // end while
   19
   20    cout << "Total is " << total << endl; // display result
   21 } // end main
```

*For Exercises 4.13–4.16, perform each of these steps:*

+   a) Read the problem statement.
+   b) Formulate the algorithm using pseudocode and top-down, stepwise refinement.
+   c) Write a C++ program.
+   d) Test, debug and execute the C++ program.

**4.13** *(Gas Mileage)* Drivers are concerned with the mileage obtained by their automobiles. One driver has kept track of several tankfuls of gasoline by recording miles driven and gallons used for each tankful. Develop a C++ program that uses a while statement to input the miles driven and gallons used for each tankful. The program should calculate and display the miles per gallon obtained for each tankful and print the combined miles per gallon obtained for all tankfuls up to this point.

```
    Enter miles driven (-1 to quit): 287
    Enter gallons used: 13
    MPG this tankful: 22.076923
    Total MPG: 22.076923

    Enter miles driven (-1 to quit): 200
    Enter gallons used: 10
    MPG this tankful: 20.000000
    Total MPG: 21.173913

    Enter miles driven (-1 to quit): 120
    Enter gallons used: 5
    MPG this tankful: 24.000000
    Total MPG: 21.678571

    Enter the miles used (-1 to quit): -1
```

**4.14** *(Credit Limit Calculator)* Develop a C++ program that will determine whether a department-store customer has exceeded the credit limit on a charge account. For each customer, the following facts are available:

+   a) Account number (an integer)
+   b) Balance at the beginning of the month
+   c) Total of all items charged by this customer this month
+   d) Total of all credits applied to this customer's account this month
+   e) Allowed credit limit

The program should use a while statement to input each of these facts, calculate the new balance (= beginning balance + charges – credits) and determine whether the new balance exceeds the customer's credit limit. For those customers whose credit limit is exceeded, the program should display the customer's account number, credit limit, new balance and the message "Credit Limit Exceeded."