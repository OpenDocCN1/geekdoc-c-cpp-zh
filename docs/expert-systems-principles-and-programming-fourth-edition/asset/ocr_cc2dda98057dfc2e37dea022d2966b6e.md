+   • compositional rule:

```
X is F
(X,Y) is R
Y is F o R
```

where R is a binary relation over the binary variable (X,Y) and:

```
μ_R o S (y) = sup_x [μ_R(x) ∧ μ_S(x,y)]
```

and the **supremum**, symbolized by **sup**, is the **least upper bound**. Generally the supremum is the same as the max function. The difference arises in cases where there is no maximum value, such as the real-number interval of numbers less than 0. Since there is no maximum real number less than 0, the supremum is used to take 0 as the least upper bound.

+   • generalized modus ponens:

```
X is F
Y is G if X is H
Y is F o (H' ⊕ G)
```

where H' is the fuzzy negation of H and the bounded sum is defined:

```
μ_H' o G(x,y) = 1 ∧ [1 - μ_H(x) + μ_G(y)]
```

The generalized modus ponens does not require that the antecedent "X is H" be identical with the premise "X is F". Notice that this is very different from classical logic, which requires that they match exactly. The generalized modus ponens is actually a special case of the compositional rule of inference. Unlike conventional expert systems, in which modus ponens is the basic rule of inference, the compositional rule of inference is the basic rule in fuzzy expert systems.

Expert systems using approximate reasoning may use a number of different methods such as truth value restriction, and compositional inference. In Whalen's survey of eleven fuzzy expert systems, nearly all used compositional inference. It's difficult to predict which method works best in advance so empirical modeling is used to see which best fits the data. This is not as bad as it sounds since in statistics, the use of linear regression is tried first because it's the simplest and people assume the population distribution is Gaussian. If that doesn't work, they will try a more complex model such as a polynomial fit and so forth until the errors are acceptable.

# 5.6 THE STATE OF UNCERTAINTY

Wow! If you have read every single word in the last five chapters and derived every equation and worked every problem, then you either have an unquench-