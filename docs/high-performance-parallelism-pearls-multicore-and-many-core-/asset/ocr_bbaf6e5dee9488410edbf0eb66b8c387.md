| | GNU Compiler Collection | Intel Parallel Composer |
|---|---|---|
| Include File | include <intrin.h> | include <immintrin.h> |
| Intrinsics | m256 a; | m256 a; |
| C/C++ Single | typedef float vsf __attribute__((vector_size (16))); | F32vec8 vsf; |
| C/C++ Double | typedef double vdf __attribute__((vector_size (16))); | F64vec4 vdf; |

# FIGURE 8.9

Vector intrinsic and vector extension in GCC and Intel composer XE 2015.

```
F32vec8 baw_vecopt(F32vec8 S, F32vec8 X, F32vec8 r,
    F32vec8 b, F32vec8 sigma,F32vec8 time);
```

# FIGURE 8.10

Vector routine declaration using vector class in Intel composer XE 2015.

The rest of this section uses Intel vector class wherever possible when we declare and handle the vector data. Figure 8.10 shows the profile of our American pricing function with vector data types.

# VECTOR ARITHMETIC OPERATIONS

One of the benefits of using C++ class syntax is that C/C++ operators, such as + − * /, can easily be overloaded to operate on the vector class. Statements such as:

F32vec8 sigma_sqr = sigma*sigma; work because of C++ operator overloading. However, the vector syntax does not allow mixed scalar vector operation. You cannot write F32vec8 nn_1 = 2.0f*b/sigma_sqr − 1.0f. Nevertheless, the code in Figure 8.11 is perfectly fine.

One of the benefits of using vector classes is that this syntax allows you to mix your code with the intrinsic code if you don’t find the operation you want. In this example, we explicitly use one of the swizzle instructions, vector blend for branch statement.

The benefit of using vector classes, as opposed to intrinsics, is that vector classes rely on the compiler to do instruction selection, while direct intrinsic usage shifts that responsibility to the programmer. Target-dependent instructions such as FMA can be generated automatically when using vector classes, and may have to be explicitly rewritten for each new target when intrinsics have been used.

```
F32vec8 twof = F32vec8(2.0f);
F32vec8 onef = F32vec8(1.0f);
F32vec8 nn_1 = twof*b/sigma_sqr - onef;
```

# FIGURE 8.11

Simple arithmetic operation using vector class in Intel composer XE 2015.