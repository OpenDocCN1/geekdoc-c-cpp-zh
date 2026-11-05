+   - Rob Miles the individual (because that is who I am)
+   - A university lecturer (because that is what I can do)

If you think of me as a lecturer you would be using the interface that contains methods like GiveLecture. And you can use the same methods with any other lecturer (i.e. person who implements that interface). From the point of view of the university, which has to manage a large number of interchangeable lecturers, it is much more useful for it to think of me as a lecturer, rather than Rob Miles the individual.

So, with interfaces we are moving away from considering classes in terms of what they are, and starting to think about them in terms of what they can do. In the case of our bank, this means that we want to deal with objects in terms of IAccount, (the set of account abilities) rather than CustomerAccount (a particular account class).

In C# terms this means that we need to be able to create reference variables which refer to objects in terms of interfaces they implement, rather than the particular type that they are. It turns out that this is quite easy:

```
IAccount account = new CustomerAccount();
account.PayInFunds(50);
```

The account variable is allowed to refer to objects which implement the IAccount interface. The compiler will check to make sure that CustomerAccount does this, and if it does, the compilation is successful.

Note that there will never be an instance of IAccount interface. It is simply a way that we can refer to something which has that ability (i.e. contains the required methods).

This is the same in real life. There is no such physical thing as a "lecturer", merely a large number of people who can be referred to as having that particular ability or role.

# 4.8.5 Using interfaces

Now that we have our system designed with interfaces it is much easier to extend it. I can create a BabyAccount class which implements the IAccount interface. This implements all the required methods, but they behave slightly differently because we want all withdrawals of over ten pounds to fail:

```
public class BabyAccount : IAccount
{
    private decimal balance = 0;
    public bool WithdrawFunds ( decimal amount )
    {
        if (amount > 10)
        {
            return false ;
        }
        if (balance < amount)
        {
            return false ;
        }
        balance = balance - amount ;
        return true;
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