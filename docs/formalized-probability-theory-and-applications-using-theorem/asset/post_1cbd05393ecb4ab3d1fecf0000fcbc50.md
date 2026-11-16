
## 9.1 FORMALIZATION OF RADON-NIKODYM DERIVATIVE

The Radon-Nikodym derivative of a measure v with respect to the measure u is defined as a non-negative measurable function f, satisfying the following formula, for any measurable set A.

\int_A f du = v(A) (9.1)

The Radon-Nikodym derivative is formalized in HOL4 as (Mhamdi, 2013):

```
Definition 9.1
|- RN_deriv m v =
   @f. f IN measurable (X,S) Borel /\ 
   (forall x \in X, 0 <= f x /\ 
   forall a \in S, integral m (\x. f x * Ia x) = v a
```

where @ denotes the Hilbert-choice operator. The existence of the Radon-Nikodym derivative is guaranteed for absolutely continuous measures by the Radon-Nikodym theorem stating that if v is absolutely continuous with respect to u, then there exists a non-negative measurable function f such that for any measurable set A,

\int_A f du = v(A) (9.2)

The Radon-Nikodym theorem can be verified in HOL4 for finite measures, which can be easily generalized to sigma-finite measures.

```
Theorem 9.1
|- forall m v s st.
   measure_space (s, st, m) /\ 
   measure_space (s, st, v) /\ 
   abs_cont (s, st, m) (s, st, v) ==> 
   exists f measurable (s, st) Borel /\ 
   (forall x \in s, 0 <= f x /\ 
   forall a \in st, integral m (\x. f x * Ia x) = v a
```

The formal reasoning about the above theorem is primarily based on the Lebesgue monotone convergence and the following lemma (Lemma 9.1) which, to the best of our knowledge, has not been referred in mathematical texts before:

If P is a non-empty set of extended-real valued functions closed under the max operator, g is monotone over P and g(P) is upper bounded, then there exists a monotonically increasing sequence f(n) of functions, elements of P, such that:

\(sup_x g(f(n)) = sup_x g(f)\) (9.3)

Proving the Radon-Nikodym theorem consists in defining the set F of non-negative measurable functions such that for any measurable set A, \(\int_A f d\mu = \nu(A)\). This set can be verified to be non-empty, upper bounded by the finite measure of the space and closed under the max operator. Next, using the monotonicity of the integral and the lemma above, the existence of a monotonically increasing sequence f(n) of functions in F can be verified such that:

\(sup_x \int_X f_n d\mu = sup_x \int_X f d\mu\) (9.4)

Finally, it can be verified that the function g, defined below, satisfies the conditions of the theorem.

\(\forall x . g(x) = sup_n f_n(x)\) (9.5)

One of the main reasons why the extended reals have been used in the formalization of probability theory is the inability to verify the Radon-Nikodym theorem without considering infinite values. In fact, the Lebesgue monotone convergence is used to prove that:

\(\int_X g d\mu = sup_n \int_X f_n d\mu\) (9.6)

On the other hand, if the extended reals were not used then the proof of Lebesgue monotone convergence requires the sequence f(n) to be convergent, which is not necessarily the case here and cannot be added as an assumption because the sequence f(n) is generated within the proof. The Lebesgue monotone convergence theorem with the extended reals is valid even for sequences that are not convergent since it uses the sup operator instead of the limit lim.

Now, properties of the Radon-Nikodym derivative can be formally verified in a straightforward manner. For instance, for absolutely continuous measures defined over a finite space, the derivative can be verified to be reduced to:

### Theorem 9.2

```
|- ∀ b u v x. x ∈ s ∧ u { x } ≠ 0 ⇒ RN_deriv u v x = v { x } / u { x }
```

The following properties play a vital role in formally reasoning about the Radon-Nikodym derivative and have also been formally verified in HOL.

```
|- ∀x ∈ s ∧ 0 ≤ RN_deriv m v x < ∞
|- RN_deriv m v ∈ measurable (s,st) Borel
|- ∀a ∈ st, integral m (λx. RN_deriv m v x × Ia x) = v a
```

## 9.2 FORMALIZATION OF KULLBACK-LEIBLER DIVERGENCE

The Kullback-Leibler (KL) divergence DKL (u ‖ v) is a measure of the distance between two distributions u and v. It can be used to define most information-theoretic measures, such as the mutual information and entropy and can, hence, be used to provide a unified framework to formalize most information leakage measures. Mathematically, the KL divergence is defined as:

```
DKL(μ ‖ ν) = - ∫x log(dν/dμ) dμ (9.7)
```

where dν/dμ is the Radon-Nikodym derivative of v with respect to u. The KL divergence is formalized in HOL4 as:

### Definition 9.2

```
|- ∀ b m v. KL_divergence b m v =
-integral m (λx. logr b (RN_deriv m v x))
```

where b is the base of the logarithm. DKL is measured in bits when b = 2. This definition can now be used to verify some classical properties of DKL. For instance, for absolutely continuous measures over a finite space, the DKL reduces to:

```
D_{KL}(\mu || \nu) = \sum_{x \in s} \mu \{x\} \log \frac{\mu \{x\}}{\nu \{x\}} (9.8)
```

### Theorem 9.3

```
|- ∀ b u v. KL_divergence b u v =
SIGMA (λx. u { x } logr b (u { x } / v { x })) s
```

Some other formally verified properties of DKL in HOL4 are

```
|- ∀ b u. KL_divergence b u u = 0
```

```
|- ∀ b u v. 1 ≤ b ⇒ 0 ≤ KL_divergence b u v
```

The non-negativity of the KL divergence for absolutely continuous probability measures over finite spaces is extensively used to prove the properties of information theory measures like the mutual information and entropy. Next, we present the use of the KL divergence to formalize the mutual information, Shannon entropy, conditional entropy and the conditional mutual information, which are some of the most commonly used measures of information.

## 9.3 FORMALIZATION OF MUTUAL INFORMATION

The mutual information I (X; Y) of two random variables is a measure of the mutual dependence of the two random variables in the sense that it measures how much uncertainty about one of these variables is reduced when the other variable is known. The mutual information is usually used as a measure of information leakage from the secure inputs X of a program to its public outputs Y. It is defined as the KL divergence between the joint distribution and the product of marginal distributions. The following is a formalization of the mutual information in HOL.

### Definition 9.3

```
|- ∀ X Y. I (X ; Y) = KL_divergence b (joint_distribution p X Y)
prod_measure (distribution p X) (distribution p Y)
```

Various properties of the mutual information have been verified in HOL, such as the non-negativity, symmetry and reduced expression for finite spaces, using the result that the joint distribution is absolutely continuous w.r.t the product of marginal distributions.

```
|- ∀ b X Y p s. I (X; Y) =
SIGMA (λ (x, y). p ( (x, y) ) logr b (p ( (x, y) ) / p ( x ) * p ( y ))) s
```

## 9.4 ENTROPY

The Shannon entropy H(X) is a measure of the uncertainty associated with a random variable. Moreover, it is also a measure of the average information content missing when the value of the random variable is unknown. The Shannon entropy was one of the first measures to be proposed to analyze anonymity protocols and secure communications (Diaz, Seys, Claessens, & Preneel, 2003). It can be defined as the expectation of pX or simply as I (X; X).

### Definition 9.4

```
|- ∀ X. H (X) = I (X; X)
```

It can also be expressed in terms of the KL divergence between p_X and the uniform distribution p'_X where N is the size of the alphabet of X.

### Definition 9.5

```
|- ∀ X N p. H (X) =
log (N) - KL_divergence b (distribution p X) (uniform_dist p X)
```

Cross entropy H(X; Y), which measures how much entropy is contained in a joint system of two random variables, is the entropy of the random variable (X; Y) and hence there is no need for a separate formalization of the cross entropy.

The conditional entropy H (X | Y) quantifies the remaining uncertainty about the random variable X given that the value of the random variable Y is known. It is defined in terms of the KL divergence as follows:

### Definition 9.6

```
|- ∀ X Y N p. H (X | Y) =
log (N) - KL_divergence b (joint_distribution p X Y)
prod_measure (uniform_dist p X)
(distribution p Y)
```
