![](bbox=[0.1, 0.12, 0.75, 0.48])

**Figure 11.18.** Call graph of a C++ program visualized using a force-directed layout. The node colors indicate the function types. The graph contains 314 nodes (functions) and 718 edges (calls).

Figure 11.18 shows a call graph of a C++ program of approximately 1000 lines of code, visualized using a force-directed layout.10 The graph nodes, depicting functions, are drawn using spherical glyphs colored to indicate the function type, in a manner similar to Figure 11.14. Warm colors show methods of the five core application classes; green indicates methods of string handling classes; blue indicates methods of Standard Template Library (STL) container classes, e.g., trees, maps, and sets [Plaugher et al. 00]; and white indicates other functions, such as those from the standard C library. The program entry point (main()) function is shown by a slightly larger cyan spherical glyph. The edges are drawn using Gourand-shaded lines, similar to Figure 11.5, from dark (caller) to white (called).

Several aspects are visible in this image. Arguably the most salient elements we see are the three similar-color node clusters corresponding to the core functions (warm colors), containers (blue), and string functions (green). These indi-

10The layout is computed by the neato program, which is part of the freely available GraphViz software [GraphViz 14].