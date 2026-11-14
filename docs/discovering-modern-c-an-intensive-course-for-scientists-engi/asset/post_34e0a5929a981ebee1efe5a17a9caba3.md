
A matrix multiplication is easily implemented with three nested loops. One of the six possible ways of nesting is a dot-product-like calculation for each entry from C:

$c_{ik} = A_i \cdot B^k$

where $A_i$ is the i-th row of A and $B^k$ the k-th column of B. We use a temporary in the innermost loop to decrease the cache-invalidation overhead of writing to C's elements in each operation:

```cpp
template <typename Matrix>
inline void mult(const Matrix& A, const Matrix& B, Matrix& C)
{
    assert(A.num_rows() == B.num_rows()); // ...
    typedef typename Matrix::value_type value_type;
    unsigned s = A.num_rows();
    for (unsigned i = 0; i < s; ++i)
        for (unsigned k = 0; k < s; k++) {
            value_type tmp(0);
            for (unsigned j = 0; j < s; j++)
                tmp += A(i, j) * B(j, k);
            C(i, k) = tmp;
        }
}
```

For this implementation, we provide a backward-compatible benchmark in Appendix A.9.6. The run time and performance of our canonical implementation (with 128 x 128 matrices) are:

Compute time mult(A, B, C) is 1980 $\mu$s. These are 2109 MFlops.

This implementation is our reference regarding performance and results. For the development of the unrolled implementation, we go back to 4 x 4 matrices. In contrast to Section 5.4.6, we do not unroll a single reduction but perform multiple reductions in parallel. Regarding the three loops, this means that we unroll the two outer loops and perform block operations in the inner loop; i.e., multiple i and j values are handled in each iteration. This block is realized by a size-parameterizable functor.

As in the canonical implementation, the reduction is not performed directly on elements of C but in temporaries. For this purpose, we use the class multi_tmp from §5.4.6.3. For the sake of simplicity, we limit ourselves to matrix sizes that are multiples of the unroll parameters (a full implementation for arbitrary matrix sizes is realized in MTL4). The unrolled matrix multiplication is shown in the following function:

```cpp
template <unsigned Size0, unsigned Size1, typename Matrix>
inline void mult(const Matrix& A, const Matrix& B, Matrix& C)
{
    using value_type = typename Matrix::value_type;
    unsigned s = A.num_rows();
    mult_block<0, Size0-1, 0, Size1-1> block;
    for (unsigned i = 0; i < s; i+= Size0)
        for (unsigned k = 0; k < s; k+= Size1) {
            mult_tmp<Size0 * Size1, value_type> tmp(value_type(0));
            for (unsigned j = 0; j < s; j++)
                block(tmp, A, i, j, k);
            block.update(tmp, C, i, k);
        }
}
```

We still have to implement the functor mult_block. The techniques are essentially the same as in the vector operations, but we have to deal with more indices and their respective limits:

```cpp
template <unsigned Index0, unsigned Max0, unsigned Index1,
unsigned Max1>
struct mult_block<Index0, Max0, Index1+1, Max1>
{
    typedef mult_block<Index0, Max0, Index1+1, Max1> next;
    template <typename Tmp, typename Matrix>
    void operator()(Tmp & tmp, const Matrix& A, const Matrix& B,
        unsigned i, unsigned j, unsigned k)
    {
        tmp.value += A(i + Index0, j) * B(j, k + Index1);
        next()(tmp.sub, A, B, i, j, k);
    }
    template <typename Tmp, typename Matrix>
    void update(const Tmp & tmp, Matrix& C, unsigned i, unsigned k)
    {
        C(i + Index0, k + Index1) = tmp.value;
        next().update(tmp.sub, C, i, k);
    }
};
```

```cpp
template <unsigned Index0, unsigned Max0, unsigned Max1>
struct mult_block<Index0+1, Max0, 0, Max1>
{
    typedef mult_block<Index0+1, Max0, 0, Max1> next;
    template <typename Tmp, typename Matrix>
    void operator()(Tmp & tmp, const Matrix& A, const Matrix& B,
        unsigned i, unsigned j, unsigned k)
    {
        tmp.value += A(i + Index0, j) * B(j, k + Max1);
        next()(tmp.sub, A, B, i, j, k);
    }
    template <typename Tmp, typename Matrix>
    void update(const Tmp & tmp, Matrix& C, unsigned i, unsigned k)
    {
        C(i + Index0, k + Max1) = tmp.value;
        next().update(tmp.sub, C, i, k);
    }
};
```

```cpp
template <unsigned Max0, unsigned Max1>
struct mult_block<Max0, Max0, Max1, Max1>
{
    template <typename Tmp, typename Matrix>
    void operator()(Tmp & tmp, const Matrix& A, const Matrix& B,
                    unsigned i, unsigned j, unsigned k)
    {
        tmp.value += A(i + Max0, j) * B(j, k + Max1);
    }

    template <typename Tmp, typename Matrix>
    void update(const Tmp & tmp, Matrix& C, unsigned i, unsigned k)
    {
        C(i + Max0, k + Max1) = tmp.value;
    }
};
```

With appropriate logging, we can show that the same operations are performed for each entry of C as in the canonical implementation. We can also see that calculations regarding the entries are interleaved. In the following logging, we multiply 4 x 4 matrices and unroll 2 x 2 blocks. From the four temporaries, we observe two:

```
tmp.4 -= A[1][0] * B[0][0]
tmp.3 -= A[1][0] * B[0][1]
tmp.4 += A[1][1] * B[1][0]
tmp.3 += A[1][1] * B[1][1]
tmp.3 -= A[1][1] * B[1][0]
tmp.4 -= A[1][2] * B[2][0]
tmp.3 -= A[1][2] * B[2][1]
tmp.4 += A[1][3] * B[3][0]
tmp.3 += A[1][3] * B[3][1]
C[1][0] = tmp.4
C[1][1] = tmp.3
tmp.4 -= A[3][0] * B[0][0]
tmp.3 -= A[3][0] * B[0][1]
tmp.4 += A[3][1] * B[1][0]
tmp.3 += A[3][1] * B[1][1]
tmp.3 -= A[3][1] * B[1][0]
tmp.4 -= A[3][2] * B[2][0]
tmp.3 -= A[3][2] * B[2][1]
tmp.4 += A[3][3] * B[3][0]
tmp.3 += A[3][3] * B[3][1]
C[3][0] = tmp.4
C[3][1] = tmp.3
```

In temporary number 4, we accumulate A1 · B0 and store the result to c1,0. This is interleaved with the accumulation of A1 · B1 in temporary 3, allowed for using multiple pipelines of super-scalar processors. We can also see that

$c_{ik} = \sum_{j=0}^3 a_{ij} b_{jk} \forall i, k.$

The implementation above can be simplified. The first functor specialization only differs from the general functor in the way the indices are incremented. We can factor this out with an additional loop2 class:

```cpp
template <unsigned Index0, unsigned Max0, unsigned Index1,
              unsigned Max1>
struct loop2
{
    static const unsigned next_index0 = Index0,
                          next_index1 = Index1 + 1;
};
```

```cpp
template <unsigned Index0, unsigned Max0, unsigned Max1>
struct loop2<Index0, Max0, Max1, Max1>
{
    static const unsigned next_index0 = Index0 + 1, next_index1 = 0;
};
```

Such a general class has a high potential for reuse. With this class, we can fuse the functor template and the first specialization:

```cpp
template <unsigned Index0, unsigned Max0, unsigned Index1,
              unsigned Max1>
struct mult_block
{
    typedef loop2<Index0, Max0, Index1, Max1> l;
    typedef mult_block<l::next_index0, Max0,
                       l::next_index1, Max1> next;
};
```

```cpp
template <typename Tmp, typename Matrix>
void operator()(Tmp& tmp, const Matrix& A, const Matrix& B,
                unsigned i, unsigned j, unsigned k)
{
    tmp.value += A(i + Index0, j) * B(j, k + Index1);
    next()(tmp.sub, A, B, i, j, k);
}
```

```cpp
template <typename Tmp, typename Matrix>
void update(const Tmp& tmp, Matrix& C, unsigned i, unsigned k)
{
    C(i + Index0, k + Index1) = tmp.value;
    next().update(tmp.sub, C, i, k);
};
```

The other specialization remains unaltered.

Last but not least, we want to see the impact of our not-so-simple matrix product implementation. The benchmark yielded on our test machine:

| Configuration | Time | MFlops |
|---------------|------|--------|
| mult<1, 1> | 1968 µs | 2122 |
| mult<1, 2> | 1356 µs | 3079 |
| mult<1, 4> | 1038 µs | 4022 |
| mult<1, 8> | 871 µs | 4794 |
| mult<1, 16> | 2039 µs | 2048 |
| mult<2, 1> | 1394 µs | 2996 |
| mult<4, 1> | 1142 µs | 3658 |
| mult<8, 1> | 1127 µs | 3705 |
| mult<16, 1> | 2307 µs | 1810 |
| mult<2, 2> | 1428 µs | 2923 |
| mult<2, 4> | 1012 µs | 4126 |
| mult<2, 2> | 2081 µs | 2007 |
| mult<4, 4> | 1988 µs | 2100 |

We can see that mult<1, 1> has the same performance as the original implementation, which in fact is performing the operations in exactly the same order (so far the compiler optimization does not change the order internally). We also see that most unrolled versions are faster, up to a factor of 2.3.

With double matrices, the performance is slightly lower in general:

| Configuration | Time | MFlops |
|---------------|------|--------|
| mult | 1996 µs | 2092 |
| mult<1, 1> | 1989 µs | 2099 |
| mult<1, 2> | 1463 µs | 2855 |
| mult<1, 4> | 1251 µs | 3337 |
| mult<1, 8> | 1068 µs | 3908 |
| mult<1, 16> | 2078 µs | 2009 |
| mult<2, 1> | 1450 µs | 2880 |
| mult<4, 1> | 1188 µs | 3514 |
| mult<8, 1> | 1143 µs | 3652 |
| mult<16, 1> | 2332 µs | 1791 |
| mult<2, 2> | 1218 µs | 3430 |
| mult<2, 4> | 1040 µs | 4014 |
| mult<2, 2> | 2101 µs | 1987 |
| mult<4, 4> | 2001 µs | 2086 |

This shows that other parameterizations yield more acceleration and that the performance could be doubled.

Which configuration is the best and why is—as mentioned before—not the topic of this book; we only show programming techniques. The reader is invited to try this program on his/her own computer. The techniques in this section are intended for best L1 cache usage. When matrices are larger, we should use more levels of blocking. A general-purpose methodology for locality on L2, L3, main memory, local disk, ... is recursion. This avoids reimplementation for each cache size and performs even reasonably well in virtual memory; see, for instance, [20].
