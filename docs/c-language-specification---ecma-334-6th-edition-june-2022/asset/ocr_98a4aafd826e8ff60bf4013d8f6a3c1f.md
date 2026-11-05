+   - v has the same definite assignment state on the control flow transfer from the beginning of stmt to do_body as at the beginning of stmt.
+   - v has the same definite assignment state at the beginning of expr as at the end point of do_body.
+   - If v is definitely assigned at the end of expr, then it is definitely assigned on the control flow transfer to the end point of stmt.
+   - If v has the state "definitely assigned after false expression" at the end of expr, then it is definitely assigned on the control flow transfer to the end point of stmt, but not definitely assigned on the control flow transfer to do_body.

# 9.4.4.10 For statements

Definite assignment checking for a for statement of the form:

```
for ( for_initializer ; for_condition ; for_iterator ) embedded_statement
```

is done as if the statement were written:

```
{
    «for_initializer» ;
    while ( «for_condition» )
    {
        «embedded_statement» ;
        LLoop: «for_iterator» ;
    }
}
```

with continue statements that target the for statement being translated to goto statements targeting the label LLoop. If the for_condition is omitted from the for statement, then evaluation of definite assignment proceeds as if for_condition were replaced with true in the above expansion.

# 9.4.4.11 Break, continue, and goto statements

The definite assignment state of v on the control flow transfer caused by a break, continue, or goto statement is the same as the definite assignment state of v at the beginning of the statement.

# 9.4.4.12 Throw statements

For a statement stmt of the form

```
throw expr ;
```

the definite assignment state of v at the beginning of expr is the same as the definite assignment state of v at the beginning of stmt.

# 9.4.4.13 Return statements