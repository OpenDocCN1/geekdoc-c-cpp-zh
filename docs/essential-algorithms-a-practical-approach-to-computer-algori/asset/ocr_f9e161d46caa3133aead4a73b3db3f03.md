# 106 Chapter 4 Arrays

> NOTE If you are unfamiliar with matrices and matrix operations, you may want to review the article "Matrix" at http://en.wikipedia.org/wiki
/Matrix(mathematics).

```
AddArrays(Integer: array1[], Integer: array2[], Integer: result[])
For i = 0 To <maximum bound for dimension 1>
  For j = 0 To <maximum bound for dimension 2>
    result[i, j] = array1[i, j] + array2[i, j]
  Next j
Next i
EndArrays
```

The following algorithm shows how you can multiply two-dimensional matrices:

```
MultiplyArrays(Integer: array1[], Integer: array2[], Integer: result[])
For i = 0 To <maximum bound for dimension 1>
  For j = 0 To <maximum bound for dimension 2>
    // Calculate the [i, j] result
    result[i, j] = 0
    For k = 0 To <maximum bound for dimension 2>
      result[i, j] = result[i, j] + array1[i, k] * array2[k, j]
    Next k
  Next j
EndMultiplyArrays
```

These algorithms work with triangular or sparse arrays, but they are inefficient because they examine every item in both arrays even if those entries are not present.

For example, a triangular array is missing values [i, j] where j > i, so adding or multiplying these entries takes on special meaning. If the missing entries are assumed to be 0, adding or multiplying them doesn't add to the result (If such entries are assumed to have some other default value, adding or multiplying the arrays will result in a nontriangular array, so you may need to add or multiply the arrays completely).

Instead of considering every entry, the algorithm should consider only the entries that are actually present. For triangular arrays, this isn't too confusing. Writing and multiplication algorithms for triangular arrays are topics for Exercises 12 and 13. If you get stuck on them, you can read the solution in Appendix B.

The situation is a bit more confusing for sparse arrays, but the potential time savings is even greater. For example, when you add two sparse matrices, there's no need to iterate over rows and columns that are not present in either of the input arrays.

The following high-level algorithm adds two sparse matrices:

```
AddArrays(SparseArray: array1[], SparseArray: array2[])
```