> **NOTE** `IDisposable` *is a relatively simple interface because it defines only one method. Most interfaces contain more members. The correct implementation of `IDisposable` is not really that simple; it’s covered in Chapter 5.*

# Defining and Implementing Interfaces

This section illustrates how to define and use interfaces by developing a short program that follows the interface inheritance paradigm. The example is based on bank accounts. Assume that you are writing code that will ultimately allow computerized transfers between bank accounts. Assume also for this example that there are many companies that implement bank accounts, but they have all mutually agreed that any classes representing bank accounts will implement an interface, `IBankAccount`, which exposes methods to deposit or withdraw money, and a property to return the balance. It is this interface that enables outside code to recognize the various bank account classes implemented by different bank accounts. Although the aim is to enable the bank accounts to communicate with each other to allow transfers of funds between accounts, that feature isn’t introduced just yet.

To keep things simple, you keep all the code for the example in the same source file. Of course, if something like the example were used in real life, you could surmise that the different bank account classes would not only be compiled to different assemblies, but also be hosted on different machines owned by the different banks. That’s all much too complicated for the purposes of this example. However, to maintain some realism, you define different namespaces for the different companies.

To begin, you need to define the `IBankAccount` interface (code file `UsingInterfaces/IBankAccount.cs`):

```
namespace Wrox.ProCSharp
{
    public interface IBankAccount
    {
        void PayIn(decimal amount);
        bool Withdraw(decimal amount);
        decimal Balance { get; }
    }
}
```

Notice the name of the interface, `IBankAccount`. It’s a best-practice convention to begin an interface name with the letter I, to indicate it’s an interface.