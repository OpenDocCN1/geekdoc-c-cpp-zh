# 5

# n-maps

An n-map is a combinatorial data structure allowing to describe an n-dimensional oriented quasi-manifold with or without boundary. The main difference with n-Gmaps introduced in the previous chapter is the fact that n-maps cannot describe nonorientable quasi-manifolds. The main interest of n-maps comparing to n-Gmaps is to use twice less darts for representing orientable quasi-manifolds¹. The main drawback is the “inhomogeneity” of the definition, which often involves more complex algorithms. We structure this chapter as for n-Gmaps, in order to emphasize the similarities and the differences between the two data structures. n-maps are defined in Section 5.1, as the basic notions of cells, incidence and adjacency relations between the cells. Some basic operations allowing to modify existing n-maps are presented in Section 5.2. These operations allow to add/remove darts, increase/decrease the dimension of an n-map, merge/split n-maps; the sew/unsew operations allow to identify cells. We show in Section 5.3 that these operations make a small basis of operations allowing to build any n-map. Moreover, it is pointed out that it is possible to take multi-incidence between cells into account, and some specific configurations are illustrated, related to multi-incidence such as dangling cells and folded cells. A possible data structure for implementing n-maps is proposed in Section 5.4, and also some algorithms allowing to develop a computer software handling n-maps. Some additional notions related to n-maps are presented in Section 5.5. The relations between n-maps and n-Gmaps are studied in Section 5.5.2.

# 5.1 Basic Definitions

As seen in chapter 3, an n-map is defined by a set of darts on which permutations and involutions act, which satisfy some constraints. This leads to the following definition of n-maps.

Definition 26 (n-map) An n-dimensional combinatorial map, or n-map, with 0 ≤ n, is an (n + 1)-tuple M = (D, β₁, …, βₙ) where:

¹ When an orientable quasi-manifold is represented, the corresponding n-Gmap represents the two possible orientations, but the corresponding n-map represents only one orientation.