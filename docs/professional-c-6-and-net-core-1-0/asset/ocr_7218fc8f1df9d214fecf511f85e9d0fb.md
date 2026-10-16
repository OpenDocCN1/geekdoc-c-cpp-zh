classes (which means that SaverAccount is derived directly from System.Object). By the way, derivation from interfaces acts completely independently from derivation from classes.

Being derived from IBankAccount means that SaverAccount gets all the members of IBankAccount; but because an interface doesn’t actually implement any of its methods, SaverAccount must provide its own implementations of all of them. If any implementations are missing, you can rest assured that the compiler will complain. Recall also that the interface just indicates the presence of its members. It’s up to the class to determine whether it wants any of them to be virtual or abstract (though abstract functions are only allowed if the class itself is abstract). For this particular example, you don’t have any reason to make any of the interface functions virtual.

To illustrate how different classes can implement the same interface, assume that the Planetary Bank of Jupiter also implements a class to represent one of its bank accounts—a Gold Account (code file UsingInterfaces/JupiterBank.cs):

```
namespace Wrox.ProCSharp.JupiterBank
{
    public class GoldAccount: IBankAccount
    {
        // etc
    }
}
```

The details of the GoldAccount class aren’t presented here; in the sample code, it’s basically identical to the implementation of SaverAccount. We stress that GoldAccount has no connection with SaverAccount, other than they both happen to implement the same interface.

Now that you have your classes, you can test them. You first need a few using statements:

```
using Wrox.ProCSharp;
using Wrox.ProCSharp.VenusBank;
using Wrox.ProCSharp.JupiterBank;
using static System.Console;
```

Now you need a Main method (code file UsingInterfaces/Program.cs):

```
namespace Wrox.ProCSharp
{
    class Program
    {
        static void Main()
        {
            IBankAccount venusAccount = new SaverAccount();
            IBankAccount jupiterAccount = new GoldAccount();

            venusAccount.PayIn(200);
            venusAccount.Withdraw(100);
            WriteLine(venusAccount.ToString());

            jupiterAccount.PayIn(500);
```