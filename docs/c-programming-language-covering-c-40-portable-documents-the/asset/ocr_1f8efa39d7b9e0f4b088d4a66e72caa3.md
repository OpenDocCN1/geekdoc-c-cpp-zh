# 5.3.3.27 ?? Expressions

For an expression expr of the form expr-first ?? expr-second:

+   - The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
+   - The definite assignment state of v before expr-second is the same as the definite assignment state of v after expr-first.
+   - The definite assignment state of v after expr is determined by:
+     - If expr-first is a constant expression (§7.19) with value null, then the state of v after expr is the same as the state of v after expr-second.
+   - Otherwise, the state of v after expr is the same as the definite assignment state of v after expr-first.

# 5.3.3.28 ?: Expressions

For an expression expr of the form expr-cond ? expr-true : expr-false:

+   - The definite assignment state of v before expr-cond is the same as the state of v before expr.
+   - The definite assignment state of v before expr-true is definitely assigned if and only if the state of v after expr-cond is definitely assigned or "definitely assigned after true expression."
+   - The definite assignment state of v before expr-false is definitely assigned if and only if the state of v after expr-cond is definitely assigned or "definitely assigned after false expression."
+   - The definite assignment state of v after expr is determined by:
+     - If expr-cond is a constant expression (§7.19) with value true, then the state of v after expr is the same as the state of v after expr-true.
+     - Otherwise, if expr-cond is a constant expression (§7.19) with value false, then the state of v after expr is the same as the state of v after expr-false.
+     - Otherwise, if the state of v after expr-true is definitely assigned and the state of v after expr-false is definitely assigned, then the state of v after expr is definitely assigned.
+     - Otherwise, the state of v after expr is not definitely assigned.