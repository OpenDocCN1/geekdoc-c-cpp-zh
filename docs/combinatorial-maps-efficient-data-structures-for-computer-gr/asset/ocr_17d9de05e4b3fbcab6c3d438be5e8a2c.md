# FIGURE 3.5

(a) 2-map of the example of Fig. 3.4.
(b) Representation showing for each dart, its corresponding parts of vertex, oriented edge and oriented face.

1 is ⟨β₂ ∘ β₁⁻¹⟩(1) = {1,6,9}; the edge containing dart 1 is ⟨β₂⟩(1) = {1,5} and the face containing dart 1 is ⟨β₁⟩(1) = {1,2,3,4}. More generally, each cell is composed by the set of all the darts that are part of the same cell; the structure of the cell is given by the βᵢ relations (see Fig. 3.6).

This decomposition process can be applied for any 2D oriented quasi-manifold without boundary. A subdivision of a plane is depicted in Fig. 3.4, a subdivided torus is depicted in Fig. 3.7.

As for the 1D case, several 2D oriented quasi-manifolds can be simultaneously represented. Each quasi-manifold is described by a distinct connected component, the whole 2-map describes all the considered objects. Two darts d₁ and d₂ belong to the same connected component if there is a path of darts two by two linked by β₁ or by β₂ between d₁ and d₂. For any dart d, ⟨β₁, β₂⟩(d) denotes the connected component containing d: starting from d, the set of all the darts of its connected component is retrieved by applying β₁ and β₂ as many times as possible.

# 3.1.1.3 3D

Of course, a similar process can be used to decompose a 3D oriented quasi-manifold without boundary in order to obtain a 3-map. The 3D quasi-manifold depicted in Fig. 3.8(a) is composed by three volumes (a hexahedron in dark gray, a pyramid with square base in light gray plus an unbounded volume), ten faces, sixteen edges and nine vertices. First, the quasi-manifold is decomposed into isolated oriented volumes by splitting each face in two. This produces the set of isolated oriented volumes shown in Fig. 3.8(b); the information that two split faces described the same face before the split is represented by adding a

![](bbox=[0.15, 0.12, 0.4, 0.42])

![](bbox=[0.5, 0.1, 0.88, 0.42])