# CHAPTER 6. IMPLEMENTATION

![](bbox=[0.2, 0.115, 0.8, 0.439])

Figure 6.2: The graph viewer with an example PDG

# 6.2 Analyses based on SDGs

The generated dependence graphs are stored on disk, from where they are parsed with an ANTLR² grammar, and stored in the open source graph library JGraphT.¹ When we decided to use that library, the author first contributed Java 5's generics to that library, resulting in type-safe graphs (specifically no explicit casts for node and edge types) for our custom algorithms. The Joana library based on JGraphT provides a long list of algorithms for slicing, chopping, and related analyses. In particular, all presented and implemented in the original Valsoft [Kri03a] have been integrated. This core library forms the basis for nearly all other libraries and Eclipse plugins in the sequel.

# 6.3 Graph Viewer

The Vast infrastructure [Kri03a] already contained a visualization component for dependence graphs. However, a crucial library of that program has been provided by a company in form only, such that graphs with new features like interference could not be parsed and displayed with that software. Therefore we decided to re-implement the viewer based on the JGraph

+   * http://www.antlr.org/
* http://jgraph.sourceforge.net
* http://www.jgraph.com/