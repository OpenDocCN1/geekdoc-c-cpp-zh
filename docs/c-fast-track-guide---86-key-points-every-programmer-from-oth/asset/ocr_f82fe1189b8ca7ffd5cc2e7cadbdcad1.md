# 7. PROPERTIES CONTROL ACCESS TO FIELDS IN C#

In C#, properties are used to provide controlled access to fields in a class. Properties can be used to define how the values of private fields are set or retrieved. By using getters (accessors) and setters (mutators), properties allow you to hide the implementation details of the field while providing an interface for external code to interact with the field.

Let's look at a simple example of using properties to control access to a field:

[Code Example]

```
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