+   - *Intel header*: Intel provides two header-only libraries that contain very basic C++ SIMD types for the Intel Xeon Phi coprocessor (micvec.h) and the Intel Xeon processor (dvec.h). They are supplied as part of Intel Composer.
+   - *VCL / VCLKNC*: A similar implementation is the Vector Class Library (VCL) by Agner Fog. Intel Xeon Phi coprocessor support is provided via VCLKNC, an extension developed by Przemysław Karpiski at CERN.
+   - *Vc*: The Vc project provides a more advanced C++ library. In contrast to the other implementations, its API provides a generic vector type of an abstract SIMD width. Vc also offers a scalar fall-back implementation for architectures without actual SIMD hardware, utility functions for memory management, and vector math functions. Vc is developed at the Goethe University Frankfurt.

Figure 19.14 shows the mapping of the corresponding types of OpenCL and the SIMD libraries. In our OpenCL and OpenMP code, we use an abstract `real_t` and `real_vec_t`. This, in combination with a compile time constant for the actual SIMD width, and another one for switching between single and double precision, makes sure the code remains portable. The Hexcitron benchmark code can be built using any of the three SIMD libraries using a compile time switch.

# FURTHER OPTIMIZING THE OpenMP 4.0 KERNEL

After porting the fully optimized OpenCL kernels with the described pattern, we applied further optimizations that were not possible or beneficial in OpenCL. For the automatically vectorized kernel, we manually permuted the `simd` loop. Moving it from the second to the third level had the highest impact on performance. We also noticed that declaring the buffer pointers with the `restrict` keyword is very important for the efficiency of the generated memory accesses, while it made no difference in the OpenCL kernel. In this context, we also learned that using explicit vectorization, like the `simd` directive, can lead to a completely different compilation result, i.e., performance, compared with just hinting the vectorization potential via `ivdep` to the compiler. It often is a particular combination of directives,

| OpenCL | micvec.h | VCLKNC | Vc | HEOM |
|---|---|---|---|---|
| double4 | F64vec4 | Vec4d | Vc::double_v | real_vec_t |
| double8 | F64vec8 | Vec8d | Vc::double_v | real_vec_t |
| float8 | F32vec16 | Vec16f | Vc::float_v | real_vec_t |
| float16 | F32vec8 | Vec8f | Vc::float_v | real_vec_t |
| ... | ... | ... | ... | ... |

FIGURE 19.14

Vector types of OpenCL and the different C++ SIMD libraries. Only Vc offers types with an abstract size which directly allows for writing portable code that works on different SIMD extensions. In the HEOM code, we defined a single vector type that is mapped to one of the other types at compile time.