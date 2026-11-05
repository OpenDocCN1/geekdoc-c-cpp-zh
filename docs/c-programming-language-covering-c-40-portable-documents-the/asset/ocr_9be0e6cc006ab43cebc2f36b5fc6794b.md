```
{
    // i definitely assigned
}
else
{
    // i not definitely assigned
}
// i not definitely assigned
}
```

the variable i is considered definitely assigned in one of the embedded statements of an if statement but not in the other. In the if statement in method F, the variable i is definitely assigned in the first embedded statement because execution of the expression (i = y) always precedes execution of this embedded statement. In contrast, the variable i is not definitely assigned in the second embedded statement, because x >= 0 might have tested false, resulting in the variable i being unassigned.

# 5.3.3.25 || Expressions

For an expression expr of the form expr-first || expr-second:

+   - The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
+   - The definite assignment state of v before expr-second is definitely assigned if the state of v after expr-first is either definitely assigned or “definitely assigned after false expression.” Otherwise, it is not definitely assigned.
+   - The definite assignment state of v after expr is determined by:
+     - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
+     - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is “definitely assigned after true expression,” then the state of v after expr is definitely assigned.
+     - Otherwise, if the state of v after expr-second is definitely assigned or “definitely assigned after false expression,” then the state of v after expr is “definitely assigned after false expression.”
+     - Otherwise, if the state of v after expr-first is “definitely assigned after true expression,” and the state of v after expr-second is “definitely assigned after true expression,” then the state of v after expr is “definitely assigned after true expression.”
+     - Otherwise, the state of v after expr is not definitely assigned.