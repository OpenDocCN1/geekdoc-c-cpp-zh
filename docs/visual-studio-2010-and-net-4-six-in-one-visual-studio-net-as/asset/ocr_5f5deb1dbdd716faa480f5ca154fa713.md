# DYNAMIC LOOKUP

C# developers are familiar with the fact that types and operations are strictly checked during the compilation process. The compiler generates Microsoft Intermediate Language (MSIL) code that explicitly carries out those operations by invoking methods. The good side of this approach is the thorough checks that increase operation safety; the bad side is its rigidity.

There is no other galaxy in the universe of programming languages: dynamic languages. The compiler makes a few checks over types and their operations; the majority of them are postponed to the execution of the corresponding operation at run-time.

In addition to the dynamic languages, there are script languages and object models (for example, COM objects from the Microsoft Office functionality, the DTE object in Visual Studio, the HTML DOM in Internet Explorer, and so on) that also check operations at run-time.

In this complex world, these tools and languages should operate so that they could boost developer performance. Scripting tools and languages like JavaScript, PowerShell, and many others, as well as dynamic languages such as Python or Ruby, are very popular today. They provide a unified approach to objects, and operate independently of where they are coming from, and how they are working behind the scenes. These tools focus on the most important thing: providing the simplest and most intuitive way to use the object's exploited functionality.

For a long time, C# could not compete with the flexibility of these languages and tools. But that is no longer the case.

# Dynamic Binding

The new version of C# provides dynamic binding as a unified approach to selecting and carrying out operations dynamically. Operations can be performed upon various units of objects of whether a specific object comes from COM (through interoperability), IronRuby, IronPython, the HTML DOM, or from any other dynamic context. The run-time takes this responsibility away from developers, and it will determine what a given operation means for a particular object.

This approach can simplify your code using the Main methods in Listing 24-1 and Listing 24-2), and adds you flexibility. However, the compiler assumes dynamic objects support any operation, and this behavior has two drawbacks:

+   - It will occur only at run-time if a specific object does not support a certain operation, and you will get it an error. Contrast this to static typing, where the compiler gives an error message.

+   - Run-time checks incur a kind of performance penalty.

In many cases, these drawbacks do not come with any loss, because the objects providing the operations would not have a static type anyway. Of course, there are cases where tradeoff should be made between safety and brevity. If brevity is important, safety can be strengthened by appropriate software development procedures (by using unit testing and code review).

Dynamic binding is implemented in C# 4.0 as an explicit mechanism where you can opt in or out whether you want to utilize this behavior. However, when you port your code and running C# 3.0 code