
triangular solver of a linear system, which we find in MTL4; more precisely, the k-th vector of U^-1 is the solution of:

Ux = e_k

where e_k is the k-th unit vector. First we define a temporary variable for the result:

```
Matrix Inv(n, n);
```

Then we iterate over the columns of Inv:

```
for (unsigned k = 0; k < n; ++k) {
}
```

In each iteration we need the k-th unit vector:

```
dense_vector<double> e_k(n);
for (unsigned i = 0; i < n; ++i)
    if (i == k)
        e_k[i] = 1.0;
    else
        e_k[i] = 0.0;
```

The triangular solver returns a column vector. We could assign the entries of this vector directly to entries of the target matrix:

```
for (unsigned i = 0; i < n; ++i)
    Inv[i][k] = upper_trisolve(A, e_k)[i];
```

This is nice and short but we would compute upper_trisolve n times! Although we said that performance is not our primary goal at this point, the increase of overall complexity from order 3 to 4 is too wasteful of resources. Many programmers make the mistake of optimizing too early, but this does not mean that we should accept (without serious reasons) an implementation with a higher order of complexity. To avoid the superfluous recomputations, we store the triangle solver result and copy the entries from there:

```
dense_vector<double> res_k(n);
res_k = upper_trisolve(A, e_k);
for (unsigned i = 0; i < n; ++i)
    Inv[i][k] = res_k[i];
```

Finally, we return the temporary matrix. The function in its complete form looks as follows:

```
Matrix inverse_upper(Matrix const& A)
{
    const unsigned n = num_rows(A);
    if (num_cols(A) != n)
        throw "Matrix must be square";

    Matrix Inv(n, n);

    for (unsigned k = 0; k < n; ++k) {
        dense_vector<double> e_k(n);
        for (unsigned i = 0; i < n; ++i)
            if (i == k)
                e_k[i] = 1.0;
            else
                e_k[i] = 0.0;

        dense_vector<double> res_k(n);
        res_k = upper_trisolve(A, e_k);
        for (unsigned i = 0; i < n; ++i)
            Inv[i][k] = res_k[i];
    }

    return Inv;
}
```

Now that the function is complete, we first run our test. Evidently, we have to comment out part of the test because we have only implemented one function so far. Nonetheless, it is good to know early whether this first function behaves as expected. It does, and we could be happy with it now and turn our attention to the next task; there are still many. But we will not. Instead we'll spend some time to improve our implementation. Such improvements are called *Refactoring*. Experience has shown that it takes much less time to refactor immediately after implementation than later when bugs are discovered or the software is ported to other platforms. Obviously, it is much easier to simplify and structure our software immediately when we still know what is going on than after some weeks/months/years.

The first thing we might dislike is that something so simple as the initialization of a unit vector takes five lines. This is rather verbose:

```
for (unsigned i = 0; i < n; ++i)
    if (i == k)
        e_k[i] = 1.0;
    else
        e_k[i] = 0.0;
```

We can write this more compactly with the conditional operator:

```
for (unsigned i = 0; i < n; ++i)
    e_k[i] = i == k ? 1.0 : 0.0;
```

The conditional operator ?: usually takes some time to get used to but it results in a more concise representation. Although we have not changed anything semantically in the program and it seems obvious that the result will still be the same, it cannot hurt to run our test again. You will see that often you are sure that your program modifications could never change the behavior—but still they do. The sooner we find an unexpected behavior, the less work it is to fix it. With the test(s) that we have already written, it only takes a few seconds and makes us feel more confident.

If we would like to be really cool, we could explore some insider knowhow. The expression `i == k` returns a boolean, and we know that `bool` can be converted implicitly into `int` and subsequently to `double`. In this conversion, `false` turns into 0 and `true` into 1 according to the standard. These are precisely the values that we want as `double`:

```
e_k[i] = static_cast<double>(i == k);
```

In fact, the conversion from `int` to `double` is performed implicitly and can be omitted as well:

```
e_k[i] = i == k;
```

As cute as this looks, it is some stretch to assign a logical value to a floating-point number. It is well defined by the implicit conversion chain `bool → int → double`, but it can confuse potential readers and you might end up explaining to them what is happening on a mailing list or adding a comment to the program. In both cases you end up writing more text for the explanation than you saved in the program.

Another thought that might occur to us is that it is probably not the last time that we need a unit vector. So, why not write a function for it?

```
dense_vector<double> unit_vector(unsigned k, unsigned n)
{
    dense_vector<double> e_k(n, 0.0);
    e_k[k] = 1;
    return e_k;
}
```

Since the function returns the unit vector, we can just take it as an argument for the triangular solver:

```
res_k = upper_trisolve(A, unit_vector(k, n));
```

For a dense matrix, MTL4 allows us to access a matrix column as a column vector (instead of a sub-matrix). Then, we can assign the result vector directly without a loop:

```
Inv[irange(0, n)][k] = res_k;
```

As a short explanation, the bracket operator is implemented in such a manner that integer indices for rows and columns return the matrix entry while ranges for rows and columns return a sub-matrix. Likewise, a range of rows and a single column gives us a column of the corresponding matrix —or part of this column. Conversely, a row vector can be extracted from a matrix with an integer as a row index and a range for the columns.

This is an interesting example of how to deal with the limitations as well as the possibilities of C++. Other languages have ranges as part of their intrinsic notation; e.g., Python has a symbol : for expressing ranges of indices.⁵

## 5. C++20 introduces ranges and you find their description in Section 4.1.5.

C++ does not provide such a symbol, but we can introduce a new type—like MTL4's irange—and define the behavior of operator[] for this type. This leads to an extremely powerful mechanism: overload operators for multiple types to allow for a much larger functionality with intuitive notation. The operator semantics on user types shall be intuitive and shall be consistent with the operator priority (see an example in §13.10). Back to our algorithm. We store the result of the solver in a vector and then we assign it to a matrix column. In fact, we can assign the triangular solver’s result directly:

```
Inv[irange{0, n}][k] = upper_trisolve(A, unit_vector(k, n));
```

The range of all indices is predefined as iall:

```
Inv[iall][k] = upper_trisolve(A, unit_vector(k, n));
```

Next, we explore some mathematical background. The inverse of an upper triangular matrix is also upper triangular. Thus, we only need to compute the upper part of the result and set the remainder to 0—or the whole matrix to zero before computing the upper part. Of course, we need smaller unit vectors now and only sub-matrices of A. This can be nicely expressed with ranges:

```
Inv = 0;
for (unsigned k = 0; k < n; ++k)
    Inv[irange(0, k+1)][k] =
    upper_trisolve(A[irange{0, k+1}][irange{0, k+1}],
        unit_vector(k, k+1));
```

Admittedly, the irange makes the expression a bit harder to read. We created irange objects on the fly and passed them to operator[]. As we use the same range three times, it is better to create a variable for it:

```
for (unsigned k = 0; k < n; ++k) {
   irange r(0, k+1);
```
