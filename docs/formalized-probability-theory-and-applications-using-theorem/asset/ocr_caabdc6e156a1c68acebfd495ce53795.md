going to tackle the generic case and then instantiate it for the given border monitoring application. Hence, we simply denote (prob p (p_space p DIFF (udset n k s L Ts q))) by (Pd_wsn p n k s L Ts q) and (delay_wsn p n D k q) as (D_wsn p D n k q). In the context of our application, we basically verify two main properties of interest related to the detection probability of the events of interest and the detection delay. Thus, we easily check in HOL4 that (prob p (p_space p DIFF (udset n k s L Ts (0.28)))) equals

```
1 - ((1 - s) \times \left( 1 - \frac{\lfloor L/T_s \rfloor}{k} \times (0.28) \right)^n - s \times \left( 1 - \frac{\lfloor L/T_s \rfloor}{k} + 1 \times (0.28) \right)^n
```

and, the expected detection delay, (delay_wsn p D n k (0.28)), is

```
\sum_{j=1}^n E(D|c=j) \times C_n^j \times (0.28)^j \times (1-(0.28))^{n-j}
```

where E (D | c = j) represents the expression specified in Equation (14.30). Next, we simply denote Equation (14.31) and Equation (14.32), by (Pd surv p n k s L Ts (0.28)) and (D_surv p D n k (0.28)), respectively. It is important to note that, for space constraints, and in all the asymptotic analysis below, we only mention the main mathematical assumptions related to the used variables in the detection probability and delay.

Hence, we formally verify that the detection probability is an increasing function of n, i.e., a larger n value leads to a better detection probability.

# Lemma 14.1

```
\vdash \forall p k q s L Ts. (1 < k) \land (0 < s < 1) \land (0 < L) \land (0 < Ts) \land (L < s (k-1) \times Ts) \land (0 < q < 1) \Rightarrow (mono_incr (\lambda n. Pd_wsn p n k s L Ts q)) .
```

where mono_incr is the HOL4 definition of an increasing sequence, which we define as follows:

# Definition 14.7

```
\vdash \forall f. mono_incr f \iff \forall n. f n \le f (SUC n) .
```