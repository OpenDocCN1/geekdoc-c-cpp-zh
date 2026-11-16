
All the properties, presented in the previous chapter, for measurable functions are obviously valid for random variables.

## Theorem 5.1

If X and Y are random variables and c \in R then the following functions are also random variables: cX, |X|, X^n, X + Y, XY and max(X, Y). Two random variables X and Y are independent iff \forall A, B \in B(R), the events { X \in A } and { Y \in B } are independent. The set { X \in A } denotes the set of outcomes \omega for which X(\omega) \in A. In other words, { X \in A } = X^{-1} (A).

## Definition 5.4

```
\vdash \forall p X Y s t. indep_rv p X Y s t \Leftrightarrow \forall A B. A \subseteq subsets s \land B \subseteq subsets t \Rightarrow indep p (PREIMAGE X A I p_space p) (PREIMAGE Y B \cap p_space p)
```

The event { X \in A } is used to define the probability mass function (PMF) of a random variable. The probability mass function p_x of a random variable X is defined as the function assigning to A the probability of the event { X \in A }, i.e., \forall A \in B(R), p_x (A) = p ({ X \in A }) = p ( X^{-1} (A)).

## Definition 5.5

```
\vdash \forall p X. distribution p X = (\lambda A. prob p (PREIMAGE X A \cap p_space p))
```

The cumulative distribution function (CDF) of a random variable is defined as:

F_X (x) = P (X \le x) (5.1)

which can be formalized in HOL4 as:

## Definition 5.6

```
\vdash \forall p X. CDF p X = (\lambda x. distribution p X ( \{ y | y \le x \} ))
```

The joint distribution of two random variables can be formalized in HOL4 as:

## Definition 5.7

```
|- \forall p X Y . joint_distribution p X Y = (\lambda a. prob p (PREIMAGE (\lambda x. (X x, Y x)) a \cap p_space p))
```

Now, the following properties of the joint distribution can be verified in HOL:

```
|- p_{xy} (a \times b) = p_{yx} (b \times a)
|- p_{xy} (a \times b) \leq p_{x} (a)
|- p_{xy} (a \times b) \leq p_{y} (b)
|- FINITE (p_space p) \Rightarrow SIGMA (_(x, y) . p_{XY} f (x, y) g) (X() \times Y()) = 1
|- FINITE (p_space p) \Rightarrow p_{X} (a) = SIGMA (_x. p_{XY} (a_xfg)) Y()
|- FINITE (p_space p) \Rightarrow p_{Y} (b) = SIGMA (_x. p_{XY} (f_xg_b)) X()
|- FINITE (p_space p) \Rightarrow
SIGMA (\lambda (x, y) . p_{XY} { (x, y) } * f x) (X(Q) \times Y(Q)) =
SIGMA (\lambda x. p_{X} { x } * f x) X(Q)
```

## 5.2 FORMALIZATION OF STATISTICAL PROPERTIES

### 5.2.1 Expectation

In this section, we provide a formalization of the expectation of a random variable in HOL (Hasan & Tahar, 2010a). This definition uses the Lebesgue integration formalization and, hence, is valid for both discrete and continuous random variables. The expectation of a random value X is defined as the integral of X with respect to the probability measure. E[X] = \int X dp

## Definition 5.8

```
|- expectation = integral
```

The following properties of the expectation of random variables can be verified based on the above definition:

```
|- \forall X Y . E [ X + Y ] = E [ X ] + E [ Y ]
|- \forall X a . E [ a X ] = a E [ X ]
|- \forall a . E [ a ] = a
|- \forall X Y . X \leq Y \Rightarrow E [ X ] \leq E [ Y ]
|- \forall X Y . X and Y independent \Rightarrow E [XY] = E [ X ] E [ Y ]
```

For the special case when the sample space is finite, the definition of the expectation can be simplified to:

```
|- ∀ p X. FINITE (p_space p) ⇒
E [ X ] = SIGMA (λ x. r * distribution p X { r }) (IMAGE X
(p_space p))
```

We provide an alternative definition for the expectation of real-valued random variables. This formula is derived from Equation 4.5 and provides an easier way to compute the expectation of random variables without the need to work with integrals.

⊢ E[X] = sup_n Σ_{k=0}^{4^n-1} k/2^n × ( F_X((k+1)/2^n) - F_X(k/2^n) ) + 2^n × (1 - F_X(2^n)) (5.2)

### 5.2.2 Variance and Covariance

In the field of probabilistic analysis, it is often desirable to summarize the essential properties of distribution of a random variable by certain suitably defined measures. In the previous section, we formalized one such measure, i.e., the expectation, which yields the weighted average of the possible values of a random variable. Quite frequently, along with the average value, we are also interested in finding how typical is the average value or in other words the chances of observing an event far from the average. One possible way to measure the variation, or spread, of these values is to consider the quantity E|X - E[X]|, where |y| denotes the absolute value of y. However, it turns out to be mathematically inconvenient to deal with this quantity, so a more tractable quantity called variance is usually considered, which returns the expectation of the square of the difference between X and its expectation. Similarly, another closely related measure is the covariance, which is a measure of the correlation between two random variables. The covariance of two random variables X and Y is defined as Cov(X, Y) = E [ (X - E [ X ]) (Y - E [ Y ]) ]. Two random variables X and Y are uncorrelated iff Cov(X, Y) = 0.

Some of the formally verified properties for the variance and covariance include:

```
|- ∀ X. Var (X) = E [ X ^ 2 ] - E [ X ] ^ 2
|- ∀ X Y. Cov (X, Y) = E [ X Y ] - E [ X ] E [ Y ]
|- ∀ X. Var (X) ≥ 0
|- ∀ a ∈ R. Var (aX) = a^2 Var (X)
|- ∀ p X Y. Var (X+Y) = Var (X) + Var (Y) + 2 Cov(X,Y)
|- ∀ X Y. X and Y uncorrelated ⇒ Var (X + Y) = Var (X) + Var (Y)
```

```
⊢ ∀ i j X N. (i ≠ j) ∧ Xi and Xj are uncorrelated => Var(Σ(Xi)) = Σ Var(Xi)
```

## 5.3 HEAVY HITTER PROBLEM

Given a Universe U, a data stream of length n and a parameter λ \in [0, 1], the Heavy Hitter problem is to find the λ-Heavy Hitter list which contains the elements of the Universe that occur in the data stream at least λn times. The algorithms for the Heavy Hitter problem are widely used to identify frequently encountered items of streams in a compact way. For example, they have been used to identify heavily traded stocks in streams of financial transactions, to detect viruses spread in networks, to monitor network traffic for statistical data collection and to detect Distributed Denial of Services (DDoS). An algorithm for the heavy hitter problem is as follows:

```
Input: the frequency λ, a data stream DS and a Universe U with length n
Output: the list L of elements from U occurring at least λ * n times in DS
L ← [ ]
for i = 1 → n do
if freq (DS[i]) ≥ λ then
L ← L INSERT DS[i]
end if
end for
```

The major goal of analyzing such a problem is to predict the behavior of some precise elements in a data stream. For example, controlling specific transactions in a financial flow. The biggest challenge in this analysis is the unpredictable nature of the input data stream. Therefore, probabilistic techniques are used for the analysis where the algorithm is modeled by an appropriate random variable.

In this section, we conduct the formal probabilistic analysis of the heavy hitter problem using theorem proving. For this purpose, we first formalize the above algorithm in higher-order logic along with the random input behavior. This is followed by the formal verification of an interesting performance characteristic, i.e., Chebychev’s inequality based bound on the probability of identifying a heavy hitter, within the sound environment of a theorem prover. The analysis results can

### 5.3.1 Formalization of the Heavy Hitter Problem

The Heavy Hitter Problem can be formalized in HOL4 by modeling the sample set of elements and the data stream as lists (Halali, Hasan & Tahar, 2012). Then we model a function, freq, that returns the frequency of an element in a list.

## Definition 5.9

```
|- ∀ L e. freq e L =
(LENGTH (FILTER (λ r.r = e) L)) / (LENGTH L)
```

where LENGTH returns the length of a list, and FILTER returns a filtered list out of its argument list with elements that satisfy the given condition. The above function will be required later, to report the list of the α-heavy hitter elements. Next, we model another function, HeavyHitter_lst, which takes as parameters two lists and a real value and returns the list of heavy hitters corresponding to the algorithm of heavy hitter problem.

## Definition 5.10

```
|- ∀ L M α. HeavyHitter_lst L M α =
FILTER (λ r. α <= (freq (EL r L) M)) L
```

So far, the formalization has been based on deterministic functions. We now introduce the randomness in our models using appropriate random variables and our probabilistic analysis of the algorithm for the heavy hitter problem would be based upon the characteristics of these random variables. In our analysis, we need a Bernoulli variable X, with outcomes 1 or 0. In order to formalize this random behavior, we have to define a probability space that has the set {0, 1} as its space and power set, POW {0, 1}, as the events space and the probability measure will be a new function that returns pr if the set in parameter implements the fact that f(x), which refers to our random variable in this case, is equal to 1, and returns 1 - pr otherwise. The corresponding probability measure is defined in HOL4 as follows:

## Definition 5.11

```
|- ∀ g pr. mu g pr =
(λ a. if (a = {x | g x = 1}) then pr else (1 - pr))
```
