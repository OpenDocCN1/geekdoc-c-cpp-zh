prob p ( n ( ... ) )
=> (prob p (p_space p DIFF (udset n k s L Ts q)) =
1 - (1 - s) x ( ... )

where

+   - sn_covers p is the Binomial random variable.
+   - intr_distr_rv is the intrusion random variable.
+   - sbst_empty_sch_rv is the higher-order-logic formalization of an empty sub-network in HOL. We modeled such behavior by a Bernoulli random variable with success probability ( 1 - 1/k ), and the corresponding HOL4 function is as follows:

```
|- !V X p pr. bernoulli_distr_rv X p pr = (real random variable
X p) ^
(IMAGE p (X p_space p) = {0 ; 1} ^
(distribution p X {1} = pr).
```

+   - The assumption (indep_rv p IT X Borel Borel) ensures the independence between the two random variables X and IT.
+   - The HOL function (udset n k s L Ts q) models the main event of non-detection UD, as specified in Equation (14.1). This function depends on various design parameters, i.e., n: the number of sensor nodes, k: the number of sub-networks, L: the intrusion period, Ts: the scheduling time slot, and s: the remainder of L in terms of Ts.
+   - The assumption (cond p prob p (udset n k L Ts q) (PREIMAGE X {0 } p p_space p) = 1) reflects the first case, discussed at the beginning of this subsection.
+   - The events A12, A22, and Hic are the HOL4 formalizations of the same events used throughout our mathematical reasoning.
+   - The last assumption is the probability equality discussed just after Equation (14.9).