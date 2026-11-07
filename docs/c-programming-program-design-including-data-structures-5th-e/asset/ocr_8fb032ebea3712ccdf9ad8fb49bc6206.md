![](bbox=[0.204, 0.107, 0.889, 0.436])

**FIGURE 18-36** UML class diagram of the class `customerType`

The definitions of the member functions of the class `customerType` follow easily from their descriptions. Next, we give the definitions of the member functions of the class `customerType`.

The function `setCustomerInfo` uses the values of the parameters to initialize `customerNumber`, `arrivalTime`, `waitingTime`, and `transactionTime`. The definition of `setCustomerInfo` is:

```
void customerType::setCustomerInfo(int customerN, int arrvTime,
                                  int wTime, int tTime)
{
    customerNumber = customerN;
    arrivalTime = arrvTime;
    waitingTime = wTime;
    transactionTime = tTime;
}
```

The definition of the constructor is similar to the definition of the function `setCustomerInfo`. It uses the values of the parameters to initialize `customerNumber`, `arrivalTime`, `waitingTime`, and `transactionTime`. To make debugging easier, we use the function `setCustomerInfo` to write the definition of the constructor, which is given next, as follows: