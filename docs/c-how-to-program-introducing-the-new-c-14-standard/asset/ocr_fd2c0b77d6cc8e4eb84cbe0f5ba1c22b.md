# # Exercises

1. 6.11 Show the value of `x` after each of the following statements is performed:

+   A. `x = fabs(7.5);`
+   B. `x = floor(7.5);`
+   C. `x = fabs(0.0);`
+   D. `x = ceil(0.0);`
+   E. `x = fabs(-6.4);`
+   F. `x = ceil(-6.4);`
+   G. `x = ceil(-fabs(-8 + floor(-5.5)));`

2. 6.12 **_Parking Charges_** A parking garage charges a $20.00 minimum fee to park for up to three hours. The garage charges an additional $5.00 per hour for each hour *or part thereof* in excess of three hours. The maximum charge for any given 24-hour period is $50.00. Assume that no car parks for longer than 24 hours at a time. Write a program that calculates and prints the parking charges for each of three customers who parked their cars in this garage yesterday. You should enter the hours parked for each customer. Your program should print the results in a neat tabular format and should calculate and print the total of yesterday’s receipts. The program should use the function `calculateCharges` to determine the charge for each customer. Your outputs should appear in the following format: