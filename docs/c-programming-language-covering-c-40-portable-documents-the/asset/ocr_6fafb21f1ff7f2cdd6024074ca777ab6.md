+   - v has the same definite assignment state at the beginning of expr as at the end point of do-body.
+   - If v is definitely assigned at the end of expr, then it is definitely assigned on the control flow transfer to the end point of stmt.
+   - If v has the state "definitely assigned after false expression" at the end of expr, then it is definitely assigned on the control flow transfer to the end point of stmt.

# 5.3.3.9 for Statements

Definite assignment checking for a for statement of the form:

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

is done as if the statement were written:

```
{
    for-initializer ;
    while ( for-condition ) {
        embedded-statement ;
        for-iterator ;
    }
}
```

If the for-condition is omitted from the for statement, then evaluation of definite assignment proceeds as if for-condition were replaced with true in the above expansion.

# 5.3.3.10 break, continue, and goto Statements

The definite assignment state of v on the control flow transfer caused by a break, continue, or goto statement is the same as the definite assignment state of v at the beginning of the statement.

# 5.3.3.11 throw Statements

For a statement stmt of the form:

```
throw expr ;
```

# 5.3.3.12 return Statements

For a statement stmt of the form:

```
return expr ;
```