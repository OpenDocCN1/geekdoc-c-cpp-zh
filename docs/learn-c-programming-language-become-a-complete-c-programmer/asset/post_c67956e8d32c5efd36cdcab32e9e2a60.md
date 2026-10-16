
```
for (size_t j = 0; j!=n; ++j) res(i) += m(i,j)*v(j);
```

Note that the declaration of **res** initializes its elements to **T{}**, which is zero for numeric types, so that the **+=** starts out from zero.
The N-by-M matrix times M-by-P matrix is handled similarly:

```
template<typename T>
Matrix<T,2> operator*(const Matrix<T,2>& m1, const Matrix<T,2>& m2)
{

const size_t n = m1.extent(0);
const size_t m = m1.extent(1);
assert(m==m2.extent(0)); // columns must match rows

const size_t p = m2.extent(1);
Matrix<T,2> res(n,p);
for (size_t i = 0; i!=n; ++i)
for (size_t j = 0; j!=m; ++j)
for (size_t k = 0; k!=p; ++k)
res(i,j) = m1(i,k)*m2(k,j);
return res;
}
```

There are numerous ways of optimizing this important operation.
That innermost loop could be more elegantly expressed as:

```
res(i,j) = dot_product(m1[i],m2.column(j))
```

Here, **dot_product()** is simply an interface to the standard-library **inner_product()** (§40.6.2):

```
template<typename T>
T dot_product(const Matrix_ref<T,1>& a, const Matrix_ref<T,1>& b)
{

return inner_product(a.begin(),a.end(),b.begin(),0.0); }
```

## 29.4 **Matrix** Implementation

So far, I have delayed the presentation of the most complicated (and for some programmers the most interesting) “mechanical” parts of the **Matrix** implementation. For example: What is a **Matrix_ref**? What is a **Matrix_slice**? How do you initialize a **Matrix** from a nest of **initializer_lists** and make sure the dimensions are reasonable? How do we ensure that we don’t instantiate a **Matrix** with an unsuitable element type?

### 29.4.1 **slice()**

A simple **slice** as used for **slice** subscripting describes a mapping from an integer (subscript) to an element location (index) in terms of three values:

```
struct slice {
slice() :start(-1), length(-1), stride(1) { }
explicit slice(size_t s) :start(s), length(-1), stride(1) { }
slice(size_t s, size_t l, size_t n = 1) :start(s), length(l), stride(n) { }

size_t operator()(size_t i) const { return start+i*stride; }
static slice all;

size_t start; // first index
size_t length; // number of indices included (can be used for range checking)
size_t stride; // distance between elements in sequence
};
```

There is a standard-library version of **slice**; see §40.5.4 for a more thorough discussion. This version provides notational convenience (e.g., the default values provided by the constructors).

### 29.4.2 **Matrix Slices**

A **Matrix_slice** is the part of the **Matrix** implementation that maps a set of subscripts to the location of an element. It uses the idea of generalized slices (§40.5.6):

```
template<size_t N>
struct Matrix_slice {
Matrix_slice() = default; // an empty matrix: no elements
Matrix_slice(size_t s, initializer_list<size_t> exts); // extents
Matrix_slice(size_t s, initializer_list<size_t> exts, initializer_list<size_t> strs);// extents and strides
template<typename... Dims> // Nextents Matrix_slice(Dims... dims);
template<typename... Dims,
typename = Enable_if<All(Convertible<Dims,size_t>()...)>>
size_t operator()(Dims... dims) const; // calculate index from a set of subscripts
size_t size; // total number of elements
size_t start; // starting offset
array<size_t,N> extents; // number of elements in each dimension
array<size_t,N> strides; // offsets between elements in each dimension
};
```

In other words, a **Matrix_slice** describes what is considered rows and columns in a region of memory. In the usual C/C++ row-major layout of a matrix, the elements of rows are contiguous, and the elements of a column are separated by a fixed number of elements (a stride). A **Matrix_slice** is a function object, and its **operator()** does a stride calculation (§40.5.6):

```
template<size_t N>
template<typename... Dims>
size_t Matrix_slice<N>::operator()(Dims... dims) const {
static_assert(sizeof...(Dims) == N, "");
size_t args[N] { size_t(dims)... }; // Copy arguments into an array
return inner_product(args,args+N,strides.begin(),size_t(0));
}
```

Subscripting must be efficient. This is a simplified algorithm that needs to be optimized. If nothing else, specialization can be used to eliminate the simplifying copy of subscripts out of the variadic template’s parameter pack. For example:

```
template<>
struct Matrix_slice<1> {
// ...
size_t operator()(size_t i) const
{
return i;
}
}
```

```
template<>
struct Matrix_slice<2> {
// ...
size_t operator()(size_t i, size_t j) const
{
return i*strides[0]+j;
}
}
```

The Matrix_slice is fundamental for defining the shape of a Matrix (its extents) and for implementing N-dimensional subscripting. However, it is also useful for defining submatrices.

### 29.4.3 Matrix_ref

A Matrix_ref is basically a clone of the Matrix class used to represent subMatrices. However, a Matrix_ref does not own its elements. It is constructed from a Matrix_slice and a pointer to elements:

```
template<typename T, size_t N>
class Matrix_ref {
public:
Matrix_ref(const Matrix_slice<N>& s, T* p) :desc{s}, ptr{p} {}
// ... mostly like Matrix...
private:
Matrix_slice<N> desc; // the shape of the matrix
T*ptr; // the first element in the matrix
};
```

A Matrix_ref simply points to the elements of “its” Matrix. Obviously, a Matrix_ref should not outlive its Matrix. For example:

```
Matrix_ref<double ,1> user()
{
Matrix<double ,2> m = {{1,2}, {3,4}, {5,6}}; return m.row(1);
}
```

```
auto mr = user(); // trouble
```

The great similarity between Matrix and Matrix_ref leads to duplication. If that becomes a bother, we can derive both from a common base:

```
template<typename T, size_t N>
class Matrix_base {
// ... common stuff ...
};
```

```
template<typename T, size_t N>
class Matrix : public Matrix_base<T,N> {
// ... special to Matrix ...
private:
Matrix_slice<N> desc; // the shape of the matrix
vector<T> elements;
};
```

```
template<typename T, size_t N>
class Matrix_ref : public Matrix_base<T,N> {
// ... special to Matrix_ref ...
private:
Matrix_slice<N> desc; // the shape of the matrix
T* ptr;
};
```

### 29.4.4 Matrix List Initialization

The Matrix constructor that constructs from an initializer_list takes as its argument type the alias Matrix_initializer:

```
template<typename T, size_t N>
using Matrix_initializer = typename Matrix_impl::Matrix_init<T, N>::type;
```

Matrix_init describes the structure of a nested initializer_list.

Matrix_init<T,N> simply has Matrix_init<T,N-1> as its member type:

```
template<typename T, size_t N>
struct Matrix_init {
using type = initializer_list<typename Matrix_init<T,N-1>::type>;
};
```

The N==1 is special. That is where we get to the (most deeply nested) initializer_list<T>:

```
template<typename T>
struct Matrix_init<T,1> {
using type = initializer_list<T>;
};
```

To avoid surprises, we define N=0 to be an error:

```
template<typename T>
struct Matrix_init<T,0>; // undefined on purpose
```

We can now complete the Matrix constructor that takes a Matrix_initializer:

```
template<typename T, size_t N>
Matrix<T, N>::Matrix(Matrix_initializer<T,N> init)
{
Matrix_impl::derive_extents(init,desc.extents); // deduce extents from initializer list (§29.4.4) elems.reserve(desc.size); // make room for slices
Matrix_impl::insert_flat(init,elems); // initialize from initializer list (§29.4.4)
assert(elems.size() == desc.size);
}
```

To do so, we need two operations that recurse down a tree of initializer_lists for a Matrix<T,N>:

- derive_extents() determines the shape of the Matrix:
  - Checks that the tree really is N deep
  - Checks that each row (subinitializer_list) has the same number of elements
  - Sets the extent of each row

- insert_flat() copies the elements of the tree of initializer_list<T>s into the elems of a Matrix. The derived_extents() called from a Matrix constructor to initialize its desc looks like this:

```
template<size_t N, typename List>
array<size_t, N> derive_extents(const List& list)
{
array<size_t,N> a;
auto f = a.begin();
add_extents<N>(f,list); // put extents from list into f[]
return a;
}
```

You give it an initializer_list and it returns an array of extents.

The recursion is done from N to the final 1 where the initializer_list is an initializer_list<T>.

Section 29.4.4 Matrix List Initialization 845
