infers the type of a method's local variable from the type of the expression you are assigning to it:

```
```csharp
using System;
using System.Collections.Generic;
...
internal sealed class SomeType {
    private static void SomeMethod() { }

        // Compiler infers that dtl is of type
        // System.Collections.Generic.List<System.DateTime>
        var dtl = new List<DateTime>();

        ...
    }
}
```
```

# ## Code Explosion

When a method that uses generic type parameters is JIT-compiled, the CLR takes the method's IL, substitutes the specified type arguments, and then creates native code that is specific to that method operating on the specified data types. This is exactly what you want and is one of the main features of generics. However, there is a downside to this: the CLR keeps generating native code for every method/type combination. This is referred to as code explosion. This can end up increasing the application's working set substantially, thereby hurting performance.

Fortunately, the CLR has some optimizations built into it to reduce code explosion. First, if a method is called for a particular type argument, and later, the method is called again using the same type argument, the CLR will compile the code for this method/type combination just once. So if one assembly uses List<DateTime>, and a completely different assembly (loaded in the same AppDomain) also uses List<DateTime>, the CLR will compile the methods for List<DateTime> just once. This reduces code explosion substantially.

The CLR has another optimization: the CLR considers all reference type arguments to be identical, and so again, the code can be shared. For example, the code compiled by the CLR for List<String>'s methods can be used for List<Stream>'s methods, since String and Stream are both reference types. In fact, for any reference type, the same code will be used. The CLR can perform this optimization because all reference type arguments or variables are really just pointers (all 32 bits on a 32-bit Windows system and 64 bits on a 64-bit Windows system) to objects on the heap, and object pointers are all manipulated in the same way.

But if any type argument is a value type, the CLR must produce native code specifically for that value type. The reason is because value types can vary in size. And even if two value types are the same size (such as Int32 and UInt32, which are both 32 bits), the CLR still can't share the code because different native CPU instructions can be used to manipulate these values.