```
template <unsigned Index0, unsigned Max0,
          unsigned Index1, unsigned Max1>
struct mult_block
{
    using next= mult_block<Index0, Max0, Index1+1, Max1>;
    using next_row= mult_block<Index0+1, Max0, 0, Max1>;
```

```
template <typename Tmp, typename Matrix>
static void eval(Tmp& tmp, const Matrix& A, const Matrix&
B,
unsigned i, unsigned j, unsigned k)
{
    tmp.value+= A(i + Index0, j) * B(j, k + Index1);
    if constexpr(Index1 == Max1) {
    if constexpr(Index0 < Max0())
    next_row::eval(tmp.sub, A, B, i, j, k);
    } else
    next::eval(tmp.sub, A, B, i, j, k);
}
```

```
template <typename Tmp, typename Matrix>
static void update(const Tmp& tmp, Matrix& C, unsigned i,
unsigned k)
{
    C(i + Index0, k + Index1)= tmp.value;
    if constexpr(Index1 == Max1) {
    if constexpr(Index0 < Max0)
    next_row::update(tmp.sub, C, i, k);
    } else
    next::update(tmp.sub, C, i, k);
}
```

With appropriate logging, we can show that the same operations are performed for each entry of C as in the canonical implementation. We can also see that calculations regarding the entries are interleaved. In the following logging, we multiply 4 x 4 matrices and unroll 2 x 2 blocks. From the four temporaries, we observe two:

```
tmp.4+= A[1] [0] * B[0] [0]
tmp.3+= A[1] [0] * B[0] [1]
tmp.4+= A[1] [1] * B[1] [0]
tmp.3+= A[1] [1] * B[1] [1]
tmp.4+= A[1] [2] * B[2] [0]
tmp.3+= A[1] [2] * B[2] [1]
tmp.4+= A[1] [3] * B[3] [0]
```