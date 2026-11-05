*end example*

# ### 9.4.4.27 || expressions

For an expression *expr* of the form:

*expr_first* || *expr_second*

+   - The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.
+   - The definite assignment state of *v* before *expr_second* is definitely assigned if and only if the state of *v* after *expr_first* is either definitely assigned or “definitely assigned after true expression”. Otherwise, it is not definitely assigned.
+   - The definite assignment statement of *v* after *expr* is determined by:
+       - If the state of *v* after *expr_first* is definitely assigned, then the state of *v* after *expr* is definitely assigned.
+       - Otherwise, if the state of *v* after *expr_second* is definitely assigned, and the state of *v* after *expr_first* is “definitely assigned after true expression”, then the state of *v* after *expr* is definitely assigned.
+       - Otherwise, if the state of *v* after *expr_second* is definitely assigned or “definitely assigned after false expression”, then the state of *v* after *expr* is “definitely assigned after false expression”.
+       - Otherwise, if the state of *v* after *expr_first* is “definitely assigned after true expression”, and the state of *v* after *expr_second* is “definitely assigned after true expression”, then the state of *v* after *expr* is “definitely assigned after true expression”.
+       - Otherwise, the state of *v* after *expr* is not definitely assigned.

*Example:* In the following code

```
```csharp
class A
{
    static void G(int x, int y)
    {
        int i;
        if (x >= 0 || (i = y) >= 0)
        {
            // i not definitely assigned
        }
        else
        {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```
```

the variable `i` is considered definitely assigned in one of the embedded statements of an `if` statement but not in the other. In the `if` statement in method `G`, the variable `i` is definitely assigned in the second embedded statement because execution of the expression `(i = y)` always precedes execution of this embedded statement. In contrast, the variable `i` is not definitely assigned in the first embedded statement, since `x >= 0` might have tested true, resulting in the variable `i`'s being unassigned.