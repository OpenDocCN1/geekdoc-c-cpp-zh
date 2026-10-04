```
namespace CompanyA {
    public class Phone {
        public void Dial() {
            Console.WriteLine("Phone.Dial");
            EstablishConnection();
            // Work to dial the phone here.
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("Phone.EstablishConnection");
            // Work to establish the connection.
        }
    }
}
```

Now when B compiles its BetterPhone type (derived from this new version of Anya's Phone), the compiler issues this message.

warning CS0114: 'nrB.BetterPhone.EstablishConnection()' hides inherited member 'CompanyA.Phone.EstablishConnection()'. To make the current member override that implementation, add the override keyword. Otherwise, add the new keyword.

The compiler is alerting you to the fact that both Phone and BetterPhone offer an Connection method and that the semantics of both might not be identical; simply compiling BetterPhone can no longer give the same behavior as it did when using the first version of the Phone type.

If CompanyB decides that the EstablishConnection methods are not semantically identical in both types, CompanyB can tell the compiler that the Dial and EstablishConnection method defined in BetterPhone is the correct method to use and that it has no relationship with the EstablishConnection method defined in the Phone base type. CompanyB informs the compiler by adding the new keyword to the EstablishConnection method.

```
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {
        // Keep 'new' to mark this method as having no
        // relationship to the base type's Dial method.
        public void Dial() {
            Console.WriteLine("BetterPhone.Dial");
            EstablishConnection();
            base.Dial();
        }

        // Add 'new' to mark this method as having no
    // relationship to the base type's EstablishConnection method.
        protected virtual void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Work to establish the connection.
        }
    }
}
```