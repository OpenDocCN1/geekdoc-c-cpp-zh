+   - The definite-assignment state of v on the control flow transfer to embedded_statement is the same as the state of v at the end of resource_acquisition.

# 9.4.4.19 Lock statements

For a statement stmt of the form:

```
lock ( «expr» ) «embedded_statement»
```

+   - The definite-assignment state of v at the beginning of expr is the same as the state of v at the beginning of stmt.
+   - The definite-assignment state of v on the control flow transfer to embedded_statement is the same as the state of v at the end of expr.

# 9.4.4.20 Yield statements

For a statement stmt of the form:

```
yield return «expr» ;
```

+   - The definite-assignment state of v at the beginning of expr is the same as the state of v at the beginning of stmt.
+   - The definite-assignment state of v at the end of stmt is the same as the state of v at the end of expr.

A yield break statement has no effect on the definite-assignment state.

# 9.4.4.21 General rules for constant expressions

The following applies to any constant expression, and takes priority over any rules from the following sections that might apply:

For a constant expression with value true:

+   - If v is definitely assigned before the expression, then v is definitely assigned after the expression.
+   - Otherwise v is "definitely assigned after false expression" after the expression.

Example:

```
int x;
if (true) {}
else
{
    Console.WriteLine(x);
}
end example
```

For a constant expression with value false:

+   - If v is definitely assigned before the expression, then v is definitely assigned after the expression.
+   - Otherwise v is "definitely assigned after true expression" after the expression.

Example:

```
int x;
if (false)
{
    Console.WriteLine(x);
}
```