The solution is a hybrid SoA or AoSoA layout. Figure 19.2 shows all three layouts by ways of declaring them. The size of the inner array is set to the SIMD width or a small multiple of it. The hybrid SoA layout is long known to combine locality when accessing different structure elements with contiguous iteration over the corresponding elements of multiple structures. In fact, it is already mentioned in the IA-32 Intel® Architecture Optimization Reference Manual from 1999, but rarely found in the wild. It is a generalization which collapses to SoA if the outer array size is one, and to AoS if the inner size is one. With the major fraction of today’s and tomorrow’s processor’s FLOPS coming from SIMD hardware of growing width, hybrid SoA becomes more relevant than ever to achieve contiguous vector loads/stores.

The Hexcitron benchmark code uses no explicit data structures. Instead the layout is applied with a set of index computations that work on a large buffer of floating point elements. The original and the optimized memory layout are shown in Figure 19.3. This allows a memory layout exchange by swapping the index computations without modifying the application’s arithmetic code. Figures 19.4 and 19.5 show the relevant parts of the host and kernel code for both automatic and manual vectorization.

```
// AoS
struct data_t {
  type_t elem;
  // ...
};
data_t data[N];

// SoA
struct data_t {
  type_t elem[N];
  // ...
};
data_t data;

// AoSoA or hybrid SoA
struct data_t {
  type_t elem[VEC_LEN];
  // ...
};
data_t data[N/VEC_LEN];
```

# FIGURE 19.2

The different memory layouts declared as their name implies for a buffer data.

![](bbox=[0.12, 0.55, 0.92, 0.78])

# FIGURE 19.3

Memory accesses to matrix elements that result from the outer loop vectorization scheme of OpenCL for the Hexcitron kernel (for an SIMD width of eight). The original SoA memory layout leads to noncontiguous gather/scatter operations. The improved interleaved AoSoA layout results in fully contiguous memory accesses. Not shown: real and imaginary parts of complex numbers are separated into two adjacent blocks of eight elements.