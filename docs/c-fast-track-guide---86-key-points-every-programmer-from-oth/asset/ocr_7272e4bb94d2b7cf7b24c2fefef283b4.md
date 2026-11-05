# ## 31. INSPECT AND USE TYPES AT RUNTIME WITH REFLECTION

Reflection lets you inspect and interact with types (classes, methods, properties, etc.) during runtime in C#.

Here's a simple example of using reflection to inspect a class and invoke a method dynamically.

[Code Example]

```
```csharp
using System;
using System.Reflection;
public class HelloWorld
{
public void SayHello()
{
Console.WriteLine("Hello from reflection!");
}
}
class Program
{
static void Main()
{
// Get the type info of the HelloWorld class
Type type = typeof(HelloWorld);
// Create an instance of HelloWorld dynamically
object instance = Activator.CreateInstance(type);
// Get the method info for SayHello
MethodInfo method = type.GetMethod("SayHello");
// Invoke the SayHello method on the instance
method.Invoke(instance, null);
}
}
```
```