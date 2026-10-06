To reiterate the important points: (1) NP-hard problem has a known polynomial algorithm, but (2) we cannot show that no polynomial algo-rithm exists.

# 8.7 A FIRST NP-COMPLETE PROBLEM:
BOOLEAN SATISFIABILITY

So far, we have defined NP-complete and NP-hard, but have given no examples. The first example, and the proof that it is in these two classes, is basic to all further discussion.

Recall Boolean logic, with expressions consisting of Boolean variables, with values either true or false, connected by the standard Boolean opera-tions of negation (¬), conjunction (∧), or (∨), and implies (→).

For example, with the three Boolean variables x, y, z, one can write many Boolean expressions such as:

```
¬(x ∧ y) → (z ∧ y)
```

This expression is true for many assignments to x, y, z. We say that a set of assignments to the variables x, y, z that makes it true satisfies the expression. For example, x = false, y = false, z = true (x = 0, y = 0, z = 1) will satisfy the expression above.

This expression is not in the special form called conjunctive normal form.

# Definition 8.17

A Boolean clause is a collection of terms connected by ∨. A term (or literal) is either a single variable (xi) or the negation of a single vari-able (¬xi).

# Definition 8.18

A Boolean expression E is in conjunctive normal form if it consists of a set of clauses C1, C2, ..., Cm connected by ∧.

# Fact

Any Boolean expression can be converted into conjunctive normal form.