cost function, then any lower bound for g(n) is also a lower bound for your cost function. Likewise for Θ notation.

The significance of rule (2) is that you can ignore any multiplicative constants in your equations when using big-Oh notation. This rule also holds true for Ω and Θ notations.

Rule (3) says that given two parts of a program run in sequence (whether two statements or two sections of code), you need consider only the more expensive part. This rule applies to Ω and Θ notations as well: For both, you need consider only the more expensive part.

Rule (4) is used to analyze simple loops in programs. If some action is repeated some number of times, and each repetition has the same cost, then the total cost is the cost of the action multiplied by the number of times that the action takes place. This rule applies to Ω and Θ notations as well.

Taking the first three rules collectively, you can ignore all constants and all lower-order terms to determine the asymptotic growth rate for any cost function. The advantages and dangers of ignoring constants were discussed near the beginning of this section. Ignoring lower-order terms is reasonable when performing an asymptotic analysis. The higher-order terms soon swamp the lower-order terms in their contribution to the total cost as n becomes larger. Thus, if T(n) = 3n⁴ + 5n², then T(n) is in O(n⁴). The n² term contributes relatively little to the total cost for large n.

Throughout the rest of this book, these simplifying rules are used when discussing the cost for a program or algorithm.

# 3.4.5 Classifying Functions

Given functions f(n) and g(n) whose growth rates are expressed as algebraic equations, we might like to determine if one grows faster than the other. The best way to do this is to take the limit of the two functions as n grows towards infinity,

limₙ→∞ f(n)/g(n).

If the limit goes to ∞, then f(n) is in Ω(g(n)) because f(n) grows faster. If the limit goes to zero, then f(n) is in O(g(n)) because g(n) grows faster. If the limit goes to some constant other than zero, then f(n) = Θ(g(n)) because both grow at the same rate.

# Example 3.8 If f(n) = 2n log n and g(n) = n², is f(n) in O(g(n)), Ω(g(n)), or Θ(g(n))? Because

n² / (2n log n) = n / (2 log n),