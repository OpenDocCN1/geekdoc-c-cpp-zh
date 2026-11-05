> **BRAD ABRAMS** It is interesting to note that Console.WriteLine() is simply a shortcut for Console.Out.WriteLine. Console.Out is a property that returns an implementation of the System.IO.TextWriter base class designed to output to the console. The preceding example could be written equally correctly as follows:
> 
> ```csharp
> using System;
> class Hello
> {
>     static void Main() {
>         Console.Out.WriteLine("Hello, World");
>     }
> }
> ```
> 
> Early in the design of the framework, we kept a careful eye on exactly how this section of the C# language specification would have to be written as a bellwether of the complexity of the language. We opted to add the convenience overload on Console to make “Hello, World” that much easier to write. By all accounts, it seems to have paid off. In fact, today you find almost no calls to Console.Out.WriteLine().

# 1.2 Program Structure

The key organizational concepts in C# are *programs*, *namespaces*, *types*, *members*, and *assemblies*. C# programs consist of one or more source files. Programs declare types, which contain members and can be organized into namespaces. Classes and interfaces are examples of types. Fields, methods, properties, and events are examples of members. When C# programs are compiled, they are physically packaged into assemblies. Assemblies typically have the file extension *.exe* or *.dll*, depending on whether they implement *applications* or *libraries*.

The example

```
```csharp
using System;

namespace Acme.Collections
{
    public class Stack
    {
        Entry top;

        public void Push(object data) {
            top = new Entry(top, data);
        }

        public object Pop() {
            if (top == null) throw new InvalidOperationException();
            object result = top.data;

```