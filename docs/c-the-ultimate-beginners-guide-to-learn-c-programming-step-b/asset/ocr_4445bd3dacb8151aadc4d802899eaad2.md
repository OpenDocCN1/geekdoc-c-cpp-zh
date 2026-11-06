# # Chapter 15: Polymorphism

Polymorphism[37] is a term that means taking many forms. In programming, it is expressed as **“one interface, many functions”**. Polymorphism can take two forms, static or dynamic.

For the case of static dynamism, response to the function is determined during compile time. In dynamic polymorphism, response to the function is determined during runtime.

# ## Static Polymorphism

As stated above, the response to a function in this type of polymorphism is determined during compile time. The process of linking a function to an object during compile time is known as *early binding*. It is also known as *static binding*. In C#, static polymorphism can be implemented in two ways:

+   - Function overloading
+   - Operator overloading

# ## Function Overloading

It is possible for us to have multiple definitions for the same function name within one scope. The differences between these functions are implemented by types or the number of arguments that the functions take. Function declarations cannot be overloaded by differing the return types only.

**The following example demonstrates how to overload a function in C#:**

```
```csharp
using System;

namespace PolymorphismApp {
    class DisplayData {
        void display(int x) {
            Console.WriteLine("Printing an int value: {0}", x );
        }

        void display(double y) {
```
```