object can be destroyed and its memory made available for reuse only when all the references to it have disappeared.

> **Important**
You can never destroy an object yourself by using C# code. There just isn't any syntax to do it. Instead, the .NET runtime does it for you at a time of its own choosing.

Managing the lifetime of an object is complex, which is why the designers of C# decided to prevent your code from taking on this responsibility. If it were your responsibility to destroy objects, sooner or later of the following situations would arise:

+   - You'd forget to destroy the object. This would mean that the object's finalizer (if it had) would not run, tidying up not occur, and memory would not be returned to the heap. You could easily run out of memory.

+   - You'd try to destroy an active object to which one or more variables hold reference—known as a dangling reference. A dangling reference refers to unused memory or to a completely different object that now occupies the same piece of memory. Either way, the outcome of using a dangling reference would be undefined at best and a security risk at worst. All bets would be off.

+   - You'd try to destroy the same object more than once. This might or might not be disastrous, depending on the code in the finalizer.

These problems are unacceptable in a language like C#, which places robustness and security high on its list of design goals. The garbage collector destroys objects for you. The garbage collector makes the following guarantees:

+   - Every object will be destroyed. When a program ends, all outstanding objects will be destroyed. However, any finalizers that haven't been run by the program finishes might not run at all.

+   - Every object will be destroyed at most once.

+   - Every object will be destroyed only when it becomes unreachable—that is, when there are no references to the object in the process running your application.