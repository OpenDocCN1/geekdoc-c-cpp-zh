```
void vsaxpy(int n, float a, ov_float* x, ov_float* y)
{
    int const nv = (n-1)/OV_FLOAT_WIDTH + 1;
    for (int i=0; i<nv; i++)
        y[i] = a*x[i] + y[i]; // Implicit LD/ST
}
```

```
void vsaxpy(int n, float a, float* x, float* y)
{
    // Where n is the number of floats
    // Jump to next vector address: +OV_FLOAT_WIDTH
    for (int i=0; i<n; i+=OV_FLOAT_WIDTH)
    {
        ov_float vy = ov_ldf(&y[i]); // Explicit LOAD
        ov_float vx = ov_ldf(&x[i]); // Explicit LOAD
        vy = a*vx + vy;
        ov_stf(&y[i], vy); // Explicit store
    }
}
```

# FIGURE 24.5

Implicit and explicit load/stores.

vector type will be defined as float32x4_t and on the Intel AVX type it will be __m256. To give an idea on the implementation simplicity, the AVX header file has less than a hundred lines of codes to define the single-precision implementation. One of the goals of this project is to easily add new architectures and customization.

Power users can modify or create new platforms to match their applications and precision needs keeping the code portable. For example, ARM NEON does not have native SIMD division, so one can define division as:

```
#define ov_div(x,y) ov_mulf(x, ov_rcpf(y)) // x * (1/y)
```

which can be faster but less precise than the provided version for ARM NEON. Note that as illustrated by this example, users can customize OpenVec for variable precision.