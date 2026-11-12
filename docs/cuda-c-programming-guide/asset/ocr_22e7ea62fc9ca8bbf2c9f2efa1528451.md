| Function | Maximum ulp error |
| :--- | :--- |
| x+y | 0 (IEEE-754 round-to-nearest-even) |
| x*y | 0 (IEEE-754 round-to-nearest-even) |
| x/y | 0 for compute capability ≥ 2 when compiled with -prec-div=true<br>2 (full range), otherwise |
| 1/x | 0 for compute capability ≥ 2 when compiled with -prec-div=true<br>1 (full range), otherwise |
| rsqrtf(x) | 2 (full range) |
| 1/sqrtf(x) | Applies to 1/sqrtf(x) only when it is converted to rsqrtf(x) by the compiler. |
| sqrtf(x) | 0 when compiled with -prec-sqrt=true<br>Otherwise 1 for compute capability ≥ 5.2<br>and 3 for older architectures |
| cbrtf(x) | 1 (full range) |
| rcbrtf(x) | 1 (full range) |
| hypotf(x, y) | 3 (full range) |
| rhypotf(x, y) | 2 (full range) |
| norm3df(x, y, z) | 3 (full range) |
| norm3df(x, y, z) | 2 (full range) |
| norm4df(x, y, z, t) | 3 (full range) |
| rnorm4df(x, y, z, t) | 2 (full range) |
| normf(dim, arr) | An error bound can't be provided because a fast algorithm is used with accuracy loss due to round-off |
| rnormf(dim, arr) | 3 (full range) |
| expf(x) | 2 (full range) |
| exp2f(x) | 2 (full range) |
| exp10f(x) | 2 (full range) |
| expm1f(x) | 1 (full range) |