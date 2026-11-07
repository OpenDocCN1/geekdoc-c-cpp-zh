lon obtained for each trip and print the combined miles per gallon obtained for all tankfuls up to this point.

```
```text
Enter miles driven (-1 to quit): 287
Enter gallons used: 13
MPG this trip: 22.076923
Total MPG: 22.076923

Enter miles driven (-1 to quit): 200
Enter gallons used: 10
MPG this trip: 20.000000
Total MPG: 21.379139

Enter the miles driven (-1 to quit): 120
Enter gallons used: 5
MPG this trip: 24.000000
Total MPG: 21.678571

Enter the miles used (-1 to quit): -1
```
```

# 3.4 **(Credit Limits)** Develop a C++ program to determine whether a clothing-store customer has exceeded the credit limit on a charge account. For each customer, the following facts are available:

+   a) Account number (an integer)  
+   b) Balance at the beginning of the month  
+   c) Total of all items charged by this customer this month  
+   d) Total of all credits applied to this customer's account this month  
+   e) Allowed credit limit

The program should use a while statement to input each of these facts, calculate the new balance (= beginning balance + charges − credits) and determine whether the new balance exceeds the customer's credit limit. For those customers whose credit limit is exceeded, the program should display the customer's account number, credit limit, new balance and the message “Credit Limit Exceeded.”

```
```text
Enter account number (or -1 to quit): 100
Enter beginning balance: 5394.78
Enter total charges: 1000.00
Enter total credits: 500.00
Enter credit limit: 5500.00
New balance is 5894.78
Account:      100
Credit limit: 5500.00
Balance:      5894.78
Credit Limit Exceeded

Enter Account Number (or -1 to quit): 200
Enter beginning balance: 1000.00
Enter total charges: 123.45
Enter total credits: 321.00
Enter credit limit: 1500.00
New balance is 802.45

Enter Account Number (or -1 to quit): -1
```
```