# 35. UNDERSTANDING C# RECORDS FOR IMMUTABLE DATA STRUCTURES

Records in C# are a type of reference object meant to store data immutably. Once created, their data cannot be changed.

Here’s a basic example of using a C# record to represent a person, showing how the data stays fixed after creation.

[Code Example]

```
// Define a record type with two properties
public record Person(string FirstName, string LastName);
class Program
{
static void Main()
{
// Create a new record instance
var person1 = new Person("Alice", "Smith");
// Use 'with' expression to create a new record with one changed property
var person2 = person1 with { LastName = "Johnson" };
Console.WriteLine(person1); // Output: Person { FirstName = Alice, LastName = Smith }
Console.WriteLine(person2); // Output: Person { FirstName = Alice, LastName = Johnson }
}
}
```

[Execution Result]

Person { FirstName = Alice, LastName = Smith }

Person { FirstName = Alice, LastName = Johnson }

record types in C# were introduced in C# 9.