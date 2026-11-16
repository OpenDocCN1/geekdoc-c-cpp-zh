We call this a *linear ordering*. In a linear ordering you can begin at the first element and repeatedly visit successor elements until you reach the last element. There never is any ambiguity about which element comes next in a sequence.

The data structures we examine in this chapter, `std::vectors`, primitive arrays, and `std::arrays`, are all sequence types.

# 11.1 Vectors

A vector in C++ is an object that manages a block of memory that can hold multiple values simultaneously; a vector, therefore, represents a collection of values. A vector has a name, and we may access the values it contains via their position within the block of memory managed by the vector. A vector stores a sequence of values, and the values must all be of the same type. A collection of values all of the same type is said to be *homogeneous*.

# 11.1.1 Declaring and Using Vectors

In order to use a vector object within a C++ program, you must add the preprocessor directive

```
#include <vector>
```

The vector type is part of the standard (`std`) namespace, so its full name is `std::vector`, just like the full name of `cout` is `std::cout` (see Section 2.1). If you include the directive

```
using std::vector;
```

in your source file, you can use the shorter name `vector` within your code.

We may declare a vector object that can hold integers as simply as

```
std::vector<int> vec_a;
```

The type within the angle brackets may be any valid C++ data type. When declared this way, the vector `vec_a` initially is empty.

We can declare a vector with a particular initial size as follows:

```
std::vector<int> vec_b(10);
```

Here `vec_b` initially holds 10 integers. All 10 elements are zero by default. Note that the vector's size appears within parentheses following the vector's name.

We may declare a vector object of a given size and specify the initial value of all of its elements:

```
std::vector<int> vec_c(10, 8);
```

In this example `vec_c` initially holds 10 integers, all having the value 8. Note that the first number within the parentheses following the vector's name indicates the number of elements, and the second argument specifies the initial value of all the elements.

We may declare a vector and specify each and every element separately:

```
std::vector<int> vec_d{10, 20, 30, 40, 50};
```