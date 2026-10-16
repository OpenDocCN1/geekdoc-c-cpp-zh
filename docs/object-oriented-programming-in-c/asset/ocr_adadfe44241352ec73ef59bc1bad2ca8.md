modifications and improvements were driven by the requirements of the object-oriented concept of C++. Some of these were introduced to make the C++ program more reliable and readable. All the features of C++ functions are discussed in Chapter 4.

# Pointers

Pointers are declared and initialized as in C. Examples:

```
int *ip;        // int pointer
ip = &x;        // address of x assigned to ip
*ip = 10;       // 10 assigned to x through indirection
```

C++ adds the concept of constant pointer and pointer to a constant.

```
char * const ptr1 = "GOOD";   // constant pointer
```

We cannot modify the address that ptr1 is initialized to.

```
int const * ptr2 = &m;  // pointer to a constant
```

ptr2 is declared as pointer to a constant. It can point to any variable of correct type, but the contents of what it points to cannot be changed.

We can also declare both the pointer and the variable as constants in the following way:

```
const char * const cp = "xyz";
```

This statement declares cp as a constant pointer to the string which has been declared a constant. In this case, neither the address assigned to the pointer cp nor the contents it points to can be changed.

Pointers are extensively used in C++ for memory management and achieving polymorphism.

# 3.8 Symbolic Constants

There are two ways of creating symbolic constants in C++:

+   - Using the qualifier const, and
+   - Defining a set of integer constants using enum keyword.

In both C and C++, any value declared as const cannot be modified by the program in any way. However, there are some differences in implementation. In C++, we can use const in a