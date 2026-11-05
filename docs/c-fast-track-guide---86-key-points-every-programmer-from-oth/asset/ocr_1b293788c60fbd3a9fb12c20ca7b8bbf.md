# 29. CONSTRAINING GENERICS WITH WHERE

C# allows you to add constraints to generics using the where clause. This ensures that the generic type parameter meets specific requirements like being a class, having a default constructor, or implementing a specific interface.

The following code shows how to use the where clause to restrict a generic method so that it only accepts types that implement a specific interface.

# [Code Example]

```
```csharp
using System;

// Define an interface
interface IPrintable {
    void Print();
}

// A class that implements IPrintable
class Report : IPrintable {
    public void Print() {
        Console.WriteLine("Printing report...");
    }
}

// Generic class with a constraint
class Printer<T> where T : IPrintable {
    public void PrintItem(T item) {
        item.Print(); // Safe to call Print() because T is guaranteed to implement IPrintable
    }
}

class Program {
    static void Main() {
```
```