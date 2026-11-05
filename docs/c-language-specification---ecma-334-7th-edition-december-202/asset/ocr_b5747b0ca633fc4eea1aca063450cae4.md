declares Eg.M as a conditional method associated with the two conditional compilation symbols ALPHA and BETA.

*end example*

A call to a conditional method is included if one or more of its associated conditional compilation symbols is defined at the point of call, otherwise the call is omitted.

A conditional method is subject to the following restrictions:

+   - The conditional method shall be a method in a `class_declaration` or `struct_declaration`. A compile-time error occurs if the `Conditional` attribute is specified on a method in an interface declaration.
+   - The conditional method shall have a return type of `void`.
+   - The conditional method shall not be marked with the `override` modifier. A conditional method can be marked with the `virtual` modifier, however. Overrides of such a method are implicitly conditional, and shall not be explicitly marked with a `Conditional` attribute.
+   - The conditional method shall not be an implementation of an interface method. Otherwise, a compile-time error occurs.
+   - The parameters of the conditional method shall not have the `out` modifier.

In addition, a compile-time error occurs if a delegate is created from a conditional method.

*Example:* The example

```
```csharp
#define DEBUG
using System;
using System.Diagnostics;

class Class1
{
    [Conditional("DEBUG")]
    public static void M()
    {
        Console.WriteLine("Executed Class1.M");
    }
}

class Class2
{
    public static void Test()
    {
        Class1.M();
    }
}
```
```

declares Class1.M as a conditional method. Class2's Test method calls this method. Since the conditional compilation symbol DEBUG is defined, if Class2.Test is called, it will call M. If the symbol DEBUG had not been defined, then Class2.Test would not call Class1.M.

*end example*

It is important to understand that the inclusion or exclusion of a call to a conditional method is controlled by the conditional compilation symbols at the point of the call.

*Example:* In the following code