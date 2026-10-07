# CHAPTER 2

Cocoa Objects

```
return O;
```

This code creates and uses several objects: an autorelease pool for memory management, collection objects (arrays and a set) for 'uniquing' and sorting the specified words, and an enumerator object for iterating the elements in the final array and printing them to standard output.

The first thing you probably notice about this code is that it is short, perhaps shorter than a typical ANSI C version of the same program. Much of this code might look strange to you, many of its elements are elementary ANSI C. These include assignment operators, control-flow statements (while), calls to C-library routines, and primitive scalar types. Objective-C obviously has ANSI underpinnings.

The rest of this chapter explores the Objective-elements of this code, using them as examples in discussions on subjects ranging from the mechanics of message-sending to the techniques of memory management. If you haven't seen Objective-C before, the code in the example might seem convoluted and obscure, but that impression will soon melt away. Objective-C is actually a simple, elegant programming language that is easy to learn and intuitive to program.

# Object-Oriented Programming with Objective-C

Cocoa is pervasively object-oriented, from its paradigms and mechanisms to its event-driven architecture. Objective-C, the development language for Cocoa, is thoroughly object-oriented, despite its grounding in ANSI C. It provides runtime support for message dispatch and specifies syntactic conventions for defining new classes. Objective-C supports most of the abstractions and methods found in other object-oriented languages like C++ and Java. These include inheritance, encapsulation, reusability, and polymorphism.

But Objective-C is different from these other object-oriented languages, often in many ways. For example, Objective-C, unlike C++, does not allow overloading, templates, or multiple inheritance.

Although Objective-C doesn't have these features, its strengths as an object-oriented programming language more than compensate. What follows is an exploration of the special capabilities of Objective-C.

> Further Reading: Much of this summarizes information from the definitive guide to Objective-C, The Objective-C Programming Language. Consult this document for a detailed and comprehensive description of Objective-C.

# The Objective-C Advantage

If you're a procedural programmer new to object-oriented concepts, it might help at first to think of an object as essentially a structure with functions associated with it. This notion is not too far off the reality, particularly in terms of runtime implementation.

Every Objective-C object hides a data structure first member—or instance variable—the isa pointer. (Remaining members are defined by the object's class and superclasses). The isa pointer, as the name suggests, points to the object's class, which is an object in its own right (see Figure 2-1) and is compiled from the class definition. The class object maintains a dispatch table consisting of pointers to the methods it implements; it also holds a pointer to its superclass, which has its own dispatch table and super