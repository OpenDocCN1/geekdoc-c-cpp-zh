# # 1.8 Arrays, Pointers, and References

# ## 1.8.1 Arrays

The intrinsic array support of C++ has certain limitations and some strange behaviors. Nonetheless, we feel that every C++ programmer should know it and be aware of its problems.

An array is declared as follows:

```
```cpp
int x[10];
```
```

The variable x is an array with 10 int entries. In standard C++, the size of the array must be constant and known at compile time. Some compilers (e.g., gcc) support run-time sizes.

Arrays are accessed by square brackets: x[i] is a reference to the i-th element of x. The first element is x[0]; the last one is x[9]. Arrays can be initialized at the definition:

```
```cpp
float v[] = {1.0, 2.0, 3.0}, w[] = {7.0, 8.0, 9.0};
```
```

In this case, the array size is deduced.

The list initialization in C++11 cannot be narrowed any further. This will rarely make a difference in practice. For instance, the following:

C++11

```
```cpp
int v[] = {1.0, 2.0, 3.0}; // Error in C++11: narrowing
```
```

was legal in C++03 but not in C++11 since the conversion from a floating-point literal to int potentially loses precision. However, we would not write such ugly code anyway.

Operations on arrays are typically performed in loops; e.g., to compute x = v - 3w as a vector operation is realized by

```
```cpp
float x[3];
for (int i = 0; i < 3; ++i)
    x[i] = v[i] - 3.0 * w[i];
```
```

We can also define arrays of higher dimensions:

```
```cpp
float A[7][9]; // a 7 by 9 matrix
int q[3][2][3]; // a 3 by 2 by 3 array
```
```

The language does not provide linear algebra operations upon the arrays. Implementations based on arrays are inelegant and error-prone. For instance, a function for a vector addition would look like this:

```
```cpp
void vector_add(unsigned size, const double v1[], const double v2[],
                double s[])
{
    for (unsigned i = 0; i < size; ++i)
        s[i] = v1[i] + v2[i];
}
```
```