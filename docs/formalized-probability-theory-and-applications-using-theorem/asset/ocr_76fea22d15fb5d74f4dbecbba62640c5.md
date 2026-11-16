# 9.1 FORMALIZATION OF RADON-NIKODYM DERIVATIVE

The Radon-Nikodym derivative of a measure v with respect to the measure u is defined as a non-negative measurable function f, satisfying the following formula, for any measurable set A.

\int_A f du = v(A) (9.1)

The Radon-Nikodym derivative is formalized in HOL4 as (Mhamdi, 2013):

```
Definition 9.1
|- RN_deriv m v =
   @f. f IN measurable (X,S) Borel /\ 
   (forall x \in X, 0 <= f x /\ 
   forall a \in S, integral m (\x. f x * X Ia x) = v a
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
   (forall x \in s, 0 <= f x <^> 
   forall a \in st, integral m (\x. f x * X Ia x) = v a
```