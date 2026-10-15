# Algorithm 45: unsewNMap(cm,d,i): i-unsew two darts for n-maps

Input: cm: an n-map;
 d ∈ cm.Darts: a non i-free dart;
 i ∈ {2,…,n}.
Result: i-unsew darts d and βi(d).

```
1 foreach dart e ∈ ⟨β1,…,βi−2,βi+2,…,βn⟩(d) do
2   (e.Betas[i]).Betas[i] ← cm.null_dart;
3   e.Betas[i] ← cm.null_dart;
```

{3,…,n}, i < j}⟩(d) and o2 = ⟨β3,…,βn⟩(β1(d))\{⟨{βi∘βj | ∀i,j ∈ {3,…,n}, i < j}⟩(β1(d)).

# Algorithm 46: 1unsewNMap(cm,d): 1-unsew two darts for n-maps

Input: cm: an n-map;
 d ∈ cm.Darts: a non 1-free dart.
Result: 1-unsew darts d and β1(d).

```
1 foreach dart e ∈ ⟨β3,…,βn⟩(d) do
2   if e ∈ {⟨{βi∘βj | ∀i,j ∈ {3,…,n}, i < j}⟩}(d) then
3     (e.Betas[1]).Betas[0] ← cm.null_dart;
4     e.Betas[1] ← cm.null_dart;
5 foreach dart e ∈ ⟨β3,…,βn⟩(d.Betas[1]) do
6   if e ∉ {⟨{βi∘βj | ∀i,j ∈ {3,…,n}, i < j}⟩}(d.Betas[1]) then
7     (e.Betas[1]).Betas[0] ← cm.null_dart;
8     e.Betas[1] ← cm.null_dart;
```

The complexity of the two unsew algorithms is linear in the number of darts of the traversed orbit ⟨β1,…,βi−2,βi+2,…,βn⟩(d). For the 1-unsew operation, the darts belonging to {⟨{βi∘βj | ∀i,j ∈ {3,…,n}, i < j}⟩}(d) and to {⟨{βi∘βj | ∀i,j ∈ {3,…,n}, i < j}⟩(β1(d))} are marked. Test if a dart belongs to these orbits or not can thus be done in constant time.

# 5.5 Complements

In this section, some additional definitions and properties are studied: the notion of boundary map; the relations between n-Gmaps and n-maps; a classification of 2-maps, corresponding to the classification of surfaces; the duality notion.

Algorithms corresponding to these new notions are not described, but they