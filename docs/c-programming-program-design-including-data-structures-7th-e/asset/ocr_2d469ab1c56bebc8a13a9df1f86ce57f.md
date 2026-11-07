```
```cpp
int noOfPChannels;   //number of premium channels
double bAmount;      //billing amount
```
```

The definition of the function residential can now be written as follows:

```
```cpp
double residential()
{
    int noOfPChannels;   //number of premium channels
    double bAmount;      //billing amount

    cout << "Enter the number of premium "
         << "channels used: ";
    cin >> noOfPChannels;
    cout << endl;

    bAmount= RES_BILL_PROC_FEES +
             RES_BASIC_SERV_COST +
             noOfPChannels * RES_COST_PREM_CHANNEL;

    return bAmount;
}
```
```

Function business: To compute the business bill, you need to know the number of both the basic service connections and the premium channels to which the customer subscribes. Then, based on these numbers, you can calculate the billing amount. The billing amount is then returned using the `return` statement. The following six steps describe this function:

+   a. Prompt the user for the number of basic service connections.
+   
+   b. Read the number of basic service connections.
+   
+   c. Prompt the user for the number of premium channels.
+   
+   d. Read the number of premium channels.
+   
+   e. Calculate the amount due.
+   
+   f. Return the amount due.

This function contains the statements to prompt the user to enter the number of basic service connections and premium channels (Steps a and c). The function also contains statements to input the number of basic service connections and premium channels (Steps b and d). Other items needed to calculate the billing amount, such as the cost of basic service connections and bill processing fees, are defined as named constants (before the definition of the function main). It follows that to calculate the billing amount this function does not need to get any values from the function main. Therefore, it has no parameters.

From the preceding discussion, it follows that the function business requires variables to store the number of basic service connections and the number of premium channels, as well as the billing amount. In fact, this function needs only these three local variables to calculate the billing amount:

```
```cpp
int noOfBasicServiceConnections;
int noOfPChannels;   //number of premium channels
double bAmount;      //billing amount
```
```