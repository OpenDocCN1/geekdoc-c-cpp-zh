```
//scalar: 40 iterations
for (int i=0; i<40; i++)
z[i] = x[i] + y[i];
```

```
//vector: 10 iterations
for (int i=0; i<40; i+=4)
z[i:i+3] = x[i:i+3] + y[i:i+3];
```

# FIGURE 24.1

Scalar loop with 40 iterations vectorized to 10 iterations, assuming a processor with vector register that can hold 4 scalar elements.

are transformed into a vector instruction that operates on multiple pairs of operands at once, as exemplified in Figure 24.1.

Today, most commodity processors are based on hardware architectures that feature SIMD vector instructions. Intel MMX/SSE/VX/AVX-512, IBM Power AltiVec and Cell SPU, and ARM NEON are examples of instruction sets enabling loop vectorization.

This wide range of hardware implementations makes maintenance of explicit manual vectorization almost impossible across multiple architectures and vendors. The differences can be attributed to multiple factors like:

SIMD width: Intel’s Streaming SIMD Extensions (SSE) supports vectorization of four single-precision floating-point or two double-precision floating-point values. More recently, the Advanced Vector Extensions (AVX) introduced 256-bit registers doubling from the SSE vectorization length to either eight packed single-precision floating-point values or four-packed double-precision floating-point values. Intel’s Initial Many-Core Instructions (IMCI) vector instructions on the Intel® Xeon Phi™ coprocessor have 512-bit vector registers (16-packed single-precision, or 8-packed double-precision values) that are present in the AVX-512 instruction set. AltiVec is also a SIMD instruction set for integer and floating-point vector computations. It features 128-bit registers that allow computations with four-packed 32-bit integers or single-precision floating-point values (IBM Power6 or later) and two-packed 64-bit double-precision floating-point values (IBM Power7 or later). It is important to note that although the register width and the HPC functionality of interest (ADD, MUL, etc.) are basically similar between SSE and AltiVec, the translation between the associated intrinsics can be troublesome. NEON (or Advanced SIMD) is the counterpart of SIMD instruction set devised for ARM-based architectures. Depending on the version, it can support from 8-bit to 64-bit integers and 32-bit single-precision floating point. Its latest versions can process 128-bit (four single-precision floating-point values) in the same execution cycle (for each architecture, see “For more information” at the end of this chapter).

Extended instructions: AVX2 added fused-multiply-add support and nondestructive three-operand instructions that preserve source operands values. Together with IMCI, it also introduced comprehensive support for scatter/gather vector operations.