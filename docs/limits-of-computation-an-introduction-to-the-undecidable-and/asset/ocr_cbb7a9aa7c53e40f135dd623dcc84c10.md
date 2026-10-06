# Other Interesting Questions and Classes ■ 245

A variable is bound if it occurs within the scope of a quantifier; otherwise it is free. All variables are bound in the above expressions.

# Example

$x_1, x_2, x_3$ are bound in the formula below; $x_4$ and $x_5$ are free:

```
$\forall x_3 \exists x_2 \forall x_3 \quad x_1 \wedge \neg x_2 \wedge x_5 \Rightarrow \neg x_4 \vee x_2 \vee x_3$
```

# 10.9.1 Quantified Boolean Formulas (QBFs)

A quantified Boolean formula (QBF) is a Boolean expression in prenex form with no free variables. Thus, it has the form

```
$Q_{x_1} Q_{x_2} \dots Q_{x_n} E$
```

where E is a Boolean expression in $x_1, ..., x_n$, and each $Q_i$ is either the quantifier $\forall$ or $\exists$.

The decision problem is whether this formula is true or not.
To prove QBF is PSPACE-complete, we need to know two things: (1) the problem is in PSPACE, and (2) that every problem in PSPACE is polynomially reducible to QBF. Neither of these properties is immediately obvious.

# Theorem 10.13

QBF is in PSPACE.

# Proof

This is another application of recursion, similar to REACHABILITY. We will use recursion to remove the quantifiers, one at a time. The recursive algorithm requires only polynomial space.
Let E be a Boolean expression in prenex form, possibly with quantifiers:

+   1. If E contains no quantifiers, then it contains no variables and consists of the Boolean constants 0 and 1 with connectors; simply evaluate it.