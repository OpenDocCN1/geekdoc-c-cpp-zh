We know that this is a valid argument since it is a valid syllogism. Can we prove its validity using propositional logic? To answer this question, let's first write the argument as a schema:

```
p = All men are mortal
q = Socrates is a man
r = Socrates is mortal
```

and so the argument schema is:

```
p
q
.: r
```

Notice that there are no logical connectives in the premises or conclusions and so each premise and each conclusion must have a different logical variable. Also, propositional logic has no provision for quantifiers and so there is no way to represent the quantifier "all" in the first premise. The only representation of this argument in propositional logic is thus the schema above of three independent variables.

To determine if this is a valid argument, consider the truth table of three independent variables for all possible combinations of T and F, shown in Table 3.11. The second row of this truth table shows the argument to be invalid because the premises are true while the conclusion is false.

Table 3.11 Truth Table for the Schema p, q :. r

| p | q | ..:r |
|---|---|---|
| T | T | T |
| T | T | F |
| T | F | T |
| T | F | F |
| F | T | T |
| F | T | F |
| F | F | T |
| F | F | F |

The invalidity of this argument should not be interpreted as meaning the conclusion is incorrect. Any person would recognize this as a correct argument. The invalidity simply means that the argument cannot be proven under propositional logic. The argument can be proven valid if we examine the internal structure of the premises. For example, we would have to attribute some meaning to "all" and recognize "men" as the plural of "man". However, syllogisms and the propositional calculus do not allow the internal structure of propositions to be examined. This limitation is overcome by predicate logic, and this argument is a