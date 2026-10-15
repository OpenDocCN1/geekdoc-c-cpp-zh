keyword. Both are valid C# references to the System.String data type, and the resultant CIL code is unaffected by which version is chosen.

# ADVANCED TOPIC

# Nested using Directives

Not only can you have using directives at the top of a file, but you also can include them at the top of a namespace declaration. For example, if a new namespace, EssentialCSharp, were declared, it would be possible to add a using declarative at the top of the namespace declaration (see Listing 4.7).

```
```csharp
namespace EssentialCSharp
{
    using System;

    class HelloWorld
    {
        static void Main()
        {
            // No need to qualify Console with System
            // because of the using directive above.
            Console.WriteLine("Hello, my name is Inigo Montoya");
        }
    }
}
```
```

The results of Listing 4.7 appear in Output 4.3.

```
```text
Hello, my name is Inigo Montoya
```
```

The difference between placing the using directive at the top of a file and placing it at the top of a namespace declaration is that the directive is active only within the namespace declaration. If the code includes a new