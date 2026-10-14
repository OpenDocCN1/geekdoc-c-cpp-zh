```
```text
.method public hidebysig specialname instance float64
       get_InRadians() cil managed
{
    .custom instance void [System.Runtime]
        System.Runtime.CompilerServices.IsReadOnlyAttribute::.ctor()
        = (01 00 00 00 )
} // --snip--
```
```

*Listing 4-29: A read-only automatic property*

The compiler adds the IsReadOnlyAttribute indicator for automatic properties in the compiled code and can check for the presence of the attribute cheaply, even when the type of the parameter is declared in a different compiled assembly. In a positional record struct, the compiler generates the properties for the parameters given to the type. The get accessors of those generated properties also have IsReadOnlyAttribute applied.

When we use an in parameter variable to call methods or access property values, the compiler checks those methods and properties. If this attribute is present, the compiler knows it can avoid making defensive copies.

# Read-Only Reference Variables

Defensive copies are also required when we use read-only local reference variables, unless the compiler is satisfied that accessing the variable can’t change its value. We explored in Chapter 3 how local reference variables are used in cooperation with reference return values.

A method or property of a class or a record—but not a struct or record struct—can return an instance held by reference. If we return a value by reference, no copy of the value is made. Making it read-only ensures that the value can’t be modified using that reference. For example, the Projectile class in Listing 4-30 has properties that return instance fields by reference.

```
```csharp
public sealed class Projectile
{
    public Projectile(Speed speed, Angle angle)
        => (initial, direction) = (speed, angle);

    public ref readonly Speed Speed => ref initialSpeed;
    public ref readonly Angle Angle => ref initialDirection;

    private readonly Speed initialSpeed;
    private readonly Angle initialDirection;
}
```
```

*Listing 4-30: Defining ref return values for the Projectile class*

The references returned by these Angle and Speed properties can never outlive the Projectile instance because Projectile is a class, so its instances are allocated on the heap and their lifetimes are governed by the garbage collector. Value types are not permitted to return their fields by reference because the instance’s lifetime might end before any reference to its internals.