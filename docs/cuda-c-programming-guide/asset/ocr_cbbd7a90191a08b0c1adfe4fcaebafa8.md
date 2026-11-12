must be a multiple of 16 bytes. The layout of the output matrix must be specified as either `mem_row_major` or `mem_col_major`. The values of `mptr`, `ldm`, `layout` and all template parameters for a must be the same for all threads in the warp.

# fill_fragment

Fill a matrix fragment with a constant value `v`. Because the mapping of matrix elements to each fragment is unspecified, this function is ordinarily called by all threads in the warp with a common value for `v`.

# mma_sync

Waits until all warp lanes have arrived at `mma_sync`, and then performs the warp-synchronous matrix multiply-accumulate operation `D=A*B+C`. The in-place operation, `C=A*B+C`, is also supported. The value of `satf` and template parameters for each matrix fragment must be the same for all threads in the warp. Also, the template parameters `m`, `n` and `k` must match between fragments `A`, `B`, `C` and `D`. This function must be called by all threads in the warp, or the result is undefined.

Saturation on integer accumulators will clamp the output to the maximum (or minimum) 32-bit signed integer value. Otherwise, if the accumulation would overflow, the value wraps.

> For floating point accumulators, the `satf` (saturate-to-finite value) mode parameter is deprecated. Using it can lead to unexpected results.

For floating point accumulators, if `satf` (saturate to finite value) mode is `true`, the following additional numerical properties apply for the destination accumulator:

+   - If an element result is +Infinity, the corresponding accumulator will contain +MAX_NORM
+   - If an element result is -Infinity, the corresponding accumulator will contain -MAX_NORM
+   - If an element result is NaN, the corresponding accumulator will contain +0

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