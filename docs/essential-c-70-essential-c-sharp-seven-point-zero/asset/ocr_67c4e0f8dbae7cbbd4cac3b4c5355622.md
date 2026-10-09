# Casting between Base and Derived Types

As Listing 7.4 shows, because derivation forms an “is a” relationship, a derived type value can always be directly assigned to a base type variable.

# LISTING 7.4: Implicit Base Type Casting

```
```
public class Program
{
    public static void Main()
    {
        // Derived types can be implicitly converted to
        // base types
        Contact contact = new Contact();
        PdaItem item = contact;
        // ...

        // Base types must be cast explicitly to derived types
        contact = (Contact)item;
        // ...
    }
}
```
```

The derived type, Contact, is a PdaItem and can be assigned directly to a variable of type PdaItem. This is known as an **implicit conversion** because no cast operator is required and the conversion will, on principle, always succeed; that is, it will not throw an exception.

The reverse, however, is not true. A PdaItem is not necessarily a Contact; it could be an Appointment or some other derived type. Therefore, casting from the base type to the derived type requires an **explicit cast**, which could fail at runtime. To perform an explicit cast, you identify the target type within parentheses prior to the original reference, as Listing 7.4 demonstrates.

With the explicit cast, the programmer essentially communicates to the compiler to trust her—she knows what she is doing—and the C# compiler allows the conversion to proceed if the target type is derived from the originating type. Although the C# compiler allows an explicit