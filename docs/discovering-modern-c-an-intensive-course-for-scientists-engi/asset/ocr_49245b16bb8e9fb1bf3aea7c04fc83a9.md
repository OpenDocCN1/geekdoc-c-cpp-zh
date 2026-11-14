```
for (unsigned i = 0; i < s; i+= Size0)
    for (unsigned k = 0; k < s; k+= Size1) {
        mult_tmp<Size0 * Size1, value_type> tmp(value_type(0));
        for (unsigned j= 0; j < s; j++)
            block(tmp, A, i, j, k);
        block.update(tmp, C, i, k);
    }
}
```

We still have to implement the functor mult_block. The techniques are essentially the same as in the vector operations, but we have to deal with more indices and their respective limits:

```
template <unsigned Index0, unsigned Max0, unsigned Index1,
unsigned Max1>
struct mult_block<Index0, Max0, Index1+1, Max1>
{
    typedef mult_block<Index0, Max0, Index1+1, Max1> next;
    template <typename Tmp, typename Matrix>
    void operator()(Tmp & tmp, const Matrix& A, const Matrix& B,
        unsigned i, unsigned j, unsigned k)
    {
        tmp.value+= A(i + Index0, j) * B(j, k + Index1);
        next()(tmp.sub, A, B, i, j, k);
    }
    template <typename Tmp, typename Matrix>
    void update(const Tmp & tmp, Matrix& C, unsigned i, unsigned k)
    {
        C(i + Index0, k + Index1)= tmp.value;
        next().update(tmp.sub, C, i, k);
    }
};
```

```
template <unsigned Index0, unsigned Max0, unsigned Max1>
struct mult_block<Index0+1, Max0, 0, Max1>
{
    typedef mult_block<Index0+1, Max0, 0, Max1> next;
    template <typename Tmp, typename Matrix>
    void operator()(Tmp & tmp, const Matrix& A, const Matrix& B,
        unsigned i, unsigned j, unsigned k)
    {
        tmp.value+= A(i + Index0, j) * B(j, k + Max1);
        next()(tmp.sub, A, B, i, j, k);
    }
    template <typename Tmp, typename Matrix>
    void update(const Tmp & tmp, Matrix& C, unsigned i, unsigned k)
    {
```