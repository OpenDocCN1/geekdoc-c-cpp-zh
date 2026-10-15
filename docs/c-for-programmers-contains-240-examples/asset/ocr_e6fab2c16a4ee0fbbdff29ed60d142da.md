If an object has member objects, and if an exception is thrown before the outer object is fully constructed, then destructors will be executed for the member objects that have been constructed prior to the occurrence of the exception. If an array of objects has been partially constructed when an exception occurs, only the destructors for the constructed objects in the array will be called.

An exception could preclude the operation of code that would normally release a resource, thus causing a resource leak. One technique to resolve this problem is to initialize a local object to acquire the resource. When an exception occurs, the destructor for that object will be invoked and can free the resource.

# Error-Prevention Tip 16.4

When an exception is thrown from the constructor for an object that is created in a new expression, the dynamically allocated memory for that object is released.

# 16.10 Exceptions and Inheritance

Various exception classes can be derived from a common base class, as we discussed in Section 16.3, when we created class DivideByZeroException as a derived class of class exception. If a catch handler catches a pointer or reference to an exception object of a base-class type, it also can catch a pointer or reference to all objects of classes publicly derived from that base class—this allows for polymorphic processing of related errors.

# Error-Prevention Tip 16.5

Using inheritance with exceptions enables an exception handler to catch related errors with concise notation. One approach is to catch each type of pointer or reference to a derived-class exception object individually, but a more concise approach is to catch pointers or references to base-class exception objects instead. Also, catching pointers or references to derived-class exception objects individually is error prone, especially if you forget to test explicitly for one or more of the derived-class pointer or reference types.

# 16.11 Processing new Failures

The C++ standard specifies that, when operator new fails, it throws a bad_alloc exception (defined in header file <new>). However, some compilers are not compliant with the C++ standard and therefore use the version of new that returns 0 on failure. For example, the Microsoft Visual C++ 2005 throws a bad_alloc exception when new fails, while the Microsoft Visual C++ 6.0 returns 0 on new failure.

Compilers vary in their support for new-failure handling. Many older C++ compilers return 0 by default when new fails. Some compilers support new throwing an exception if header file <new> (or <new.h>) is included. Other compilers throw bad_alloc by default, regardless of whether header file <new> is included. Consult the compiler documentation to determine the compiler’s support for new-failure handling.

In this section, we present three examples of new failing. The first example returns 0 when new fails. The second example uses the version of new that throws a bad_alloc exception when new fails. The third example uses function set_new_handler to handle new failures. [Note: The examples in Figs. 16.5–16.7 allocate large amounts of dynamic memory, which could cause your computer to become sluggish.]