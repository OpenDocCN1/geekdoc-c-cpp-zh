The options of the show and plot commands are endless, and well-documented. At the very least we should mention the figsize = 15 option, which specifies the resolution of the image and will prove useful for large graphs.

# 16.2 Methods of the Graph Class

The Graph class has more than 250 methods available, excluding those defined exclusively in the DiGraph class, or those appearing only in extension modules. This makes Sage an expressive and complete library for graph theory, allowing us to concentrate on the essentials — that is, we can spend less time programming basic functions, and more time on the problems in which we are actually interested.

As when learning any programming language (or library), it is useful to give its list of functions at least one look over in order to familiarise ourselves with its capabilities. This (non-exhaustive) section attempts to introduce the Graph methods succinctly. It is advisable for the reader to sacrifice a few minutes to look over the contents of each category of methods — and even the complete list of methods; the time will prove infinitely well-spent when faced with graph problems. It is also advisable to have a Sage session open to consult the online documentation for each of the methods presented (for example g.degree_constrained_subgraph?), as some accept many options, or have names that are not fully explicit.

# 16.2.1 Modification of Graph Structure

Of course, much of the Graph class is made up of natural methods for defining and modifying graphs — necessary but not particularly remarkable functionality.

Access and modification methods of the Graph class

| add_cycle | add_edge | add_edges |
|---|---|---|
| adjacency_matrix | allow_loops | allow_multiple_edges |
| allow_loops | delete_edge | clear |
| delete_edge | delete_edges | delete_multiedge |
| delete_vertex | delete_vertices | edge_iterator |
| edges | edge_label | edges |
| edges_incident | get_vertex | get_vertices |
| has_edge | has_loops | has_multiple_edges |
| has_vertex | incidence_matrix | latex_options |
| loop_edges | loop_vertices | loops |
| merge_vertices | neighbors | multiple_edges |
| neighbor_iterator | num_verts | networkx_graph |
| num_edges | relabel | number_of_loops |
| order | rename | remove_loops |
| remove_multiple_edges | set_edge_label | reset_name |
| set_vertex | set_vertices | set_vertices |
| subdivide_edge | subdivide_edges | size |
| vertices | weighted | vertex_iterator |
| | | weighted_adjacency_matrix |

# 16.2.2 Operators

Along the same lines, we find methods that act as operators, which return instances of the Graph class (or DiGraph). For example, the complement method applied