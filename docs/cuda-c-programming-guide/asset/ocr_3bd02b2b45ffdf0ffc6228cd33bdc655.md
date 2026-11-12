3. In separate compilation mode, the presence or absence of a definition of a function or variable with external linkage shall not depend on whether `__CUDA_ARCH__` is defined or on a particular value of `__CUDA_ARCH__` 11.

# Example:

```
```cpp
#if !defined( __CUDA_ARCH__ )
void foo(void) { }
// error: The definition of foo()
// is only present when __CUDA_ARCH__
// is undefined
#endif
```
```

4. In separate compilation, `__CUDA_ARCH__` must not be used in headers such that different objects could contain different behavior. Or, it must be guaranteed that all objects will compile for the same compute_arch. If a weak function or template function is defined in a header and its behavior depends on `__CUDA_ARCH__`, then the instances of that function in the objects could conflict if the objects are compiled for different compute arch.

For example, if an a.h contains:

```
```cpp
template<typename T>
__device__ T* getptr(void)
{
#if __CUDA_ARCH__ == 200
return NULL; /* no address */
#else
__shared__ T arr[256];
return arr;
#endif
}
```
```

Then if a.cu and b.cu both include a.h and instantiate getptr for the same type, and b.cu expects a non-NULL address, and compile with:

```
```bash
nvcc -arch=compute_20 -dc a.cu
nvcc -arch=compute_30 -dc b.cu
nvcc -arch=sm_30 a.o b.o
```
```

At link time only one version of the getptr is used, so the behavior would depend on which version is picked. To avoid this, either a.cu and b.cu must be compiled for the same compute arch, or `__CUDA_ARCH__` should not be used in the shared header function.

The compiler does not guarantee that a diagnostic will be generated for the unsupported uses of `__CUDA_ARCH__` described above.

# F.3.3. Qualifiers

# F.3.3.1. Device Memory Space Specifiers

The `__device__`, `__shared__`, `__managed__` and `__constant__` memory space specifiers are not allowed on:

+   class, struct, and union data members,

11 This does not apply to entities that may be defined in more than one translation unit, such as compiler generated template instantiations.