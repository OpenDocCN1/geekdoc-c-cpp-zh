Example:

```
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
```

# F.3.16.6.1. Inline unnamed namespaces

The following entities cannot be declared in namespace scope within an inline unnamed namespace:

+   - __managed__, __device__, __shared__ and __constant__ variables
+   - __global__ function and function templates
+   - variables with surface or texture type

Example:

```
```cpp
inline namespace {
namespace N2 {
template <typename T>
__global__ void foo(void); // error
__global__ void bar(void) ( // error
template <>
__global__ void foo<int>(void) ( // error
__device__ int x1b; // error
__constant__ int x2b; // error
__shared__ int x3b; // error
texture<int> q2; // error
surface<int> s2; // error
}
```
```

# F.3.16.7. thread_local

The `thread_local` storage specifier is not allowed in device code.

# F.3.16.8. __global__ functions and function templates

If the closure type associated with a lambda expression is used in a template argument of a `__global__` function template instantiation, the lambda expression must either be defined in the immediate or nested block scope of a `__device__` or `__global__` function, or must be an extended lambda.