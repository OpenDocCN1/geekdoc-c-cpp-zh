to C# 4.0, it will not change its behavior implicitly. The compiler will make the same strong type and operation checks as before.

# The dynamic Type

The key to dynamic binding is a new static type introduced in C# 4 called dynamic. (That sounds funny — a static type that is dynamic — doesn't it?) When you have an object of type dynamic, you can ask it to do whatever you want. The compiler will only check a few things by syntax and basic semantics, and let the runtime resolve the operations. Here is a two-line sample:

```
dynamic dyn = GetDynamicObject(...);
dyn.DoingSomething("C# 4.0 Rocks!", 42);
```

Assume the GetDynamicObject retrieves an object of type dynamic. It is stored in dyn. The compiler analyzes the second line during compilation and creates code that can be described like this:

> "Ask the runtime to call an operation named DoSomething with a string as its first argument, and an int as its second. When the runtime recognizes this operation, it will call 'C# 4.0 Rocks!' and 42 as the actual parameters of the DoSomething."

At runtime, the actual object that dyn will be examined to determine what it means to "call DoSomething with a string and an int," and if the dyn object knows how to handle the call, it executes it with the actual parameters passed to it.

The dynamic type can be thought of as a special version of the System.Object type, which signals that the object can be used dynamically.

It is easy to opt in or out of dynamic behavior — any object can be implicitly converted to dynamic, "suspending belief" until run-time. Listing 24-3 illustrates this with the dynamic behavior of "Hello, world."

+   LISTING 24-3: Program.cs file of HelloWorldDynamic

![](bbox=[0.093, 0.656, 0.143, 0.693])

```
using System;

namespace HelloWorldDynamic
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic dyn = Console.Out;
            dyn.WriteLine("Hello, (0) from dynamic console, "world!");
        }
    }
}
```