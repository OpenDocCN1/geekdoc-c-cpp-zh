```
$2^{2(k+1)} - 1$ is also divisible by 3:

\( 2^{2(k+1)} - 1 = 2^{2k+2} - 1 \) \quad properties of exponents
\( = 2^{2k} \cdot 2^2 - 1 \)
\( = 4 \cdot 2^{2k} - 1 \) \quad algebra
\( = 4 \cdot 2^{2k} - 4 + 4 - 1 \)
\( = 4(2^{2k} - 1) + 3 \) \quad algebra
\( = 4(3m) + 3 \) \quad the inductive hypothesis
\( = 3(4m + 1) \) \quad algebra
```

and from the last line we see that \( 2^{2k+1} \) is in fact divisible by 3. (The third step—subtracting and adding 4—was done to enable us to use our inductive hypothesis.)

Altogether, we have proved that P(0) holds and that, for all k, P(k) \(\rightarrow\) P(k + 1) is true. Therefore, by the principle of induction, P(n) is true for all n in N, i.e. \( 2^{2n} - 1 \) is divisible by 3 for all n in N. \(\blacksquare\)

The principal of mathematical induction gives a method for proving P(n) for all n in the set N. It should be clear that if M is any natural number, a similar method can be used to show that P(n) is true for all natural numbers n that satisfy n \(\ge\) M. Just start the induction with a base case of n = M instead of with a base case of n = 0. I leave the proof of this extension of the principle of induction as an exercise. We can use the extended principle of induction to prove a result that was first mentioned in Section 1.1.

# **Theorem 1.9.** Suppose that a compound proposition contains exactly n propositional variables, where n \(\ge\) 1. Then there are exactly 2\(^n\) different ways of assigning truth values to the n variables.

# **Proof.** Let P(n) be the statement “There are exactly 2\(^n\) different ways of assigning truth values to n propositional variables.” We will use induction to prove the P(n) is true for all n \(\ge\) 1.

Base case: First, we prove the statement P(1). If there is exactly one variable, then there are exactly two ways of assigning a truth value to that variable. Namely, the variable can be either true or false. Since 2 = 2\(^1\), P(1) is true.

Inductive case: Suppose that P(k) is already known to be true. We want to prove that, under this assumption, P(k + 1) is also true. Suppose that p\(_1\), p\(_2\), ..., p\(_{k+1}\) are k + 1 propositional variables. Since we are assuming