
Example:

```cpp
inline namespace N1 {
namespace N2 {
__device__ int Gvar;
}
namespace N2 {
__device__ int Gvar;
}
// <-- CUDA compiler inserts reference to "::N2:Gvar" at this point in
// the translation unit. This reference will be considered ambiguous by
// the host compiler and compilation will fail.
```

### F.3.16.6.1. Inline unnamed namespaces

The following entities cannot be declared in namespace scope within an inline unnamed namespace:

- __managed__, __device__, __shared__ and __constant__ variables
- __global__ function and function templates
- variables with surface or texture type

Example:

```cpp
inline namespace {
namespace N2 {
template <typename T>
__global__ void foo(void); // error
__global__ void bar(void) { // error
template <>
__global__ void foo<int>(void) { // error
__device__ int x1b; // error
__constant__ int x2b; // error
__shared__ int x3b; // error
texture<int> q2; // error
surface<int> s2; // error
}
}
```

### F.3.16.7. thread_local

The `thread_local` storage specifier is not allowed in device code.

### F.3.16.8. __global__ functions and function templates

If the closure type associated with a lambda expression is used in a template argument of a `__global__` function template instantiation, the lambda expression must either be defined in the immediate or nested block scope of a `__device__` or `__global__` function, or must be an extended lambda.

Example:

```cpp
template <typename T>
__global__ void kernel(T in) {}

__device__ void foo_device(void)
{
    // All kernel instantiations in this function
    // are valid, since the lambdas are defined inside
    // a <device> function.
    kernel<<<1,1>>>([] __device__ () {});
    kernel<<<1,1>>>([] __host__ __device__ () {});
    kernel<<<1,1>>>([] () {});
}

auto lam1 = [] {};
auto lam2 = [] __host__ __device__ {};

void foo_host(void)
{
    // OK: instantiated with closure type of an extended __device__ lambda
    kernel<<<1,1>>>([] __device__ () {});

    // OK: instantiated with closure type of an extended __host__ __device__
    // lambda
    kernel<<<1,1>>>([] __host__ __device__ () {});

    // error: unsupported: instantiated with closure type of a lambda
    // that is not an extended lambda
    kernel<<<1,1>>>([] () {});

    // error: unsupported: instantiated with closure type of a lambda
    // that is not an extended lambda
    kernel<<<1,1>>>(lam1);

    // error: unsupported: instantiated with closure type of a lambda
    // that is not an extended lambda
    kernel<<<1,1>>>(lam2);
}
```

A __global__ function or function template cannot be declared as constexpr.

A __global__ function or function template cannot have a parameter of type std::initializer_list or va_list.

A __global__ function cannot have a parameter of rvalue reference type.

A variadic __global__ function template has the following restrictions:

- Only a single pack parameter is allowed.
- The pack parameter must be listed last in the template parameter list.

Example:

```cpp
// ok

template <typename...> class Wrapper, typename... Pack>
__global__ void foo(Wrapper<Pack...>);

// error: pack parameter is not last in parameter list
template <typename... Pack, template <typename...> class Wrapper>
__global__ void foo2(Wrapper<Pack...>);

// error: multiple parameter packs
template <typename... Pack1, int... Pack2, template<typename...> class Wrapper1,
          template <int...> class Wrapper2>
__global__ void foo3(Wrapper1<Pack1...>, Wrapper2<Pack2...>);
```

### F.3.16.9. __device__ / __constant__ / __shared__ variables

__device__, __constant__ and __shared__ variables cannot be marked with the keyword constexpr.

### F.3.16.10. Defaulted functions

Execution space specifiers on a function that is explicitly-defaulted on its first declaration are ignored by the CUDA compiler. Instead, the CUDA compiler will infer the execution space specifiers as described in Implicitly-declared and explicitly-defaulted functions.

Execution space specifiers are not ignored if the function is explicitly-defaulted, but not on its first declaration.

Example:

```cpp
struct S1 {
    // warning: __host__ annotation is ignored on a function that
    //          is explicitly-defaulted on its first declaration
    __host__ S1() = default;
};

__device__ void foo1() {
    // note: __device__ execution space is derived for S1::S1
    //        Based on implicit call from within __device__ function
    //        foo1
    S1 s1;
}

struct S2 {
    __host__ S2();
};

// note: S2::S2 is not defaulted on its first declaration, and
//        its execution space is fixed to __host__ based on its
//        first declaration.
S2::S2() = default;

__device__ void foo2() {
    // error: call to __device__ function 'foo2' to
    //        __host__ function 'S2::S2'
    S2 s2;
}
```

### F.3.17. C++14 Features

C++14 features enabled by default by the host compiler are also supported by nvcc. Passing nvcc -std=c++14 flag turns on all C++14 features and also invokes the host preprocessor, compiler and linker with the corresponding C++14 dialect option 20. This section describes the restrictions on the supported C++14 features.

### F.3.17.1. Functions with deduced return type

A __global__ function cannot have a deduced return type.

If a __device__ function has deduced return type, the CUDA frontend compiler will change the function declaration to have a void return type, before invoking the host compiler. This may cause issues for introspecting the deduced return type of the __device__ function in host code. Thus, the CUDA compiler will issue compile-time errors for referencing such deduced return type outside device function bodies, except if the reference is absent when __CUDA_ARCH__ is undefined.

Examples:

```cpp
__device__ auto fn1(int x) {
    return x;
}

__device__ decltype(auto) fn2(int x) {
    return x;
}

__device__ void device_fn1() {
    // OK
    int (*pl)(int) = fn1;
}

// error: referenced outside device function bodies
decltype(fn1(10)) g1;

void host_fn1() {
    // error: referenced outside device function bodies
    int (*pl)(int) = fn1;
}

struct S_local_t {
    // error: referenced outside device function bodies
    decltype(fn2(10)) m1;
    S_local_t() : m1(10) { }
};

// error: referenced outside device function bodies
template <typename T = decltype(fn2)>
void host_fn2() { }

template<typename T> struct S1_t { };

// error: referenced outside device function bodies
struct S1_derived_t : S1_t<decltype(fn1)> { };
```

20 At present, the -std=c++14 flag is supported only for the following host compilers : gcc version >= 5.1, clang version >= 3.7 and icc version >= 17

### F.3.17.2. Variable templates

A __device__ / __constant__ variable template cannot have a const qualified type when using the Microsoft host compiler.

Examples:

```cpp
// error: a __device__ variable template cannot
// have a const qualified type on Windows
template <typename T>
__device__ const T d1(2);

int *const x = nullptr;
// error: a __device__ variable template cannot
// have a const qualified type on Windows
template <typename T>
__device__ T const d2(x);

// OK
template <typename T>
__device__ const T *d3();

__device__ void f() {
    int t1 = d1<int>();

    int *const t2 = d2<int>();

    const int *t3 = d3<int>();
}
```

## F.4. Polymorphic Function Wrappers

A polymorphic function wrapper class template nvstd::function is provided in the nvfunctional header. Instances of this class template can be used to store, copy and invoke any callable target, e.g., lambda expressions. nvstd::function can be used in both host and device code.

Example:

```cpp
#include <nvfunctional>

__device__ int foo_d() { return 1; }
__host__ __device__ int foo_hd() { return 2; }
__host__ int foo_h() { return 3; }

__global__ void kernel() {
    nvstd::function<int()> fn1 = foo_d;
    nvstd::function<int()> fn2 = foo_hd;
    nvstd::function<int()> fn3 = []() { return 10; };
    *result = fn1() + fn2() + fn3();
}

__host__ __device__ void hostdevice_func(int *result) {
    nvstd::function<int()> fn1 = foo_hd;
    nvstd::function<int()> fn2 = []() { return 10; };
    *result = fn1() + fn2();
}

__host__ void host_func(int *result) {
    nvstd::function<int()> fn1 = foo_h;
    nvstd::function<int()> fn2 = foo_hd;
    nvstd::function<int()> fn3 = []() { return 10; };
    *result = fn1() + fn2() + fn3();
}
```

Instances of nvstd::function in host code cannot be initialized with the address of a __device__ function or with a functor whose operator() is a __device__ function. Instances of nvstd::function in device code cannot be initialized with the address of a __host__ function or with a functor whose operator() is a __host__ function.

nvstd::function instances cannot be passed from host code to device code (and vice versa) at run time. nvstd::function cannot be used in the parameter type of a __global__ function, if the __global__ function is launched from host code.
