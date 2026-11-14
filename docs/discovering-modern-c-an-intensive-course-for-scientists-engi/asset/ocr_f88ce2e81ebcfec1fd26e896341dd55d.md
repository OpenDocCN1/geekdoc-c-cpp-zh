Here we assume that the `Matrix` class supplies an operator() accepting two arguments for the row and column index and returns a reference to the corresponding entry $a_{ij}$. We further suppose that type traits are defined for value_type and size_type. This is all we need to know about the referred matrix in this mini-example (ideally we would specify a concept for a simple matrix). Real template libraries like MTL4 of course provide larger interfaces. However, this small example is good enough to demonstrate the usage of meta-programming in certain views.

An object of class `transposed_view` can be treated like a regular matrix; e.g., it can be passed to all function templates expecting a matrix. The transposition is achieved on the fly by calling the referred object's operator() with switched indices. For every matrix object, we can define a transposed view that behaves like a matrix:

```
mtl::dense2D<float> A = {{2, 3, 4},
                             {5, 6, 7},
                             {8, 9, 10}};

transposed_view<mtl::dense2D<float>> At(A);
```

When we access `At(i, j)`, we will get `A(j, i)`. We also define a non-const access so that we can even change entries:

```
At(2, 0) = 4.5;
```

This operation sets `A(0, 2)` to 4.5.

The definition of a transposed view object does not lead to particularly concise programs. For convenience, we add a function that returns the transposed view:

```
template <typename Matrix>
inline transposed_view<Matrix> trans(Matrix& A)
{
    return transposed_view<Matrix>(A);
}
```

Now we can use the trans elegantly in our scientific software, for instance, in a matrix-vector product:

```
v = trans(A) * q;
```

In this case, a temporary view is created and used in the product. Since most compilers will inline the view's operator(), computations with `trans(A)` will be as fast as with `A`.

# 5.2.3.2 Dealing with const-ness

So far, our view works nicely. Problems arise when we build the transposed view of a constant matrix:

```
const mtl::dense2D<float> B(A);
```

We still can create the transposed view of `B` but we cannot access its elements:

```
cout << "trans(B)(2, 0) = " << trans(B)(2, 0) << '\n'; // Error
```

The compiler will tell us that it cannot initialize a `float&` from a const float. When we look at the location of the error, we realize that this happens in the non-const overload of the operator. This raises the question of why the constant overload is not used which returns a constant reference and fits our needs perfectly.