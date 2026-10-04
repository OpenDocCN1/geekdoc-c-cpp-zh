```
{
    public SubClass()
    {
        Console.WriteLine("Constructing SubClass (default)");
    }
    public SubClass(int i)
    {
        Console.WriteLine("Constructing SubClass (int)");
    }
}
```

Executing this program generates the following result:

```
Invoking SubClass()
Constructing BaseClass (default)
Constructing SubClass (default)

Invoking SubClass(int)
Constructing BaseClass (default)
Constructing SubClass (int)
Press Enter to terminate...
```

The program first creates a default object. As expected, C# invokes the default SubClass constructor, which first passes control to the default BaseClass constructor. The program then creates an object, passing an integer argument. Again as expected, C# invokes the SubClass(int). This constructor invokes the default BaseClass constructor, just as in the earlier example, because it has no data to pass.

# Getting specific with base

A subclass constructor can invoke a specific base class constructor using the keyword base.

![](bbox=[0.11, 0.62, 0.18, 0.7])

This feature is similar to the way that one constructor invokes another within the same class by using the this keyword.

For example, consider this small program, InvokeBaseConstructor:

![](bbox=[0.1, 0.73, 0.18, 0.82])

```
// InvokeBaseConstructor -- Demonstrate how a subclass can
//     invoke the base class constructor of its choice using
//     the base keyword.
using System;
namespace InvokeBaseConstructor
{
    public class BaseClass
    {
        public BaseClass()
        {
            Console.WriteLine("Constructing BaseClass (default)");
        }
        public BaseClass(int i)
        {
            Console.WriteLine("Constructing BaseClass({0})", i);
        }
```