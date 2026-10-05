# 4.2. Optimizing memory access

The cache is too small to hold 8 GB data. So none of the load instructions will hit the cache. Every byte accessed by sum() must be loaded from memory.

Each double is 8 bytes, if the function sum() takes c cycles to execute, we may take the bandwidth to memory to be 8n/c bytes per cycle. The bandwidth to memory on a 2.66 GHz SSE2 machine (see table A1 for the full names of the machines) was measured to 4.36 bytes per cycle, or equivalently, 11.6 GB/s. On a more recent 2.20 GHz AVX machine, the bandwidth was 5.40 bytes per cycle or 11.9 GB/s.

We use strided memory accesses to lead up to what is perhaps the most important item a programmer should know about accessing memory. The following function sums entries of the array[], beginning with the zeroth entry and in steps of length

```
double sumstride(double *restrict a, long int n,
    int stride){
    double s = 0;
    for(long int i=0; i < n; i+=stride)
        s += a[i];
    return s;
}
```

The bandwidth to memory realized in strided access is

| 8n |
| c × stride |

assuming the function takes c cycles.

Before we begin making measurements with non-unit strides, it is a good idea to try stride=1. It turns out that sumstride realizes a bandwidth of only 2.4 bytes cycle on the SSE2 machine for unit stride, which is well short of the 4.36 bytes per cycle realized by sum(). Evidently, the compiler is not optimizing as well when stride is passed as a parameter.

We make the stride a const int to coax the compiler to optimize better. For unit stride, we use the definition

```
const int STR=1;
```