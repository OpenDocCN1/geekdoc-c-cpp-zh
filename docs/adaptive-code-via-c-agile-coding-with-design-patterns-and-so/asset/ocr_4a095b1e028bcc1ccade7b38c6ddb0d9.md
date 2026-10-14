Taking this pattern to its logical conclusion, you can even pass in one or more instances of the CompositeComponent interface to the Add method, forming a chain of composite instances in a hierarchical tree structure.

# Where should the composite live?

Chapter 2 introduced the Entourage anti-pattern, which states that implementations should not live in the same assemblies as their interfaces. However, there is an exception to that rule: implementations whose dependencies are a subset of their interface’s dependencies.

Depending on how the composite is implemented, it is likely that no further dependencies will be introduced. If this is true, the assembly in which the interface resides could also include the composite implementation.

In Chapter 2, classes were shown to be modeled as object graphs. That theme continues here, to further demonstrate how the Composite pattern works. In Figure 5-6, the nodes of the graph represent object instances, and the edges represent method calls.