# Static and Dynamic Binding

In most traditional programming languages the compiler calls fixed function identifiers based on the source code. The linker then takes these identifiers and replaces them with a physical address.

This is called early or static binding because function identifiers are associated with physical addresses before runtime during the process of compilation and linkage. The problem with early binding is that the programmer must predict what objects will be used in all function calls in every situation. This is not only limiting, but its sometimes impossible.

The best thing about early binding is that it is fast. The only runtime overhead incurred is:

+   * passing arguments
+   * performing a function call
+   * and cleaning up the stack

In C++, a polymorphic function can become associated with one of many possible functions only when an actual object is passed to the polymorphic function. In other words, the source code itself doesn't always tell you how a section of code is going to execute. A function call is only indicated in the source code without specifying the exact function to call. This is called late or dynamic binding.

The problem with late binding is its runtime efficiency. The code itself must deduce at runtime which function to invoke, and then invoke it. Some languages such as Smalltalk use late binding exclusively, which results in a powerful language but one that suffers from certain speed penalties. On the other hand, ANSI C uses early binding exclusively, resulting in high speed but a lack of flexibility.