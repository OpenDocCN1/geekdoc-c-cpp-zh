```
fsize_mat_vec_mult_cm<Matrix>::my_rows-1,
    Cols-1>()(A, v_in, v_out);
v_out[0]+= A[0][Cols] * v_in[Cols];
};
}
```

The partial specialization for column 0 must also initialize the entry of the output vector:

```
template <int Rows>
struct fsize_mat_vec_mult_cm<Rows, 0>
{
    template <typename Matrix, typename VecIn, typename VecOut>
    void operator()(const Matrix& A, const VecIn& v_in, VecOut& v_out)
    {
        fsize_mat_vec_mult_cm<Rows-1, 0>()(A, v_in, v_out);
        v_out[Rows] = A[Rows][0] * v_in[0];
    }
};
```

Finally, we still need a specialization for row and column 0 to terminate the recursion. This can be reused from the previous functor:

```
template <>
struct fsize_mat_vec_mult_cm<0, 0>
{
    : fsize_mat_vec_mult_cm<0, 0> {};
};
```

Note that we perform the same operation on different data from which SIMD architectures can benefit. SIMD stands for Single Instruction, Multiple Data. Modern processors contain SSE units that perform arithmetic operations simultaneously on multiple floating-point numbers. To use these SSE commands, the processed data must be aligned and contiguous in memory and the compiler must be aware of it. In our examples, we did not address the alignment issue, but the unrolled code makes it clear that identical operations are executed on contiguous memory.

# 5.4.2.2 Using Registers

Another feature of modern processors that we should keep in mind is cache coherency. Processors are nowadays designed to share memory while retaining consistency in their caches. As a result, every time we write a data structure in memory like our vector w, a cache invalidation signal is sent to other cores and processors. Regrettably, this slows down computation perceptively.

Fortunately, the cache invalidation bottleneck can be avoided in many cases, simply by introducing temporaries in functions that reside in registers when the types allow for it. We can rely on the compiler to make good decisions where temporaries are located. C++03 had the keyword register. However, it was a mere hint and the compiler was not obliged to store variables in registers. Especially when a program is compiled for a target platform that was not considered in the development process, it would do more harm than good if the register use was mandatory. Thus, the keyword was deprecated in C++11 given that compilers have pretty good heuristics to locate variables platform-dependently without help from the programmer.