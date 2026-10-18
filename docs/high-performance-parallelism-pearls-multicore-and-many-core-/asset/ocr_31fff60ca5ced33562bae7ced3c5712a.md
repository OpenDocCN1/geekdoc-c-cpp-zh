```
/* SCALAR SAXPY */
void saxpy(int n, float a, float* x, float* y)
{
    // n is the number of float elements
    for (int i=0; i<n; i++)    y[i] = a*x[i] + y[i];
}
```

```
/* OpenVec SIMD SAXPY */
void vsaxpy(int n, float a, ov_float* x, ov_float* y)
{
    //nv is the number of SIMD elements
    int const nv = (n-1)/OV_FLOAT_WIDTH + 1;
    for (int i=0; i<nv; i++) y[i] = a*x[i] + y[i];
}
```

# FIGURE 24.2

Scalar SAXPY and OpenVec SIMD SAXPY.

“d,” e.g., ov_alld. On Intel SSE, ARM Neon and IBM Altivec double precision is implemented with the scalar backend since there’s no vector instructions for double precision. On these platforms, the OV_DOUBLE_WIDTH will be one. Never assume OV_DOUBLE_WIDTH to have the same value of OV_FLOAT_WIDTH.

# THE VECTOR TYPE

To avoid overhead, all the implementation is contained in OpenVec header files. To enable OpenVec, the developer must include “openvec.h.” This header file maps OpenVec portable intrinsics to vendor proprietary vector intrinsics. Also it creates proper arithmetic operator definitions if the language is C++.

The OpenVec vector type ov_float creates an instance of OV_FLOAT_WIDTH floats, you declare it like a regular float. For example in ARM Neon, IBM Altivec, and Intel SSE, OV_FLOAT_WIDTH=4 giving four floats per ov_float variable; on Intel IMCI and AVX-512 OV_FLOAT_WIDTH=16; therefore, the ov_float variable contains multiple float elements and all operations are performed on all elements.

The compile time constant OV_FLOAT_WIDTH represents the SIMD width for floats and is defined for each architecture as the number of floats per ov_float type. On the scalar backend, OV_FLOAT_WIDTH=1 and ov_float is defined as type float.