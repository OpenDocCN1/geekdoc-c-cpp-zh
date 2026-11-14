replaced with literal values in the compiler-generated IL. The following construct does not compile. You cannot initialize a compile-time constant using the new operator, even when the type being initialized is a value type:

```
// Does not compile; use readonly instead:
private const DateTime classCreation = new
    DateTime(2000, 1, 1, 0, 0, 0);
```

Compile-time constants are limited to numbers and strings. Read-only values are also constants, in that they cannot be modified after the constructor has executed. But read-only values are different in that they are assigned at runtime. You have much more flexibility in working with run-time constants. For one thing, runtime constants can be any type. You must initialize them in a constructor, or you can use an initializer. You can make readonly values of the DateTime structures; you cannot create DateTime values with const.

You can use readonly values for instance constants, storing different values for each instance of a class type. Compile-time constants are, by definition, static constants.

The most important distinction is that readonly values are resolved at runtime. The IL generated when you reference a readonly constant references the IL variable, not the value. This distinction has far-reaching implications on maintenance over time. Compile-time constants generate the same IL as though you've used the numeric constants in your code, even across assemblies: A constant in one assembly is still replaced with the value when used in another assembly.

The way in which compile-time and runtime constants are evaluated affects runtime compatibility. Suppose you have defined both const and readonly fields in an assembly named Infrastructure:

```
public class UsefulValues
{
    public static readonly int StartValue = 5;
    public const int EndValue = 10;
}
```

In another assembly, you reference these values:

```
for (int i = UsefulValues.StartValue;
     i < UsefulValues.EndValue; i++)
    Console.WriteLine("value is {0}", i);
```