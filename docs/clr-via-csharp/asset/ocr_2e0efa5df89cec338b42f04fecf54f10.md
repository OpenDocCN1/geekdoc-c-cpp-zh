Fortunately, C# does offer a way to use simplified syntax to refer to a generic closed type while not affecting type equivalence at all; you can use the good old **using** directive at the top of your source code file. Here is an example:

```
```csharp
using DateTimeList = System.Collections.Generic.List<System.DateTime>;
```
```

Here, the **using** directive is really just defining a symbol called **DateTimeList**. As the code compiles, the compiler substitutes all occurrences of **DateTimeList** with **System.Collections.Generic.List<System.DateTime>**. This just allows developers to use a simplified syntax without affecting the actual meaning of the code, and therefore, type identity and equivalence are maintained. So now, when the following line executes, **sameType** will be initialized to **true**.

```
```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```
```

As another convenience, you can use C#’s implicitly typed local variable feature, where the compiler infers the type of a method’s local variable from the type of the expression you are assigning to it:

```
```csharp
using System;
using System.Collections.Generic;

internal sealed class SomeType {
    private static void SomeMethod () {

        // Compiler infers that DateTimeList is of type
        // System.Collections.Generic.List<System.DateTime>
        var dt1 = List<DateTime>();

    }
}
```
```

# Code Explosion

When a method that uses generic type parameters is JIT-compiled, the CLR takes the method’s IL, substitutes the specified type arguments, and then creates native code that is specific to that method operating on the specified data types. This is exactly what you want and is one of the main features of generics. However, there is a downside to this: the CLR keeps generating native code for every method/type combination. This is referred to as *code explosion*. This can end up increasing the application’s working set substantially, thereby hurting performance.

Fortunately, the CLR has some optimizations built into it to reduce code explosion. First, if a method is called for a particular type argument, and later, the method is called again using the same type argument, the CLR will compile the code for this method/type combination just once. So if one assembly uses **List<DateTime>**, and a completely different assembly