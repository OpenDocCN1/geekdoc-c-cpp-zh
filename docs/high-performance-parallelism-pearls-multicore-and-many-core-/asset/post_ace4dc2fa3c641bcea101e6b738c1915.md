
These functions return an ov_maskf type, which is architecture dependent; do not assume the size of ov_maskf to be equal to the size of ov_floatf. The next section will present an optimization to avoid execution of a masked code in certain conditions.

## TO MASK OR NOT TO MASK?

What if only a few elements go to the else path? Imagine a loop that must handle the points in the edges of the data, this is very common on numeric simulations with special conditions on the borders of the simulation models. In these cases, the exception code is usually the else block, and it will be executed only at a few points at the border. If we do a simple masked vectorization, as done in previous section, many compute cycles will be wasted computing the else block and applying and merging masks, especially if the else code block has more calculations than the if.

OpenVec provides a simple but powerful way to optimize for a divergent path inside a SIMD vector: comparison reduction functions. For example, we can use the comparison reduction function ov_allf to detect if all comparisons are TRUE, the f suffix means float, this function will accept a float mask from a comparison expression like vector_a < vector_b or from a comparison function like ov_ltf. If all elements inside the SIMD vector evaluate to TRUE, they follow the same code path and there’s no need to apply an expensive MASK merge of two code paths. We use the slower masked code only on the corner cases. Figure 24.9 shows an optimized version of the code from Figure 24.7 using a comparison reduction function:

Different than the functions to obtain a mask, the comparison reduction functions will return a single answer to all elements of the SIMD vector, a single TRUE or FALSE that can be used in conjunction

```
for (int i=0; i<n; i+=OV_FLOAT_WIDTH)
{
    ov_float const vx=ov_ld f(&x[i]); // load x and y
    ov_float const vy=ov_ld f(&y[i]);
    ov_float result;
    /* no apply MASK involved, no compute of else block */
    if (ov_allf(vx>vy)) result = vx-vy;
    /* If not all elements, then use slow masked version*/
    else result = ov_conditionalf(vx>vy, vx-vy, vy+vx);
    ov_stf(&simd_result[i], result); // Store the results
}
```

### FIGURE 24.9

IF/ELSE vectorization optimization.

with an if statement, as shown in the example by the comparison reduction function ov_allf. Do not make the assumption that TRUE is integer 1 and FALSE is integer 0, for optimization reasons we keep architecture-dependent types the only valid assumption that will work in conjunction with if/else statements. Here are the reduction comparison functions:

```
ov_allf(mask) TRUE if all mask elements are true
ov_anyf(mask) TRUE if at least one mask element is true
```

We have variations for comparison to zero value because in some architectures this comparison is faster and is accomplished testing only the sign bits using dedicated instructions such as the SSE _mm_movemask_ps. These functions receive an ov_float vector and return a single answer. Here is a list of reduction comparison to zero functions:

```
ov_any_lt_0f(x) TRUE if at least one element <0.0f
ov_any_ge_0f(x) TRUE if at least one element >= 0.0f
ov_all_lt_0f(x) TRUE if all elements are <0.0f
ov_all_ge_0f(x) TRUE if all elements are >= 0.0f
```

## HANDLING VECTOR TAILS

Up to now, all loop examples go from 0 to n-1, jumping OV_FLOAT_WIDTH elements every step, but what happens if n is not multiple of OV_FLOAT_WIDTH ? More elements will be done exceeding the upper limit n-1, to be more precise, n modulo OV_FLOAT_WIDTH more elements.

If you allocate memory with ov_malloc, it will allocate an extra tail of OV_FLOAT_WIDTH elements and if n is the total size of your array, then you code the loops like previous examples and it will work fine, the extra elements will be written to the extra allocated memory.

But if you are not updating the whole array in your loop or you need to exit your loop at exactly element length, than you have to code your loop twice, the first loop will handle the upper limit that’s multiple of the SIMD size, and the second loop will be a scalar code loop to handle the remaining tail, the tail trip count will be always smaller than OV_FLOAT_WIDTH.

You can try to avoid making your grid first dimension (the dimension that runs faster in memory) multiple of OV_FLOAT_WIDTH, also if done that will keep the proper alignment constrains to get optimized code.

If you cannot avoid handling the vector tail, Figure 24.10 shows an array copy example handling a vector tail.

The first loop subtracts OV_FLOAT_TAIL from the upper limit, which will cause the next element to be done be multiple of OV_FLOAT_WIDTH and under the upper limit. The second loop will take the remaining elements (vector tail).

The provided constant OV_FLOAT_TAIL is equal OV_FLOAT_WIDTH minus one.

The compile time optimization with macro #if, creating the first loop only on SIMD sizes greater than one is not mandatory.

## MATH REDUCTIONS

Sometimes you need to do operations with elements inside the vector type, like adding up all elements. OpenVec provides reductions functions like ov_all_sumf that takes one ov_float vector and returns a single float with the sum. Figure 24.11 shows a code to add all elements of one array:

```
void memcpy_f(float *dst, float*src, int upperLimit)
{
    // upperLimit is not always multiple of OV_FLOAT_WIDTH
    int i=0; /* first element */

    /* First loop: multiple of OV_FLOAT_WIDTH elements */
#if OV_FLOAT_WIDTH > 1
    /* Loop below won't be compiled in the scalar backend */
    for (; i<upperLimit -OV_FLOAT_TAIL ; i+=OV_FLOAT_WIDTH)
    {
        ov_float vx = ov_ldf(&src[i]);
        ov_stf(&dst[i], vx);
    }
#endif

    /* Second loop goes up to upper limit
        it's regular scalar code */
    for (; i<upperLimit; i++) dst[i]=src[i];
}
```

### FIGURE 24.10

Handling vector tails.

The results may get different compared to scalar sum because the order your sum floats will interfere in the final result, e.g., adding a huge value to a tiny value, the tiny value won’t contribute to the sum.

In the current implementation, math reduction functions are not optimized for each architecture, we provide only scalar code for all architectures. However, since these functions are usually called only once for the trailing elements that are less than vector width, the performance impact should be small for large arrays. Here are math reduction functions:

```
/* n is not always multiple of OV_FLOAT_WIDTH */
float vsum=0.0f; /* Total sum = 0 scalar */
i=0; /* first loop element */
#if OV_FLOAT_WIDTH > 1
/* In the scalar backend this LOOP won't be compiled */
ov_float tmp=ov_zero; // Vector temp sum = {0,0,...,0}
for (; i<n-OV_FLOAT_TAIL; i+=OV_FLOAT_WIDTH)
{
    ov_float vx = ov_ldf(&x[i]);
    tmp = ov_addf(tmp, vx); // Add SIMD elements per step
}
vsum = ov_all_sumf(tmp); /* Reduction function */
#endif

/* Second loop handles the tail going up to n
   it's regular scalar code */
for (; i<n; i++) vsum += x[i];
```

**FIGURE 24.11**

Math reduction.

- ov_all_sumf(x) Sum all SIMD elements
- ov_all_prodf(x) Multiplies all SIMD elements
- ov_all_maxf(x) Returns maximum element
- ov_all_minf(x) Returns minimum element

## COMPILING OpenVec CODE

To use OpenVec, the developer must include “openvec.h” header file; no library is needed. It auto detects the target architecture based on compiler flags, if you want to override auto-detection, use -D_OV_NOAUTO plus the desired architecture macro. Figure 24.12 shows compiler flags and correspondent override macro flags.

| Override macro flags | Architecture | Compiler | Target flag |
|---|---|---|---|
| `-D_OV_NOAUTO -D_OV_MIC` | Intel KNC KNF | Intel C++ | `-m mic` |
| `-D_OV_NOAUTO -D_OV_AVX` | Intel AVX | Intel C++ | `-xAVX` |
| `-D_OV_NOAUTO -D_OV_AVX2` | Intel AVX 2 | Intel C++ | `-xCORE-AVX2` |
| `-D_OV_NOAUTO -D_OV_AVX512` | Intel AVX 512 | Intel C++ | `-xCORE-AVX512` |
| `-D_OV_NOAUTO -D_OV_AVX` | Intel AVX | g++/llvm | `-mavx` |
| `-D_OV_NOAUTO -D_OV_AVX2` | Intel AVX 2 | g++/llvm | `-mavx2` |
| `-D_OV_NOAUTO -D_OV_SSE` | Intel SSE | g++/llvm | `-msse` |
| `-D_OV_NOAUTO -D_OV_SSE4` | Intel SSE4 | g++/llvm | `-msse4` |
| `-D_OV_NOAUTO -D_OV_SSE` | Intel SSE | Intel C++ | `-xSSE` |
| `-D_OV_NOAUTO -D_OV_SSE4` | Intel SSE4 | Intel C++ | `-xSSE4.1` |
| `-D_OV_NOAUTO -D_OV_NEON` | ARM Neon | g++/llvm | `-mfpu=neon` |
| `-D_OV_NOAUTO -D_OV_NEON` | ARM Neon 64 bit | g++/llvm | — |
| `-D_OV_NOAUTO -D_OV_ALTIVEC` | IBM Altivec | g++ | `-mvsx -maltivec` |
| `-D_OV_NOAUTO` | Any (scalar) | Any | Any |

### FIGURE 24.12

Compiler flags.

In all of our tests auto-detection worked fine so we found no need to use override macro flags. With the Intel Parallel Studio Compiler suite, you can use -xHOST to get the highest architecture set optimization for the machine that’s compiling the code.

OpenVec is C89 compliant but some provided C examples use loop initial declarations which require the -std=c99 flag. The macro ov_restrict is defined and works as a C99 restrict modifier, so it can be used both in C and C++ codes.

## REAL-WORLD EXAMPLE

Modern seismic acoustic imaging techniques like reverse time migration (RTM) and full waveform inversion are based on computing finite difference (FD) to model and generate the image of geological volumes, which in turn are used to find new reserves of oil and gas. Hence, optimizing this type of computations leads to performance improvements in seismic imaging processing.
