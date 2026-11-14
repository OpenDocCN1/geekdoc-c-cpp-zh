The return statement can be simplified with the helper function make_tuple deducing the type parameters:

```
tuple<matrix, vector> lu(const matrix& A)
{
    ...
    return make_tuple(LU, p);
}
```

make_tuple is especially convenient in combination with auto variables:

```
auto t = make_tuple(LU, p, 7.3, 9, LU*p, 2.0+9.0i);
```

The caller of our function lu will probably extract the matrix and the vector from the tuple with the function get:

```
tuple<matrix, vector> t = lu(A);
matrix LU = get<0>(t);
vector p = get<1>(t);
```

Here, all types can be deduced as well:

```
auto t = lu(A);
auto LU = get<0>(t);
auto p = get<1>(t);
```

The function get takes two arguments: a tuple and a position therein. The latter is a compile-time parameter. Otherwise the type of the result would not be known. If the index is too large, the error is detected during compilation:

```
auto t = lu(A);
auto am_i_stupid = get<2>(t); // Error during compilation
```

In C++14, the tuple entries can also be accessed by their type if this is unambiguous:

```
auto t = lu(A);
auto LU = get<matrix>(t);
auto p = get<vector>(t);
```

Then we are not obliged any longer to memorize the internal order in the tuple. Alternatively, we can use the function tie to separate the entries in the tuple. This is often more elegant.

In this case, we have to declare compatible variables beforehand:

```
matrix LU;
vector p;
tie(LU, p) = lu(A);
```

tie looks quite mysterious at first but its implementation is surprisingly simple: it creates an object with references to function arguments. Assigning a tuple to that object performs assignments of each tuple member to the respective reference.

The implementation with tie has a performance advantage over the implementation with get. When we pass the result of function lu directly to tie, it is still an rvalue (it has no name) and we can move the entries. With an intermediate variable, it becomes an lvalue