if we use weak pointers because they also need another counter. These features may hinder certain compiler optimisations.

For unique pointers, there is no run-time penalty when compared to raw pointers. Unique pointers are typically used for *factory* objects and object *engines* that create objects in a given scope. When application objects have been constructed, the factory objects are cleaned up by going out of scope. For problems that cannot be directly resolved in C++11 it is possible to resort to the *Boost Smart Pointer* library that has more smart pointer classes than in C++11 (see Demming and Duffy, 2010). We note that shared pointers are not thread-safe. This fact will have major consequences when porting single-threaded code to multithreaded code. There are functions in C++11 to perform *atomic* and *thread-safe* operations on shared pointers that we shall discuss in Chapter 28. In short, you need to determine what smart pointers can and cannot do and what the consequences are when you use them in code. Issues such as performance and maintainability are central. A special project would be to upgrade *legacy code* that uses raw pointers to code that uses smart pointers.

# 2.4 EXTENDED EXAMPLES OF SMART POINTERS USAGE

In the previous sections we gave a discussion of the new pointer classes in C++. The next question to answer is how they represent an improvement on raw pointers. To this end, we discuss how to design user-defined assemblies and aggregations containing embedded pointers and we re-engineer the popular *Factory Method* design pattern (GOF, 1995) that uses raw pointers.

# 2.4.1 Classes with Embedded Pointers

A common occurrence in software development is when we create *composite* and *whole–part* objects consisting of collections whose components are of built-in or user-defined types (a discussion can be found in POSA, 1996). Our interest here is the variant in which the components can be accessed by clients external to the container. This is the *shared parts* variant. They are pointers that have been initialised elsewhere, possibly in dedicated factories. In a sense, this property breaks encapsulation. Some of the issues and attention points when using raw pointers to implement the components are:

+   - Which component(s) are responsible for the lifetime management of the heap-based container components? In GOF (1995), for example, a tactic is that composites are responsible for deleting their children.
+   - A component’s resource may be destroyed by one of its owners, thereby invalidating the component and thus delivering a null pointer.
+   - Implementing code in a composite to explicitly manage component lifetime leads to a class with more than one major responsibility, leading to potential maintenance problems.
+   - The code is not thread-safe (because shared pointers are not thread-safe). Non-deterministic behaviour and *race conditions* are bound to occur when multiple independent threads access shared resources.

Smart pointers in C++ resolve some of these issues. An example of use is (notice that we use the user-defined delete from Section 2.3.1):