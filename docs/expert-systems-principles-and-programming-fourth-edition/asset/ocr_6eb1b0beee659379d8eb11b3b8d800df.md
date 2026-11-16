| Hedge | Operator Definition |
|---|---|
| Very F | CON(F) = F² |
| More or Less F | DIL(F) = F^0.5 |
| Plus F | F^2.5 |
| Not F | 1 - F |
| Not Very F | 1 - CON(F) |
| Slightly F | INT [NORM (PLUS F And NOT (VERY F))] |

As shown by the “Not Very F” hedge, other compound hedges can be made by combining operators. Notice that the “And” in the “Slightly” hedge is the fuzzy set operator for intersection, ∩, acting on the fuzzy sets “Plus F” and “Not (Very F)”.

The hierarchy of the linguistic variable Appetite is illustrated in Figure 5.16. The LIGHT and HEAVY fuzzy sets are assumed to be S-functions while the MODERATE set is taken as a Π-function.

![](bbox=[0.12, 0.43, 0.92, 0.68])

Notice that there is overlap of the fuzzy sets such as LIGHT and MODERATE and even LIGHT and HEAVY. In classical crisp sets there would be no overlap since all these sets would be disjoint. That is, a LIGHT appetite could not be a MODERATE or HEAVY appetite. However, in fuzzy sets there are usually not (unless defined) sharp boundaries between sets.

The hedged sets are shown as dashed curves within the borders of the fuzzy sets. The hedges, such as Very, act as modifiers to the linguistic values to yield the fuzzy sets Very LIGHT, Very MODERATE, and Very HEAVY.

A linguistic variable must have a valid syntax and semantics, which can be specified by fuzzy sets or rules. A syntactic rule defines the well-formed expressions in T(L). For example, the term-set: