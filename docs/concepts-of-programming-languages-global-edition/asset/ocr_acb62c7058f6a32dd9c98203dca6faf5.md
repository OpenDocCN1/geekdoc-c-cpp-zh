In C and C++, all arrays use zero as the lower bound of their subscript ranges, and array names without subscripts always refer to the address of the first element. Consider the following declarations:

```
int list [10];
int *ptr;
```

Now consider the assignment

```
ptr = list;
```

This assigns the address of list[0] to ptr. Given this assignment, the following are true:

+   - *(ptr + 1) is equivalent to list[1].
+   - *(ptr + index) is equivalent to list[index].
+   - ptr[index] is equivalent to list[index].

It is clear from these statements that the pointer operations include the same scaling that is used in indexing operations. Furthermore, pointers to arrays can be indexed as if they were array names.

Pointers in C and C++ can point to functions. This feature is used to pass functions as parameters to other functions. Pointers are also used for parameter passing, as discussed in Chapter 9.

C and C++ include pointers of type void *, which can point at values of any type. In effect they are generic pointers. However, type checking is not a problem with void * pointers, because these languages disallow dereferencing them. One common use of void * pointers is as the types of parameters of functions that operate on memory. For example, suppose we wanted a function to move a sequence of bytes of data from one place in memory to another. It would be most general if it could be passed two pointers of any type. This would be legal if the corresponding formal parameters in the function were void * type. The function could then convert them to char * type and do the operation, regardless of what type pointers were sent as actual parameters.

# 6.11.5 Reference Types

A reference type variable is similar to a pointer, with one important and fundamental difference: A pointer refers to an address in memory, while a reference refers to an object or a value in memory. As a result, although it is natural to perform arithmetic on addresses, it is not sensible to do arithmetic on references.

C++ includes a special kind of reference type that is used primarily for the formal parameters in function definitions. A C++ reference type variable is a constant pointer that is always implicitly dereferenced. Because a C++ reference type variable is a constant, it must be initialized with the address of some