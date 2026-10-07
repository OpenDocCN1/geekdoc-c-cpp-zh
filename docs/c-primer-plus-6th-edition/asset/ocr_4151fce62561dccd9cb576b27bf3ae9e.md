Static and Dynamic Binding

# The Need for Virtual Destructors

The code in Listing 13.10 uses delete to free the objects allocated by new illustrates why the base class should have a virtual destructor, even if no destructor appears to be needed. If the destructors are not virtual, then just the destructor corresponding to the pointer type is called. In Listing 13.10, this means that the Brass destructor would be called, even if the pointer to a BrassPlus object. If the destructors are virtual, the destructor corresponding to the object type is called. So if a pointer points to a BrassPlus object, the BrassPlus destructor is called. And when a BrassPlus destructor finishes, it automatically calls the base-class constructor. Thus, using virtual destructors ensures the correct sequence of destructors is called. In Listing 13.10, this behavior isn't essential because the destructors do nothing. But if, say, BrassPlus had a do-something destructor, it would be vital for Brass to have a virtual destructor, even if it did nothing.

# Static and Dynamic Binding

Which block of executable code gets used when a program calls a function? The compiler has the responsibility of answering this question. Interpreting a function call in the source as executing a particular block of function code is termed binding the function name. With C, the task is simple because each function name corresponds to a distinct function. With C++, the task is more complex because of function overloading. The compiler has to look at the function arguments to figure out which function to use. Nevertheless, this kind of binding is a C or C++ compiler could perform during the compilation process; binding takes place during compilation is static binding (or early binding). However, virtual functions make the job more difficult. As shown in Listing 13.10, the decision of which function to use can't be made at compile time because the compiler doesn't know which kind of object the user is going to choose to. Therefore, the compiler has to generate code that allows the correct virtual method to be selected as the program runs; this is dynamic binding (or late binding).

Now that you've seen virtual methods at work, let's look at this process in greater depth, beginning with how C++ handles pointer and reference type compatibility.

# Pointer and Reference Type Compatibility

Dynamic binding in C++ is associated with methods invoked by pointers and references, and this is governed, in part, by the inheritance process. One public inheritance mode of the is-a relationship is how it handles pointers and references to objects. Normally, C++ does not allow you to assign one type to a pointer of another type. Does not let a refer to one type refer to another type:

```
double x = 2.5;
int *pi = &x; // invalid assignment, mismatched pointer type
long *rl = x; // invalid assignment, mismatched reference type
```