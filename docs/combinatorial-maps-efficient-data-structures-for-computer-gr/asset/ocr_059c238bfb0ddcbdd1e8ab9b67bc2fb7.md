{2, …, n} and let d ∈ D be a non i-free dart. The n-map obtained from M by i-unsewing d and βi(d) is Mi-unsew(d) = (D, β1, …, βi−1, βi′, βi+1, …, βn), where βi′ is defined by: ∀e ∈ D,

+   - if e ∈ ⟨β1, …, βi−2, βi, βi+2, …, βn⟩(d), βi′(e) = ∅;
+   - otherwise, βi′(e) = βi(e).

The i-unsew operation consists in setting βi to ∅ for each dart of the orbit ⟨β1, …, βi−2, βi, βi+2, …, βn⟩(d). So, the i-unsew applied to any dart of this orbit produces the same result.

For the 1-unsew operation given in Def. 48, two different orbits must be considered: first o1 = {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(d) is all the darts of the first edge having the same orientation than d, second o2 = ⟨β3, …, βn⟩(β1(d)) \ {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(β1(d)) is all the darts of the second edge having the opposite orientation than d. Each dart in o1 and in o2 must be linked by β1 with ∅, all the other relations are not modified. In case of a folded edge, o1 ∪ o2 is the set of all the darts of the folded edge.

# Definition 48 (1-unsew) Let M = (D, β1, …, βn) be an n-map and d ∈ D be a non 1-free dart. Let o1 denote ⟨{βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j}⟩(d) and o2 denote ⟨β3, …, βn⟩(β1(d)) \ {⟨βi ∘ βj | ∀i, j ∈ {3, …, n}, i < j⟩}(β1(d)). The n-map obtained from M by 1-unsewing d and β1(d) is M1-unsew(d) = (D, β1′, β2, …, βn), where β1′ is defined by: ∀e ∈ D,

+   - if e ∈ o1 ∪ o2: β1′(e) = ∅;
+   - otherwise: β1′(e) = β1(e).

It can be proven that i-sew and i-unsew are inverse from each other: applying i-sew to two i-free darts d and d′, and then applying i-unsew to d, produces the original n-map; applying i-unsew to dart d, which is non i-free, and then applying i-sew to d and d′, such that d and d′ were originally linked by βi, produces the original n-map. As a consequence, we can see examples of unsew operations by looking at the examples of sew operations and regarding figures in reverse direction. For example, considering the 3-map given in Fig. 5.6(b) and applying the 1-unsew operation to dart 4, the 3-map represented in Fig. 5.6(a) is obtained. As another example, starting from the 3-map given in Fig. 5.8(c), the 3-map given in Fig. 5.8(a) is obtained by applying the 3-unsew operation to dart 1.

# 5.3 Completeness, Multi-Incidence

Any n-map can be built thanks to the basic operations, by following one of the two basic construction methods. The first one consists in applying