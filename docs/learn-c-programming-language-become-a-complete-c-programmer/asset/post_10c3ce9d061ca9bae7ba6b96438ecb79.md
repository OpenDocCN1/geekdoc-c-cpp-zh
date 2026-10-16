
everybody.” For example, I did not list:

- Many more mathematical matrix operations
- Specialized matrices (e.g., diagonal and triangular matrices)
- Sparse **Matrix** support
- Support for parallel execution of **Matrix** operations

However valuable those properties are, they go beyond what is needed to present basic programming techniques.

To provide this, I use a combination of several language features and programming techniques:

- Classes (of course)
- Parameterization with numbers and types
- Move constructors and assignments (to minimize copying)
- RAII (relying on constructors and destructors)
- Variadic templates (for specifying extents and for indexing)
- Initializer lists
- Operator overloading (to get conventional notation)
- Function objects (to carry information about subscripting)
- Some simple template metaprogramming (e.g., for checking initializer lists and for distinguishing reading and writing for **Matrix_refs**)
- Implementation inheritance for minimizing code replication.

Obviously, a **Matrix** like this could be a built-in type (as it is in many languages), but the point here is exactly that in C++ it is *not* built in. Instead, facilities are provided for users to make their own.

## 29.2 A **Matrix** Template

To give an overview, here is the declaration of **Matrix** with its most interesting operations:

```cpp
template<typename T, size_t N>
class Matrix {
public:

    static constexpr size_t order = N; // number of dimensions
    using value_type = T;
    using iterator = typename std::vector<T>::iterator;
    using const_iterator = typename std::vector<T>::const_iterator;

    Matrix() = default;
    Matrix(Matrix&&) = default;              // move
    Matrix& operator=(Matrix&&) = default;   // move
    Matrix(Matrix const&) = default;         // copy
    Matrix& operator=(Matrix const&) = default; // copy
    ~Matrix() = default;

    template<typename U>
    Matrix(const Matrix_ref<U,N>&);

    template<typename U>
    Matrix& operator=(const Matrix_ref<U,N>&);

    // construct from Matrix_ref
    // assign from Matrix_ref

    template<typename... Exts> // specify the extents
    explicit Matrix(Exts... exts);
    Matrix(Matrix_initializer<T,N>); // initialize from list
    Matrix& operator=(Matrix_initializer<T,N>); // assign from list

    template<typename U>
    Matrix(initializer_list<U>) = delete; // don't use {} except for elements
    template<typename U>
    Matrix& operator=(initializer_list<U>) = delete;

    size_t extent(size_t n) const { return desc.extents[n]; } // #elements in the nth dimension
    size_t size() const { return elems.size(); } // total number of elements
    const Matrix_slice<N>& descriptor() const { return desc; } // the slice defining subscripting

    T* data() { return elems.data(); }
    const T* data() const { return elems.data(); }
    // "flat" element access
    // ...

private:
    Matrix_slice<N> desc;    // slice defining extents in the N dimensions
    vector<T> elems;         // the elements
};
```

Using a `vector<T>` to hold the elements relieves us from concerns of memory management and exception safety. A `Matrix_slice` holds the sizes necessary to access the elements as an N-dimensional matrix (§29.4.2). Think of it as a `gslice` (§40.5.6) specialized for our `Matrix`.

A `Matrix_ref` (§29.4.3) behaves just like a `Matrix` except that it refers to a `Matrix`, typically a subMatrix such as a row or a column, rather than owning its own elements. Think of it as a reference to a subMatrix.

A `Matrix_initializer<T,N>` is a suitably nested initializer list for a `Matrix<T,N>` (§29.4.4).

### 29.2.1 Construction and Assignment

The default copy and move operations have just the right semantics: memberwise copy or move of the `desc` (slice descriptor defining subscripting) and the elements. Note that for management of the storage for elements, `Matrix` gets all the benefits from `vector`. Similarly, the default constructor and destructor have just the right semantics.

The constructor that takes extents (numbers of elements in dimensions) is a fairly trivial example of a variadic template (§28.6):

```cpp
template<typename T, size_t N>
template<typename... Exts>
Matrix<T,N>::Matrix(Exts... exts)
    : desc{exts...},       // copy extents
      elems(desc.size)     // allocate desc.size elements and default initialize them
{
}
```

The constructor that takes an initializer list requires a bit of work:

```cpp
template<typename T, size_t N>
Matrix<T, N>::Matrix(Matrix_initializer<T,N> init)
{
    Matrix_impl::derive_extents(init, desc.extents); // deduce extents from initializer list (§29.4.4)
    elems.reserve(desc.size);                        // make room for slices
    Matrix_impl::insert_flat(init, elems);           // initialize from initializer list (§29.4.4)
    assert(elems.size() == desc.size);
}
```

The `Matrix_initializer` is a suitably nested `initializer_list` (§29.4.4). The extents are deduced by the `Matrix_slice` constructor, checked, and stored in `desc`. Then, the elements are stored in `elems` by `insert_flat()` from the `Matrix_impl` namespace.

To ensure that `{}` initialization is only used for lists of elements, I `=delete` the simple `initializer_list` constructor. This is to enforce the use of `()` initialization for extents. For example:

```cpp
enum class Piece { none, cross, naught };
Matrix<Piece,2> board1 {
    {Piece::none, Piece::none, Piece::none},
    {Piece::none, Piece::none, Piece::none},
    {Piece::none, Piece::none, Piece::cross}
};
Matrix<Piece,2> board2(3,3); // OK
Matrix<Piece,2> board3 {3,3}; // error: constructor from initializer_list<int> deleted
```

Without that `=delete`, that last definition would have been accepted.

Finally, we have to be able to construct from a `Matrix_ref`, that is, from a reference to a `Matrix` or a part of a `Matrix` (a submatrix):

```cpp
template<typename T, size_t N>
template<typename U>
Matrix<T,N>::Matrix(const Matrix_ref<U,N>& x)
    : desc{x.desc}, elems{x.begin(), x.end()} // copy desc and elements
{
    static_assert(Convertible<U,T>(), "Matrix constructor: incompatible element types");
}
```

The use of a template allows us to construct from a `Matrix` with a compatible element type. As usual, the assignments resemble the constructors. For example:

```cpp
template<typename T, size_t N>
template<typename U>
Matrix<T,N>& Matrix<T,N>::operator=(const Matrix_ref<U,N>& x)
{
    static_assert(Convertible<U,T>(), "Matrix =: incompatible element types");
    desc = x.desc;
    elems.assign(x.begin(), x.end());
    return *this;
}
```

That is, we copy the members of `Matrix`.

### 29.2.2 Subscripting and Slicing

A `Matrix` can be accessed through subscripting (to elements or rows), through rows and columns, or through slices (parts of rows or columns).

| Access | Description |
|---|---|
| `m.row(i)` | Row `i` of `m`; a `Matrix_ref<T,N-1>` |
| `m.column(i)` | Column `i` of `m`; a `Matrix_ref<T,N-1>` |
| `m[i]` | C-style subscripting: `m.row(i)` |
| `m(i,j)` | Fortran-style element access: `m[i][j]`; a `T&`; the number of subscripts must be `N` |
| `m(slice(i,n),slice(j))` | Submatrix access with slicing: a `Matrix_ref<T,N>`; `slice(i,n)` is elements `[i:i+n)` of the subscript's dimension; `slice(j)` is elements `[j:max)` of the subscript's dimension; **max** is the dimension's extent; the number of subscripts must be `N` |

These are all member functions:

```cpp
template<typename T, size_t N>
class Matrix {
public:
    // ...

    template<typename... Args> // m(i,j,k) subscripting with integers
    Enable_if<Matrix_impl::Requesting_element<Args...>(), T&>
    operator()(Args... args);

    template<typename... Args>
    Enable_if<Matrix_impl::Requesting_element<Args...>(), const T&>
    operator()(Args... args) const;

    template<typename... Args> // m(s1,s2,s3) subscripting with slices
    Enable_if<Matrix_impl::Requesting_slice<Args...>(), Matrix_ref<T, N>>
    operator()(const Args&... args);

    template<typename... Args>
    Enable_if<Matrix_impl::Requesting_slice<Args...>(), Matrix_ref<const T,N>>
    operator()(const Args&... args) const;

    Matrix_ref<T,N-1> operator[](size_t i) { return row(i); } // m[i] row access
    Matrix_ref<const T,N-1> operator[](size_t i) const { return row(i); }

    Matrix_ref<T,N-1> row(size_t n); // row access
    Matrix_ref<const T,N-1> row(size_t n) const;
    Matrix_ref<T,N-1> col(size_t n); // column access
    Matrix_ref<const T,N-1> col(size_t n) const;
    // ...
};
```

C-style subscripting is done by `m[i]` selecting and returning the i th row:

```cpp
template<typename T, size_t N>
Matrix_ref<T,N-1> Matrix<T,N>::operator[](size_t n)
{
    return row(n); // §29.4.5
}
```

Think of a `Matrix_ref` (§29.4.3) as a reference to a subMatrix. `Matrix_ref<T,0>` is specialized so that it refers to a single element (§29.4.6). Fortran-style subscripting is done by listing an index for each dimension, for example, `m(i,j,k)`, yielding a scalar:

```cpp
Matrix<int,2> m {
    {01,02,03},
    {11,12,13}
};
m(1,2) = 99; // overwrite the element in row 1 column 2; that is 13
auto d1 = m(1); // error: too few subscripts
auto d2 = m(1,2,3); // error: too many subscripts
```

In addition to subscripting with integers, we can subscript with slices. A slice describes a subset of the elements of a dimension (§40.5.4). In particular, `slice(i,n)` refers to elements `[i:i+n)` of the dimension to which it applies. For example:

```cpp
Matrix<int,2> m {
    {01,02,03},
    {11,12,13},
    {21,22,23}
```
