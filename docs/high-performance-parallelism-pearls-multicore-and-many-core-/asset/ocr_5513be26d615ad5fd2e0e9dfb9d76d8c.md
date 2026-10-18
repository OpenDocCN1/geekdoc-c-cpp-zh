# American option approximation
gain using vector extension
(unit: K options/second, 1 thread, 125.9 million options)

![](bbox=[0.16, 0.18, 0.78, 0.35])

# FIGURE 8.20

American option approximation gain on vectorization using C/C++ vector extensions on an Intel Xeon processor.

# VECTORIZATION BY ANNOTATING THE SOURCE CODE: #PRAGMA SIMD

The code vectorization we achieve so far comes from explicit handling of SIMD data types. The programmer can choose either C/C++ vector extensions using high-level language constructs or just the processor intrinsic functions. The programmer has to express the underlying algorithm using the vector syntax that usually results in a rewrite of the original scalar program. The vector code generation is the direct result of using the vector constructs in the program.

An alternate way of achieving code vectorization is by annotation of the original scalar program with high-level language directives such as #pragma. The explicit vector programming is achieved by the programmer using #pragma SIMD directive for the portion of the code to be vectorized. The benefit of #pragma SIMD is that the program does not have to create another vector version of the same program. Neither is there a need to choose or even care about the instructions for the vector program. The compiler analyzes the serial program and the vector directives and generates vector code on programmer’s behalf. In our example, the code annotation occurred at the caller for the scalar optimized routines, as in Figure 8.21.

To ensure the compiler can vectorize the code, the program has to tell the compiler what to do when a function call happens. The vectorizer inside the compiler has two choices. Either inline the function or find a version of the same function that takes the vector parameters. In our case, we inline the function call to baw_scalaroopt and also to a few other functions that it calls that we defined. Runtime library functions such as expf(x), logf(x), and sqrtf(x) all have their counter parts with vector parameters.

Source listing in Figure 8.22 shows how custom defined functions and runtime functions are used in annotation based vector programming.

# C/C++ VECTOR EXTENSION VERSUS #PRAGMA SIMD

In this section, we show two distinctive styles of explicit vector programming: C/C++ vector extensions and #pragma SIMD. Both result in SIMD instruction taking advantage of the vector processing unit in the modern microprocessors. But they are uniquely different. With the C/C++ vector extensions, you