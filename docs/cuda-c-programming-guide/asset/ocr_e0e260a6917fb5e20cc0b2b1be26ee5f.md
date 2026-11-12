# Example:

```
#include <initializer_list>
__device__ int foo(std::initializer_list<int> in);
__device__ void bar(void)
{
    foo({4,5,6}); // (a) initializer list containing only
    // constant expressions.
    int i = 4;
    foo({i,5,6}); // (b) initializer list with at least one
    // non-constant element.
    // This form may have better performance than (a).
}
```

# F.3.16.3. Rvalue references

By default, the CUDA compiler will implicitly consider `std::move` and `std::forward` function templates to have `__host__ __device__` execution space specifiers, and therefore they can be invoked directly from device code. The nvcc flag `--no-host-device-move-forward` will disable this behavior; `std::move` and `std::forward` will then be considered as `__host__` functions and will not be directly invokable from device code.

# F.3.16.4. Constexpr functions and function templates

By default, a constexpr function cannot be called from a function with incompatible execution space 16. The experimental nvcc flag `--expt-relaxed-constexpr` removes this restriction 17. When this flag is specified, host code can invoke a `__device__` constexpr function and device code can invoke a `__host__ constexpr function`. nvcc will define the macro `__CUDACC_RELAXED_CONSTEXPR__` when `--expt-relaxed-constexpr` has been specified. Note that a function template instantiation may not be a constexpr function even if the corresponding template is marked with the keyword `constexpr` (C++11 Standard Section [dcl.constexpr p6]).

# F.3.16.5. Constexpr variables

Let ‘V’ denote a namespace scope variable or a class static member variable that has been marked constexpr and that does not have execution space annotations (e.g., `__device__`, `__constant__`, `__shared__`). V is considered to be a host code variable.

If V is of scalar type 18 other than `long double` and the type is not volatile-qualified, the value of V can be directly used in device code. In addition, if V is of a non-scalar type then scalar elements of V can be used inside a constexpr `__device__` or `__host__ __device__` function, if the call to the function is a constant expression 19. Device source code cannot contain a reference to V or take the address of V.

16 The restrictions are the same as with a non-constexpr callee function.
17 Note that the behavior of experimental flags may change in future compiler releases.
18 C++ Standard Section [basic.types]
19 C++ Standard Section [expr.const]