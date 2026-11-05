
The variable x is considered definitely assigned after arr[x = 1] is evaluated as the left hand side of the second simple assignment. end example]

## 10.4.4.26 && expressions

For an expression expr of the form expr-first && expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is definitely assigned if and only if the state of v after expr-first is either definitely assigned or "definitely assigned after true expression". Otherwise, it is not definitely assigned.
- The definite assignment state of v after expr is determined by:
    - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
    - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is "definitely assigned after false expression", then the state of v after expr is definitely assigned.
    - Otherwise, if the state of v after expr-second is definitely assigned or "definitely assigned after true expression", then the state of v after expr is "definitely assigned after true expression".
    - Otherwise, if the state of v after expr-first is "definitely assigned after false expression", and the state of v after expr-second is "definitely assigned after false expression", then the state of v after expr is "definitely assigned after false expression".
    - Otherwise, the state of v after expr is not definitely assigned.

[Example: In the following code

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

the variable i is considered definitely assigned in one of the embedded statements of an if statement but not in the other. In the if statement in method F, the variable i is definitely assigned in the first embedded statement because execution of the expression (i = y) always precedes execution of this embedded statement. In contrast, the variable i is not definitely assigned in the second embedded statement, since x >= 0 might have tested false, resulting in the variable i's being unassigned. end example]

## 10.4.4.27 || expressions

For an expression expr of the form expr-first || expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is definitely assigned if and only if the state of v after expr-first is either definitely assigned or "definitely assigned after false expression". Otherwise, it is not definitely assigned.
- The definite assignment state of v after expr is determined by:
    - If the state of v after expr-first is definitely assigned, then the state of v after expr is definitely assigned.
    - Otherwise, if the state of v after expr-second is definitely assigned, and the state of v after expr-first is "definitely assigned after true expression", then the state of v after expr is definitely assigned.
    - Otherwise, if the state of v after expr-second is definitely assigned or "definitely assigned after false expression", then the state of v after expr is "definitely assigned after false expression".
    - Otherwise, if the state of v after expr-first is "definitely assigned after true expression", and the state of v after expr-second is "definitely assigned after true expression", then the state of v after expr is "definitely assigned after true expression".
    - Otherwise, the state of v after expr is not definitely assigned.

[Example: In the following code

```
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        } else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

the variable i is considered definitely assigned in one of the embedded statements of an if statement but not in the other. In the if statement in method G, the variable i is definitely assigned in the second embedded statement because execution of the expression (i = y) always precedes execution of this embedded statement. In contrast, the variable i is not definitely assigned in the first embedded statement, since x >= 0 might have tested true, resulting in the variable i's being unassigned. end example]

## 10.4.4.28 ! expressions

For an expression expr of the form ! expr-operand:

- The definite assignment state of v before expr-operand is the same as the definite assignment state of v before expr.
- The definite assignment state of v after expr is determined by:
    - If the state of v after expr-operand is definitely assigned, then the state of v after expr is definitely assigned.
    - Otherwise, if the state of v after expr-operand is "definitely assigned after false expression", then the state of v after expr is "definitely assigned after true expression".
    - Otherwise, if the state of v after expr-operand is "definitely assigned after true expression", then the state of v after expr is "definitely assigned after false expression".
    - Otherwise, the state of v after expr is not definitely assigned.

## 10.4.4.29 ?? expressions

For an expression expr of the form expr-first ?? expr-second:

- The definite assignment state of v before expr-first is the same as the definite assignment state of v before expr.
- The definite assignment state of v before expr-second is the same as the definite assignment state of v after expr-first.
- The definite assignment state of v after expr is determined by:
    - If expr-first is a constant expression (§12.20) with value null, then the state of v after expr is the same as the state of v after expr-second.
    - Otherwise, the state of v after expr is the same as the definite assignment state of v after expr-first.

## 10.4.4.30 ?: expressions

For an expression expr of the form expr-cond ? expr-true : expr-false:

- The definite assignment state of v before expr-cond is the same as the state of v before expr.
- The definite assignment state of v before expr-true is definitely assigned if the state of v after expr-cond is definitely assigned or "definitely assigned after true expression".
- The definite assignment state of v before expr-false is definitely assigned if the state of v after expr-cond is definitely assigned or "definitely assigned after false expression".
- The definite assignment state of v after expr is determined by:
    - If expr-cond is a constant expression (§12.20) with value true then the state of v after expr is the same as the state of v after expr-true.
    - Otherwise, if expr-cond is a constant expression (§12.20) with value false then the state of v after expr is the same as the state of v after expr-false.
    - Otherwise, if the state of v after expr-true is definitely assigned and the state of v after expr-false is definitely assigned, then the state of v after expr is definitely assigned.
    - Otherwise, the state of v after expr is not definitely assigned.

## 10.4.4.31 Anonymous functions

For a lambda-expression or anonymous-method-expression expr with a body (either block or expression) body:

- The definite assignment state of a parameter is the same as for a parameter of a named method (§10.2.6, §10.2.7).
- The definite assignment state of an outer variable v before body is the same as the state of v before expr. That is, the definite assignment state of outer variables is inherited from the context of the anonymous function.
- The definite assignment state of an outer variable v after expr is the same as the state of v before expr.

[Example: The example

```
delegate bool Filter(int i);
void F() {
    int max;
    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;
    max = 5;
    DoWork(f);
}
```

generates a compile-time error since max is not definitely assigned where the anonymous function is declared. end example]

[Example: The example

```
delegate void D();
void F() {
    int n;
    D d = () => { n = 1; };
    d();
    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```

