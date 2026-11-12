# ### 6.2. Searching in Possibly Empty Two Dimensional Sequences

![](bbox=[0.354, 0.074, 0.671, 0.209])

# #### Invariant

The invariant states that x is not in the already-searched rows a[0..i − 1] and not in the already-searched columns a[i, 0..j − 1] of the current row i.

![](bbox=[0.354, 0.361, 0.671, 0.509])

**Invariant:**

`0 ≤ m ∧ 0 ≤ j ≤ n ∧`

`searchable-region` is bounded by `(m − i) * n − j + m − i`, i.e., the bound function is the sum of the number of values in the untested section and the number of rows in the untested section represented by `(m − i) * n − j + m − i`.

The extra value `m − i` is required here because `j` can take up the boundary value `n`, i.e., `j = n`. As an astute reader, you must have noticed that now the invariant includes `j ≤ n`, instead of `j < n`. This is required here because the number of columns, `n`, is out of bounds.

Initialization step is same as discussed earlier.

# #### Condition

Similar to the problem discussed earlier, we can think about `j ← j + 1` and/or `i ← i + 1` to maintain the invariance.

```
if i ≠ m ∧ (j ≥ n and x ≠ a[i,j]) then j ← j + 1
```

Taking this as a condition, the program can terminate when `i < m ∧ j = n`. If x is not found in the very first row, then this will terminate.