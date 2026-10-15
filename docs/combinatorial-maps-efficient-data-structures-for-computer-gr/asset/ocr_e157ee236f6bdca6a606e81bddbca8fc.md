+   3. the space/time costs of structures and operations.

Given a class C of subdivisions (e.g. quasi-manifolds), a structure S_L corresponding to a larger class L (e.g. cellular complexes) uses generally more memory space than an optimized structure S_C corresponding to C: this corresponds to the fact that some information is explicit within S_L, and implicit within S_C.

It is clear that the time complexity of operations has also to be taken into account: when some operations often need to make explicit some implicit information, a less efficient model (according to space complexity) could be a better choice. For instance, it is possible to represent a polyhedron by a list of faces, but adjacency and incidence relations are thus not explicitly represented; so, this representation is often not efficient when constructing objects, since adjacency and incidence information are used by many construction operations. Conversely, many algorithms do not need all information contained in the whole geometric data structures, and specialized structures can be a better choice [190] (e.g. a list of faces for some rendering algorithms).

+   4. the cost of operation conception.

For instance, the definitions of several structures do not take into account the constraints of consistency which have to be satisfied by the represented objects (e.g. an edge incident to three vertices can be represented by an incidence graph). The construction process has thus to control the object validity. For instance, Euler operators have been defined in order to construct any subdivision of any orientable surface without boundary [173, 171]: each operator simultaneously creates or removes several cells; so, the conception of Euler operators for handling incidence graphs, even if not complicated, is not so easy than the conception of other basic operations defined for handling structures in which the constraints of consistency are directly taken into account, e.g. inserting a dart and sewing for n-Gmaps. Moreover, Euler operators have never been generalized for constructing n-dimensional quasi-manifolds; is it inefficient, difficult or both?

So, it is clear for us that “one best structure” does not exist, but some structures can be well suited for particular processes. Thus, conversion algorithms which can be deduced from the general frame presented in this book are very important for practical purposes.

# Combinatorial maps

When cellular objects have to be handled for some reason (“nature” of represented objects, or specificities of operations), we think that combinatorial maps are a good starting point for the design of a data structure:

+   1. consistency properties are taken into account in the very definition