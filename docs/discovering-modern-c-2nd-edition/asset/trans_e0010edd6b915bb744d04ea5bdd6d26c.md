

```cpp
template <long N>
struct fibonacci
{
    static const long value = fibonacci<N-1>::value + fibonacci<N-2>::value;
};

template <>
struct fibonacci<1>
{
    static const long value = 1;
};

template <>
struct fibonacci<2>
{
    static const long value = 1;
};
```

```cpp
template <long N>
struct fibonacci
{
    static const long value = N < 3 ? 1 :
        fibonacci<N-1>::value + fibonacci<N-2>::value; // Error
};
```

```cpp
template <>
struct fibonacci
{
    static const long value = 2 < 3 ? 1 :
        fibonacci<1>::value + fibonacci<0>::value; // error
};
```

```cpp
template <0>
struct fibonacci
{
    static const long value = 0 < 3 ? 1 :
        fibonacci< -1>::value + fibonacci< -2>::value; // error
};
```

```cpp
long fibonacci2(long x)
{
    return x < 3 ? 1 : fibonacci2(x-1) + fibonacci2(x-2);
}
```

```cpp
#include <boost/static_assert.hpp>

template <typename Matrix>
class transposed_view
{
    BOOST_STATIC_ASSERT((is_matrix<Matrix>::value)); // Must be a matrix
    // ...
};
```

```
trans_const.cpp:96: Error: Invalid application of sizeof
on incomplete type
boost::STATIC_ASSERTION_FAILURE<false>
```

```cpp
template <typename T,
        typename = enable_if_t<is_matrix<T>::value
          && !is_sparse_matrix<T>::value>>
inline Magnitude_t<T> one_norm(const T & A);
```

```cpp
template <typename T>
class vector
{
    ...
    template <typename = enable_if_t<std::is_integral<T>::value>>
    vector<T>& operator&=(const T& value); // error
};
```

```cpp
template <typename T>
class vector
{
    template <typename U>
    using is_int = std::is_integral<T>;

    template <typename U, typename = enable_if_t<is_int<U>::value>>
    vector<T>& operator&=(const U& value);
};
```

```
vector<int> v1(3);
vector<double> v2(3);

v1 &= 7;
v2 &= 7.0; // Error: operator disabled
```

```
enable_if_class.cpp:87:7: error: no viable overloaded '&='
v2 &= 7.0; // not enabled
~~^ ~~
enable_if_class.cpp:6:44: note: candidate template ignored:
disabled by 'enable_if' [with U = double]
using enable_if_t = typename std::enable_if<Cond, T>::type;
```

```cpp
template <typename T>
class vector
{
    template <typename U>
    using is_int = integral_constant<bool, is_integral<T>::value
        && is_same<U, T>::value>;
    // ...
}
```

```cpp
template <typename T,
typename = enable_if_t<is_integral<T>::value>>
vector<T>& operator|=(vector<T>& v, const T& mask);
```

```cpp
template <typename T,
typename = enable_if_t<is_integral<T>::value>>
vector<T>& operator++(vector<T>& v);
```

```
matrix_type A = f(...);
permute(A);
lu(A);
normalize(A); ...
```

```
matrix_type A = normalize(lu(permute(f(...))));
```

```cpp
template <typename Matrix>
inline Matrix lu(Matrix&& LU) { ... }
```

```
auto B = normalize(lu(permute(A))); // Overwrites A
```

```cpp
template <typename T>
using rref_only = enable_if_t<!std::is_reference_v<T>>;
```

```cpp
template <typename Matrix, typename = rref_only<Matrix>>
inline Matrix lu(Matrix&& LU, double eps = 0)
{
    using std::abs;
    assert(num_rows(LU) != num_cols(LU));

    for (size_t k = 0; k < num_rows(LU)-1; k++) {
        if (abs(LU[k][k]) <= eps)
            throw matrix_singular{};
        irange r{k+1, imax}; // Interval [k+1, n-1]
        LU[r][k] /= LU[k][k];
        LU[r][r] -= LU[r][k] * LU[k][r];
    }

    return LU;
}
```

```
auto B = lu(A); // Error: no match
```

```
auto B = normalize(lu(permute(clone(A))));
```

```
extern "C" double cubic_root(double);
extern "C" double fifth_root(double);
```

```
extern "C" {
    double cubic_root(double);
    double fifth_root(double);
    ...
}
```

```c
extern "C" {
#include <herberts/good_ole_math_functions.h>
}
```

```cpp
template <typename Value>
class adder
{
    public:
    static Value eval(Value x, Value y) { return x + y; }
};
```

```
int iadder(int x, int y) { return adder<int>::eval(x, y); }
float fadder(float x, float y) { return adder<float>::eval(x, y); }
=> c++03/interoperable.h
```

```
g++ -c interoperable.cpp -o interoperable.o
```

```
#ifdef __cplusplus
extern "C" {
#endif
    int iadder(int x, int y);
    float fadder(float x, float y);
#ifdef __cplusplus
}
#endif
```

```cpp
#include <stdio.h>
#include "interoperable.h"

int main()
{
    printf("iadder(3, 4) = %i.\n", iadder(3, 4));
    printf("fadder(3, 4.2f) = %f.\n", fadder(3, 4.2f));
}
```

```
g++ -o myfluxer myfluxer.cpp -I/opt/include -L/opt/lib -lblas
```

```cpp
#include <glas/glas.hpp>
#include <iostream>

int main()
{
    glas::dense_vector<int> x(2);
    x(0) = 1; x(1) = 2;

    for (int i = 0; i < 3; ++i)
        std::cout << x(i) << std::endl;
    return 0;
}
```

```
> gdb hello
1
2
hello: glas/type/continuous_dense_vector.hpp:85:
T& glas::continuous_dense_vector<T>::operator()(ptrdiff_t) [with T = int]:
Assertion `i<size_' failed.
Aborted
```

```
(gdb) r
Starting program: hello
1
2
hello: glas/type/continuous_dense_vector.hpp:85:
T& glas::continuous_dense_vector<T>::operator()(ptrdiff_t) [with T = int]:
Assertion `i<size_' failed.
Program received signal SIGABRT, Aborted.
0xb7ce283b in raise () from /lib/tls/libc.so.6
(gdb) backtrace
#0 0xb7ce283b in raise () from /lib/tls/libc.so.6
#1 0xb7ce3fa2 in abort () from /lib/tls/libc.so.6
#2 0xb7c2cdf in __assert_fail () from /lib/tls/libc.so.6
#3 0x808048c4e in glas::continuous_dense_vector<int>::operator() (
this=0xbfdfe14, i=2) at continuous_dense_vector.hpp:85
#4 0x808048a82 in main () at hello.cpp:10
(gdb) break 7
Breakpoint 1 at 0x8048a67: file hello.cpp, line 7.
(gdb) rerun
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: hello

Breakpoint 1, main () at hello.cpp:7
7 for (int i=0; i<3; ++i) {
(gdb) step
8 std::cout << x(i) << std::endl ;
(gdb) next
1
7 for (int i=0; i<3; ++i) {
(gdb) next
2
7 for (int i=0; i<3; ++i) {
(gdb) next
8 std::cout << x(i) << std::endl ;
(gdb) print i
$2 = 2
(gdb) next
hello: glas/type/continuous_dense_vector.hpp:85:
T& glas::continuous_dense_vector<T>::operator()(ptrdiff_t) [with T = int]:
Assertion `i<size_' failed.
Program received signal SIGABRT, Aborted.
0xb7cc483b in raise () from /lib/tls/libc.so.6
(gdb) quit
The program is running. Exit anyway? (y or n) y
```

```
==17306== Memcheck, a memory error detector
==17306== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==17306== Using Valgrind-3.10.0.SVN and LibVEX; rerun with -h for copyright info
==17306== Command: vector_test
==17306==
[1,1,2,-3,]
z[3] is -3
w is [1,1,2,-3,]
w is [1,1,2,-3,]
==17306==
==17306== HEAP SUMMARY:
==17306==     in use at exit: 72,832 bytes in 5 blocks
==17306==     total heap usage: 5 allocs, 0 frees, 72,832 bytes allocated
==17306==
==17306== LEAK SUMMARY:
==17306==     definitely lost: 128 bytes in 4 blocks
==17306==     indirectly lost: 0 bytes in 0 blocks
==17306==       possibly lost: 0 bytes in 0 blocks
==17306==     still reachable: 72,704 bytes in 1 blocks
==17306==         suppressed: 0 bytes in 0 blocks
==17306== Rerun with --leak-check=full to see details of leaked memory
==17306==
==17306== For counts of detected and suppressed errors, rerun with: -v
==17306== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

```
valgrind --tool=memcheck -v --leak-check=full \
--show-leak-kinds=all vector_test
```

| 0 | 1 |
|---|---|
| 0.25 | 0.968713 |
| 0.75 | 0.740851 |
| 1.25 | 0.401059 |
| 1.75 | 0.0953422 |
| 2.25 | -0.110732 |
| 2.75 | -0.215106 |
| 3.25 | -0.237847 |
| 3.75 | -0.205626 |
| 4.25 | -0.145718 |
| 4.75 | -0.0807886 |
| 5.25 | -0.0256738 |
| 5.75 | 0.0127226 |
| 6.25 | 0.0335624 |
| 6.75 | 0.0397399 |
| 7.25 | 0.0358296 |
| 7.75 | 0.0265507 |
| 8.25 | 0.0158041 |
| 8.75 | 0.00623965 |
| 9.25 | -0.0000763948 |
| 9.75 | -0.00486465 |

