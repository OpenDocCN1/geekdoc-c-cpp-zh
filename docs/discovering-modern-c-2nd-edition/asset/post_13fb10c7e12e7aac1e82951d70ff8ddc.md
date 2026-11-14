
The type traits that many programmers have already used for several years from the Boost library were standardized in C++11 and provided in <type_traits>. We refrain at this point from enumerating them completely and refer you instead to the before-mentioned online manuals. Some of the type traits—like is_const (§5.2.3.3)—are very easy to implement by partial template specialization. Establishing domain-specific type traits in this style (e.g., is_matrix) is not difficult and can be quite useful. Other type traits that reflect the existence of functions or properties thereof—such as is_nothrow_assignable—are quite tricky to implement. Providing type traits of this kind requires a fair amount of expertise (and some black magic).

With all the new features, C++11 did not forget its roots. There are type traits that allow us to check the compatibility with C. A class that behaves like one from C is called Plain Old Data type (POD). There actually used to be a type trait named is_pod to check this but it is deprecated in C++20. For testing whether a class properly works in a C program, we can use the type trait is_standard_layout. In contrast to the former, it only tells us whether a class has the same memory layout like a C class. This is a sufficient condition to use the type in C code regardless of its behavior in a C++ program. To illustrate this, we define a class that can be used in both C and C++ programs:

Click here to view code image

```cpp
struct simple_point
{
#ifdef __cplusplus
    simple_point(double x, double y) : x(x), y(y) {}
    simple_point() = default;
    simple_point(initializer_list<double> il)
    {
        auto it = begin(il);
        x = *it;
        y = *next(it);
    }
#endif

    double x, y;
};
```

The macro __cplusplus is defined in all C++ compilers and with conditional compilation we can provide constructors and other member functions that can be used in a C++ program only. Thus, simple_point objects can be constructed with an initializer list:

```cpp
simple_point p1 = {3.0, 7.0};
```

and at the same time be used in C programs. Similar examples can be found in the CUDA library where some types are defined once for both C and C++. However, such hybrid constructs should only be used when really necessary to avoid surplus maintenance effort and inconsistency risks. The compatibility with C can be verified as follows:

Click here to view code image

```cpp
cout << "simple_point can be used in C: " << boolalpha
<< is_standard_layout<simple_point>::value << endl;
```

We can add more member functions in the C++-only part and still be compatible with C. What we cannot use are virtual functions as they inject a vtable in each object. Neither can we have member variables or base classes that have no standard layout. Exceptions are static member variables because they aren't stored in the object. If you are interested in this topic be our guest and play with the before-mentioned code uploaded on GitHub. A more detailed discussion is found in Andreas Fertig's book [15], planned for release in September 2021, and on his blog [14].

=> c++11/memcpy_test.cpp

Sufficiently simple data like simple_point can be copied as raw data without calling a copy assignment. This is achieved with the traditional functions memcpy or memmove. However, as responsible programmers we check up front with is_trivially_copyable whether the compiler agrees with our optimization:

Click here to view code image

```cpp
simple_point p1{3.0, 7.1}, p2;
static_assert(std::is_trivially_copyable<simple_point>::value,
"simple_point is not as simple as you think "
"and cannot be memcpy'd!");
std::memcpy(&p2, &p1, sizeof(p1));
```

To be trivially copyable it is necessary that the user hasn't provided their own copy or move operation. Simpler and more generic is the usage of the STL function copy:

```cpp
copy(&x, &x + 1, &y);
```

This always works regardless of our class's implementation. copy internally uses memmove or memcpy when the types allow for it.

[C++14] C++14 adds some template aliases like:

```cpp
conditional_t<B, T, F>
```

as a shortcut for

```cpp
typename conditional<B, T, F>::type
```

Likewise, enable_if_t is an abbreviation for the type of enable_if.

[C++17] Templated constants for value-based type traits allow us in C++17 to replace for instance:

```cpp
is_trivially_copyable<T>::value
```

with

```cpp
is_trivially_copyable_v<T>
```

## [C++11] 4.4 Utilities

C++11 adds new libraries that make modern programming style easier and more elegant. For instance, we can return multiple results more easily, refer to functions and functors more flexibly, and create containers of references. Further utilities were added in C++17 which allow us for instance to deal with values that might not be defined sometimes or to handle values of different types in type-safe fashion.

### [C++17] 4.4.1 optional

When we compute square roots in real numbers, the result is not defined (in R). To express this, we can return an extra `bool` to indicate whether our computation was successful. Preferably we return our numerical result together with the `bool` in a class; and this is exactly what `optional` provides and makes our square-root computation quite clear:

Click here to view code image

```cpp
optional<double> square_root(double x)
{
    if (x < 0.0)
        return nullopt;
    else
        return sqrt(x);
}
```

nullopt is an object (of type `nullopt_t`) to construct an `optional` object without value. This is equivalent to the class's default constructor but the `nullopt` version is more expressive.

For convenience, `optional` provides an implicit conversion to `bool` which indicates whether a value is defined and allows us a direct usage in `if`-statements. The concisest way to access the value is with `operator*`. A conditional output of square roots can be written in a pretty compact fashion:

Click here to view code image

```cpp
vector<double> v = {4.0, -4.0, -0.09, 0.25};
for (double d : v)
    if (auto s = square_root(d); s)
        cout << "Square root of " << d << " is " << *s << '\n';
    else
        cout << d << " has no square root.\n";
```

Using the initializer feature of `if`, we didn't even need braces.

### C++11 4.4.2 tuple

When a function computes multiple results, they used to be passed as mutable reference arguments. Assume we implement an LU factorization with pivoting taking a matrix A and returning the factorized matrix LU and the permutation vector p:

Click here to view code image

```cpp
void lu(const matrix& A, matrix& LU, vector& p) { ... }
```

We could also return either LU or p as function results and pass the other object by reference. This mixed approach is even more confusing.

=> c++11/tuple_move_test.cpp

To return multiple results without implementing a new class, we can bundle them into a Tuple. A tuple (from <tuple>) differs from a container by allowing different types. In contrast to most containers, the number of objects must be known at compile time. With a tuple we can return both results of our LU factorization at once:

Click here to view code image

```cpp
tuple<matrix, vector> lu(const matrix& A)
{
    matrix LU(A);
    vector p(n);
    // ... some computations
    return tuple<matrix, vector>(LU, p);
}
```

The return statement can be simplified with the helper function make_tuple deducing the type parameters:

Click here to view code image

```cpp
tuple<matrix, vector> lu(const matrix& A)
{
    ...
    return make_tuple(LU, p);
}
```

C++17 With C++17 we can use class- and return-type deduction:

```cpp
auto lu(const matrix& A)
{
    ...
    return tuple{LU, p}
}
```

make_tuple is convenient in C++11 and C++14 when combined with auto variables:

Click here to view code image

```cpp
// 9.0i is complex<double>{0.0, 9.0} in C++14
auto t = make_tuple(LU, p, 7.3, 9, LU*p, 2.0*9.0i);
```

### C++17

In C++17 we can deduce the template arguments of tuple in the constructor:

```cpp
tuple t{LU, p, 7.3, 9, LU*p, 2.0*9.0i};
```

The caller of our function lu will probably extract the matrix and the vector from the tuple with the function get:

Click here to view code image

```cpp
tuple<matrix, vector> t = lu(A);
matrix LU = get<0>(t);
vector p = get<1>(t);
```

Here, all types can be deduced as well:

```cpp
auto t = lu(A);
auto LU = get<0>(t);
auto p = get<1>(t);
```

The function get takes two arguments: a tuple and a position therein. The latter is a compile-time parameter. Otherwise the type of the result would not be known. If the index is too large, the error is detected during compilation:

Click here to view code image

```cpp
auto t = lu(A);
auto am_i_stupid = get<2>(t); // Error during compilation
```

### C++14

In C++14, the tuple entries can also be accessed by their type if this is unambiguous:

```cpp
auto t = lu(A);
auto LU = get<matrix>(t);
auto p = get<vector>(t);
```

Then we are not obliged any longer to memorize the internal order in the tuple. Alternatively, we can use the function tie to separate the entries in
