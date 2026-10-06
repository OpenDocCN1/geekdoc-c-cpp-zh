246 ■ Limits of Computation

+   2. If E begins with $\exists x_i$, then it only needs to be true for either 0 or 1.
So, first evaluate recursively with the quantifier removed and 0 substituted for $x_i$.
If true, accept (no need for another recursive call).
Otherwise, reevaluate with 1 for $x_i$, if true accept.
\u200a\003. If E begins with $\forall x_i$, then it must be true for both 0 and 1.
Again, substitute 0 for $x_i$, and call recursively; if false, there is no need to call recursively.
If true with $x_i = 0$, return result of call with $x_i = 1$.

The depth of the recursion is the number of variables, and at each stage, need only store the value of the variable. Thus, the space used is linear in the number of variables.

# Theorem 10.14

QBF is PSPACE-hard.

# Proof

We need to show that any problem X solved by a TM M in polynomial space $P(n)$, with n the length of the input, can be polynomially reduced to QBF. As in Cook-Levin, we can encode Turing machine configurations with Boolean variables.

If we write all the Boolean expressions as in Cook-Levin, we have expressions as $S[i, j, t]$ for cell i holds symbol j at time t, where i is bounded by polynomially space, j is bounded by the constant $|Q|$, but t is only bounded by $2^{Kp(n)}$. That will not do.

So, we will use a version of reachability to construct a reduction.
Suppose $c_1$ and $c_2$ are two configurations of a polynomially space-bounded TM.

Reach($c_1, c_2, t$) will be a quantified Boolean formula that is true exactly when $c_2$ is reachable from $c_1$ in $t$ steps.

```
Reach($c_1, c_2, 0$) $\Leftrightarrow$ $c_1 = c_2$
```

Reach($c_1, c_2, 1$) $\Leftrightarrow$ $c_2$ is reachable from $c_1$ by one move