programming. Consequently, C does not have vectors available to represent sequence types. The C language uses a more primitive construct called an array. True to its C roots, C++ supports arrays as well as vectors. Some C++ libraries use arrays instead of vectors. In addition, C++ programs can use any of the large number of C libraries that have been built up over the past 40+ years, and many of these libraries process arrays. While a more modern construct like `std::vector` may be better suited for may of the roles an array has played in the past, it nonetheless is important for C++ programmers to be familiar with arrays.

An array is a variable that refers to a block of memory that, like a vector, can hold multiple values simultaneously. An array has a name, and the values it contains are accessed via their position within the block of memory designated for the array. Also like a vector, the elements within an array must all be of the same type. Arrays may be local or global variables. Arrays are built into the core language of both C and C++. This means you do not need to add any `#include` directives to use an array within a program.

# 11.2.1 Static Arrays

Arrays come in two varieties, static and dynamic. A programmer must supply the size of a static array when declaring it; for example, the following statement:

```
```cpp
// list is an array of 25 integers
int list[25];
```
```

declares `list` to be an array of 25 integers. The value within the square brackets specifies the number of elements in the array, and the size is fixed for the life of the array. The value within the square brackets must be a constant value determined at compile time. It can be a literal value or a symbolic constant, but it cannot be a variable. This is in contrast to vector declarations in which the initial vector size may be specified by a variable with a value determined at run time:

```
```cpp
int x;
std::cin >> x;          // Get x's value from the user at run time
int list1[x];           // Illegal for a static array
std::vector<int> list2(x); // OK for a vector
```
```

It is possible to declare an array and initialize it with a sequence of elements, with a syntax similar to that of vectors:

```
```cpp
double collection[] = { 1.0, 3.5, 0.5, 7.2 };
```
```

The compiler can count the elements in the initializer list, so you need not supply a number within the square brackets. If you provide a number within the square brackets, it should be at least as large as the number of elements in the initialization list. The equals symbol is required for array initialization. You optionally can use the equals symbol as shown here when initializing vectors, but it is not required for vectors.

If the declaration omits an initializer list, as in:

```
```cpp
int arr[100];
```
```

the initial values of the elements of the array depend on the context of the declaration:

+   - An executing program does not initialize the contents of a local arrays.
+   - The run-time environment initializes the values of global numeric arrays to all zeros.

As with vectors, once we declare an array, we can access its elements using the square bracket operator: