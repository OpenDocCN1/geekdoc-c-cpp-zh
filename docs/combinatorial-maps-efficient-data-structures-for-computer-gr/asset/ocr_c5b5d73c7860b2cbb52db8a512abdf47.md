# FIGURE 4.19

A 3-sew operation creating folded cells in a 3-Gmap.

(a) 3-Gmap (D, α₀, α₁, α₂, Id_D) contains forty-eight darts.

(b) The corresponding 3D quasi-manifold has one volume, six faces, twelve edges and eight vertices.

(c) 3-Gmap G³-sew(1, 6).

(d) The corresponding 3D quasi-manifold. Face (v₁, v₂, v₃, v₄) is folded on itself. It is incident twice to the edge (v₁', v₂'), which is the result of the identification of the two edges (v₁, v₂) and (v₄, v₃). Moreover, the two edges containing darts 3 and 7 are folded as they are incident twice to the same vertex.

# 4.4 Data Structures, Iterators and Algorithms

In this section, data structures and algorithms are defined in order to handle n-Gmaps in computer softwares. We choose to use an algorithmic language to facilitate the coding in different programming languages. To simplify notations, we do not make the distinction in algorithms between a pointer to an element and the element itself.

The objective is here to describe one way to encode darts and involutions. Here we choose the solution based on structures with pointers, but it is easy to modify the algorithms given here to deal with other possibilities. Note that we describe here only the combinatorial part of the data structure. You can see chapter 7 for two examples showing how is it possible to represent the geometrical part. The solution presented here is the one used for example in Moka, a 3D geometrical modeler based on 3-Gmaps [211].

# 4.4.1 Data Structures

As we have seen in the definition of n-Gmaps, the basic element is the dart. Thus the main data structure is the one which implements the darts. In dimension n, a dart structure contains an array Alphas of n + 1 pointers to represent the different αᵢ links.

In addition to the n + 1 pointers, a dart structure contains an array Marks