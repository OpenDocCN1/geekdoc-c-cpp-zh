However, the expression m[i][j] is (correctly) interpreted as *(* (m+i)+j), although that is unlikely to be what the programmer intended. A correct solution is:

```
void print_mij(int* m, int dim1, int dim2)
{
for (int i = 0; i!=dim1; i++) {
for (int j = 0; j!=dim2; j++)
cout << m[i*dim2+j] << '\t'; // obscure
cout << '\n';
}
}
```

The expression used for accessing the members in print_mij() is equivalent to the one the compiler generates when it knows the last dimension.

To call this function, we pass a matrix as an ordinary pointer:

```
int test()
{
int v[3][5] = {
{0,1,2,3,4}, {10,11,12,13,14}, {20,21,22,23,24} ;
print_m35(v);
print_mi5(v,3);
print_mij(&v[0][0],3,5);
}
```

Note the use of &v[0][0] for the last call; v[0] would do because it is equivalent, but v would be a type error. This kind of subtle and messy code is best hidden. If you must deal directly with multidimensional arrays, consider encapsulating the code relying on it. In that way, you might ease the task of the next programmer to touch the code. Providing a multidimensional array type with a proper subscripting operator saves most users from having to worry about the layout of the data in the array (§29.2.2, §40.5.2).

The standard vector (§31.4) doesn’t suffer from these problems.

# 7.5 Pointers and const

C++ offers two related meanings of “constant”:

+   - **constexpr**: Evaluate at compile time (§2.2.3, §10.4).
+   - **const**: Do not modify in this scope (§2.2.3).

Basically, constexpr’s role is to enable and ensure compile-time evaluation, whereas const’s primary role is to specify immutability in interfaces. This section is primarily concerned with the second role: interface specification.

Many objects don’t have their values changed after initialization:

+   - Symbolic constants lead to more maintainable code than using literals directly in code.
+   - Many pointers are often read through but never written through.
+   - Most function parameters are read but not written to.

To express this notion of immutability after initialization, we can add const to the