
Note that the number of *n*-boundaries, the Euler-Poincaré characteristic and the orientability notion are defined for any *n*-Gmaps whatever their dimension is (cf. Section 8.3.2.1 page 329 for Euler-Poincaré characteristic), but for *n* > 2, they do not provide a classification.

## 5 n-maps

An n-map is a combinatorial data structure allowing to describe an n-dimensional oriented quasi-manifold with or without boundary. The main difference with n-Gmaps introduced in the previous chapter is the fact that n-maps cannot describe nonorientable quasi-manifolds. The main interest of n-maps comparing to n-Gmaps is to use twice less darts for representing orientable quasi-manifolds¹. The main drawback is the “inhomogeneity” of the definition, which often involves more complex algorithms. We structure this chapter as for n-Gmaps, in order to emphasize the similarities and the differences between the two data structures. n-maps are defined in Section 5.1, as the basic notions of cells, incidence and adjacency relations between the cells. Some basic operations allowing to modify existing n-maps are presented in Section 5.2. These operations allow to add/remove darts, increase/decrease the dimension of an n-map, merge/split n-maps; the sew/unsew operations allow to identify cells. We show in Section 5.3 that these operations make a small basis of operations allowing to build any n-map. Moreover, it is pointed out that it is possible to take multi-incidence between cells into account, and some specific configurations are illustrated, related to multi-incidence such as dangling cells and folded cells. A possible data structure for implementing n-maps is proposed in Section 5.4, and also some algorithms allowing to develop a computer software handling n-maps. Some additional notions related to n-maps are presented in Section 5.5. The relations between n-maps and n-Gmaps are studied in Section 5.5.2.

¹ When an orientable quasi-manifold is represented, the corresponding n-Gmap represents the two possible orientations, but the corresponding n-map represents only one orientation.

### 5.1 Basic Definitions

As seen in chapter 3, an n-map is defined by a set of darts on which permutations and involutions act, which satisfy some constraints. This leads to the following definition of n-maps.

**Definition 26 (n-map)** An n-dimensional combinatorial map, or n-map, with 0 ≤ n, is an (n + 1)-tuple M = (D, β₁, …, βₙ) where:

1. $D$ is a finite set of darts;
2. $\beta_1$ is a partial permutation on $D$; let $\beta_0$ denote $\beta_1^{-1}$;
3. $\forall i \in \{2,\ldots,n\}:\ \beta_i$ is a partial involution on $D$;
4. $\forall i \in \{0,\ldots,n-2\},\ \forall j \in \{3,\ldots,n\}$, such that $i+2\leq j$, $\beta_i\circ\beta_j$ is a partial involution.

![](img/6ba3cf72cbe3568e76a174448323bb33_156_0.png)

**FIGURE 5.1** Examples of 1-map, 2-map and 3-map. (a) A 1-map $(D,\beta_1)$. (b) A 2-map $(D,\beta_1,\beta_2)$. (c) A 3-map $(D,\beta_1,\beta_2,\beta_3)$.

A 0-map $(D)$ is a set of darts representing isolated vertices, a 1-map $(D,\beta_1)$ represents the structure of oriented polygonal curves (cf. Fig. 5.1(a)), a 2-map $(D,\beta_1,\beta_2)$ represents the structure of oriented subdivided surfaces (cf. Fig. 5.1(b)), a 3-map $(D,\beta_1,\beta_2,\beta_3)$ represents the structure of assemblies of oriented volumes (cf. Fig. 5.1(c)) ...

$\beta_0=\beta_1^{-1}$ is a partial permutation. For $i\in\{2,\ldots,n\}$, $\beta_i$ is a partial involution, and thus $\beta_i=\beta_i^{-1}$.

Since all $\beta$ relations are partial relations, darts can be linked with $\varnothing$: this corresponds to the fact that $n$-maps can describe objects with boundaries. Dart $d$ is $i$-free if it is linked with $\varnothing$ by $\beta_i$, and it is $i$-sewn otherwise (cf. Def. 27 and example in Fig. 5.2).

**Definition 27 ($i$-free, $i$-sewn)**

Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map, $d\in D$, and $i\in\{0,\ldots,n\}$:

- $d$ is $i$-free if $\beta_i(d)=\varnothing$;
- $d$ is $i$-sewn with dart $d_2\in D$ if $\beta_i(d)=d_2$.

![](img/6ba3cf72cbe3568e76a174448323bb33_157_0.png)

**FIGURE 5.2** A 2-map with 1-boundary and 2-boundary.

For example dart 1 is 0-free, i.e. $\beta_0(1)=\varnothing$. Thus dart 1 belongs to an edge which has no previous edge in the same face. Dart 2 is 1-free, i.e. $\beta_1(2)=\varnothing$. Thus dart 2 belongs to an edge which has no next edge in the same face. Dart 3 is 2-free, i.e. $\beta_2(3)=\varnothing$, so it belongs to an edge which is incident to only one face.

In all generality, boundaries can exist in all dimensions; in practical applications, $n$D objects are often without boundary, except for dimension $n$, i.e. there are no free darts except for $\beta_n$.

Note that a 0-boundary (i.e. an edge incident to only one vertex, as for instance an edge cut by a plane) corresponds to a dart free for all $i\in\{1,\ldots,n\}$. Indeed, as soon as a dart $d_1$ is $i$-sewn with a dart $d_2$, for $i\in\{1,\ldots,n\}$, the edge containing dart $d_1$ is incident to two vertices: the vertex containing dart $d_1$, and the vertex containing dart $d_2$ (cf. definition of cells below).

As seen in the intuitive presentation, an $n$-map can contain different connected components. The set of darts belonging to the same connected component as a given dart can be retrieved, thanks to Def. 28. This is the set of darts of the orbit made of all the permutations.

**Definition 28 (connected component)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map, and $d\in D$. $\langle\beta_1,\ldots,\beta_n\rangle(d)$ is the connected component containing $d$.*

As said before, according to the context, an orbit denotes either a set of darts, or this set of darts together with the corresponding $\beta$ relations. Thanks to this definition, it can be directly tested if a given $n$-map is connected, i.e. made of only one connected component, simply by testing if the connected component containing a dart is the set of all the darts of the $n$-map (cf. Def. 29).

**Definition 29 (connected $n$-map)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map. $M$ is connected if $\langle\beta_1,\ldots,\beta_n\rangle(d)$ is equal to $D$, with $d\in D$.*

As for graph theory, the notion of connectivity is related to the notion of path given in Def. 30.

**Definition 30 (path)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map and $d,d'\in D$. A path between $d$ and $d'$ is a sequence of darts $(d_1,\ldots,d_k)$ such that $d_1=d$, $d_k=d'$ and $\forall i\in\{2,\ldots,k\}$, $d_i=\beta_{k_i}(d_{i-1})\in D$, with $k_i\in\{0,\ldots,n\}$.*

Given any pair of darts $d$ and $d'$ that belong to the same connected component, a path exists between $d$ and $d'$. Reciprocally, if $d$ and $d'$ do not belong to the same connected component, there is no path between $d$ and $d'$.

In an $n$-map, a dart corresponds to an $(n+1)$-tuple of oriented cells of different dimensions (vertex, edge, face, volume ...), each pair of cells in this tuple being incident. Moreover, the vertex is the origin of the oriented edge. In other words, a dart describes a “small part” of each oriented cell (this explains why cells are not the basic elements of $n$-maps). A consequence is the fact that very local notions and operations can be defined: for instance, if an edge is a loop, its two extremities can be distinguished, even if it is incident to only one vertex. More generally, $n$-maps naturally take multi-incidence into account, and this can be useful for representing free-form objects.

As we have seen in the intuitive presentation, a cell containing a given dart corresponds to some specific orbit (cf. Def. 31).

**Definition 31 ($i$-cell)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map, $d\in D$ and $i\in\{0,\ldots,n\}$. The $i$-dimensional cell (or $i$-cell) containing $d$ is $c_i(d)$:*

- if $i=0$, $c_0(d)=\langle\{\beta_j\circ\beta_k\mid \forall j,k\in\{1,\ldots,n\},\ j<k\}\rangle(d)$;
- otherwise, $c_i(d)=\langle\beta_1,\ldots,\beta_{i-1},\beta_{i+1},\ldots,\beta_n\rangle(d)$.

The cells can equivalently be defined as the connected components of the $(n-1)$-map of cells defined in Def. 32. For $i=0$, this property is only satisfied for $n$-maps without 1-boundary. Indeed, in such a map, the 0-cell definition is equal to the simplified form $\langle\beta_2\circ\beta_0,\ldots,\beta_n\circ\beta_0\rangle$ while this is not true for $n$-maps with 1-boundary (as shown for the example given in Fig. 3.16 page 68).

**Definition 32 ($(n-1)$-map of $i$-cells)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map, with $n\ge 1$, and $i\in\{0,\ldots,n\}$. The $(n-1)$-map of $i$-cells is $M_{c_i}$:*

- if $i=0$, $M_{c_0}=(D,\beta_2\circ\beta_0,\ldots,\beta_n\circ\beta_0)$;
- otherwise, $M_{c_i}=(D,\beta_1,\ldots,\beta_{i-1},\beta_{i+1},\ldots,\beta_n)$.

Thanks to this definition of cells, the incidence and adjacency relations between cells can be directly retrieved (cf. Def. 33).

**Definition 33 (incidence and adjacency)** *Let $M=(D,\beta_1,\ldots,\beta_n)$ be an $n$-map, $d,d'\in D$, and $i,j\in\{0,\ldots,n\}$, $i\ne j$.*
