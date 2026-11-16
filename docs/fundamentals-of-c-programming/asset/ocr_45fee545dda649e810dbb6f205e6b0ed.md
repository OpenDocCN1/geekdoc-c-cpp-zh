On one system the program prints

```
Creating widget 5
Entering main
Creating widget 10
10
5
Destroying widget 10
Destroying widget 5
```

Observe that on this particular system the program does not run to completion, as it does not print Leaving main. The program crashes after attempting to free up the global memory that was not dynamically allocated on the heap. One some systems during some executions the program will run to completion with no apparent problem, but this is because this program is very simple and does very little after the erroneous deletion. Regardless of how the program behaves, it involves code identified as undefined behavior and, therefore, contains a bug that must be addressed.

While we can see the implementations of get_widget1 and get_widget2 in the source code for Listing 18.1 (howdelete.cpp), the problem would be more challenging if these functions were part of a precompiled library for which we do not have the source code. It is important to read the library documentation for functions that return pointers to know how callers are expected to manage the memory to which those pointers refer.

# 18.3 Linked Lists

An object in C++ can hold just about any type of data, but there are some limitations. Consider the following struct definition:

struct definition:

```
struct Node {
    int data;
    Node next; // Error, illegal self reference
};
```

(Here we use a struct instead of a class since we will consider a Node object a primitive data type that requires no special protection from clients.) How much space should the compiler set aside for a Node object? A Node contains an integer and a Node, but this contained Node field itself would contain an integer and a Node, and the nested containment would go on forever. Such a structure understandably is illegal in C++, and the compiler will issue an error. You are not allowed to have a class or struct field of the same type within the class or struct being defined.

Another object definition looks similar, but it is a legal structure:

```
struct Node {
    int data;
    Node *next; // Self reference via pointer is legal
};
```

The reason this second version is legal is because the compiler now can compute the size of a Node object. A pointer is simply a memory address under the hood, so all pointer variables are the same size regardless of their declared type. The pointer solves the infinitely nested containment problem.

This ability of a object to refer to an object like itself is not merely an interesting curiosity; it has practical applications. Suppose we wish to implement a sequence structure like a vector. We can use