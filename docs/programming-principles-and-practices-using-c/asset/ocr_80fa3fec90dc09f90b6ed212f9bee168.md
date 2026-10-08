```
```python
cout << "\n';
```
}
```

So, **dim1()** is the number of elements in the first dimension, **dim2()** the number of elements in the second dimension, and so on. The type of the elements and the number of dimensions are part of the **Matrix** type, so we cannot write a function that takes any **Matrix** as an argument (but we could write a template to do that):

```
```cpp
void init(Matrix& a);  // error: element type and number of dimensions missing
```
```

Note that the **Matrix** library doesn’t supply matrix operations, such as adding two 4D **Matrices** or multiplying a 2D **Matrix** with a 1D **Matrix**. Doing so elegantly and efficiently is currently beyond the scope of this library. Matrix libraries of a variety of designs could be built on top of the **Matrix** library (see exercise 12).

# ### 24.5.2 1D **Matrix**

What can we do to the simplest **Matrix**, the 1D (one-dimensional) **Matrix**?

We can leave the number of dimensions out of a declaration because 1D is the default:

```
```cpp
Matrix<int,1> a1(8);  // a1 is a 1D Matrix of ints
Matrix<int> a(8);     // means Matrix<int,1> a(8);
```
```

So, **a** and **a1** are of the same type (**Matrix**<**int,1**>). We can ask for the size (the number of elements) and the dimension (the number of elements in a dimension). For a 1D **Matrix**, those are the same.

```
```cpp
a.size();            // number of elements in Matrix
a.dim1();            // number of elements in 1st dimension
```
```

We can ask for the elements as laid out in memory, that is, a pointer to the first element:

```
```cpp
int* p = a.data();   // extract data as a pointer to an array
```
```

This is useful for passing **Matrix** data to C-style functions taking pointer arguments. We can subscript:

```
```cpp
a(i);    // ith element (Fortran style), but range checked
a[i];    // ith element (C style), range checked
a(1,2);  // error: a is a 1D Matrix
```
```