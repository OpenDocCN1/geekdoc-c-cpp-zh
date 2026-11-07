# PROBLEM ANALYSIS AND ALGORITHM DESIGN

The purpose of this program is to calculate and print the billing amount. To calculate the billing amount, you need to know the customer for whom the billing amount is calculated (whether the customer is residential or business) and the number of premium channels to which the customer subscribes. In the case of a business customer, you also need to know the number of basic service connections and the number of premium channels. Other data needed to calculate the bill, such as the bill processing fees and the cost of a premium channel, are known quantities. The program should print the billing amount to two decimal places, which is standard for monetary amounts. This problem analysis translates into the following algorithm:

+   1. Set the precision to two decimal places.
+   2. Prompt the user for the account number and customer type.
+   3. Based on the customer type, determine the number of premium channels and basic service connections, compute the bill, and print the bill:
+      a. If the customer type is `r` or `R`,
+         i. Prompt the user for the number of premium channels.
+         ii. Compute the bill.
+         iii. Print the bill.
+      b. If the customer type is `b` or `B`,
+         i. Prompt the user for the number of basic service connections and the number of premium channels.
+         ii. Compute the bill.
+         iii. Print the bill.

# Variables

Because the program will ask the user to input the customer account number, customer code, number of premium channels, and number of basic service connections, you need variables to store all of this information. Also, because the program will calculate the billing amount, you need a variable to store the billing amount. Thus, the program needs at least the following variables to compute and print the bill:

```
```cpp
int accountNumber;       // variable to store the customer's
                         // account number
char customerType;       // variable to store the customer code
int numOfPremChannels;   // variable to store the number
                         // of premium channels to which the
                         // customer subscribes
int numOfBasicServConn;  // variable to store the
                         // number of basic service connections
                         // to which the customer subscribes
double amountDue;        // variable to store the billing amount
```
```