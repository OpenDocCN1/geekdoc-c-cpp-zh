On Intel AVX-enabled architectures, the YMM registers (256-bits wide) can be used for parameter passing and results as they have twice the bit width of the XMM registers (which are 128-bits wide). As this uses a nonstandard calling convention, it needs to be carefully specified for the function to affect the function compilation and calls to the function so that parameters and results are placed in YMM registers. To enable usage of YMM registers, the processor(...) clause needs to be added to the declaration directive as shown in Figure 22.12. In this case, the parameter-passing interface is changed to that of a core_4th_gen_avx architecture for this function. Note: this clause needs to be added separately to each function.

As can be seen in Figure 22.14, targeting the core_4th_gen_avx architecture increases the vector length to simdlen = 4 due to the use of the YMM registers to pass parameters. Setting simdlen to anything other than a multiple of what fits in a YMM register does not make sense for efficiency. This means the programmer also needs to update the simdlen(...) clause of the FindPosition() function. The vector report after recompiling the modified sources is shown in Figure 22.13. Note that the correct simdlen = 4 is highlighted in boldface.

```
#pragma omp declare simd uniform (vals)\n    processor(core_4th_gen_avx)
double Interpolate(double x, const point* vals);

#pragma omp declare simd simdlen(4) \
    processor(core_4th_gen_avx)
int FindPosition(double x);
...
```

# FIGURE 22.12

Declaration of specific processor in a vector function.

```
...
remark #15489: --- begin vector function matching report ---
remark #15490: Function call: Interpolate(double, const point *)
    with simdlen=8, actual parameter types:
    (vector,uniform)   [ main.c(56,18) ]
remark #15492: A suitable vector variant was found (out of 2)
    with ymm2, simdlen=4, unmasked, formal parameter
    types: (vector,uniform)
remark #15493: --- end vector function matching report ---
...
```

# FIGURE 22.13

Extending method declarations for uniform calls.