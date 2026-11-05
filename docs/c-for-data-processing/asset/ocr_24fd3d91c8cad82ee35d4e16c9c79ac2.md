```
```csharp
public override void Save(System.IO.TextWriter textOut)
{
    base.Save(textOut);
    textOut.WriteLine(parentName);
}
```
```

This method overrides the Save method in the parent CustomerAccount. However, it first calls the overridden method in the parent to save the CustomerAccount data. Then it performs the save behaviour required by the BabyAccount class. This is very good design, as it means that if the data content and save behaviour of the parent class changes we don't need to change the behaviour of the child.

# Loading a child class

We could create a static load method for the BabyAccount which reads in the information and constructs a new BabyAccount:

```
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
```

However, I'm not particularly keen on this approach. This method breaks one of the rules of good design, in that we now have a dependency between the two classes which means that when I change the CustomerAccount class (perhaps to add a new field called customerID) I also have to update the Load method in the BabyAccount class to make sure that this extra data is loaded. If I forget to do this the program will compile, but when it runs it will not work correctly.

What we really want to do is make the CustomerAccount responsible for loading its data and the BabyAccount just look after its content; in a similar way to the way the save method uses the base keyword to save the parent object.

The way to do this is to go back to the construction process. We know that a constructor is a method which gets control when an instance of a class is being created. A constructor can be used to set up the data in the instance, and it can be passed information to allow it to do this. In the code above there is a constructor for the BabyAccount class which accepts the three data items that the BabyAccount holds and then sets the instance up with these values.

What we do is create constructors for the CustomerAccount and BabyAccount classes which read their information from a stream that is supplied to them:

```
```csharp
public CustomerAccount(System.IO.TextReader textIn)
{
    name = textIn.ReadLine();
    string balanceText = textIn.ReadLine();
    balance = decimal.Parse(balanceText);
}
```
```

This constructor sets up the new CustomerAccount instance by reading the values from the stream that it is supplied with. I can therefore write code like this: