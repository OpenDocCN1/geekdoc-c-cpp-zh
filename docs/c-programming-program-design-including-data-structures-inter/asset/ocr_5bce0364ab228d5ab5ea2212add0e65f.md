amount, the function returns the billing amount using the return statement. The following four steps describe this function:

+   a. Prompt the user for the number of premium channels.
+   b. Read the number of premium channels.
+   c. Calculate the bill.
+   d. Return the amount due.

This function contains a statement to prompt the user to enter the number of premium channels (Step a) and a statement to read the number of premium channels (Step b). Other items needed to calculate the billing amount, such as the cost of basic service connection and bill processing fees, are defined as named constants (before the definition of the function main). Therefore, to calculate the billing amount, this function does not need to get any value from the function main. This function, therefore, has no parameters.

From the previous discussion, it follows that the function residential requires variables to store both the number of premium channels and the billing amount. This function needs only two local variables to calculate the billing amount:

```
int noOfPChannels;  //number of premium channels
double bAmount;     //billing amount
```

The definition of the function residential can now be written as follows:

```
double residential()
{
    int noOfPChannels;  //number of premium channels
    double bAmount;     //billing amount

    cout << "Enter the number of premium "
         << "channels used: ";
    cin >> noOfPChannels;
    cout << endl;

    bAmount = RES_BILL_PROC_FEES +
              RES_BASIC_SERV_COST +
              noOfPChannels * RES_COST_PREM_CHANNEL;

    return bAmount;
}
```

Function business: To compute the business bill, you need to know the number of both the basic service connections and the premium channels to which the customer subscribes. Then, based on these numbers, you can calculate the billing amount. The billing amount is then returned using the return statement. The following six steps describe this function:

+   a. Prompt the user for the number of basic service connections.
+   b. Read the number of basic service connections.
+   c. Prompt the user for the number of premium channels.