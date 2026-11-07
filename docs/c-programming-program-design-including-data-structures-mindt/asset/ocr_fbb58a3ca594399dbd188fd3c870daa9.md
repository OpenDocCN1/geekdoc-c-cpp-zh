Although assert statements are useful during program development, after a program has been developed and put into use, if an assert statement fails for some reason, an end user would have no idea what the error means. Therefore, after you have developed and tested a program, you might want to remove or disable the assert statements. In a very large program, it could be tedious, and perhaps impossible, to remove all of the assert statements that you used during development. In addition, if you plan to modify a program in the future, you might like to keep the assert statements. Therefore, the logical choice is to keep these statements but to disable them. You can disable assert statements by using the following preprocessor directive:

```
#define NDEBUG
```

This preprocessor directive `#define NDEBUG` must be placed before the directive `#include <cassert>`.

# PROGRAMMING EXAMPLE: Cable Company Billing

![](bbox=[0.099, 0.419, 0.163, 0.492])

This programming example demonstrates a program that calculates a customer’s bill for a local cable company. There are two types of customers: residential and business. There are two rates for calculating a cable bill: one for residential customers and one for business customers. For residential customers, the following rates apply:

+   - Bill processing fee: $4.50
+   - Basic service fee: $20.50
+   - Premium channels: $7.50 per channel

For business customers, the following rates apply:

+   - Bill processing fee: $15.00
+   - Basic service fee: $75.00 for first 10 connections, $5.00 for each additional connection
+   - Premium channels: $50.00 per channel for any number of connections

The program should ask the user for an account number (an integer) and a customer code. Assume that R or r stands for a residential customer, and B or b stands for a business customer.

**Input**  The customer’s account number, customer code, number of premium channels to which the user subscribes, and, in the case of business customers, number of basic service connections.

**Output**  Customer’s account number and the billing amount.