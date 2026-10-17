
![](img/6ba3cf72cbe3568e76a174448323bb33_237_1.png)

## FIGURE 6.27

1-contraction for 2-Gmap.

- (a) 2-Gmap `G`.
- (b) 2-Gmap `$G_{C_1}\{3,4,9,10\}$`.

![](img/6ba3cf72cbe3568e76a174448323bb33_237_2.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_237_3.png)

## FIGURE 6.28

2-contraction for 2-Gmap.

- (a) 2-Gmap `G`.
- (b) 2-Gmap `G_{C2}({1, 2, 3, 4})`.

In 2D, the edge contraction is the dual of the edge removal: cf. Fig. 6.27. In this example, edge `{3, 4, 9, 10}` is contracted, by modifying `α₁` for the four darts `2`, `5`, `11` and `18`. For each dart, a path of darts is followed, starting with `α₁` and applying `α₁ ∘ α₀`. In the resulting 2-Gmap `G_{C₁}({3, 4, 9, 10})` (cf. Fig. 6.27(b)), edge `{3, 4, 9, 10}` is contracted and its two incident vertices are merged.

In 2D, the face contraction is the dual of the vertex removal: cf. Fig. 6.28. Face `{1, 2, 3, 4}` is contracted by modifying `α₂` for the four darts `5`, `6`, `13` and `14`. For each dart, a path of darts is computed, starting with `α₂` and applying `α₂ ∘ α₁`. In the resulting 2-Gmap `G_{C₂}({1, 2, 3, 4})` (cf. Fig. 6.28(b)), face `{1, 2, 3, 4}` is contracted, and its two incident edges are merged.

The contractibility condition characterizes the i-cells which can be contracted: cf. Def. 63. This condition can be deduced from the i-removability condition, by replacing i + 1 (resp. i + 2) by i − 1 (resp. i − 2), according to duality.

### Definition 63 (contractible cell)
An i-cell `C` in an n-Gmap `G = (D, α₀, …, αₙ)` is contractible if:
- `i = 1`;
- or `1 < i ≤ n`, and, `∀d ∈ C, α_{i−1} ∘ α_{i−2}(d) = α_{i−2} ∘ α_{i−1}(d)`.

The i-contraction operation can be deduced from the i-removal operation, by duality. Let `C` be a contractible i-cell. The n-Gmap resulting from the i-contraction of `C` is obtained by removing the darts of `C`, and by modifying `α_i` for the darts linked with `C`, by following the paths of darts corresponding to `(α_i ∘ α_{i−1})^k ∘ α_i`.

### Definition 64 (cell contraction)
Let `G = (D, α₀, …, αₙ)` be an n-Gmap and `C` be a contractible i-cell. Let `D^S = α_i(C) \ C` be the set of darts i-linked

![](img/6ba3cf72cbe3568e76a174448323bb33_238_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_239_0.png)

# **图 6.29**

1-收缩一个悬挂边。

(a) 2-Gmap `$G$`；边 `{3,4,5,6}` 是一个悬挂边。

(b) 2-Gmap `$G_{C_1}(\{3,4,5,6\})$`。

with `C` which do not belong to `C`. The n-Gmap resulting from the i-contraction of `C` in `G` is `G_{C_i}=(D',α'_0,…,α'_n)` defined by:
- `D'=D\setminus C`;
- `∀ j∈{0,…,n}, j≠ i, α'_j=α_j\vert_{D'}`;
- `∀ d∈ D'\setminus D^S, α'_i(d)=α_i(d)`;
- `∀ d∈ D^S, α'_i(d)=(α_i∘α_{i-1})^k∘α_i(d)`,  
  `k` being the smaller positive integer such that `(α_i∘α_{i-1})^k∘α_i(d)∈ D^S`.

As for the removal operation, `k` can be greater than 1. For instance, a dangling edge is contracted in the example presented in Fig. 6.29. Starting from dart `2`, the dart corresponding to `(α_1∘α_0)^2∘α_1` leads to dart `7`, which does not belong to the contracted edge. Note that removing or contracting edge `{3,4,5,6}` produce, in this configuration, the same 2-Gmap.

It is easy to prove that given an n-Gmap `G` and a contractible i-cell `C`, `G_{C_i}(C)` obtained by the contraction of `C` in `G` is an n-Gmap. Note that the contraction operation can be extended in order to simultaneously contract several disjoint cells of same or different dimensions. Moreover, a general operation can be defined in order to simultaneously contract and remove several disjoint cells of same or different dimensions (see [77]).

The algorithms implementing the test of i-contractibility condition and the contraction operation, given in Algorithms 55 and 56, correspond to the algorithms described for the removal operation, in which `i+1` (resp. `i+2`) is replaced by `i-1` (resp. `i-2`).

The complexities of these two algorithms are the same than the complexities for the removal operation, i.e. linear in number of darts of the contracted cell.

# Algorithm 55: isContractibleNGMap(gm,d,i): test if an i-cell is contractible for n-Gmaps

```
Input: gm: an n-Gmap;
    d ∈ gm.Darts: a dart;
    i ∈ {0,...,n}.
Output: True iff c_i(d) is contractible.
1 if i = 0 then return false;
2 if i = 1 then return true;
3 foreach dart d' ∈ c_i(d) do
4   if d'.Alphas[i - 2].Alphas[i - 1] ≠ d'.Alphas[i - 1].Alphas[i - 2]
5     then
6       return false;
7 return true;
```

# Algorithm 56: contractNGMap(gm,d,i): contract an i-cell for n-Gmaps

```
Input: gm: an n-Gmap;
    d ∈ gm.Darts: a dart such that c_i(d) is contractible;
    i ∈ {1,...,n}.
Result: Contract the i-cell c_i(d).
1 ma ← reserveMarkNGMap(gm);
2 mark all the darts in c_i(d) for ma;
3 foreach dart d' ∈ c_i(d) do
4   d1 ← d'.Alphas[i];
5   if not isMarkedNGMap(d1,ma) then
6     d2 ← d'.Alphas[i - 1].Alphas[i];
7     while isMarkedNGMap(d2,ma) do
8       d2 ← d2.Alphas[i - 1].Alphas[i];
9     d1.Alphas[i] ← d2;
10 foreach dart d' ∈ c_i(d) do
11   remove d' from gm.Darts;
12 freeMarkNGMap(gm,ma);
```

# FIGURE 6.30

1-contraction for 1-map.

- (a) 1-map `M`.
- (b) 1-map `M_{C1}({4})`.

![](img/6ba3cf72cbe3568e76a174448323bb33_241_0.png)

# FIGURE 6.31

1-contraction for 2-Gmap.

- (a) 2-map `M`.
- (b) 2-map `M_{C1}({4,5})`.

![](img/6ba3cf72cbe3568e76a174448323bb33_241_1.png)

## 6.3.2 For n-maps

As explained above, the i-contraction operation is the dual of the (n − i)-removal operation. In 1D, as illustrated in the example given in Fig. 6.30, the 1-contraction is the dual of the 0-removal. In this example, edge `{4}` is contracted, by setting `β′1(3) = 5`. Note that this produces the same 1-map than the removal of vertex `{4}`.

Figure 6.31 represents an example of 1-contraction in a 2-map. Edge `{4,5}` is contracted by modifying `β1` for darts `3` and `9`, by following paths of darts related to `β1 ∘ β1`. So, `β′1(3) = 1` and `β′1(9) = 6`. Edge `{4,5}` is contracted and its two incident vertices are merged.

For the example represented in Fig. 6.32, face `{1,2}` is contracted, by modifying `β2` for darts `3` and `7`, by following paths of darts related to `β2 ∘ β1 ∘ β2`.

![](img/6ba3cf72cbe3568e76a174448323bb33_242_0.png)

# FIGURE 6.32

2-contraction for 2-map.

- (a) 2-map `M`.
- (b) 2-map `M_{C2}({1,2})`.

So, `β₂'(3) = 7` and `β₂'(7) = 3`. Face `{1,2}` is contracted and its two incident edges are merged.

The contractibility condition is defined in Def. 65. This definition is the direct transposition of the same definition for n-Gmaps. The only difference is the use of `β_{i-2}^{-1}` instead of `α_{i-2}`; this is important for `i = 2` and `i = 3`, since `β₁` is a partial permutation.

### Definition 65 (contractible cell)
An i-cell `C` in an n-map `M = (D, β₁, …, βₙ)` is contractible if:
- `i = 1`;
- or `1 < i ≤ n`, and `∀d ∈ C, β_{i-1} ∘ β_{i-2}(d) = β_{i-2}^{-1} ∘ β_{i-1}(d)`.

Note that when `i = 2`, this condition becomes `β₁ ∘ β₀(d) = β₁ ∘ β₁(d)`. Thus a face, i.e. a 2-cell, is contractible if each of its darts is either a loop, i.e. it is linked with itself by `β₁`, or belongs to a cycle of two darts linked by `β₁`. Indeed, all other configurations are prohibited by this condition.

The i-contraction operation, for `i ≥ 2`, is defined in Def. 66.

### Definition 66 (cell contraction)
Let `M = (D, β₁, …, βₙ)` be an n-map, and `C` be a contractible i-cell, `i ≥ 2`. Let `D^S = βᵢ(C) \ C`. The n-map resulting from the i-contraction of `C` in `M` is `M_{Cᵢ} = (D', β₁', …, βₙ')`, defined by:
- `D' = D \ C`;
- `∀j ∈ {1, …, n}, j ≠ i, βⱼ' = βⱼ|_{D'}`;
- `∀d ∈ D' \ D^S, βᵢ'(d) = βᵢ(d)`;
- `∀d ∈ D^S, βᵢ'(d) = (βᵢ ∘ β_{i-1})ᵏ ∘ βᵢ(d)`, `k` being the smaller positive integer s.t. `(βᵢ ∘ β_{i-1})ᵏ ∘ βᵢ(d) ∉ C`.

![](img/6ba3cf72cbe3568e76a174448323bb33_243_0.png)

# **FIGURE 6.33**

1-contraction of a dangling edge.

(a) 2-map `$M$`; edge `${2,3}$` is dangling.

(b) 2-map `$M_{C_1}({2,3})$`.
