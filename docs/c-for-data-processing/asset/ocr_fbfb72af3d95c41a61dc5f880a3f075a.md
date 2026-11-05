# ### 4.8.3 Implementing an Interface in C#

Interfaces become interesting when we make a class implement them. Implementing an interface is like setting up a contract between the supplier of services and the consumer. If a class implements an interface it is saying that for every method described in the interface, it has a corresponding implementation.

In the case of the bank account, I am going to create a class which implements the interface, so that it can be thought of as an account component, irrespective of what it really is:

```
```csharp
public class CustomerAccount : IAccount
{
    private decimal balance = 0;

    public bool WithdrawFunds ( decimal amount )
    {
        if ( balance < amount )
        {
            return false ;
        }
        balance = balance - amount ;
        return true ;
    }

    public void PayInFunds ( decimal amount )
    {
        balance = balance + amount ;
    }

    public decimal GetBalance ()
    {
        return balance;
    }
}
```
```

The code above does not look that different from the previous account class. The only difference is the top line:

```
```csharp
public class CustomerAccount : IAccount
{
    ...
}
```
```

The highlighted part of the line above is where the programmer tells the compiler that this class implements the `IAccount` interface. This means that the class contains concrete versions of all the methods described in the interface. If the class does not contain a method that the interface needs you will get a compilation error:

```
```
error CS0535: 'AccountManagement.CustomerAccount' does not
implement interface member
'AccountManagement.IAccount.PayInFunds(decimal)'
```
```

In this case I missed out the `PayInFunds` method and the compiler complained accordingly.

# ### 4.8.4 References to Interfaces

Once we have made the `CustomerAccount` class compile, we have now got something which can be regarded in two ways:

+   - as a `CustomerAccount` (because that is what it is)
+   - as an `IAccount` (because that is what it can do)

People do this all the time. You can think of me in a whole variety of ways, here are two: