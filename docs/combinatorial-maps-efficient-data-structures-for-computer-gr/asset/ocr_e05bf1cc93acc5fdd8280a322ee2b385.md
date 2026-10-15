The key point of this algorithm is the use once again of the two generic iterators. If i > 2, we use the two sequences (0, 1, …, i − 2, i + 2, …, n) and (1, 0, 2, …, i − 2, i + 2, …, n) to iterate through the two orbits by using the same β links, except for β0 and β1 which are used in reverse order (if i = 2 the two orbits are considered in the same order as they do not contain β1). Since we know that d and d′ are i-sewable, and since the generic iterator uses the indexes given in the sequence in the same order, at each step of the while loop, the two iterators point to two darts in relation by isomorphism f of Def. 45. For this reason, we only need to put the two pointed darts in relation by βi, then move the two iterators to their next positions. Note that the relation is done in both directions as βi is a partial involution (because i ∈ {2, …, n}). The algorithm ends when the two iterators reach their end positions.

Algorithm 44 shows the special case of 1-sew operation. Its principle is similar to the previous algorithm. The only difference is that there are two cases depending if it ∈ ⟨{βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j}⟩(d) or not (as seen in Def. 46 page 142).

# Algorithm 44: 1sewNMap(cm,d,d′): 1-sew two darts for n-maps

Input: cm: an n-map;
        d, d′ ∈ cm.Darts: two 1-sewable darts.
Result: 1-sew darts d and d′.

```
1 it ← generic iterator(cm,d,(3,…,n));
2 it′ ← generic iterator(cm,d′,(3,…,n));
3 while it is not to its end do
4   if it ∈ ⟨{βi ∘ βj | ∀i,j ∈ {3,…,n}, i < j}⟩(d) then i ← 1;
5   else i ← 0;
6   it.Betas[i] ← it′;
7   it′.Betas[inv(i)] ← it;
8   advance it to its next position;
9   advance it′ to its next position;
```

The complexity of the two sew algorithms is linear in the number of darts in the orbit ⟨β1,…,βi−2,βi+2,…,βn⟩(d). In the 1-sew algorithm, all the darts in ⟨{βi ∘ βj | ∀i,j ∈ {3,…,n}, i < j}⟩(d) are marked. Testing if it belongs to this orbit is done in constant time by testing if it is marked.

The i-unsew operation is given in Algorithm 45, for i ∈ {2,…,n}. As for the i-sew algorithm, it follows directly the i-unsew definition (see Def. 47 page 146). It runs through all the darts of the orbit ⟨β1,…,βi−2,βi+2,…,βn⟩(d), and we i-sew darts βi(e) and e to ∅.