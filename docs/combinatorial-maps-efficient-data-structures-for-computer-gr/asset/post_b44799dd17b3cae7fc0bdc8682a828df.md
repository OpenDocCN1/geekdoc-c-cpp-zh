
## FIGURE 5.9

Two examples of non 3-sewable darts in a 3-map.

(a) Darts 1 and 5 are not 3-sewable. It is not possible to define a one to one mapping, since the two 2-cells do not have the same number of darts.

(b) Darts 8 and 12 are not 3-sewable. Let f be the one to one mapping defined by f(8) = 12, f(9) = 15, f(10) = 14 and f(11) = 13. β₁(f(8)) = β₁(12) = ∅ while f(β₁⁻¹(8)) = f(11) = 13. This is not an isomorphism.

An example of 3-sew operation in a 3-map is presented in Fig. 5.8. Two 2-cells are identified by linking two by two by β₃ all the darts belonging to the two initial faces. This identification of faces involves the identification of the boundaries of the two faces (each pair of edges and each pair of vertices of the two faces in relation by the isomorphism f are identified two by two). Such 3-sew operation is not always possible: the two initial faces must be 3-sewable, i.e. they must have the same structure. In this example, it is easy to verify that darts 1 and 5 are 3-sewable. o₁ = {1,2,3,4} and o₂ = {5,6,7,8} are isomorphic, the isomorphism f is defined by f(1) = 5, f(2) = 8, f(3) = 7 and f(4) = 6, and for each dart e ∈ o₁, β₁(f(e)) = f(β₁⁻¹(e)).

The 3-sew operation cannot be applied to the two examples depicted in Fig. 5.9. In the first example, darts 1 and 5 are not 3-sewable since faces c₂(1) and c₂(5) do not have the same number of darts. Thus no one to one mapping exists between o₁ and o₅. In the second example, the two faces c₂(8) and c₂(12) do not have the same structure: the first one has no 1-boundary while the second one has one 1-boundary. Thus no isomorphism exists between o₈ and o₁₂.

## 5.2.3 Unsew Operations

The i-unsew operation is defined in Def. 47 (in Def. 48 for the specific case of the 1-unsew operation); it is the inverse of the i-sew operation. It is always possible to i-unsew non i-free darts.

## Definition 47 (i-unsew) Let M = (D, β₁, …, βₙ) be an n-map, i ∈

![](img/6ba3cf72cbe3568e76a174448323bb33_168_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_168_1.png)

{2, …, n} and let d ∈ D be a non i-free dart. The n-map obtained from M by i-unsewing d and βi(d) is Mi-unsew(d) = (D, β1, …, βi−1, βi′, βi+1, …, βn), where βi′ is defined by: ∀e ∈ D,

- if e ∈ ⟨β1, …, βi−2, βi, βi+2, …, βn⟩(d), βi′(e) = ∅;
- otherwise, βi′(e) = βi(e).

The i-unsew operation consists in setting βi to ∅ for each dart of the orbit ⟨β1, …, βi−2, βi, βi+2, …, βn⟩(d). So, the i-unsew applied to any dart of this orbit produces the same result.

For the 1-unsew operation given in Def. 48, two different orbits must be considered: first o1 = {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(d) is all the darts of the first edge having the same orientation than d, second o2 = ⟨β3, …, βn⟩(β1(d)) \ {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(β1(d)) is all the darts of the second edge having the opposite orientation than d. Each dart in o1 and in o2 must be linked by β1 with ∅, all the other relations are not modified. In case of a folded edge, o1 ∪ o2 is the set of all the darts of the folded edge.

## Definition 48 (1-unsew) Let M = (D, β1, …, βn) be an n-map and d ∈ D be a non 1-free dart. Let o1 denote ⟨{βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j}⟩(d) and o2 denote ⟨β3, …, βn⟩(β1(d)) \ {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(β1(d)). The n-map obtained from M by 1-unsewing d and β1(d) is M1-unsew(d) = (D, β1′, β2, …, βn), where β1′ is defined by: ∀e ∈ D,

- if e ∈ o1 ∪ o2: β1′(e) = ∅;
- otherwise: β1′(e) = β1(e).

It can be proven that i-sew and i-unsew are inverse from each other: applying i-sew to two i-free darts d and d′, and then applying i-unsew to d, produces the original n-map; applying i-unsew to dart d, which is non i-free, and then applying i-sew to d and d′, such that d and d′ were originally linked by βi, produces the original n-map. As a consequence, we can see examples of unsew operations by looking at the examples of sew operations and regarding figures in reverse direction. For example, considering the 3-map given in Fig. 5.6(b) and applying the 1-unsew operation to dart 4, the 3-map represented in Fig. 5.6(a) is obtained. As another example, starting from the 3-map given in Fig. 5.8(c), the 3-map given in Fig. 5.8(a) is obtained by applying the 3-unsew operation to dart 1.

## 5.3 Completeness, Multi-Incidence

Any n-map can be built thanks to the basic operations, by following one of the two basic construction methods. The first one consists in applying

corresponds to the 3-sew operation, producing the 3-map shown in (d): it corresponds to the 3D subdivided object shown in (h).

The inverse operations can be applied in order to destroy a given n-map: this corresponds exactly to the decomposition process described for the intuitive presentation of n-maps (cf. Section 3.1). First, n-unsew operations are applied until having all the darts n-free, then the dimension of the n-map is decreased. This process is iterated until obtaining in 1D a set of darts on which β₁ is equal to ∅. As examples of this “destruction process”, we can consider the examples given for the construction process in reverse direction (cf. Figs. 5.10 and 5.11), and apply i-unsew (resp. decrease dimension) operations instead of i-sew (resp. increase dimension) operations.

## 5.3.2 Construction Directly in a Given Dimension

The second basic construction method consists in working directly in dimension n. Starting with an empty n-map, the operation which adds an isolated dart is applied as many times as necessary. Next, any i-sew operation can be applied, for i ∈ {1, …, n} (contrary to the previous construction where only k-sew operations can be applied to a k-map).

Fig. 5.12 represents an example of the construction of the object depicted in Fig. 5.10, applying this second construction method. The main differences with the first one are:

- the initial map is an n-map having its final dimension, and containing isolated darts (here a 2-map, see Fig. 5.12(a));
- different sew operations can be applied, in any order; for example, 1-sew operations can be first applied (see Fig. 5.12(b)), and then the 2-sew operation; conversely, 2-sew operations can be first applied (see Fig. 5.12(c)), then 1-sew operations. In both cases, the same 2-map is obtained: cf. Fig. 5.12(d).

A second construction of the object depicted in Fig. 5.11 is presented in Fig. 5.13. The initial 3-map contains a set of isolated darts (see (a)). Then the sew operations can be applied in any order. For example, the same order than in Fig. 5.11 can be followed: start by 1-sew operations, then 2-sew operations and finish by 3-sew operation. The 3-maps obtained after each step are similar to the ones in Fig. 5.11(a), (b), (c) and (d), the only difference being the dimension of the maps which is always 3 along the whole construction process. For this reason, the corresponding cellular objects are different since each dart describes always a part of a vertex, an edge, a face and a volume (contrary to the objects shown in Fig. 5.11).

Another order is chosen in Fig. 5.13. First, 3-sew operations are applied; the resulting 3-map is shown in (b). Then, 1-sew operations are applied, producing the 3-map shown in (c). The four 1-sew operations between darts that are not 3-free imply the modification of β₁ for the darts linked by β₃ (in order

## FIGURE 5.10

Construction of a 2D object by using the first method. The first line shows the different n-maps, and the second line the corresponding objects.
(a) 1-map (D, β₁ = ∅) corresponds to (e), a set of isolated oriented edges.
(b) 1-map (D, β₁) obtained after seven 1-sew operations. This 1-map corresponds to the two oriented polygonal lines shown in (f).
(c) 2-map (D, β₁, β₂ = ∅) corresponds to the two oriented faces shown in (g).
(d) 2-map (D, β₁, β₂) obtained after one 2-sew operation. In (h) the corresponding 2D subdivided object.

## FIGURE 5.12

Construction of a 2D object by applying the second method. The first line shows the different 2-maps, and the second line the corresponding objects.

(a) 2-map (D, β₁ = ∅, β₂ = ∅) corresponds to (e), a set of isolated oriented faces with boundaries.

(b) 2-map (D, β₁, β₂ = ∅) obtained from (a) after seven 1-sew operations; it corresponds to the object shown in (f).

(c) 2-map (D, β₁ = ∅, β₂) obtained from (a) after one 2-sew operation; it corresponds to the object shown in (g).

(d) 2-map (D, β₁, β₂) corresponds to the 2D oriented subdivided object shown in (h). This 2-map is either obtained from (b) after one 2-sew operation, or obtained from (c) after seven 1-sew operations.

![](img/6ba3cf72cbe3568e76a174448323bb33_174_0.png)
