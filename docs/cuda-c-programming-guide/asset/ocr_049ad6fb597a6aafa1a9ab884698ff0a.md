# F.3.17.2. Variable templates

A __device__ / __constant__ variable template cannot have a const qualified type when using the Microsoft host compiler.

# Examples:

```
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

# F.4. Polymorphic Function Wrappers

A polymorphic function wrapper class template nvstd::function is provided in the nvfunctional header. Instances of this class template can be used to store, copy and invoke any callable target, e.g., lambda expressions. nvstd::function can be used in both host and device code.