```
float v[]= {1.0, 2.0, 3.0}, w[]= {7.0, 8.0, 9.0};
```

In this case, the array size is deduced.

[C++11] The list initialization in C++11 forbids the narrowing of the values. This will rarely make a difference in practice. For instance, the following:

Click here to view code image

```
int v []= {1.0, 2.0, 3.0}; // Error in C++11: narrowing
```

was legal in C++03 but not in C++11 since the conversion from a floating-point literal to int potentially loses precision. However, we would not write such ugly code anyway.

Operations on arrays are typically performed in loops; e.g., to compute x = v - 3w as a vector operation is realized by

Click here to view code image

```
float x[3];
for (int i= 0; i < 3; ++i)
    x[i]= v[i] - 3.0 * w[i];
```

We can also define arrays of higher dimensions:

Click here to view code image

```
float A[7][9]; // a 7 by 9 matrix
int q[3][2][3]; // a 3 by 2 by 3 array
```

The language does not provide linear algebra operations upon the arrays. Implementations based on arrays are inelegant and error prone. For instance, a function for a vector addition would look like this:

Click here to view code image

```
void vector_add(unsigned size, const double v1[], const
double v2[],
    double s[])
{
    for (unsigned i= 0; i < size; ++i)
        s[i]= v1[i] + v2[i];
}
```

Note that we passed the size of the arrays as the first function parameter whereas array parameters don't contain size information.17 In this case, the