$$X = < \sum_{j=0}^{k-1} X_j$$ (13.2)

where Xj is the Bernoulli random variable whose value is 1 in case of a non-empty subset. Similar to the specification of an empty subset in Definition 13.6, we can model a non-empty sub-network by a Bernoulli random variable with the complement probability of (1 – 1/k) “.

# **Definition 13.7**
\(\vdash \forall p \ x \ k \ n. \ sbst\_non\_empty\_rv \ x \ p \ k \ n =\)
\(bernoulli\_distr\_rv \ x \ p \ (1 - (1 - 1/k \ ) \ ”)\)

According to the above description, we model the coverage behavior of a specific point (Equation 13.1) by the following predicate cvrg insty pt that accepts five parameters: p: the probability space, X: a random variable that returns an extended real number, k: the number of sub-networks, s: the summation set whose cardinality is k, and c: the number of nodes covering that point.

# **Definition 13.8**
\(\vdash \forall p \ x \ k \ s \ c. \ cvrg\_insty\_pt \ p \ x \ k \ s \ (c:num) =\)
\(expectation \ p \ (x. \ SIGMA \ (\lambda i. \ x \ i \ x) \ s) \ / \ (\&k)\)

The following mathematical expression for the coverage intensity of a point has been formally verified.

# **Theorem 13.3**
\(\vdash \forall p \ x \ k \ c. \ (prob\_space \ p) \land (FINITE \ (p \ space \ p)) \land (1 < k) \land\)
\(FINITE \ s \land (CARD \ s = k)\)
\(\land (\forall i. \ i \in s) \ sbst\_non\_empty\_rv \ (x \ i) \ p \ k \ c)\)
\(\Rightarrow (cvrg\_insty\_pt \ p \ x \ k \ s \ c = Normal \ ((1 - (1 - 1/(\&k) \ ) \ ”))\)

where

+   - The assumption FINITE (p\_space p) ensures that the sample space is finite.
+   - The assumption ((∀ i. i ∈ s) sbst\_non\_empty\_rv (X i) p k c) indicates that every element of the set s is a random variable of type sbst non empty rv (Definition 13.7).
+   - The HOL function Normal is used to convert a real value to its corresponding value in an extended real.