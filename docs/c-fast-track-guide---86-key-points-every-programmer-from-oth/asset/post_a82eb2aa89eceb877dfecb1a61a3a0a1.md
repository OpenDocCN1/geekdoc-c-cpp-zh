
- **Reduces Garbage Collection Overhead:** Since fewer temporary objects are created, memory management is more efficient.

### Performance Comparison

```csharp
using System;
using System.Diagnostics;
using System.Text;
class Program
{
static void Main()
{
int iterations = 10000;
// Using string
Stopwatch sw = Stopwatch.StartNew();
string result = "";
for (int i = 0; i < iterations; i++)
{
result += i.ToString(); // Creates a new string each time
}
sw.Stop();
Console.WriteLine("String time: " + sw.ElapsedMilliseconds + "ms");
// Using StringBuilder
sw.Restart();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < iterations; i++)
{
sb.Append(i.ToString()); // Modifies existing buffer
}
sw.Stop();
Console.WriteLine("StringBuilder time: " + sw.ElapsedMilliseconds + "ms");
}
}
```

Expected Output: String time: 150ms (varies based on system)

StringBuilder time: 2ms (much faster)

StringBuilder is significantly faster for large concatenations. If modifying a string once or twice, string is fine. For repetitive modifications, StringBuilder is the best choice.

### Supplement

StringBuilder is part of System.Text. The default capacity is 16 characters, but it expands automatically. StringBuilder.AppendFormat() allows formatted text insertion. Use .ToString() to retrieve the final string. sb[0] = 'X'; lets you modify characters directly, unlike string.

## 7. PROPERTIES CONTROL ACCESS TO FIELDS IN C#

In C#, properties are used to provide controlled access to fields in a class. Properties can be used to define how the values of private fields are set or retrieved. By using getters (accessors) and setters (mutators), properties allow you to hide the implementation details of the field while providing an interface for external code to interact with the field.

Let's look at a simple example of using properties to control access to a field:

[Code Example]

```csharp
using System;
public class Person
{
private string name; // Private field
// Property to access the private field
public string Name
{
get { return name; } // Getter
set { name = value; } // Setter
}
}
public class Program
{
public static void Main()
{
Person person = new Person();
person.Name = "John Doe"; // Set the value using the setter
Console.WriteLine(person.Name); // Get the value using the getter
}
}
```

### Execution Result

John Doe

In the example above, we have a private field name, and we use the property Name to access and modify its value. The get accessor retrieves the value of the name field, and the set accessor assigns a value to it. The value keyword represents the value passed to the setter. By using properties, we can easily add logic to the getter or setter in the future if needed, without affecting external code that uses the property.

Properties are very useful for implementing validation or modifying data before storing it. You can even use properties to encapsulate more complex logic, such as lazy loading or calculations.

### Supplement

In C#, properties are an essential part of object-oriented programming because they allow encapsulation. They prevent direct access to a field while still providing a way to interact with it. The use of properties can make your code more maintainable and safer by ensuring that fields are only modified in a controlled manner.

## 8. AUTO-IMPLEMENTED PROPERTIES SIMPLIFY CODE

Auto-implemented properties in C# are a shorthand for creating properties when no additional logic is needed in the getter or setter. This simplifies the code by automatically generating a private, anonymous backing field for the property, which eliminates the need to manually define the field and the getter/setter methods.

Let's look at how we can simplify the previous code using an auto-implemented property:

[Code Example]

```csharp
using System;
public class Person
{
    // Auto-implemented property (no need for a private field or getter/setter)
    public string Name { get; set; }
}
public class Program
{
    public static void Main()
    {
        Person person = new Person();
        person.Name = "Jane Doe"; // Set the value using the setter
        Console.WriteLine(person.Name); // Get the value using the getter
    }
}
```

### Execution Result

Jane Doe

In this example, we used an auto-implemented property for Name. This version of the property automatically provides the backing field for you, so there's no need to explicitly define it. The property still provides controlled access to the field, but the C# compiler automatically handles the behind-the-scenes implementation.

Auto-implemented properties are extremely helpful when you don't need to add extra logic to the getter or setter, making your code simpler and more concise. They are a great way to reduce boilerplate code and improve readability, especially for simple classes.

### Supplement

Auto-implemented properties were introduced in C# 3.0, making it easier to create simple properties without manually defining private fields. However, if you need to add validation, logging, or other logic in the getter or setter, you'll need to define the property manually (as shown in the first example). You can also add access modifiers (like private set) to auto-implemented properties for more control over who can modify the property.

## 9. READONLY FIELDS MUST BE SET IN THE CONSTRUCTOR

In C#, a readonly field can only be assigned when it is declared or inside the constructor of the class.

This code shows how a readonly field can be set in the constructor, but not elsewhere.

[Code Example]

```csharp
using System;
class Person
{
    // Readonly field
    public readonly string Name;

    // Constructor assigns the readonly field
    public Person(string name)
    {
        Name = name; // OK: assigning in constructor
    }

    public void ChangeName(string newName)
    {
        // Name = newName; // ERROR: Cannot assign to readonly field here
    }
}
class Program
{
    static void Main()
    {
        Person p = new Person("Alice");
        Console.WriteLine(p.Name);
    }
}
```

### Execution Result

Alice

A readonly field is a variable that can only be assigned once, and only in the following places:

- At declaration, like `public readonly int x = 5;`
- Inside a constructor of the class in which it's defined
- Once set, its value cannot be changed elsewhere, even inside other methods of the same class.
- Trying to modify it outside the constructor causes a compile-time error:
- "A readonly field cannot be assigned to (except in a constructor or a variable initializer)"
- This makes readonly great for values that are determined when the object is created and should not change afterward, like configuration values or identifiers.
- Unlike const, readonly allows setting the value at runtime using constructor parameters.

### Supplement

If you have a value that can’t be known until runtime (like user input), but still should not change after being set, readonly is the correct choice.

readonly fields can also be used with reference types; you can change the content of the object, but not the reference itself. Example:

```csharp
readonly List<int> numbers; → You can do numbers.Add(5);; but not
numbers = new List<int>();
```

### Execution Result

Pi: 3.14159

Created At: [current date and time]

const values are replaced directly into the code during compilation. That means they must be assigned with constant expressions like numbers, strings, etc.

Example:

```csharp
const int MaxScore = 100;
```

```csharp
const DateTime Now = DateTime.Now; (Not allowed — not a constant expression)
```

readonly fields can use values that are only known at runtime, such as system time or user input.

That's why DateTime.Now is okay for readonly, but not for const.

const is implicitly static, meaning it's shared across all instances of the class. readonly is per-instance, unless explicitly marked static.

Trying to assign a runtime value to a const field causes a compile-time error:

> "The expression being assigned to 'const' must be constant"

### Supplement
