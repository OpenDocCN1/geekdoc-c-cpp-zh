darts 1 and 7. This produces the 2-Gmap shown in (c), which corresponds to the subdivided surface shown in (f).

A second example is presented in Fig. 4.13, showing the construction of a 3D object. The first steps are similar to the previous 2D example. Starting from a 0-Gmap made of isolated darts (not shown), 0-sew and increase dimension operations are applied, producing the 1-Gmap shown in (a). Then 1-sew operations are applied, and the dimension of the 1-Gmap is increased (see (b)). Then 2-sew operations are applied, and the dimension of the 2-Gmap is increased (see (c)). The last step is the application of 3-sew operation. This produces the 3-Gmap shown in (d), which corresponds to the 3D subdivided object shown in (h).

The inverse operations can be applied in order to destroy a given n-Gmap: this corresponds exactly to the decomposition process used for the intuitive presentation of n-Gmaps (cf. Section 3.2). First, n-unsew operations are applied until having all the darts n-free, then the dimension of the n-Gmap is decreased. This process is iterated until obtaining a 0-Gmap in which α₀ is equal to the identity. As examples for this “destruction process”, we can consider the examples given for the construction process in reverse direction (given in Figs. 4.11, 4.12 and 4.13), by applying i-unsew (resp. decrease dimension) operations instead of i-sew (resp. increase dimension) operations.

# 4.3.2 Construction Directly in a Given Dimension

The second construction method consists in working directly in dimension n. Starting from an empty n-Gmap, the operation which adds an isolated dart is applied as many times as necessary. Next, i-sew operations can be applied in this n-Gmap, for i ∈ {0, …, n} (contrary to the previous construction where only k-sew operations can be applied to a k-Gmap).

An example of construction is presented in Fig. 4.14: it corresponds to the same object than in Figs. 4.11 and 4.12, but now the second construction method is applied. The main differences with the first one are:

+   - the initial n-Gmap has its final dimension, and contains isolated darts (here a 2-Gmap, see Fig. 4.14(a));
+   - sew operations can be applied in any order; for example 0-sew operations can be first applied (see Fig. 4.14(b)), then 2-sew operations (see Fig. 4.14(c)) and finally 1-sew operations (see Fig. 4.14(d)).

A second construction of the object depicted in Fig. 4.13 is presented in Fig. 4.15. The initial 3-Gmap contains a set of isolated darts (not shown). Then the sew operations can be applied in any order. For example, they can be applied in the same order than in Fig. 4.13: start by 0-sew operations, then 1-sew operations, then 2-sew operations and finish by 3-sew operation. The 3-Gmaps obtained after each step are similar to the ones in Fig. 4.13(a), (b), (c) and (d), the only difference being the dimension of the Gmaps, which is always