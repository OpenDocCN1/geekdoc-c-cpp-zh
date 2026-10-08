Figure 10-1 shows how strongly typed and dynamic languages can use the DLR.

| Statically-typed languages | | Dynamically-typed languages |
|---|---|---||
| C# | VB | Others | Python | Ruby | Others |
| | | | Dynamic Language Runtime |
| Common Language Runtime | |

**FIGURE 10-1:** Utilizing the DLR

Strongly typed languages (such as Visual Basic and C#) use the CL directly to execute applications. Dynamically typed languages (such as Python and Ruby) cannot easily run directly on top of the CL, because the CL provides this missing layer for dynamically typed languages, and also helps statically typed access objects and services developed in a dynamic way.

Following are the fundamental services of the DLR (of course, there are others):

+   - **Call sites** — These provide a caching mechanism for operation in dynamic code. Every time you execute an operation with MyOp(A, B), the DLR would have to analyze what MyOp means with A and B as operations. For example, when MyOp is A as a floating-point number, and B is an integer, MyOp(B) results in a floating-point number representing A+B. With caching, this performance penalty can be significantly reduced.
- **Expression trees** — These are the extensions of expression trees introduced in .NET 3.5 with LINQ providers. They are key players in the lowering of the bar for posting (dynamic) languages to .NET, and are absolutely one of the core pillars of the DLR. Expression trees are compiled (the DLR ships this compiler as part of its services), and the result is a delegate invoking the code represented by the tree.
- **Dynamic object interoperability** — As a core principle of dynamic operations, objects receive messages describing operations with their actual parameters. Dynamic object interoperability is about providing service types to create that can translate these messages to explicit operations.

Depending on the physical type of the object to be accessed dynamically, separate communication models can be used. For example, to access CLR-hosted objects, some mechanism built over .NET reflection can be used. For COM objects, the standard IDispatch-based mechanism can be