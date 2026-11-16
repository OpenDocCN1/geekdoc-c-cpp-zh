```
T(Age) = {OLD, Very OLD, Very Very OLD, ...}
```

can be generated recursively using the following syntactic rule:

```
T^(i+1) = {OLD} ∪ {Very T^i}
```

For example,

```
T^0 = ∅ (the null set)
T^1 = {OLD}
T^2 = {OLD, Very OLD}
T^3 = {OLD, Very OLD, Very Very OLD}
```

The semantic rule associated with T(L) defines the meaning of a term, Li, in L, by a fuzzy set. For example, the semantic rule for Very OLD could be defined as:

```
Very OLD = μ^2_OLD
```

where the membership function could be defined as the S-function following:

```
μ_OLD(X) = S(x; 60, 70, 80)
```

A primary term is a term such as YOUNG, OLD, CHOCOLATE, STRAWBERRY, and so on, whose meaning must be defined before a hedge. Hedges modify the meaning of the primary terms to yield other terms in a term set, such as Very YOUNG, Very OLD, Very CHOCOLATE, Slightly CHOCOLATE, and so forth. The meaning of the hedged fuzzy sets is determined by applying the appropriate fuzzy set operators. For example,

```
μ_Very CHOCOLATE = μ^2_CHOCOLATE
μ_Not CHOCOLATE = 1 − μ_CHOCOLATE
μ_More or Less CHOCOLATE = μ^0.5_CHOCOLATE
μ_Not Very CHOCOLATE = 1 − μ_Very CHOCOLATE
```

Just as conventional language grammars can be defined by BNF notation (see Section 2.2), so too can a fuzzy grammar. In fact, the grammar described in Section 2.2 used a fuzzy modifier, “heavy,” as in:

```
<adjective> → heavy
```