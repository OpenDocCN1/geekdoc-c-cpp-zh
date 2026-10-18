percentage of the peak performances of up to 36%. The over-all speedups are 2.9× on the Intel Xeon processor and 6.4× on the Intel Xeon Phi coprocessor. The performance gain for the Intel Xeon Phi coprocessor over a dual Sandy Bridge and a dual Haswell Intel Xeon processor is 2.1× and 1.5×, respectively.

Many optimization techniques have interacting effects, which means after successfully applying one optimization, previously failed approaches could become beneficial again and have to be retried. This process, especially with directive-based vectorization can be very unsatisfying. Manual vectorization using vector types offers a straight-forward and abstract way of implementing efficient code for SIMD architectures and offers multiple advantages such as compiler independence and a higher level of control. It is important to write such codes for an abstract SIMD width in order to keep the code portable. Using manual vectorization should at least be taken into consideration whenever writing new code or rewriting major portions of legacy code.

The most important lesson learned here is that not vectorization alone, but only the combination of vectorization and an optimized memory layout for the resulting access pattern are the foundation for performance on today’s and tomorrow’s multicore and many-core processors. Additionally, the use of compile time constants to specialize kernels for specific input instances can significantly improve performance by enabling better compiler optimization.

We will continue our work on the GPU-HEOM code with the remaining kernels. Currently, we are working on a generalization and automatization of the OpenCL to OpenMP transition, and hope to find an elegant equivalent to OpenCL’s runtime kernel compilation. Either by including multiple precompiled kernels into the binary or by actually building and linking in kernels at runtime.

# ACKNOWLEDGMENTS

This work was supported by the German Research Foundation (DFG projects RE 1389/8, KR 2889/7) and the Intel Parallel Computing Center at ZIB. We would like to thank Tobias Kramer and Christoph Kreisbeck, the authors of the GPU-HEOM code, and our colleagues at Intel for the productive cooperation, especially Chris J. Newburn, Georg Zitzlsberger, and Serguei Preis.

# FOR MORE INFORMATION

The C++ SIMD libraries can be downloaded at:

+   - VCL: http://www.agner.org/optimize/#vectorclass
+   - VCLKNC: https://bitbucket.org/vec libknc/vclknc
+   - Vc: http://code.compeng.uni-frankfurt.de/projects/vc

The following papers and technical documents provide more detailed insights in the topics discussed in this chapter.

+   - Advanced Micro Devices, Inc., AMD Accelerated Parallel Processing OpenCL Programming Guide: Revision: 2.7.
+   - Intel Corporation., Intel™ SDK for OpenCL Applications XE 2013 R2, Optimization Guide.