
### 4.8.3 Implementing an Interface in C#

Interfaces become interesting when we make a class implement them. Implementing an interface is like setting up a contract between the supplier of services and the consumer. If a class implements an interface it is saying that for every method described in the interface, it has a corresponding implementation.

In the case of the bank account, I am going to create a class which implements the interface, so that it can be thought of as an account component, irrespective of what it really is:

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

The code above does not look that different from the previous account class. The only difference is the top line:

```csharp
public class CustomerAccount : IAccount
{
    ...
}
```

The highlighted part of the line above is where the programmer tells the compiler that this class implements the `IAccount` interface. This means that the class contains concrete versions of all the methods described in the interface. If the class does not contain a method that the interface needs you will get a compilation error:

```text
error CS0535: 'AccountManagement.CustomerAccount' does not
implement interface member
'AccountManagement.IAccount.PayInFunds(decimal)'
```

In this case I missed out the `PayInFunds` method and the compiler complained accordingly.

### 4.8.4 References to Interfaces

Once we have made the `CustomerAccount` class compile, we have now got something which can be regarded in two ways:

- as a `CustomerAccount` (because that is what it is)
- as an `IAccount` (because that is what it can do)

People do this all the time. You can think of me in a whole variety of ways, here are two:

- Rob Miles the individual (because that is who I am)
- A university lecturer (because that is what I can do)

If you think of me as a lecturer you would be using the interface that contains methods like GiveLecture. And you can use the same methods with any other lecturer (i.e. person who implements that interface). From the point of view of the university, which has to manage a large number of interchangeable lecturers, it is much more useful for it to think of me as a lecturer, rather than Rob Miles the individual.

So, with interfaces we are moving away from considering classes in terms of what they are, and starting to think about them in terms of what they can do. In the case of our bank, this means that we want to deal with objects in terms of IAccount, (the set of account abilities) rather than CustomerAccount (a particular account class).

In C# terms this means that we need to be able to create reference variables which refer to objects in terms of interfaces they implement, rather than the particular type that they are. It turns out that this is quite easy:

```csharp
IAccount account = new CustomerAccount();
account.PayInFunds(50);
```

The account variable is allowed to refer to objects which implement the IAccount interface. The compiler will check to make sure that CustomerAccount does this, and if it does, the compilation is successful.

Note that there will never be an instance of IAccount interface. It is simply a way that we can refer to something which has that ability (i.e. contains the required methods).

This is the same in real life. There is no such physical thing as a "lecturer", merely a large number of people who can be referred to as having that particular ability or role.

### 4.8.5 Using interfaces

Now that we have our system designed with interfaces it is much easier to extend it. I can create a BabyAccount class which implements the IAccount interface. This implements all the required methods, but they behave slightly differently because we want all withdrawals of over ten pounds to fail:

```csharp
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

The nice thing about this is that as it is a component we don't have to change all the classes which use it. When we create the account objects we just have to ask if a standard account or a baby account is required. The rest of the system can then pick up this object and use it without caring exactly what it is. We will of course have to create some tests especially for it, so that we can make sure that withdrawals of more than ten pounds do fail, but using the new kind of account in our existing system is very easy.

### 4.8.6 Implementing Multiple Interfaces

A component can implement as many interfaces as are required. The IAccount interface lets me regard a component purely in terms of its ability to behave as a bank account. However, I may want to regard a component in a variety of ways. For example, the bank will want the account to be able to print itself out on paper.

You might think that all I have to do is add a print method to the IAccount interface. This would be reasonable if all I ever wanted to print was bank accounts. However, there will be lots of things which need to be printed, for example warning letters, special offers and the like. Each of these items will be implemented in terms of a component which provides a particular interface (IWarning, ISpecialOffer for example). I don't want to have to provide a print method in each of these, what I really want is a way that I can regard an object in terms of its ability to print.

This is actually very easy. I create the interface:

```csharp
public interface IPrintToPaper
{
    void DoPrint();
}
```

Now anything which implements the IPrintToPaper interface will contain the DoPrint method and can be thought of in terms of its ability to print.

A class can implement as many interfaces as it needs. Each interface is a new way in which it can be referred to and accessed.

```csharp
public class BabyAccount : IAccount, IPrintToPaper
{
    ...
}
```

This means that a BabyAccount instance behaves like an account and it also contains a DoPrint method which can be used to make it print out.

### 4.8.7 Designing with Interfaces

If you apply the "abstraction" technique properly you should end up with a system creation process which goes along the lines of:

- gather as much metadata as you can about the problem; what is important to the customer, what values need to be represented and manipulated and the range of those values
- identify classes that you will have to create to represent the components in the problem
- identify the actions (methods) and the values (properties) that the components must provide
- put these into interfaces for each of the components
- decide how these values and actions are to be tested
- implement the components and test them as you go

You can't do much of this on paper, before you write any code at all. There are also graphical tools that you can use to draw formal diagrams to represent this information. The field of Software Engineering is entirely based on this process.

You should also have spotted that interfaces are good things to hang tests on. If you have a set of fundamental behaviours that all bank accounts must have (for example paying in money must always make the account balance go up) then you can write tests that bind to the `IAccount` interface and can be used to test any of the bank components that are created.

### Programmer’s Point: Interfaces are just promises

An interface is less of a binding contract, and more a promise. Just because a class has a method called `PayInFunds` does not mean that it will pay money into the account; it just means that a method with that name exists within the class. Nothing in C# allows you to enforce a particular behaviour on a method; that is down to how much you trust the programmer that made the class that you are using, and how good your tests are. In fact, we sometimes use this to good effect when building a program, in that we can create “dummy” components which implement the interface but don’t have the behaviour as such.

The interface mechanism gives us a great deal of flexibility when making our components and fitting them together. It means that once we have found out what our bank account class needs to hold for us we can then go on to consider what we are going to ask the accounts to do. This is the real detail in the specification. Once we have set out an interface for a component we can then just think in terms of what the component must do, not precisely how it does it.

For example, the manager has told us that each bank account must have an account number. This is a very important value, in that it will be fixed for the life of the account and can never be changed. No two accounts should ever have the same number.

From the point of view of interface design this means that the account number will be set when the account is created and the account class will provide a method to let us get the value (but there will not be a method to set the account number).

We don’t care what the method `GetAccountNumber` actually does, as long as it always returns the value for a particular account. So this requirement ends up being expressed in the interface that is implemented by the account class.

```csharp
interface IAccount
{
    int GetAccountNumber();
}
```

This method returns the integer which is the account number for this instance. By placing it in the interface we can say that the account must deliver this value, but we have not actually described how this should be done. The design of the interfaces in a system is just this. They state that we have a need for behaviours, but they do not necessarily state how they are made to work. I have to add comments to give more detail about what the method does.

The need for things like account numbers, which really need to be unique in the world, has resulted in the creation of a set of methods in the C# libraries to create things called Globally Unique Identifiers or GUIDs. These are data items which are created based on the date, time and certain information about the host computer. Each GUID is unique in the world. We could use these in our Account constructor to create a GUID which allows each account to have a unique number.

## 4.9 Inheritance

Inheritance is another way we can implement creative laziness. It is a way that we can pick up behaviours from classes and just modify the bits we need to make new ones. In this respect you can regard it as a mechanism for what is called code reuse. It can also be used at the design stage of a program if you have a set of related objects that you wish to create.

Inheritance lets a class pick up behaviours from the class which is its parent. You can regard an interface as a statement by a class that it has a set of behaviours because it implements a given interface. If a class is descended from a particular parent class this
