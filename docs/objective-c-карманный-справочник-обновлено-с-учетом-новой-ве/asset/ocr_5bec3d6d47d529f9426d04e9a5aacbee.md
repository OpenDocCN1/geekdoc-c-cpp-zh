# Understanding the Object Model

isolated parts of a program that pass messages between each other. Typically, these messages are delivered synchronously, so they behave a bit like a function call, but it's important to realize that they are different.

Messages are a higher level of abstraction than function calls. A function call is very simple. On many more RISC-like architectures, you push the return address onto the stack and then jump. In all cases, the destination address is fixed.

When you send a message, it is entirely up to the receiver how to handle it. The most typical way is to invoke the method with the same name as the message, but there are other alternatives. Proxy objects may forward the message to another object, and they may perform some substitution on the message arguments before they do.

Simula did not use the term “object orientation,” but a lot of Simula-like languages that postdate Smalltalk have adopted the term, leading to some confusion. Languages in this family, such as C++, use virtual function tables (vtables) to implement something that is superficially similar.

A Simula-style object contains a pointer to its vtable, or vtables if it has superclasses. When you call a virtual function, the compiler creates an offset into the vtable and then a call to the function at this offset.

One of the side effects of this difference is