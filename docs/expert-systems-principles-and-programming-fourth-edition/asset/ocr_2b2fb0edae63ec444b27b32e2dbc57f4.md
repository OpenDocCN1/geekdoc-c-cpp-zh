```
If X is F then Y is G
If X is F then Y is G with CF = α
```

where CF is the certainty factor and α is a numeric value such as 0.5.

(2) partial match between the antecedent and facts which match the antecedent patterns. In nonfuzzy expert systems, a rule does not become activated unless the patterns match the facts exactly. However, in a fuzzy expert system everything is a match of degree and all rules may be activated to some extent unless a threshold is set.

(3) fuzzy quantifiers such as Most, and fuzzy qualifiers such as Very Likely, Quite True, Definitely Possible, and so forth.

Propositions often contain implicit and/or explicit fuzzy quantifiers. As an example, consider the disposition:

```
d = desserts are WONDERFUL
```

The term disposition means a proposition that is usually true, with canonical form:

```
Usually(X is R)
```

where Usually is an implied fuzzy quantifier and R is a constraining relation acting on the constrained variable X to limit the values it may take. Many heuristic rules that people know about are dispositions. In fact, commonsense knowledge is basically a collection of dispositions about the real world.

The disposition may be translated into the explicit propositional forms:

```
p = Usually desserts are wonderful
p = Most desserts are wonderful
```

which may be expressed as a heuristic rule:

```
r = If x is a dessert
then it is likely that x is wonderful
```

Some rules of inference in fuzzy systems are the following:

+   • entailment principle

```
X is F
F C G
X is G
```

+   • dispositional entailment: limiting cases where Usually becomes Always:

```
Usually (X is F)
F C G
Usually (X is G)
```