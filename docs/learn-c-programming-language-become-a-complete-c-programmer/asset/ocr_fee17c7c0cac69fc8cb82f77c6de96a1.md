The C++ built-in array is an inherently low-level facility that should primarily be used inside the implementation of higher-level, better-behaved, data structures, such as the standard-library vector or array. There is no array assignment, and the name of an array implicitly converts to a pointer to its first element at the slightest provocation (§7.4). In particular, avoid arrays in interfaces (e.g., as function arguments; §7.4.3, §12.2.2) because the implicit conversion to pointer is the root cause of many common errors in C code and C-style C++ code. If you allocate an array on the free store, be sure to delete[] its pointer once only and only after its last use (§11.2.2). That’s most easily and most reliably done by having the lifetime of the free-store array controlled by a resource handle (e.g., string (§19.3, §36.3), vector (§13.6, §34.2), or unique_ptr (§34.3.1)). If you allocate an array statically or on the stack, be sure never to delete[] it. Obviously, C programmers cannot follow these pieces of advice because C lacks the ability to encapsulate arrays, but that doesn’t make the advice bad in the context of C++.

One of the most widely used kinds of arrays is a zero-terminated array of char. That’s the way C stores strings, so a zero-terminated array of char is often called a C-style string. C++ string literals follow that convention (§7.3.2), and some standard-library functions (e.g., strcpy() and strcmp(); §43.4) rely on it. Often, a char* or a const char* is assumed to point to a zero-terminated sequence of characters.

# 7.3.1 Array Initializers

An array can be initialized by a list of values. For example:

```
int v1[] = { 1, 2, 3, 4 };
char v2[] = { ‘a’, ‘b’, ‘c’, 0 };
```

When an array is declared without a specific size, but with an initializer list, the size is calculated by counting the elements of the initializer list. Consequently, v1 and v2 are of type int[4] and char[4], respectively. If a size is explicitly specified, it is an error to give surplus elements in an initializer list. For example:

```
char v3[2] = { ‘a’, ‘b’, 0 }; // error : too many initializers
char v4[3] = { ‘a’, ‘b’, 0 }; // OK
```

If the initializer supplies too few elements for an array, 0 is used for the rest. For example:

```
int v5[8] = { 1, 2, 3, 4 };
```

is equivalent to

```
int v5[] = { 1, 2, 3, 4 , 0, 0, 0, 0 };
```

There is no built-in copy operation for arrays. You cannot initialize one array with another (not even of exactly the same type), and there is no array assignment:

```
int v6[8] = v5; // error :can’t copyanarray(cannot assign an int* to an array)
v6 = v5; // error : no array assignment
```

Similarly, you can’t pass arrays by value. See also §7.4.
When you need assignment to a collection of objects, use a vector (§4.4.1, §13.6, §34.2), an array (§8.2.4), or a valarray (§40.5) instead.
An array of characters can be conveniently initialized by a string literal (§7.3.2).