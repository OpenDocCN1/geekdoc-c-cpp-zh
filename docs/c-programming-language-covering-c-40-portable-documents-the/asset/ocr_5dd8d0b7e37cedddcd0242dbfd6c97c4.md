Since a destructor is required to have no parameters, it cannot be overloaded, so a class can have, at most, one destructor.

Destructors are invoked automatically, and cannot be invoked explicitly. An instance becomes eligible for destruction when it is no longer possible for any code to use that instance. Execution of the destructor for the instance may occur at any time after the instance becomes eligible for destruction. When an instance is destructed, the destructors in that instance's inheritance chain are called, in order, from most derived to least derived. A destructor may be executed on any thread. For further discussion of the rules that govern when and how a destructor is executed, see §3.9.

> ERIC LIPPERT Clearly, code running in a destructor is running in a potentially very different environment than code anywhere else in your program. It is a really bad idea to do anything complicated, dangerous, side-effecting, or lengthy. In particular, the following code, which produces a complicated side effect of writing to the console is for pedagogic purposes, is not an example of what you should do in a real destructor.

# The example

```
using System;
class A
{
    ~A()
    {
        Console.WriteLine("A's destructor");
    }
}
class B : A
{
    ~B()
    {
        Console.WriteLine("B's destructor");
    }
}
class Test
{
    static void Main()
    {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```