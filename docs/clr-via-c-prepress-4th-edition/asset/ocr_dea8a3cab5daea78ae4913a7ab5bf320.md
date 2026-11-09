```
```csharp
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
```csharp
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

```
```csharp
namespace CompanyA {
    public class Phone {
        public void Dial() {
            Console.WriteLine("Phone.Dial");
            EstablishConnection();
            // Do work to dial the phone here.
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("Phone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```
```