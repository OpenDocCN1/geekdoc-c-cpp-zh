is a formally valid deductive argument if and only if:

```
P₁ ∧ P₂ ∧ ... ∧ Pₙ ⇒ C
```

is a tautology. As an example,

```
(p ∧ q) → p
```

is a tautology because it is true for any values, T or F, of p and q. You can verify this by constructing the truth table.

The argument of modus ponens,

```
p → q
p
____
∴ q
```

is valid because it can be expressed as a tautology:

```
(p → q) ∧ p → q
```

Note that we are assuming that the arrow has lower precedence than conjunction and disjunction. This saves writing additional parentheses such as:

```
((p → q) ∧ p) → q
```

The truth table for modus ponens is shown in Table 3.4. It is a tautology because the values of the argument, shown in the rightmost column, are all true no matter what the values of its premises. Notice that in the third, fourth, and fifth columns, the truth values are written under certain operators such as the → and ∧. These are called the main connectives because they connect the two main parts of a compound proposition.

| p | q | p → q | (p → q) ∧ p | (p → q) ∧ p → q |
|---|---|---|---|---|
| T | T | T | T | T |
| T | F | F | F | T |
| F | T | T | F | T |
| F | F | T | F | T |