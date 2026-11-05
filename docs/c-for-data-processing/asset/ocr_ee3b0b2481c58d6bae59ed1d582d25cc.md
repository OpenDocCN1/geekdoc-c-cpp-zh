how you really could make a working bank, but it assumes a very good understanding of class hierarchies, method overriding/overloading and constructor chaining. The good news is that when you do understand this stuff you really can call yourself a fully-fledged C# programmer.

# ## Banks and Flexibility

We know that when our system is actually used in a bank there will be a range of different kinds of account class, some of which will be based on others. As an example, we have previously discussed the BabyAccount, a special account for young people which limits the amount that can be withdrawn to no more than 10 pounds. The customer has also asked that the BabyAccount class contains the name of the "parent" account holder. We could implement such behaviour by creating an account which extends the CustomerAccount class and adds the required behaviours and properties:

```
```csharp
public class BabyAccount : CustomerAccount
{
    private string parentName;

    public string GetParentName()
    {
        return parentName;
    }

    public override bool WithdrawFunds(decimal amount)
    {
        if (amount > 10)
        {
            return false;
        }
        return base.WithdrawFunds(amount);
    }

    public BabyAccount(
        string newName,
        decimal initialBalance,
        string inParentName)
        : base(newName, initialBalance)
    {
        parentName = inParentName;
    }
}
```
```

This is a complete BabyAccount implementation. It contains an additional property, parentName, and overrides the WithdrawFunds method to provide the new behaviour. Note that I have created a constructor which is supplied with the name of the account holder, the starting balance and the name of the parent. This makes use of the constructor in the parent to set the balance and name, and then sets the parent name. I can create a BabyAccount as follows:

```
```csharp
BabyAccount babyJane = new BabyAccount ("Jane", 20, "John");
```
```

This would create a new BabyAccount instance and set the reference babyJane to refer to it.

# ## Saving a child class

When we want to save a BabyAccount we also need to save the information from the parent class. This turns out to be very easy, as long as we use the save method which sends the information to a stream.