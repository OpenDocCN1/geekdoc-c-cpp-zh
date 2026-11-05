# Chapter 45: Partial class and methods

Partial classes provides us an option to split classes into multiple parts and in multiple source files. All parts are combined into one single class during compile time. All parts should contain the keyword partial,should be of the same accessibility. All parts should be present in the same assembly for it to be included during compile time.

# Section 45.1: Partial classes

Partial classes provide an ability to split class declaration (usually into separate files). A common problem that can be solved with partial classes is allowing users to modify auto-generated code without fearing that their changes will be overwritten if the code is regenerated. Also multiple developers can work on same class or methods.

```
```csharp
using System;

namespace PartialClassAndMethods
{
    public partial class PartialClass
    {
        public void ExampleMethod() {
            Console.WriteLine("Method call from the first declaration.");
        }
    }

    public partial class PartialClass
    {
        public void AnotherExampleMethod()
        {
            Console.WriteLine("Method call from the second declaration.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            PartialClass partial = new PartialClass();
            partial.ExampleMethod(); // outputs "Method call from the first declaration."
            partial.AnotherExampleMethod(); // outputs "Method call from the second declaration."
        }
    }
}
```
```

# Section 45.2: Partial classes inheriting from a base class

When inheriting from any base class, only one partial class needs to have the base class specified.

```
```csharp
// PartialClass1.cs
public partial class PartialClass : BaseClass {}
// PartialClass2.cs
public partial class PartialClass {}
```
```

You can specify the same base class in more than one partial class. It will get flagged as redundant by some IDE tools, but it does compile correctly.

```
```csharp
// PartialClass1.cs
public partial class PartialClass : BaseClass {}
```
```