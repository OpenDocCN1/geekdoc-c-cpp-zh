As mentioned previously, in the evaluation of logical expressions, the evaluation process stops as soon as the outcome, true or false, is known (short circuit.)

For example, if `expr1` is false (0), then in the statement:

```
expr1 && expr2
```

expr2 will not be evaluated because the value of the logical expression is already determined to be zero.

Likewise, if `expr1` is true (non-zero), then in the statement:

```
expr1 || expr2
```

expr2 will not be evaluated because the value of the logical expression is already determined to be 1.

# De Morgan's Laws

De Morgan's Laws can sometimes make it more convenient for us to express a logical expression. De Morgan's Laws can be expressed mathematically as follows:

```
~(P or Q) = ~P and ~Q
~(P and Q) = ~P or ~Q
```

In C, these laws state that the expression:

```
!(condition1 && condition2)
```

is logically equivalent to the expression:

```
(!condition1 || !condition2)
```