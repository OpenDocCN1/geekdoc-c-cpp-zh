When CompanyB attempts to compile its code, the C# compiler issues the following message: "warning CS0108: 'CompanyB.BetterPhone.Dial()' hides inherited member 'CompanyA.Phone.Dial()'. Use the new keyword if hiding was intended." This warning is notifying the developer that CompanyB is defining a Dial method, which will hide the Dial method defined in Phone. This new method could change the semantic meaning of Dial (as defined by CompanyA when it originally created the Dial method).

It's a very nice feature of the compiler to warn you of this potential semantic mismatch. The compiler also tells you how to remove the warning by adding the new keyword before the definition of Dial in the BetterPhone class. Here's the fixed BetterPhone class:

```
```
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {
        // This Dial method has nothing to do with Phone's Dial method.
        public new void Dial() {
            Console.WriteLine("BetterPhone.Dial");
            EstablishConnection();
            base.Dial();
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```
```

At this point, CompanyB can use BetterPhone.Dial in its application. Here's some sample code that CompanyB might write:

```
```
public sealed class Program {
    public static void Main() {
        CompanyB.BetterPhone phone = new CompanyB.BetterPhone();
        phone.Dial();
    }
}
```
```

When this code runs, the following output is displayed:

```
```
BetterPhone.Dial
BetterPhone.EstablishConnection
Phone.Dial
```
```

This output shows that CompanyB is getting the behavior it desires. The call to Dial is calling the new Dial method defined by BetterPhone, which calls the virtual EstablishConnection method and then calls the Phone base type's Dial method.

Now let's imagine that several companies have decided to use CompanyA's Phone type. Let's further imagine that these other companies have decided that the ability to establish a connection in the Dial method is a really useful feature. This feedback is given to CompanyA, which now revises its Phone class: