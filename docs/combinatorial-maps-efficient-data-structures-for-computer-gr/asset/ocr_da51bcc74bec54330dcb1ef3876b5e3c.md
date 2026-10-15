of combinatorial maps. For instance, any *n*-GMap represents a *n*-dimensional quasi-manifold. So, any operation constructing an *n*-GMap construct a valid quasi-manifold; it is not necessary to control its validity through Euler operators, for instance;

+   2. few basic operations make it possible to construct any combinatorial map. It is possible to conceive many low- or high-level operations, in order to satisfy different construction needs for various applications, and to prove the validity of these operations;

+   3. local operations can be defined, for carefully controlling the modifications of the object during its construction. Global operations have also been defined, based on these local operations, for instance for different processes related to geometric modeling, computational geometry, discrete geometry, computer graphics, image processing and analysis;

+   4. optimized structures can be defined for the efficient representation of subclasses of cellular subdivisions. Since the structures are close to each other, it is possible to:
+   
+   - either reuse for a structure parts of a software conceived for another structure;
+   - either conceive the software in order to efficiently implement several structures;

+   5. combinatorial maps are based on a single type of elements, i.e. the darts, and functions between darts satisfying clear and simple consistency constraints. This simplifies the implementation of related data structures and algorithms.

For representing subdivisions of the plane, and more generally surface subdivisions, 2-maps and 2-Gmaps correspond to the kernel of other well-known data structures. This makes it possible to clearly distinguish the structure information from the shape information or redundant information added for optimizing some processes. Based on combinatorial maps, several implementations have been proposed, including more or less explicit information, in order to get efficient data structures.

Advantages of combinatorial maps increase for higher dimensions, since defining specific data structures becomes more difficult. It is thus possible to safely conceive many local and global construction operations, operations for computing topological properties, and to deduce efficient implementations for different types of (linear or curved) embeddings.

More specifically, both *n*-maps and *n*-Gmaps correspond to quasi-manifolds with or without boundary, but *n*-maps represent orientable quasi-manifolds while *n*-Gmaps can also represent nonorientable ones. However the two structures have their one advantages, and the choice of one