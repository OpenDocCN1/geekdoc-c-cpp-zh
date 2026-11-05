or an object creation expression expr of the form:

```
new type ( arg1, arg2, ..., argx )
```

+   - For an invocation expression, the definite assignment state of v before primary_expression is the same as the state of v before expr.
+   - For an invocation expression, the definite assignment state of v before arg_i is the same as the state of v after primary_expression.
+   - For an object creation expression, the definite assignment state of v before arg_i is the same as the state of v before expr.
+   - For each argument arg_i, the definite assignment state of v after arg_i is determined by the normal expression rules, ignoring any ref or out modifiers.
+   - For each argument arg_i, for any i greater than one, the definite assignment state of v before arg_i is the same as the state of v after arg_{i-1}.
+   - If the variable v is passed as an out argument (i.e., an argument of the form “out v”) in any of the arguments, then the state of v after expr is definitely assigned. Otherwise, the state of v after expr is the same as the state of v after arg_x.
+   - For array initializers (§11.7.15.5), object initializers (§11.7.15.3), collection initializers (§11.7.15.4) and anonymous object initializers (§11.7.15.7), the definite assignment state is determined by the expansion that these constructs are defined in terms of.

# 9.4.4.25 Simple assignment expressions

For an expression expr of the form:

```
w = expr_rhs
```

+   - The definite assignment state of v before w is the same as the definite assignment state of v before expr.
+   - The definite assignment state of v before expr_rhs is the same as the definite assignment state of v after w.
+   - If w is the same variable as v, then the definite assignment state of v after expr is definitely assigned. Otherwise, if the assignment occurs within the instance constructor of a struct type, and w is a property access designating an automatically implemented property P on the instance being constructed and v is the hidden backing field of P, then the definite assignment state of v after expr is definitely assigned. Otherwise, the definite assignment state of v after expr is the same as the definite assignment state of v after expr_rhs.

Example: In the following code

```
class A
{
    static void F(int[] arr)
    {
        int x;
        arr[x = 1] = x; // ok
    }
}
```

the variable x is considered definitely assigned after arr[x = 1] is evaluated as the left hand side of the second simple assignment.