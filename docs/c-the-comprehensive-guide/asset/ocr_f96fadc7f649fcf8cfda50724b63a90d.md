The output is the `{{4, 3, -3}, {11, -1, -8}, {13, 0, -3}}` matrix, which represents the product of the matrix multiplication. Note that matrix multiplication should only receive matrices and size specifications that are compatible for this operation.

With `a[slice(...)]` and `b[slice(...)]`, a row or column is cleverly sliced out here. And as the rule of matrix multiplication states, these are then multiplied element-wise and summed up: this is done with `valarray` in the innocuous-looking expression `(row * col).sum()`.

I deliberately used the compiler’s type inference with `auto` for row and col, instead of writing `valarray<int>` for the row and column. It is possible that the compiler optimizes here with a special object.

The program's output is this:

```
1   0  -1
2   2  -3
3   4   0
-times-
 3   4  -1
 1  -3   0
-1   1   2
-results in-
 4   3  -3
11  -1  -8
13   0  -3
```

valarray is not very common. However, you can find more examples in *Thinking in C++*.