```
```csharp
// Implementation
}
public class B : A
{
    // Implementation
}
public class C : B
{
    // Implementation
}
```
```

# Polymorphism

Polymorphism refers to the technique where multiple functionality is performed through a single operation. Static polymorphism is performed at compile time whereas the dynamic polymorphism is decided at the run time. In static polymorphism, C# allows programmers to implement the following two approaches:

# Function Overloading

Function overloading provides multiple definitions for the same function name in the given scope. Moreover, function definition should differ from each other by types so that you do not overload function declarations that have a different return type.

# Constructors

In C# programming, a constructor is automatically called whenever a struct or class is created. As a class can have multiple constructors to handle different arguments, constructors allow the programmers to set limit instantiation and default values as well.

Syntax for creating constructors:

```
```csharp
public class Person
{
    private string last;
    private string first;

        public Person(string lastName, string firstName)
```
```