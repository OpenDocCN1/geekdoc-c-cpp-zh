cyber network and a simple oil and gas pipeline structure. In fact, given the generic nature of the proposed method, we were able to formally verify generic reliability relationships for arbitrary-node cyber network and an arbitrary-component pipeline structure and our results can be specialized to obtain the reliability of any specific network and pipeline as well.

The RBD-based analysis is based on the assumption that the reliability events, associated with the systems’ subcomponents, are mutual independent from one another. This section provides a generic formalization of ensuring mutual independence of n events and we will use it for the formalization of all the RBD configurations later.

Any two events, A and B, are termed as mutually independent iff Pr (A ∩ B) = Pr (A) Pr (B). Generally, reliability assessment of systems involves more than two random variables, i.e., Pr (∩i=0n Li) = ∏i=0n Pr (Li). Thus, we formalize the mutual independence of a list of random variables as (Ahmad, Hasan, Tahar & Hamdi, 2014):

# Definition 12.3

```
|- V p p. L. mutual_indep p L = V L1 n. PERM L L1 ^
2 <= n /\ n <= LENGTH L =>
prob p (inter_set p (TAKE n L1)) =
list_prod (list_prob p (TAKE n L1))
```

# Table 1. HOL4 functions used in Definition 12.3

| Function | HOL Definition |
|---|---|
| PERM | |- V L1 L2. PERM L1 L2 = V x.FILTER(=x) L1 = FILTER(=x) L2 |
| LENGTH | - (LENGTH [] = 0) /\ V h. LENGTH (h::x) = SUC (LENGTH x) |
| TAKE | - (V n. TAKE n ([]:α) = []) /\ V n x xs. TAKE n (x::xs) = if n = 0 then [] else x:TAKE (n - 1) xs |
| inter_list | - (V p. inter_list p [] = p_space p) /\ V p b t. inter_list p (b::t) = b ∩ inter_list p t |
| list_prod | - (list_prod [] = 1) /\ V h t.list_prod (h::t) = h * list_prod t |
| list_prob | - (V p. list_prob p [] = []) /\ V p h t. list_prob p (h::t) = prob p (h) * list_prob p t |
| compl_list | - (V p L. compl_list p L = MAP (λa. p_space p DIFF a) L |
| min | - Vx y.min x y = if x ≤ y then x else y |
| min_rel | - (V f t. min_rel f ([]:)) = 1) /\ V f b t. min_rel f (b::t) = min (f b) (min_rel f t) |