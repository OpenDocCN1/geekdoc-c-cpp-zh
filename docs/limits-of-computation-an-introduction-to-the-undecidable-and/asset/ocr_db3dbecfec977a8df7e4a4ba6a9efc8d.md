# 232 Limits of Computation

become O(2^(n!)) by the proof given. If some means of doing the transformation could be found that did not introduce an exponent, we would have P = NP.

+   2. Is NP = co-NP?

This is another open question. Notice that if NP = P, then NP = co-NP. However, the reverse is not true. It is possible that NP = co-NP but still NP ≠ P.

Can any problem in co-NP also be NP-complete? It is possible that problems such as SAT might also be NP-complete (although it is not clear that such problems are even in NP). However, if there are any problems in co-NP ∩ NP-complete, then NP = co-NP.

# Theorem 10.5

If any NP-complete problem is also in co-NP, then NP = co-NP.

# Proof

Assume some NP-complete problem Z is also in co-NP. This means (1) for any X in NP, X ≤p, Z, and (2) Z is also in NP.

First, to show NP ⊆ co-NP, assume that X is in NP. But, X ≤p Z so X ≤p Z (why?). Now X is polynomially reducible to an element of NP, so X is also in NP. Then, of course, X is in co-NP.

One must also show that co-NP ⊆ NP; the proof is very similar and leaves as an exercise.

# 10.5 ARE THERE ANY PROBLEMS IN NP-P BUT NOT NP-COMPLETE?

Essentially all the decision problems that we have examined so far have in either P or NP-complete. It would seem that there should be problems that are harder than P but not as hard as in NP-complete. We might call such problems NP-intermediate. The next theorem says that as long as P ≠ NP, such problems must exist. However, it (so far) is not possible to describe a good example in this class.