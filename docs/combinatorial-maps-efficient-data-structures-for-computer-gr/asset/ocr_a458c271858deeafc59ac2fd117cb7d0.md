![](bbox=[0.111, 0.094, 0.813, 0.336])

# **FIGURE 3.19**

(a) A 1D quasi-manifold without boundary which is a loop.
(b) The decomposition produces two vertices linked together both by α₀ and α₁.
(c) Representation of the corresponding 1-Gmap.

ple shown in Fig. 3.19(a) where vertex v₁ is incident twice to edge e₁. The corresponding 1-Gmap shown in Fig. 3.19(c) contains only two darts which are linked together both by α₀ and α₁.

A 1-Gmap can represent several 1D quasi-manifolds and thus can contain several connected components: see for instance three disjoint 1D quasi-manifolds (Fig. 3.20(a)) and the corresponding 1-Gmap (Fig. 3.20(b)) which contains three connected components corresponding to sets of darts {1, . . . , 10}, {11, . . . , 18} and {19, . . . , 24}. Two darts d₁ and d₂ belong to the same connected component if there is a path of darts between d₁ and d₂, i.e. a sequence of darts linked by α₀ and α₁. For any dart d, ⟨α₀, α₁⟩(d) is the connected component containing d, and it is easy, starting from d, to retrieve all the darts of its connected component, by applying α₀ and α₁ as many times as possible.

# 3.2.1.2   2D

The same process can be applied for 2D quasi-manifolds without boundary. The quasi-manifold given in Fig. 3.21(a) is composed of four faces, labeled from f₁ to f₄, nine edges and seven vertices. The decomposition process applied to the example given in Fig. 3.4 page 56 for 2-maps produces here the set of isolated edges given in Fig. 3.21(b) plus two relations: α₂ links two split edges and α₁ links two split vertices. The only difference with 2-maps is the fact that the quasi-manifold is not oriented and thus no element is oriented, and each relation is symmetric. Thus α₁ and α₂ are involutions.

Then one more decomposition is added: the boundary of each edge is decomposed into vertices, producing a set of isolated vertices plus the relation α₀ that links two vertices that belonged to the same edge before the decomposition (cf. Fig. 3.21(c)). These isolated vertices are the darts of the 2-Gmap describing the initial 2D quasi-manifold.

In order to obtain the 2-Gmap describing the original 2D quasi-manifold, all the α relations are propagated onto darts. This is straightforward for α₀