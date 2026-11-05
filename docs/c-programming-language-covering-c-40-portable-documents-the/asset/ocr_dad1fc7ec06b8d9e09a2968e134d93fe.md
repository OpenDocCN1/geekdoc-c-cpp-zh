Each of these expressions has one or more subexpressions that are unconditionally evaluated in a fixed order. For example, the binary % operator evaluates the left-hand side of the operator, then the right-hand side. An indexing operation evaluates the indexed expression, and then evaluates each of the index expressions, in order from left to right. For an expression expr that has subexpressions expr₁, expr₂, ..., exprₙ, evaluated in that order:

+   - The definite assignment state of v at the beginning of expr₁ is the same as the definite assignment state at the beginning of expr.
+   - The definite assignment state of v at the beginning of exprᵢ (i greater than 1) is the same as the definite assignment state at the end of exprᵢ₋₁.
+   - The definite assignment state of v at the end of expr is the same as the definite assignment state at the end of exprₙ.

# ### 5.3.3.22 Invocation Expressions and Object Creation Expressions

For an invocation expression expr of the form:

```
primary-expression ( arg₁ , arg₂ , ... , argₙ )
```

or an object creation expression of the form:

```
new type ( arg₁ , arg₂ , ... , argₙ )
```

+   - For an invocation expression, the definite assignment state of v before primary-expression is the same as the state of v before expr.
+   - For an invocation expression, the definite assignment state of v before arg₁ is the same as the state of v after primary-expression.
+   - For an object creation expression, the definite assignment state of v before arg₁ is the same as the state of v before expr.
+   - For each argument argᵢ, the definite assignment state of v after argᵢ is determined by the normal expression rules, ignoring any ref or out modifiers.
+   - For each argument argᵢ for any i greater than 1, the definite assignment state of v before argᵢ is the same as the state of v after argᵢ₋₁.
+   - If the variable v is passed as an out argument (i.e., an argument of the form “out v”) in any of the arguments, then the state of v after expr is definitely assigned. Otherwise, the state of v after expr is the same as the state of v after argₙ.
+   - For array initializers (§7.6.10.4), object initializers (§7.6.10.2), collection initializers (§7.6.10.3), and anonymous object initializers (§7.6.10.6), the definite assignment state is determined by the expansion that these constructs are defined in terms of.