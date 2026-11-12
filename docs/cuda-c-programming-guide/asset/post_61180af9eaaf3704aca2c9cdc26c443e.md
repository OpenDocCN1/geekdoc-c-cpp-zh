
width must be a power-of-2 (i.e., 2, 4, 8, 16 or 32). Results are unspecified for other values.

## B.16.4. Examples

### B.16.4.1. Broadcast of a single value across a warp

```
#include <stdio.h>

__global__ void bead(int arg) {
    int laneId = threadIdx.x & 0x1f;
    int value;
    if (laneId == 0)     // Note unused variable for
        value = arg;     // all threads except lane 0
    value = __shfl_sync(0xffffffff, value, 0); // Synchronize all threads in
    // warp, and get "value" from lane 0
    if (value == arg)
        printf("Thread %d failed.\n", threadIdx.x);
}

int main() {
    bead<<< 1, 32 >>>(1234);
    cudaDeviceSynchronize();
    return 0;
}
```

### B.16.4.2. Inclusive plus-scan across sub-partitions of 8 threads

```
#include <stdio.h>

__global__ void scan4() {
    int laneId = threadIdx.x & 0x1f;
    // Seed sample starting value (inverse of lane ID)
    int value = 31 - laneId;

    // Loop to accumulate scan within my partition.
    // Scan requires log2(n) == 3 steps for 8 threads
    // It works by an accumulated sum up the warp
    // by 2^i, i=0..2.
    for (int i=0; i<=2; i++) {
        // We do the __shfl_sync unconditionally so that we
        // can read even from threads which won't do a
        // sum, and then conditionally assign the result.
        int n = __shfl_up_sync(0xffffffff, value, 1, 8);
        if ((laneId & 7) >= 1)
            value += n;
    }

    printf("Thread %d final value = %d\n", threadIdx.x, value);
}

int main() {
    scan4<<< 1, 32 >>>();
    cudaDeviceSynchronize();
    return 0;
}
```

### B.16.4.3. Reduction across a warp

```
#include <stdio.h>

__global__ void warpReduce() {
  int laneId = threadIdx.x & 0x1f;
  // Seed starting value as Inverse lane ID
  int value = 31 - laneId;

  // Use XOR mode to perform butterfly reduction
  for (int i=16; i>0; i/=2)
    value += __shfl_xor_sync(0xffffffff, value, i, 32);

  // "value" now contains the sum across all threads
  printf("Thread %d final value = %d\n", threadIdx.x, value);
}

int main() {
  warpReduce<<< 1, 32 >>>();
  cudaDeviceSynchronize();
  return 0;
}
```

## B.17. Warp matrix functions

C++ warp matrix operations leverage Tensor Cores to accelerate matrix problems of the form D=A*B+C. These operations are supported on mixed-precision floating point data for devices of compute capability 7.0 or higher. This requires co-operation from all threads in a warp. In addition, these operations are allowed in conditional code only if the condition evaluates identically across the entire warp, otherwise the code execution is likely to hang.

### B.17.1. Description

All following functions and types are defined in the namespace nvcuda::wmma. Sub-byte operations are considered preview, i.e. the data structures and APIs for them are subject to change and may not be compatible with future releases. This extra functionality is defined in the nvcuda::wmma::experimental namespace.

```
template<typename Use, int m, int n, int k, typename T, typename Layout=void>
class fragment;

void load_matrix_sync(fragment<...>& a, const T* mptr, unsigned ldm);
void load_matrix_sync(fragment<...>& a, const T* mptr, unsigned ldm, layout_t layout);
void store_matrix_sync(T* mptr, const fragment<...>& a, unsigned ldm, layout_t layout);
void fill_fragment(fragment<...>& a, const T& v);
void wmma_sync(fragment<...>& d, const fragment<...>& a, const fragment<...>& b, const fragment<...>& c, bool satf=false);
```

### fragment

An overloaded class containing a section of a matrix distributed across all threads in the warp. The mapping of matrix elements into `fragment` internal storage is unspecified and subject to change in future architectures.

Only certain combinations of template arguments are allowed. The first template parameter specifies how the fragment will participate in the matrix operation. Acceptable values for `Use` are:

- `matrix_a` when the fragment is used as the first multiplicand, `A`,
- `matrix_b` when the fragment is used as the second multiplicand, `B`, or
- `accumulator` when the fragment is used as the source or destination accumulators (`C` or `D`, respectively).

The `m`, `n` and `k` sizes describe the shape of the warp-wide matrix tiles participating in the multiply-accumulate operation. The dimension of each tile depends on its role. For `matrix_a` the tile takes dimension `m x k`; for `matrix_b` the dimension is `k x n`, and `accumulator` tiles are `m x n`.

The data type, `T`, may be `__half`, `char`, or `unsigned char` for multiplicands and `__half`, `float`, or `int` for accumulators. As documented in Element Types & Matrix Sizes, limited combinations of accumulator and multiplicand types are supported. The layout parameter must be specified for `matrix_a` and `matrix_b` fragments. `row_major` or `col_major` indicate that elements within a matrix row or column are contiguous in memory, respectively. The `Layout` parameter for an `accumulator` matrix should retain the default value of `void`. A row or column layout is specified only when the accumulator is loaded or stored as described below.

### load_matrix_sync

Waits until all warp lanes have arrived at `load_matrix_sync` and then loads the matrix fragment `a` from memory. `mptr` must be a 256-bit aligned pointer pointing to the first element of the matrix in memory. `ldm` describes the stride in elements between consecutive rows (for row major layout) or columns (for column major layout) and must be a multiple of 16 bytes (i.e., 8 `__half` elements or 4 `float` elements). If the fragment is an `accumulator`, the `layout` argument must be specified as either `mem_row_major` or `mem_col_major`. For `matrix_a` and `matrix_b` fragments, the layout is inferred from the fragment's `layout` parameter. The values of `mptr`, `ldm`, `layout` and all template parameters for `a` must be the same for all threads in the warp. This function must be called by all threads in the warp, or the result is undefined.

### store_matrix_sync

Waits until all warp lanes have arrived at `store_matrix_sync` and then stores the matrix fragment `a` to memory. `mptr` must be a 256-bit aligned pointer pointing to the first element of the matrix in memory. `ldm` describes the stride in elements between consecutive rows (for row major layout) or columns (for column major layout) and must be a multiple of 16 bytes. The layout of the output matrix must be specified as either `mem_row_major` or `mem_col_major`. The values of `mptr`, `ldm`, `layout` and all template parameters for a must be the same for all threads in the warp.

### fill_fragment

Fill a matrix fragment with a constant value `v`. Because the mapping of matrix elements to each fragment is unspecified, this function is ordinarily called by all threads in the warp with a common value for `v`.

### mma_sync

Waits until all warp lanes have arrived at `mma_sync`, and then performs the warp-synchronous matrix multiply-accumulate operation `D=A*B+C`. The in-place operation, `C=A*B+C`, is also supported. The value of `satf` and template parameters for each matrix fragment must be the same for all threads in the warp. Also, the template parameters `m`, `n` and `k` must match between fragments `A`, `B`, `C` and `D`. This function must be called by all threads in the warp, or the result is undefined.

Saturation on integer accumulators will clamp the output to the maximum (or minimum) 32-bit signed integer value. Otherwise, if the accumulation would overflow, the value wraps.

> For floating point accumulators, the `satf` (saturate-to-finite value) mode parameter is deprecated. Using it can lead to unexpected results.

For floating point accumulators, if `satf` (saturate to finite value) mode is `true`, the following additional numerical properties apply for the destination accumulator:

- If an element result is +Infinity, the corresponding accumulator will contain +MAX_NORM
- If an element result is -Infinity, the corresponding accumulator will contain -MAX_NORM
- If an element result is NaN, the corresponding accumulator will contain +0

Because the map of matrix elements into each thread's `fragment` is unspecified, individual matrix elements must be accessed from memory (shared or global) after calling `store_matrix_sync`. In the special case where all threads in the warp will apply an element-wise operation uniformly to all fragment elements, direct element access can be implemented using the following `fragment` class members.

```
enum fragment<Use, m, n, k, T, Layout>::num_elements;
T fragment<Use, m, n, k, T, Layout>::x[num_elements];
```

As an example, the following code scales an `accumulator` matrix tile by half.

```
wmma::fragment<wmma::accumulator, 16, 16, 16, float> frag;
float alpha = 0.5f; // Same value for all threads in warp
...
for(int t=0; t<frag.num_elements; t++)
frag.x[t] *= alpha;
```
