the first index
// 1isthe stride for the second index

```
void f() {
gslice s(0,lengths,strides);
for (int i=0; i<3; ++i) // foreach row
for (int j=0; j<2; ++j) // foreach element in row
cout << "(" << i << "," << j << ")->" << gsllice_index(s,i,j) << ";"; // printmapping }
```

This prints:

```
(0,0)->0; (0,1)->1; (1,0)->3; (1,1)->4; (2,0)->6; (2,1)->7
```

In this way, a gsllice with two (length,stride) pairs describes a subarray of a two-dimensional array, a gsllice with three (length,stride) pairs describes a subarray of a three-dimensional array, etc. Using a gsllice as the index of a valarray yields a gsllice_array consisting of the elements described by the gsllice. For example:

```
void f(valarray< float>& v)
{
gslice m(0,lengths,strides);
v[m] = 0; // assign 0 to v[0],v[1],v[3],v[4],v[6],v[7]
}
```

The gsllice_array offers the same set of members as slice_array(§40.5.5). A gsllice_array is the result of using a gsllice as the subscript of a valarray (§40.5.2).

# 40.6 Generalized Numerical Algorithms

In <numeric>, the standard library provides a few generalized numeric algorithms in the style of the non-numeric algorithms from <algorithm> (Chapter 32). These algorithms provide general versions of common operations on sequences of numerical values:

# Numerical Algorithms (§iso.26.7) (continues)

These algorithms take input iterators

```
x=accumulate(b,e ,i) x is the sum of i and the elements of [b:e)
x=accumulate(b,e ,i,f) accumulate using f instead of +
x=inner_product(b,e ,b2,i) x is the inner product of [b:e) and [b2:b2+(e-b)),
that is, the sum of i and (*p1)*(*p2) for each p1 in [b:e) and the corresponding p2 in [b2:b2+(e-b)) x=inner_product(b,e ,b2,i,f,f2) inner_product using f and f2 instead of + and *
```

Section 40.6 Generalized Numerical Algorithms 1177

# Numerical Algorithms (continued) (§iso.26.7)

These algorithms take input iterators

```
p=partial_sum(b,e,out) Element i of [out:p) is the sum of elements [b:b+i]
p=partial_sum(b,e,out,f) partial_sum using f instead of +
p=adjacent_difference(b,e ,out) Element i of [out:p)is (*b+i)-*(b+i-1) for i>0;
if e-b>0, then *out is *b
p=adjacent_difference(b,e ,out,f)
iota(b,e,v)
```