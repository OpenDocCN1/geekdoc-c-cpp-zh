# # Generalized Triangulations

Pooran Memari

LIX, CNRS, École Polytechnique, Université Paris Saclay, Palaiseau, France

# ## CONTENTS

+   9.1 Introduction .................................................... 147
+   9.2 Generalized primal-dual triangulations ........................ 148
+      9.2.1 Some classical examples .................................... 149
+      9.2.2 Primal-dual triangulations (PDT) ........................... 150
+   9.3 A characterization theorem ...................................... 151
+      9.3.1 Combinatorially regular triangulations (CRT) ............... 151
+      9.3.2 Equivalence between PDT and CRT ............................ 152
+      9.3.3 Parametrization of primal-dual triangulations .............. 152
+   9.4 Discrete representation using generalized triangulations ...... 153
+      9.4.1 Discrete exterior calculus framework ....................... 153
+      9.4.2 Applications in mesh optimization .......................... 154

T HE MAIN CONCEPT of barycentric coordinates is intimately linked to the duality between primal and dual complexes. This chapter presents a general framework in R^d to define a family of compatible dual complexes for a given triangulation. We derive a combinatorial characterization theorem for triangulations that admit a compatible, possibly non-orthogonal dual complex. We show how the mesh optimization methods in geometric modeling can benefit from the parameterization of the space of generalized triangulations.

# ### 9.1 INTRODUCTION

A triangle mesh is a partition of a bounded domain with simplices (triangles in 2D, tetrahedra in 3D) so that any two of these simplices are either disjoint or sharing a face. The resulting triangulation (also called tetrahedralizations in 3D) provides a discretization of space through both its primal (simplicial) elements and