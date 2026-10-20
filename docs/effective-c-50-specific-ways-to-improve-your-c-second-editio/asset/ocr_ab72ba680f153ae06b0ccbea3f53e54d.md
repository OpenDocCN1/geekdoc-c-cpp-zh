Validator, but now you need to use an international version in one installation. Rather than stick the extra functionality in this one class, you’re better off reducing the coupling between the different items. You create an interface to validate any phone number:

```
```csharp
public interface IPhoneValidator
{
    bool ValidateNumber(PhoneNumber ph);
}
```
```

Next, change the existing phone validator to implement that interface, and make it an internal class:

```
```csharp
internal class USPhoneValidator : IPhoneValidator
{
    public bool ValidateNumber(PhoneNumber ph)
    {
        // perform validation.
        // Check for valid area code, exchange.
        return true;
    }
}
```
```

Finally, you can create a class for international phone validators:

```
```csharp
internal class InternationalPhoneValidator : IPhoneValidator
{
    public bool ValidateNumber(PhoneNumber ph)
    {
        // perform validation.
        // Check international code.
        // Check specific phone number rules.
        return true;
    }
}
```
```

To finish this implementation, you need to create the proper class based on the type of the phone number. You can use the factory pattern for this purpose. Outside the assembly, only the interface is visible. The classes, which are specific for different regions in the world, are visible only inside the assembly. You can add different validation classes for different regions without disturbing any other assemblies in the system. By limiting the