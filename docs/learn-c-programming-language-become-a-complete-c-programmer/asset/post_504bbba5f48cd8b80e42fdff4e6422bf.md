
```
valarray<int> v {
{00,01,02,03}, // row0
{10,11,12,13}, // row1
{20,21,22,23} // row2
};
```

or graphically:

00 01 02 03
10 11 12 13
20 21 22 23

Following the usual C/C++ conventions, the valarray is laid out in memory with row elements first (row-major order) and contiguous:

```
for (int x : v) cout << x << ' ';
```

This produces:

```
01231011121320212223
```

## Section 40.5.4 Slices

or graphically:

column 0: 0 4 8

00 01 02 03 10 11 12 13 20 21 22 23 row0: 123

Row x is described by slice(x*4,4,1). That is, the first element of row x is the x*4th element of the vector, the next element of the row is the (x*4+1)th, etc., and there are 4 elements in each row. For example, slice{0,4,1} describes the first row of v (row 0): 00, 01, 02, 03, and slice{1,4,1} describes the second row (row 1).

Column y is described by slice(y,3,4). That is, the first element of column y is the yth element of the vector, the next element of the column is the (y+4)th, etc., and there are 3 elements in each column. For example, slice{0,3,4} describes the first column (column 0): 00, 10, 20, and slice{1,3,4} describes the second column (column 1).

In addition to its use for simulating two-dimensional arrays, a slice can describe many other sequences. It is a fairly general way of specifying very simple sequences. This notion is explored further in §40.5.6.

One way of thinking of a slice is as an odd kind of iterator: a slice allows us to describe a sequence of indices for a valarray. We could build an STL-style iterator based on that:

```
template<typename T>
class Slice_iter {
valarray<T>* v;
slice s;
size_t curr; // index of current element

T& ref(size_t i) const { return ( *v)[s.start()+i*s.stride()]; } public:
Slice_iter(valarray<T>* vv, slice ss, size_t pos =0) :v{vv}, s{ss}, curr{0} { }

Slice_iter end() const { return {this,s,s.size()}; }
Slice_iter& operator++() { ++curr; return *this; }
Slice_iter operator++(int) { Slice_iter t = *this; ++curr; return t; }
```

```
T& operator[](size_t i) { return ref(i); } T& operator()(size_t i) { return ref(i); } T& operator*() { return ref(curr); }
```

```
bool operator==(const Slice_iter& q) const {
```

```
// C-style subscript
// Fortran-style subscript // current element
```

```
return curr==q.curr && s.stride()==q.s.stride() && s.start()==q.s.start(); bool operator!=(const Slice_iter& q ) const {
```

```
return !(*this==q); }
```

```
bool operator<(const Slice_iter& q) const
```

```
{
return curr<q.curr && s.stride()==q.s.stride() && s.start()==q.s.start();
};
```

Since a slice has a size, we could even provide range checking. Here, I have taken advantage of slice::size() to provide an end() operation to provide an iterator for the one-past-the-end element of the slice.

Since a slice can describe either a row or a column, the Slice_iter allows us to traverse a valarray by row or by column.

## 40.5.5 slice_array

From a valarray and a slice, we can build something that looks and feels like a valarray but is really simply a way of referring to the subset of the array described by the slice.

```
slice_array<T> (§iso.26.6.5)
```

slice_array sa {sa2}; Copy constructor: sa refers to the same elements as sa2 does sa=sa2 Assign the element referred to by sa[i] to each

corresponding element referred to by sa2[i]

```
sa=va Assign va[i] to each corresponding element referred to by sa[i] sa=v Assign v to each element referred to by sa
```

```
sa@=va sa[i]@=va[i] for each element of sa;
```

```
@ can be /, %, +, -, ^, &, |, <<,or >>
```

A user cannot directly create a slice_array. Instead, the user subscripts a valarray to create a slice_array for a given slice. Once the slice_array is initialized, all references to it indirectly go to the valarray for which it is created. For example, we can create something that represents every second element of an array like this:

```
void f(valarray<double>& d)
{
slice_array<double>& v_even = d[slice(0,d.size()/2+d.size()%2,2)];
slice_array<double>& v_odd = d[slice(1,d.size()/2,2)];
```

```
v_even *= v_odd; // multiply element pairs and store results in even elements v_odd = 0;
```

```
// assign 0 to every odd element of d
}
```

A **slice_array** can be copied. For example:

```
slice_array<double> row(valarray<double>& d, int i) {
  slice_array<double> v = d[slice(0,2,d.size()/2)]; // ...
  return d[slice(i%2,i,d.size()/2)];
}
```

## 40.5.6 Generalized Slices

A **slice** (§29.2.2, §40.5.4) can describe a row or a column of an **n**-dimensional array. However, sometimes we need to extract a subarray that is not a row or a column. For example, we might want to extract the 3-by-2 matrix from the top-left corner of a 4-by-3 matrix:

```
00 01 02
10 11 12
20 21 22
30 31 32
```

Unfortunately, these elements are not allocated in a way that can be described by a single **slice**:

```
subarray: 0 1 2 3 4 5
00 01 02 10 11 12 20 21 22 30 31 32
```

A **gslice** is a “generalized slice” that contains (almost) the information from **n slices**:

```
class std::gslice {
// instead of 1 stride and one size like slice, gslice holds n strides and n sizes
public:
  gslice();
  gslice(size_t sz, const valarray<size_t>& lengths, const valarray<size_t>& strides);
  size_t start() const; // index of first element
  valarray<size_t> size() const; // number of elements in dimension
  valarray<size_t> stride() const; // stride for index[0], index[1], ...
};
```

The extra values allow a **gslice** to specify a mapping between **n** integers and an index to be used to address elements of an array. For example, we can describe the layout of the 3-by-2 matrix by a pair of (length,stride) pairs:

```
size_t gslice_index(const gslice& s, size_t i, size_t j) // max (i,j) to their corresponding index {
  return s.start()+i*s.stride()[0]+j*s.stride()[1];
  valarray<size_t> lengths {2,3}; // 2 elements in the first dimension
  // 3 elements in the second dimension
  valarray<size_t> strides {3,1}; // 3 is the stride for
}
```

the first index
// 1 is the stride for the second index

```
void f() {
gslice s(0,lengths,strides);
for (int i=0; i<3; ++i) // foreach row
for (int j=0; j<2; ++j) // foreach element in row
cout << "(" << i << "," << j << ")->" << gslice_index(s,i,j) << ";"; // print mapping }
```

This prints:

```
(0,0)->0; (0,1)->1; (1,0)->3; (1,1)->4; (2,0)->6; (2,1)->7
```

In this way, a gslice with two (length,stride) pairs describes a subarray of a two-dimensional array, a gslice with three (length,stride) pairs describes a subarray of a three-dimensional array, etc. Using a gslice as the index of a valarray yields a gslice_array consisting of the elements described by the gslice. For example:

```
void f(valarray< float>& v)
{
gslice m(0,lengths,strides);
v[m] = 0; // assign 0 to v[0],v[1],v[3],v[4],v[6],v[7]
}
```

The gslice_array offers the same set of members as slice_array(§40.5.5). A gslice_array is the result of using a gslice as the subscript of a valarray (§40.5.2).

## 40.6 Generalized Numerical Algorithms

In <numeric>, the standard library provides a few generalized numeric algorithms in the style of the non-numeric algorithms from <algorithm> (Chapter 32). These algorithms provide general versions of common operations on sequences of numerical values:

## Numerical Algorithms (§iso.26.7) (continues)

These algorithms take input iterators

```
x=accumulate(b,e ,i) x is the sum of i and the elements of [b:e)
x=accumulate(b,e ,i,f) accumulate using f instead of +
x=inner_product(b,e ,b2,i) x is the inner product of [b:e) and [b2:b2+(e-b)),
that is, the sum of i and (*p1)*(*p2) for each p1 in [b:e) and the corresponding p2 in [b2:b2+(e-b)) x=inner_product(b,e ,b2,i,f,f2) inner_product using f and f2 instead of + and *
```

Section 40.6 Generalized Numerical Algorithms 1177

## Numerical Algorithms (continued) (§iso.26.7)

These algorithms take input iterators

```
p=partial_sum(b,e,out) Element i of [out:p) is the sum of elements [b:b+i]
p=partial_sum(b,e,out,f) partial_sum using f instead of +
p=adjacent_difference(b,e ,out) Element i of [out:p)is (*b+i)-*(b+i-1) for i>0;
if e-b>0, then *out is *b
p=adjacent_difference(b,e ,out,f)
iota(b,e,v)
```
