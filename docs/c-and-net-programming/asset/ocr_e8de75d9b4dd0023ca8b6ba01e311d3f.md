# 5. Order of Finalizers(or destructors) in inheritance hierarchy

Destructor execution follows the opposite approach as that of constructor execution order; the derived class destructor is called first then the base class. Destructor implicitly calls Finalize on the base class of object.

# Example

```
```csharp
using System;

public class Base
{
    ~Base()
    {
        Console.WriteLine("Base destructor called");
    }
}

public class Derived : Base
{
    ~Derived()
    {
        Console.WriteLine("Derived destructor called");
    }
}

public class MainClass
{
    static void Main()
    {
        Derived derived = new Derived();
    }
}

Input
Nil
```
```

# Output

```
```text
Derived destructor called
Base destructor called
```
```

# 9.1.7 What is not being Inherited ?

**Sealed and abstract classes are never inherited.**

**Constructor and destructor are never inherited.**