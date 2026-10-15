# FIGURE 6.34

0-insertion for 1-Gmap.
(a) Two 1-Gmaps G and C, linked by bijection γ.
(b) 1-Gmap G I₀(C, γ).

# 6.4 Insertion

The insertion operation is the inverse of the removal operation. It consists in adding a new i-cell inside an existing (i+1)-cell, possibly cutting this (i+1)-cell in two. The insertion operation is defined in this chapter only for n-Gmaps; the conversion for n-maps can be done without particular difficulty. Since insertion is the inverse of removal, the examples presented in Section 6.2.1 illustrate also the insertion operation, but starting here from the results.

Look at 1-Gmaps G and C in Fig. 6.34(a). C describes a 0-cell, which is inserted into a 1-cell of G, producing 1-Gmap G I₀(C, γ) presented in Fig. 6.34(b). γ is a bijection (represented by gray dashed curves in the figures), which maps C onto the darts of the 1-cell; more precisely, γ(a) = 5 and γ(b) = 6. The set of darts of the resulting 1-Gmap is the union of the two sets of darts of G and C; its involutions are either defined according to G (when two darts of G are concerned), or to C (when two darts of C are concerned), or to γ otherwise (i.e. when a dart of G and a dart of C are concerned).

Two 2-Gmaps G and C are represented in Fig. 6.35(a). C describes an edge, which is inserted into a face of G, producing 2-Gmap G I₁(C, γ), represented in Fig. 6.35(b). Bijection γ describes the way the 1-cell is inserted into the face: more precisely, γ(a) = 2, γ(b) = 11, γ(c) = 10 and γ(d) = 3. The construction of the resulting 2-Gmap is similar to the 1D case.

Note that if the insertion is defined according to γ′, defined by γ′(a) = 3, γ′(b) = 11, γ′(c) = 10, γ′(d) = 2, the face in which the edge is inserted is not split. The resulting 2-Gmap is not orientable; more precisely, its topological characteristics are that of a Möbius strip. This illustrates the interest of describing by bijection γ the way the cell is inserted.

Examples of 0-insertion and 1-insertion in a 2-Gmap are presented in Figs. 6.36 and 6.37. In Fig. 6.37, C describes a dangling edge, and γ is defined