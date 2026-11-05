
## C# LANGUAGE SPECIFICATION

- For an object creation expression, the definite assignment state of v before arg_i is the same as the state of v before expr.
- For each argument arg_i, the definite assignment state of v after arg_i is determined by the normal expression rules, ignoring any ref or out modifiers.
- For each argument arg_i, for any i greater than one, the definite assignment state of v before arg_i is the same as the state of v after arg_{i-1}.
- If the variable v is passed as an out argument (i.e., an argument of the form "out v") in any of the arguments, then the state of v after expr is definitely assigned. Otherwise, the state of v after expr is the same as the state of v after arg_n.
- For array initializers (§7.6.10.4), object initializers (§7.6.10.2), collection initializers (§7.6.10.3) and anonymous object initializers (§7.6.10.6), the definite assignment state is determined by the expansion that these constructs are defined in terms of.

### 5.3.3.23 Simple assignment expressions

For an expression expr of the form w = expr-rhs:

- The definite assignment state of v before expr-rhs is the same as the definite assignment state of v before expr.
- If w is the same variable as v, then the definite assignment state of v after expr is definitely assigned. Otherwise, the definite assignment state of v after expr is the same as the definite assignment state of v after expr-rhs.

### 5.3.3.24 && expressions

For an expression expr of the form expr-first && expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is definitely assigned if the state of v after expr-first is either definitely assigned or "definitely assigned after true expression". Otherwise, it is not definitely assigned.
- The definite assignment state of v after expr is determined by:
  - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
  - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is "definitely assigned after false expression", then the state of v after expr is definitely assigned.
  - Otherwise, if the state of v after expr-second is definitely assigned or "definitely assigned after true expression", then the state of v after expr is "definitely assigned after true expression".
  - Otherwise, if the state of v after expr-first is "definitely assigned after false expression", and the state of v after expr-second is "definitely assigned after false expression", then the state of v after expr is "definitely assigned after false expression".
  - Otherwise, the state of v after expr is not definitely assigned.

In the example

```
class A
{
    static void F(int x, int y) {
        int i;
        if (x >= 0 && (i = y) >= 0) {
            // i definitely assigned
        }
        else {
            // i not definitely assigned
        }
        // i not definitely assigned
    }
}
```

the variable i is considered definitely assigned in one of the embedded statements of an if statement but not in the other. In the if statement in method F, the variable i is definitely assigned in the first embedded statement because execution of the expression (i = y) always precedes execution of this embedded statement. In contrast, the variable i is not definitely assigned in the second embedded statement, since x >= 0 might have tested false, resulting in the variable i being unassigned.

### 5.3.3.25 || expressions

For an expression expr of the form expr-first || expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is definitely assigned if the state of v after expr-first is either definitely assigned or “definitely assigned after false expression”. Otherwise, it is not definitely assigned.
- The definite assignment state of v after expr is determined by:
  - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
  - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is “definitely assigned after true expression”, then the state of v after expr is definitely assigned.
  - Otherwise, if the state of v after expr-second is definitely assigned or “definitely assigned after false expression”, then the state of v after expr is “definitely assigned after false expression”.
  - Otherwise, if the state of v after expr-first is “definitely assigned after true expression”, and the state of v after expr-second is “definitely assigned after true expression”, then the state of v after expr is “definitely assigned after true expression”.
  - Otherwise, the state of v after expr is not definitely assigned.

In the example

```
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        }
        else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

the variable i is considered definitely assigned in one of the embedded statements of an if statement but not in the other. In the if statement in method G, the variable i is definitely assigned in the second embedded statement because execution of the expression (i = y) always precedes execution of this embedded statement. In contrast, the variable i is not definitely assigned in the first embedded statement, since x >= 0 might have tested true, resulting in the variable i being unassigned.

### 5.3.3.26 ! expressions

For an expression expr of the form ! expr-operand:

- The definite assignment state of v before expr-operand is the same as the definite assignment state of v before expr.
- The definite assignment state of v after expr is determined by:
  - If the state of v after expr-operand is definitely assigned, then the state of v after expr is definitely assigned.
  - If the state of v after expr-operand is not definitely assigned, then the state of v after expr is not definitely assigned.
  - If the state of v after expr-operand is "definitely assigned after false expression", then the state of v after expr is "definitely assigned after true expression".
  - If the state of v after expr-operand is "definitely assigned after true expression", then the state of v after expr is "definitely assigned after false expression".

### 5.3.3.27 ?? expressions

For an expression expr of the form expr-first ?? expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is the same as the definite assignment state of v after expr-first.
- The definite assignment state of v after expr is determined by:
  - If expr-first is a constant expression (§7.19) with value null, then the state of v after expr is the same as the state of v after expr-second.
- Otherwise, the state of v after expr is the same as the definite assignment state of v after expr-first.

### 5.3.3.28 ?: expressions

For an expression expr of the form expr-cond ? expr-true : expr-false:

- The definite assignment state of v before expr-cond is the same as the state of v before expr.
- The definite assignment state of v before expr-true is definitely assigned if and only if the state of v after expr-cond is definitely assigned or "definitely assigned after true expression".
- The definite assignment state of v before expr-false is definitely assigned if and only if the state of v after expr-cond is definitely assigned or "definitely assigned after false expression".
- The definite assignment state of v after expr is determined by:
  - If expr-cond is a constant expression (§7.19) with value true then the state of v after expr is the same as the state of v after expr-true.
