# 25. ABSTRACT CLASSES: SHARED LOGIC WITHOUT INSTANTIATION

Abstract classes in C# cannot be instantiated directly, but they can include common methods and properties that derived classes inherit.

Here’s a short example to demonstrate how an abstract class provides a base for subclasses with shared functionality.

[Code Example]

```
```csharp
using System;

// Abstract class - cannot be instantiated
abstract class Animal
{
    // Concrete method (shared logic)
    public void Breathe()
    {
        Console.WriteLine("Breathing...");
    }
    // Abstract method (must be overridden)
    public abstract void MakeSound();
}

// Derived class implements the abstract method
class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Bark!");
    }
}

class Program
{
```
```