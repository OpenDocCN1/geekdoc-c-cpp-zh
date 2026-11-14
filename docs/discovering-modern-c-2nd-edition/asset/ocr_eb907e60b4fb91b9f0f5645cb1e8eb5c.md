```
int main ()
{
    compressed_matrix A;
    f(dense_matrix(A));
}
```

Here we take the `compressed_matrix` A and create a `dense_matrix`. This requires either:

+   - A constructor in `dense_matrix` that accepts a `compressed_matrix`; or
+   - A conversion operator in `compressed_matrix` to `dense_matrix`.

These methods look like this:

Click here to view code image

```
struct compressed_matrix; // forward decl. needed in
constructor
```

```
struct dense_matrix
{
    dense_matrix() = default;
    dense_matrix(const compressed_matrix& A) { ... }
};
```

```
struct compressed_matrix
{
    operator dense_matrix() { dense_matrix A; ... return A; }
};
```

When both exist, the constructor is preferred for creating new objects. With class implementation, we can also call the dense-matrix function f with implicit conversion:

```
int main ()
{
    compressed_matrix A;
    f(A);
}
```

In this case, the conversion operator is prioritized over the constructor. Note that the implicit conversion does not work with an `explicit` constructor or conversion operator. `explicit` conversion operators were introduced in C++11.