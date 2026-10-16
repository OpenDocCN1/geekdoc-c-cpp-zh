```
};
double d1 = m(1,2); // d==12
double d2 = m[1][2]; // d==12
Matrix<double ,1> m1 = m[1]; // row1:{10,11,12,13} double d3 = m1[2]; // d==12
```

We can define an output function for use in debugging like this:

```
template<typename M>
Enable_if<Matrix_type<M>(),ostream&>
operator<<(ostream& os, const M& m)
{
os << '{';
for (size_t i = 0; i!=rows(m); ++i) {
os << m[i];
if (i+1!=rows(m)) os << ',';
}
return os << '}';
}
```

Here, Matrix_type is a concept (§24.3). Enable_if is an alias for enable_if’s type (§28.4), so this operator<<( ) returns an ostream&.
Given that, cout<<m prints: {{0,1,2,3},{10,11,12,13},{20,21,22,23}}.

# 29.1.2 Matrix Requirements

Before proceeding with an implementation, consider what properties we might like to have:

+   - **N** dimensions, where **N** is a parameter that can vary from **0** to many, without specialized code for every dimension.
+   - **N**-dimensional storage is useful in general, so the element type can be anything we can store (like a **vector** element).
+   - The mathematical operations should apply to any type that can reasonably be described as a number, including a **Matrix**.
+   - Fortran-style subscripting using one index per dimension, for example, **m(1,2,3)** for a 3-D **Matrix**, yielding an element.
+   - C-style subscripting, for example, **m[7]**, yielding a row (a row is an **N−1**-D sub**Matrix** of an **N-D Matrix**).
+   - Subscripting should be potentially fast and potentially range checked.
+   - Move assignment and move constructor to ensure efficient passing of **Matrix** results and to eliminate expensive temporaries.
+   - Some mathematical matrix operations, such as **+** and **\*=**.
+   - A way to read, write, and pass around references to submatrices, **Matrix_refs**, for use for both reading and writing elements.
+   - The absence of resource leaks in the form of the basic guarantee (§13.2).
+   - Fused critical operations, for example, **m_*v+v2** as a single function call.

This is a relatively long and ambitious list, but it does not add up to “everything for