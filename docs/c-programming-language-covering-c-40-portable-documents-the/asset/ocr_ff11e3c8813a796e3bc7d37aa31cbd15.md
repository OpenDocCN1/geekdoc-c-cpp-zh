# 5.3.3.14 try-finally Statements

For a try statement stmt of the form:

```
try try-block finally finally-block
```

+   - The definite assignment state of v at the beginning of try-block is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the beginning of finally-block is the same as the definite assignment state of v at the beginning of stmt.
+   - The definite assignment state of v at the end point of stmt is definitely assigned if (and only if) at least one of the following is true:
+     - v is definitely assigned at the end point of try-block.
+     - v is definitely assigned at the end point of finally-block.

If a control flow transfer (for example, a goto statement) is made that begins within try-block and ends outside of try-block, then v is also considered definitely assigned on that control flow transfer if v is definitely assigned at the end point of finally-block. (This is not an "only if": If v is definitely assigned for another reason on this control flow transfer, then it is still considered definitely assigned.)

# 5.3.3.15 try-catch-finally Statements

Definite assignment analysis for a try-catch-finally statement of the form:

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
finally finally-block
```

is done as if the statement were a try-finally statement enclosing a try-catch statement:

```
try {
  try try-block
  catch(...) catch-block-1
  ...
  catch(...) catch-block-n
}
finally finally-block
```

The following example demonstrates how the different blocks of a try statement (§8.10) affect definite assignment.