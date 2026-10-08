
## CHAPTER 1: The Objective-C Philosophy

exposed to the programmer. Unlike C++, where the details of the vtable are private, Objective-C lets you inspect and modify everything about objects and classes.

With older runtime libraries, Objective-C classes were represented by C structures with a public definition. You could modify them directly, or create new ones and register them with the runtime system. With newer ones, these structures are private and there is a set of public functions for manipulating them as opaque types.

## Understanding the Object Model

Objective-C has a Smalltalk-like object model. If you come from Java, you will find this very easy to understand. If you come from a Simula-family language, such as C++, you may find it a bit more difficult.

Alan Kay described the idea of objects as a simple exercise in reduction. When solving a problem, you want to decompose it into simple parts. The simplest thing that can run a part of a program is the same thing that can run the whole of a program: a computer. Objects, in Alan Kay’s vision, are simple models of computers that communicate by exchanging messages.

This is exactly how objects in Objective-C, and its parent Smalltalk, behave. They are isolated parts of a program that pass messages between each other. Typically, these messages are delivered synchronously, so they behave a bit like a function call, but it's important to realize that they are different.

Messages are a higher level of abstraction than function calls. A function call is very simple. On many more RISC-like architectures, you push the return address onto the stack and then jump. In all cases, the destination address is fixed.

When you send a message, it is entirely up to the receiver how to handle it. The most typical way is to invoke the method with the same name as the message, but there are other alternatives. Proxy objects may forward the message to another object, and they may perform some substitution on the message arguments before they do.

Simula did not use the term “object orientation,” but a lot of Simula-like languages that postdate Smalltalk have adopted the term, leading to some confusion. Languages in this family, such as C++, use virtual function tables (vtables) to implement something that is superficially similar.

A Simula-style object contains a pointer to its vtable, or vtables if it has superclasses. When you call a virtual function, the compiler creates an offset into the vtable and then a call to the function at this offset.

One of the side effects of this difference is that pointer casting in Objective-C and C++ have very different semantics. When you cast a pointer to one object type to another in Objective-C, no code is generated. The cast is just a hint to the compiler’s type checker. In C++, however, a pointer cast performs some pointer arithmetic so that code that is passed the cast pointer can find the vtable at the correct location. This means that you can cast any object type to any other object type in Objective-C, whereas in C++ you need to use a special kind of cast.

This distinction is very important. In Objective-C, the only thing that affects the method lookup is the type of the object. In C++ and other Simula-family languages, the lookup is also affected by what the compiler thinks the type of the object is.

## A Tale of Two Type Systems

One of the things that can confuse people coming to Objective-C is that it has two type systems. This makes sense if you consider the original implementation as a preprocessor. The Objective-C preprocessor would perform StrongTalk-like¹ type checking and then the C compiler would perform C type checking.

> ¹StrongTalk is a dialect of Smalltalk that adds optional static type checking. The team that created the language later went to work on Java. StrongTalk was the fastest Smalltalk implementations, but the compiler did not use static type information for optimization.

C has a structural type system. Type equivalence for primitive types is based on whether two types have the same representation. Complex types are never regarded as equivalent.

Objective-C adds an algebraic type system. The type of an object is defined by its signature: the messages it claims it will respond to. You can implicitly cast an Objective-C object to its superclass, because it is guaranteed to respond to all of the messages that the superclass understands.

You can explicitly cast objects to other types. You could, for example, cast a dictionary object to an array object. As long as you then only send it messages that are understood by both dictionaries and arrays, this will work.

## C Is Objective-C

One of the most important features of Objective-C is that it is a pure superset of C. You can think of C as a domain-specific language embedded in Objective-C for low-level tasks and a subset of Smalltalk as a domain-specific language embedded in Objective-C for high-level tasks.

There is nothing wrong with solving a problem using pure C. One of the mistakes that a lot of people make when learning Objective-C is to assume that they must stop using C. For a lot of things, the C solution is the correct one.

**Note:** Objective-C also has a sister language, Objective-C++, which has the same relationship to C++ that Objective-C has to C. Objective-C++ is a pure superset of C++ and allows you to call C++ code from Objective-C objects, and vice versa. Because they have very different object models, you cannot subclass an Objective-C class with C++, or the converse; however, you can use pointers to Objective-C objects as fields in C++ objects. You can see this in the Cocoa frameworks. Not everything is an object. If you ask for a range of characters in a string, you will use NSRange structure. This is a C structure—not an Objective-C—containing a location and a length. Points, rectangles, and several other things are represented in a similar way. If these were objects, then you would use more memory, make them slower, and not really gain any flexibility.

The Ingalls test² says that you should be able to create a new kind of integer and use this in positioning a window on the screen. Objective-C fails this test, but it's not a very useful example in the real world, because most of the time designing new kinds of integers would break a lot of things that expect integers to have the standard behavior.

> ^2Named after Dan Ingalls, one of the designers of Smalltalk, who proposed it.

In Objective-C, you don't have to use the dynamic behavior, such as late binding and polymorphism, in cases where it isn't.

## The Language and the Library

It's difficult with very dynamic languages to draw the line between the language and the library. In Smalltalk, there is no equivalent of an if statement in the language. The standard library defines True and False singleton classes, which respond to -ifTrue: messages taking a closure as an argument. All complex flow control structures, such as loops or enumeration, are implemented in terms of this.

Objective-C inherits flow control from C, but all of the dynamic behavior is supplied by the runtime library. This is different from C or C++. You can compile a freestanding C or C++ binary that doesn't call any functions in libcstdc++. Every Objective-C program that isn't a pure C program, however, must link against libobjc to work.

This library traditionally provides three classes: a simple root class, a class for constant strings, and a class for protocols. The first of these provides functionality including object allocation that is part of the language in C++, Java, and similar environments. The other two are classes
