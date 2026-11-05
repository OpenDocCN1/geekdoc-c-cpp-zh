# C# LANGUAGE SPECIFICATION

+   - For an object creation expression, the definite assignment state of v before arg_i is the same as the state of v before expr.
+   - For each argument arg_i, the definite assignment state of v after arg_i is determined by the normal expression rules, ignoring any ref or out modifiers.
+   - For each argument arg_i, for any i greater than one, the definite assignment state of v before arg_i is the same as the state of v after arg_{i-1}.
+   - If the variable v is passed as an out argument (i.e., an argument of the form "out v") in any of the arguments, then the state of v after expr is definitely assigned. Otherwise; the state of v after expr is the same as the state of v after arg_n.
+   - For array initializers (§7.6.10.4), object initializers (§7.6.10.2), collection initializers (§7.6.10.3) and anonymous object initializers (§7.6.10.6), the definite assignment state is determined by the expansion that these constructs are defined in terms of.

# 5.3.3.23 Simple assignment expressions

For an expression expr of the form w = expr-rhs:

+   - The definite assignment state of v before expr-rhs is the same as the definite assignment state of v before expr.
+   - If w is the same variable as v, then the definite assignment state of v after expr is definitely assigned. Otherwise, the definite assignment state of v after expr is the same as the definite assignment state of v after expr-rhs.

# 5.3.3.24 && expressions

For an expression expr of the form expr-first && expr-second:

+   - The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
+   - The definite assignment state of v before expr-second is definitely assigned if the state of v after expr-first is either definitely assigned or "definitely assigned after true expression". Otherwise, it is not definitely assigned.
+   - The definite assignment state of v after expr is determined by:
+     - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
+     - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is "definitely assigned after false expression", then the state of v after expr is definitely assigned.
+     - Otherwise, if the state of v after expr-second is definitely assigned or "definitely assigned after true expression", then the state of v after expr is "definitely assigned after true expression".
+     - Otherwise, if the state of v after expr-first is "definitely assigned after false expression", and the state of v after expr-second is "definitely assigned after false expression", then the state of v after expr is "definitely assigned after false expression".
+     - Otherwise, the state of v after expr is not definitely assigned.

In the example