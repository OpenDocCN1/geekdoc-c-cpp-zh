For a statement stmt of the form:

```
return ;
```

+   - If v is an output parameter, then it shall be definitely assigned either:
+     - before stmt
+     - or at the end of the finally block of a try-finally or try-catch-finally that encloses the return statement.

# 9.4.4.14 Try-catch statements

For a statement stmt of the form:

```
try «try_block»
catch ( ... ) «catch_block_1»
...
catch ( ... ) «catch_block_n»
```

+   - The definite assignment state of v at the beginning of try_block is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the beginning of catch_block_i (for any i) is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the end-point of stmt is definitely assigned if (and only if) v is definitely assigned at the end-point of try_block and every catch_block_i (for every i from 1 to n).

# 9.4.4.15 Try-finally statements

For a try statement stmt of the form:

```
try try_block finally finally_block
```

+   - The definite assignment state of v at the beginning of try_block is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the beginning of finally_block is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the end-point of stmt is definitely assigned if (and only if) at least one of the following is true:
+     - v is definitely assigned at the end-point of try_block
+     - v is definitely assigned at the end-point of finally_block

If a control flow transfer (such as a goto statement) is made that begins within try_block, and ends outside of try_block, then v is also considered definitely assigned on that control flow transfer if v is definitely assigned at the end-point of finally_block. (This is not an only if--if v is definitely assigned for another reason on this control flow transfer, then it is still considered definitely assigned.)

# 9.4.4.16 Try-catch-finally statements

Definite assignment analysis for a try-catch-finally statement of the form:

```
try «try_block»
catch ( ... ) «catch_block_1»
...
catch ( ... ) «catch_block_n»
finally «finally_block»
```