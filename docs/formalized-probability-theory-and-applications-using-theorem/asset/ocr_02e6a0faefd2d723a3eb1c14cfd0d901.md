Now, we can use Definition 12.19 to guarantee that the random variable list argument of the function pipeline contains exponential random variables only and thus verify the following simplified expression for the pipeline reliability.

# Theorem 12.15

```
⊢ ∀ p L x C. prob_space p ∧ (events p = POW (p_space p)) ∧
0 ≤ x ∧ x ≤ 2 ∧ LENGTH (rel_event_list p L x) ∧ mutual_indep p
(rel_event_list p L x) ∧
list_exp p C L ∧ (LENGTH C = LENGTH L) ⇒
(pipeline p (rel_event_list p L x) = exp (-list_sum C * x))
```

The first five assumptions are the same as the ones used in Theorem 12.9. The sixth assumption list exp p C L ensures that the list of random variable L contains all exponential random variables with corresponding failure rates given in list C. The next assumption guarantees that the lengths of the two lists L and C are the same. While the conclusion of Theorem 12.5 represents desired reliability relationship for the given pipeline model. Here the function list sum recursively adds the elements of its list argument and is used to add the failure rates of all exponentially distributed random variables, which are in turn used to model the individual segments of the series RBD of the pipeline. The proof of Theorem 12.15 is based on Theorem 12.9 and some properties of the exponential function exp. The reasoning was very straightforward (about 100 lines of HOL code) compared to the reasoning for the verification of Theorem 12.9, which involved probability- theoretic guidance. This fact illustrates the usefulness of our core formalization for conducting the reliability analysis of pipelines.

The distinguishing features of this formally verified result include its generic nature, i.e., all the variables are universally quantified and thus can be specialized to obtain the reliability of the given pipeline for any given parameters, and its guaranteed correctness due to the involvement of a sound theorem prover in its verification, which ensures that all the required assumptions for the validity of the result are accompanying the theorem. Another point worth mentioning is that the individual failure rates of the pipeline segments can be easily provided to the above theorem in the form of a list, i.e., C. The above mentioned benefits are not shared by any other computer based reliability analysis approach for oil and gas pipelines and thus clearly indicate the usefulness of the proposed approach.