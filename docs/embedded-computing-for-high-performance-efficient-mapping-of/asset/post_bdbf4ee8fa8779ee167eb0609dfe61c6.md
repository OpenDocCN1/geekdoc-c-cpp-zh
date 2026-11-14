
```
for (i = 0; i < 100; i++) {
    z[i] = x[i] * y[i];
}
```

Assume arrays x, y, and z are 32-bit single precision arrays, and the CPU supports 128-bit SIMD registers. Without vectorization, the scalar multiplication instruction is executed 100 times, using only 1/4 of each SIMD register:

| x[] | empty | empty | empty |
|---|---|---|---|
| y[] | empty | empty | empty |
| z[] | empty | empty | empty |

With vectorization, all SIMD registers are used to perform four multiplications at once in a single vector instruction:

| x[i] | x[i+1] | x[i+2] | x[i+3] |
|---|---|---|---|
| y[i] | y[i+1] | y[i+2] | y[i+3] |
| z[i] | z[i+1] | z[i+2] | z[i+3] |

Hence, in our earlier example, we only need to execute 25 multiply instructions instead of the original 100 instructions, thus increasing the performance of this loop.

In C/C++, developers can manually perform the vectorization process by translating the selected code into a sequence of assembly vector instructions, or by using intrinsic functions (e.g., for SSE) provided by some compilers. These intrinsic functions include a set of C functions and associated data types providing direct access to vector instructions. Unfortunately, vectorizing by hand requires considerable effort and results in unreadable, unportable, and unmaintainable code. For this reason, it is far more convenient to allow compilers to perform the vectorization process automatically.

## ASSEMBLY AND INTRINSIC FUNCTIONS

The C programming language allows to embed assembly code using asm (or "__asm__") statements as in the following example:

```
asm("ADD x, x, #1\n" "MOV y, x\n");
```

or

```
asm {
    ADD x, x, #1
    MOV y, x
}
```

Another way is the use of intrinsic functions (also known as _intrinsics_). An intrinsic function is a function that is handled by the compiler in a special fashion, e.g., substituting it by a sequence of assembly instructions. Following are examples of intrinsics in C code targeting an ARM CPU.*
*https://gcc.gnu.org/onlinedocs/gcc-4.6.1/gcc/ARM-NEON-Intrinsics.html.

```
s1 = vld1_s16(s1+1);
c1 = vld1_s16(c+1);
o = vnal_s16(s1, c1);
```

When auto-vectorization is enabled, compilers analyze the code to verify whether vectorization can be performed such that the code generated is correct with respect to the original scalar version. Further analysis determines whether vectorization is profitable. For instance, if the compiler performs noncontiguous memory accesses, then vectorization may not be beneficial. To support vectorization, the compiler may need to apply a set of transformations, such as loop peeling and loop unrolling (see Chapter 5).

Although the auto-vectorization process has improved considerably over the years, the level of support and efficiency is not consistent across different C/C++ compilers. Some compilers are still not able to vectorize code if it does not conform to specific idioms or style, thus requiring manual effort to make the code more amenable to auto-vectorization.

The compiler options presented in Table 6.2 control the auto-vectorization process for popular C compilers, namely, GNU C Compiler (GCC) [11], Intel C Compiler (ICC) [12], and CLANG/LLVM [13]. As can be seen, each compiler has its own set of options to control auto-vectorization. For instance, auto-vectorization can be enabled implicitly when specifying a high optimization level (-O2 or -O3) or can be enabled explicitly (e.g., -free-vectorize). There are also options to disable auto-vectorization and to report how auto-vectorization was applied to each loop.

## Table 6.2 Options to control auto-vectorization for three C compilers (assuming x86 targets)

| Option | GCC | ICC | CLANG/LLVM |
| :--- | :--- | :--- | :--- |
| Version | 4.9.4 | 17.0 | 3.9 |
| Enabling vectorization | -O3 or -ftree-vectorize | -O2 or -vec | (enabled by default) |
| Disabling vectorization | -fno-tree-vectorize | -no-vec | -fno-vectorize |
| Vectorization report | -fopt-info-vec and -fdump-tree-vect-details | -vec-report=[n] | -Rpass-missed=loop-vectorize and -Rpass-analysis=loop-vectorize |

Depending on the verbose level used, if the loop was not vectorized, developers are informed what prevented the loop from being vectorized so that they can revise the code accordingly. In addition to compiler options, developers can also provide hints to the auto-vectorization process using code annotations.

The following are general guidelines applicable to all the aforementioned compilers to improve the chances of a loop being auto-vectorized:

- 1. Loop count. The number of loop iterations should be constant and preferably known at compile time.
- 2. Control flow. The loop body should have one entry point and one exit point. Furthermore, it is advisable to not include control statements, such as conditionals (e.g., if statements). However, some conditionals may be removed automatically by the compiler using predication, where control statements (e.g., if ( c ) { y=f(x); } else { y=g(x); } ) are converted to predicated expressions (e.g., y = c ? f(x) : g(x)).
- 3. Function calls. Function calls also prevent vectorization unless the compiler supports vectorized versions of these functions. These usually include math functions, supporting single and double precision, such as sin(), pow(), and round().
- 4. Data dependencies. Since each SIMD instruction operates on data elements from multiple iterations at once, the vectorization process must ensure this order change maintains the result of the original scalar version. For this purpose, the compiler must compute the dependences between loop iterations and ensure there are no read-after-write and write-after-write loop-carried dependences that prevent vectorization. Note that compilers can vectorize code with dependences when reduction idioms are detected, e.g., sum = sum + k[i].
- 5. Memory accesses. Vectorizing can be more efficient if memory load instructions access contiguous memory addresses, allowing a single SIMD instruction to load them directly, rather than using multiple load instructions.

Overall, these guidelines aim at ensuring that each data lane associated with a loop iteration executes the same set of operations, thus allowing them to be executed in parallel. Let us consider the following loop, which infringes the earlier guidelines, thus preventing auto-vectorization:

```
void no_vec(int a[]) {
    for (int i = 1; i < 100; i++) {
        a[i] = a[i-1]*2;
        if (a[i] == 100.0) {
            a[i] = f(a[i]);
            break;
        }
    }
}
```

First, the loop has a read-after-write dependence between consecutive iterations (a[i] and a[i-1]). Second, the break statement inside the if statement implies the loop count is unknown and there is more than one loop exit point. Finally, there is a call to a function f.

There are other techniques which can be applied manually to enhance the applicability of the auto-vectorization of loops (see, e.g., Refs. [11–13]), including: (a) using loop indices in array accesses instead of pointers or pointer arithmetic, (b) minimizing indirect addressing in array accesses, (c) aligning data structures to 16 byte boundaries (SSE instructions) or 32 byte boundaries (AVX instructions), (d) favoring the use of structures of arrays (SoA) over arrays of structures (AoS).

While the auto-vectorization process is performed at compile time, not all information may be available when compiling. For instance, the compiler might not know whether two pointers reference the same memory position inside a loop, thus creating a dependence and preventing vectorization. In this case, the compiler may generate a vectorized and a nonvectorized version, and invoke one of them at runtime depending on the addresses of the pointers (see Chapter 5).

## MEMORY ALIGNMENT

Memory alignment is important as it allows the concurrent execution of load/store operations from/to successive memory positions.

Alignment support for dynamically allocated memory is provided by specific functions (see the following examples), such as aligned_alloc and _aligned_malloc for Linux and Windows, respectively.

```
float *c = (TYPE *) aligned_alloc(16, sizeof(float) * N);
float *c = (TYPE *) aligned_malloc(16, sizeof(float) * N);
```

In case of a static memory allocation of array variables, it is common to provide support via attributes as depicted in the following example.

```
float c[LEN] __attribute__((aligned(16)));
```

Additional alignment information can be conveyed via the use of special built-in functions to instruct the compiler to assume aligned data as in the following example.

```
TYPE_OF_ARG *c1 = __builtin_assume_aligned (arg, 16);
```
*http://www.gnu.org/software/libc/manual/html_node/Aligned-Memory-Blocks.html.

Regarding the implementation of auto-vectorization, we can distinguish two general techniques, namely, loop level and block level. Consider the following code:

```
for (i = 0; i < 512; i++)
D[i] = A[i]+B[i]*C[i];
```

With the loop-level vectorization technique, the compiler first determines whether the loop can be vectorized. Then, it performs loop stripmining by a factor
