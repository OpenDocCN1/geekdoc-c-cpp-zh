```
    Enter the details of second account
    12 Jack 600
    Withdraw Rs 4200 from John's account
    You do not have sufficient funds in account for this operation
    Deposit Rs 2000 in Jack's account
    New Balance is 600
    The account details are
    10 john 800
    12 Jack 600
```

We have created a class named InsufficientFunds with a simple public method named as printMessage(), which prints the insufficient funds message on the user screen. The withdraw() function in Account class is being modified to throw InsufficientFunds object if operation of withdrawal is not possible as shown below:

```
    void withdraw(float amount)
    {
        if(bal-amount>=500)
        {
            bal = bal - amount;
            cout<<"New Balance is "<<bal<<endl;
        }
        else
        {
            throw InsufficientFunds();
        }
    }
```

We have thrown an object of InsufficientFunds() using the throw statement. This creates an effect of an exception in the program. If this exception is not handled, it will abruptly terminate the program. Hence, we have handled this exception by putting the function call to withdraw() in try-catch block as shown below:

```
    try
    {
        al.withdraw(4200);
    }
    catch(InsufficientFunds e)
    {
        e.printMessage();
    }
```

The catch block will be executed only if withdraw() throws an exception of type InsufficientFunds. If the method withdraw() completes successfully without an exception, the catch block will never be executed.

The statement

```
    e.printMessage();
```