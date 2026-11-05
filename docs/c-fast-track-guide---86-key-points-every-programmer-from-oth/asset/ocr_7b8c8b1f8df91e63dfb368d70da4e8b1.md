# 33. ANONYMOUS TYPES ARE IMMUTABLE AND DEFINED AT COMPILE-TIME

Anonymous types are objects without explicitly defined class names. They are used for quick grouping of data, especially useful in LINQ queries. Once created, their properties are read-only and cannot be changed.

Here's a short example that creates and uses an anonymous type.

[Code Example]

```
```csharp
using System;

class Program
{
    static void Main()
    {
        // Creating an anonymous type with two properties
        var person = new { Name = "Alice", Age = 30 };
        // Accessing the properties
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
        // person.Age = 31; // This line would cause a compile-time error because properties are read-only
    }
}
```
```

[Execution Result]

Name: Alice, Age: 30

Anonymous types are defined using the new {} syntax. They are mostly used when: