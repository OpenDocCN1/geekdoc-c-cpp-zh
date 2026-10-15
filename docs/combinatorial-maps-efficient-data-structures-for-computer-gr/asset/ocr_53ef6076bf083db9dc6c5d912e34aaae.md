# FIGURE 9.4

(a) The eleven topological elements of the radial-edge data structure.
(b) Radial-edge representation of three square faces incident to a same edge.

![](bbox=[0.18, 0.115, 0.55, 0.545])

![](bbox=[0.52, 0.22, 0.88, 0.505])

loop-use is a boundary of a face, vertex-use is a vertex; and four “geometrical entities”: face, loop, edge and vertex, which contain the corresponding geometric information and/or attributes associated with the “topological entities”. Top-down and bottom-up hierarchical relationships are represented, i.e. each topological entity of dimension i has a list of its incident elements of dimension i − 1 and i + 1. Wireframe allows to represent paths of isolated edges which do not belong to a boundary of a face, and single vertex allows to represent isolated vertices, either in a shell or in a loop. Figure 9.4(a) shows these different entities and their links.

The radial-edge data structure has been designed in order to represent the topology of 2-dimensional complexes embedded in ℝ³. Thus, solids can be implicitly represented by their boundary surfaces, and assemblies of such solids can be represented by the radial-edge data structure. So, this structure makes it possible to represent 3-dimensional subdivided objects. More precisely, if the topology of a 2D complex is described, there is no reason to define an order between the faces, through the different pointers acting on the edge-use elements. Take for instance three edges, choose one vertex for each edge, and identify these three vertices: you get a 1-dimensional complex. Embedded in ℝ³, there is no order defined on the adjacent edges. But if the object is embedded into ℝ², an order can be defined on the edges, corresponding to the fact that faces exist (in this case, one face around the edges); the object with its embedding space is a 2-dimensional manifold. This is similar for