The algorithm should find the position of a given integer x in the array a, i.e., the algorithm should find i and j such that

+   - `x = a[i, j],` or
+   - `i = m`

Let us treat the input array as some kind of a rectangular region.

The problem demands that the integer x does exist somewhere in this region. Let us label this condition as Input Assertion or Precondition.

> [
> Precondition|Precondition (aka Input Assertion) x ∈ a[0..m−1,0..n−1]
> ]

i.e., x is present somewhere in this rectangular region a.

![](bbox=[0.38, 0.368, 0.68, 0.54])

After the program terminates successfully, x has to be found in a rectangular region of a where the rectangular region consists of just one row and column. Let us label this condition as Output Assertion or Result Assertion or Postcondition.

> [
> Postcondition|Postcondition (aka Result Assertion) After the program terminates successfully, then x is in a rectangular region of a where the rectangular region consists of just one row and column, i.e., x is present at i^th row and j^th column of a, or if this is not possible then i = m, i.e., if x is not found in the array, i.e., if x ≠ a[i, j], then i = m.

So the Postcondition looks like

```
(0 ≤ i < m − 1 ∧ 0 ≤ j < n − 1 ∧ x = a[i, j]) ∨ (i = m ∧ x ∉ a)
```

Is the search space confined to a rectangular region ?