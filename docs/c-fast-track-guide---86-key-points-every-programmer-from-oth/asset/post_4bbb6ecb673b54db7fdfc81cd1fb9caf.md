
- When assigned to another variable, the **reference** (not the actual data) is copied.
- Changes in one variable **affect** the other because they point to the same object.
- Examples: `class`, `string`, `array`, `interface`, `delegate`.

### Stack vs Heap

- **Stack**: Faster access, automatic memory cleanup when out of scope.
- **Heap**: Slower but can store larger, more complex data structures.

### Common Mistakes

- 1. **Confusing Structs and Classes**
  - Structs (`struct`) are **value types** (stored in stack).
  - Classes (`class`) are **reference types** (stored in heap).
  - Use structs for small, immutable data; use classes for complex objects.
- 2. **Unintended Reference Sharing**
  - When passing a reference type to a method, changes inside the method affect the original object.
  - Use `ref` or `out` keywords if explicitly intending reference behavior with value types.
- 3. **Nullable Types**
  - Value types **cannot** be null by default. Use `Nullable<T>` or `?` (e.g., `int? myInt = null;`).
  - Reference types **can** be null, leading to potential `NullReferenceException`.

### [Supplement]

- Strings in C# are **reference types** but behave **like value types** (immutable).
- `struct` should be used for **small, immutable data** to improve performance.
- Arrays are **reference types**, even if they store value types.
- If a class contains a value type, the value type **remains in the heap** because it's part of the reference type.
- Boxing and Unboxing occur when a value type is stored as an object (`object o = 10;`).

## 3. STRUCTS VS. CLASSES: VALUE TYPES VS. REFERENCE TYPES

In C#, structs and classes serve different purposes. Structs are value types, which means they are stored directly in memory and copied when assigned or passed. Classes, on the other hand, are reference types, meaning they are stored in the heap and passed by reference. Understanding this difference is crucial for writing efficient and bug-free code.

Below is a simple example demonstrating how structs and classes behave differently when assigned to a new variable.

[Code Example]

```csharp
using System;
struct MyStruct
{
    public int Value;
}
class MyClass
{
    public int Value;
}
class Program
{
    static void Main()
    {
        // Struct Example (Value Type)
        MyStruct struct1 = new MyStruct { Value = 10 };
        MyStruct struct2 = struct1;
        struct2.Value = 20;
        Console.WriteLine($"Struct1 Value: {struct1.Value}"); // Remains 10
        Console.WriteLine($"Struct2 Value: {struct2.Value}"); // Changes to 20
        // Class Example (Reference Type)
        MyClass class1 = new MyClass { Value = 10 };
        MyClass class2 = class1;
        class2.Value = 20;
        Console.WriteLine($"Class1 Value: {class1.Value}"); // Changes to 20
        Console.WriteLine($"Class2 Value: {class2.Value}"); // Changes to 20
    }
}
```

[Execution Result]

- Struct1 Value: 10
- Struct2 Value: 20
- Class1 Value: 20
- Class2 Value: 20

Structs are stored on the stack, making them efficient for small, simple data types. Classes are stored on the heap, making them more flexible but slightly slower due to garbage collection. When assigning a struct to another variable, a copy is made, so changes in one do not affect the other. When assigning a class instance to another variable, only the reference is copied, meaning changes in one will reflect in the other. Use structs for lightweight data structures, such as coordinates, colors, or small immutable objects. Use classes when you need complex behavior, inheritance, or large objects that should not be frequently copied.

- Lightweight data structures
- Value copy on assignment
- Stack storage efficiency
- Structs
- Complex behavior support
- Reference copy on assignment
- Heap storage flexibility
- Classes

![](img/bb6e93ece31f33afd31e933e9dd494be_27_0.png)

Choose structs for efficiency; classes for complexity.

### [Supplement]

Structs cannot inherit from other structs or classes, but they can implement interfaces. Classes support polymorphism and inheritance, while structs do not. Default constructor is not allowed for structs (they always have an implicit parameterless constructor).

## 4. UNDERSTANDING ENUMS: STRONGLY-TYPED CONSTANTS

Enums in C# provide a way to define a set of named constant values, which are strongly typed and mapped to an underlying integral type (default: int). This makes code more readable and prevents invalid values from being used.

Below is an example of defining and using an enum to represent different user roles in a system.

```csharp
using System;

enum UserRole
{
    Admin = 1,
    Moderator = 2,
    User = 3
}

class Program
{
    static void Main()
    {
        UserRole role = UserRole.Moderator;
        Console.WriteLine($"Role: {role}"); // Output: Moderator
        Console.WriteLine($"Role Value: {(int)role}"); // Output: 2

        // Checking an enum value
        if (role == UserRole.Admin)
        {
            Console.WriteLine("You have admin privileges.");
        }
        else
        {
            Console.WriteLine("You do not have admin privileges.");
        }
    }
}
```

[Execution Result]

```
Role: Moderator
Role Value: 2
You do not have admin privileges.
```

By default, enums start from 0, but you can specify values explicitly. Enums improve code readability by replacing magic numbers with meaningful names. You can cast enums to and from integers, which allows compatibility with external data sources (e.g., databases). Enums can be combined using bitwise operations when marked with [Flags] (useful for permission systems). Always define default values explicitly to prevent unintended values.

### Using enums in C#

| Pros | Cons |
|---|---|
| Improved readability | Need for explicit default values |
| Explicit value assignment |  |
| Compatibility with external data |  |
| Bitwise operations |  |

### [Supplement]

The default underlying type of an enum is int, but it can be changed to other integral types (byte, short, long, etc.). Enum.Parse() can be used to convert a string into an enum value. Enums cannot contain methods, but extension methods can be used to add behavior to them.

## 5. STRINGS IN C# ARE IMMUTABLE

In C#, strings are immutable, meaning any modification to a string actually creates a new string instance in memory instead of altering the existing one.

If you change a string, a new memory allocation occurs, and the old value remains unchanged. Here’s a simple example:

[Code Example]

```csharp
using System;
class Program
{
    static void Main()
    {
        string original = "Hello";
        string modified = original + " World"; // This creates a new string instance
        Console.WriteLine("Original: " + original); // "Hello"
        Console.WriteLine("Modified: " + modified); // "Hello World"
    }
}
```

[Execution Result]

```
Original: Hello
Modified: Hello World
```

### Why Are Strings Immutable?

- **Memory Efficiency:** Immutable strings can be safely shared across multiple parts of a program.
- **Thread Safety:** Since strings can't change after creation, there's no risk of unexpected modifications in multi-threaded applications.

### C# String Immutability and Performance

![](img/bb6e93ece31f33afd31e933e9dd494be_33_0.png)

### [Supplement]

- Strings are **reference types** in C#, but they behave like **value types** due to immutability.
- `string` is an alias for `System.String`.
- The `==` operator checks **value equality** instead of reference equality for strings.
- String immutability is similar in other languages like Java and Python.
- `string.Empty` is recommended over `""` because it avoids unnecessary allocations.

## 6. USE STRINGBUILDER FOR EFFICIENT STRING MANIPULATION

`StringBuilder` is a mutable alternative to `string`, allowing efficient string concatenation and modification without creating multiple new instances.

Instead of using `+=` or `string.Concat`, use `StringBuilder` for performance improvements in loops or frequent modifications.

[Code Example]

```csharp
using System;
using System.Text;
class Program
{
    static void Main()
    {
        StringBuilder sb = new StringBuilder("Hello");
        sb.Append(" World"); // Modifies the existing instance instead of creating a new one
        Console.WriteLine(sb.ToString()); // "Hello World"
    }
}
```

[Execution Result]

```
Hello World
```

### Why Use `StringBuilder`?

- **Avoids Excessive Memory Allocation:** Instead of creating a new string every time, `StringBuilder` modifies the existing buffer.
- **Improves Performance:** Particularly useful in loops where multiple string concatenations occur.
