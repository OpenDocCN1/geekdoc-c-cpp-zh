```
```csharp
using Project = PC.MyCompany.Project;
```
```

The `using` keyword is also used to create *using statements*, which help ensure that `System.IDisposable` objects such as files and fonts are handled correctly.

# ## Using static type

You can access static members of a type without having to qualify the access with the type name:

```
```csharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```
```

# ## Remarks

The scope of a `using` directive is limited to the file in which it appears.

The `using` directive can appear:

+   - At the beginning of a source code file, before any namespace or type definitions.
- In any namespace, but before any namespace or types declared in this namespace.

Otherwise, compiler error [CS1529] is generated.

Create a `using` alias directive to make it easier to qualify an identifier to a