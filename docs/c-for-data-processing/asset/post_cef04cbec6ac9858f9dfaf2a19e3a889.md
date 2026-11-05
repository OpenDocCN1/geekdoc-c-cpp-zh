
How you really could make a working bank, but it assumes a very good understanding of class hierarchies, method overriding/overloading and constructor chaining. The good news is that when you do understand this stuff you really can call yourself a fully-fledged C# programmer.

## Banks and Flexibility

We know that when our system is actually used in a bank there will be a range of different kinds of account class, some of which will be based on others. As an example, we have previously discussed the BabyAccount, a special account for young people which limits the amount that can be withdrawn to no more than 10 pounds. The customer has also asked that the BabyAccount class contains the name of the "parent" account holder. We could implement such behaviour by creating an account which extends the CustomerAccount class and adds the required behaviours and properties:

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

This is a complete BabyAccount implementation. It contains an additional property, parentName, and overrides the WithdrawFunds method to provide the new behaviour. Note that I have created a constructor which is supplied with the name of the account holder, the starting balance and the name of the parent. This makes use of the constructor in the parent to set the balance and name, and then sets the parent name. I can create a BabyAccount as follows:

```csharp
BabyAccount babyJane = new BabyAccount ("Jane", 20, "John");
```

This would create a new BabyAccount instance and set the reference babyJane to refer to it.

## Saving a child class

When we want to save a BabyAccount we also need to save the information from the parent class. This turns out to be very easy, as long as we use the save method which sends the information to a stream.

```csharp
public override void Save(System.IO.TextWriter textOut)
{
    base.Save(textOut);
    textOut.WriteLine(parentName);
}
```

This method overrides the Save method in the parent CustomerAccount. However, it first calls the overridden method in the parent to save the CustomerAccount data. Then it performs the save behaviour required by the BabyAccount class. This is very good design, as it means that if the data content and save behaviour of the parent class changes we don't need to change the behaviour of the child.

## Loading a child class

We could create a static load method for the BabyAccount which reads in the information and constructs a new BabyAccount:

```csharp
public static BabyAccount Load(
    System.IO.TextReader textIn
)
{
    BabyAccount result = null;
    try
    {
        string name = textIn.ReadLine();
        string balanceText = textIn.ReadLine();
        decimal balance = decimal.Parse(balanceText);
        string parent = textIn.ReadLine();
        result = new BabyAccount (name, balance, parent);
    }
    catch
    {
        return null;
    }
    return result;
}
```

However, I'm not particularly keen on this approach. This method breaks one of the rules of good design, in that we now have a dependency between the two classes which means that when I change the CustomerAccount class (perhaps to add a new field called customerID) I also have to update the Load method in the BabyAccount class to make sure that this extra data is loaded. If I forget to do this the program will compile, but when it runs it will not work correctly.

What we really want to do is make the CustomerAccount responsible for loading its data and the BabyAccount just look after its content; in a similar way to the way the save method uses the base keyword to save the parent object.

The way to do this is to go back to the construction process. We know that a constructor is a method which gets control when an instance of a class is being created. A constructor can be used to set up the data in the instance, and it can be passed information to allow it to do this. In the code above there is a constructor for the BabyAccount class which accepts the three data items that the BabyAccount holds and then sets the instance up with these values.

What we do is create constructors for the CustomerAccount and BabyAccount classes which read their information from a stream that is supplied to them:

```csharp
public CustomerAccount(System.IO.TextReader textIn)
{
    name = textIn.ReadLine();
    string balanceText = textIn.ReadLine();
    balance = decimal.Parse(balanceText);
}
```

This constructor sets up the new CustomerAccount instance by reading the values from the stream that it is supplied with. I can therefore write code like this:

```csharp
System.IO.TextReader textIn =
    new System.IO.StreamReader(filename);
result = new CustomerAccount(textIn);
textIn.Close();
```

This creates a new CustomerAccount from the stream. Now I can create a constructor for the BabyAccount which uses the constructor of the parent class:

```csharp
public BabyAccount(System.IO.TextReader textIn) :
    base (textIn)
{
    parentName = textIn.ReadLine();
}
```

This removes the dependency relationship completely. If the behaviour of the CustomerAccount constructor changes we do not have to change the BabyAccount at all.

Note that these constructors do not do any error checking, they just throw exceptions if something goes wrong. Bearing in mind that the only way that a constructor can fail is to throw an exception anyway, this is reasonable behaviour.

## Interfaces and the save operation

When we started this account development we set out an interface which describes all the things which an instance of an account should be able to do. At the start this did not include the save behaviours, but it could be updated to include them:

```csharp
public interface IAccount
{
    void PayInFunds ( decimal amount );
    bool WithdrawFunds ( decimal amount );
    decimal GetBalance ();
    string GetName();

    bool Save(string filename);
    void Save(System.IO.TextWriter textOut);
}
```

We can now ask any item which implements the IAccount interface to save itself to either a file or a stream. This is very useful when we store our collection of accounts, since the account container will not have to behave differently depending on what kind of account it is saving, it just has to call the save method for the particular instance. This is a good idea.

## Loading and factories

When it comes to loading our classes back, things get a little trickier. You might think it would be sensible to add load methods to the IAccount interface, so that we can ask instances of a particular kind of account to load the data. Unfortunately this is a kind of problem here, in that when we are loading the accounts we don't actually have an instance to call any methods on. Also, bearing mind we are reading from a stream of data, we don't actually know what kind of item we are loading.

The solution to this problem is to identify the type of each instance in the stream when we save the classes. The save method for our bank could look like this:

```csharp
public void Save(System.IO.TextWriter textOut)
{
    textOut.WriteLine(bankHashtable.Count);
    foreach (CustomerAccount account in bankHashtable.Values)
    {
        textOut.WriteLine(account.GetType().Name);
        account.Save(textOut);
    }
}
```

This looks very like our original method, except that it has an additional line, which has been highlighted. This writes out the name of the class. It makes use of the method GetType(), which can be called on an instance of a class to get the type of that class. Having got the type we can then get the Name property of this type and print that. In other words, if the account is of type CustomerAccount the program will output:

```
CustomerAccount
Rob
100
```

The output now contains the name of the type of each class that has been written. This means that when the stream is read back in this information can be used to cause the correct type of class to be created. The nearest way to do this is to create a factory which will produce instances of the required class:

```csharp
class AccountFactory
{
    public static IAccount MakeAccount(
        string name, System.IO.TextReader textIn)
    {
        switch (name)
        {
            case "CustomerAccount":
                return new CustomerAccount(textIn);
            case "BabyAccount":
                return new BabyAccount(textIn);
            default:
                return null;
        }
    }
}
```

This class only contains a single method, which is static. The method is given two parameters, the name of the class to be created and a stream to read from. It uses the name to decide which item to make, creates one, and then returns that to the caller. If the name is not recognized it returns null. The bank load method can use this factory to create instances of accounts as they are loaded:

```csharp
public static HashBank Load(System.IO.TextReader textIn)
{
    HashBank result = new HashBank();
    string countString = textIn.ReadLine();
    int count = Int.Parse(countString);
    for (int i = 0; i < count; i++)
    {
        string className = textIn.ReadLine();
        IAccount account =
            AccountFactory.MakeAccount(className, textIn);
        result.bankHashtable.Add(account.GetName(), account);
    }
    return result;
}
```

Again, this looks very like our original load method, except that it uses the factory to make account instances once it has read the name of the class from the stream.

## Factory Dependencies

Note that we now have a genuine dependency between our system and the factory class. If we ever add a new type of account we need to update the behaviour of the factory so that it contains a case to deal with the new account type. There is in fact a way of removing the need to do this. It involves writing code which will search for C# classes which implement particular interfaces and creating them automatically. However this kind of stuff is beyond the scope of this text.
