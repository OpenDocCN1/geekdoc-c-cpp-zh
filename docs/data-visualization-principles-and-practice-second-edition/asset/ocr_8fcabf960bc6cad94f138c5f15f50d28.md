![](bbox=[0.078, 0.125, 0.765, 0.325])

Figure 3.12. Unstructured grids. Circle (left), head slice (middle), and 3D bunny surface (right).

scan with a plane. Slicing is treated in detail in Section 8.1.2. The boundary of the domain is drawn in red, for clarity. It is clearly difficult, if not impossible, to sample domains with such complex and irregular boundaries using structured grids. The unstructured grid has no problem representing such a domain, however. The third example (Figure 3.12 right) shows an unstructured grid representing a 3D surface of a bunny, with the grid edges drawn in red for clarity. As in the previous example, unstructured grids can represent such shapes with no problem.

# 3.6 Attributes

So far, we have described three of the four ingredients of a discrete dataset $\mathcal{D}_s = (\{p_i\}, \{c_i\}, \{f_i\}, \{\Phi_i^k\})$: the grid consisting of sample points $p_i$ and cells $c_i$, and the reference basis functions $\Phi_i^k$. This section discusses the sample values $f_i$ in more detail.

As we said in the beginning of our discussion on data representation, visualization data can be modeled by some continuous or discrete function with values in a domain $\mathbf{C} \in \mathbb{R}^c$. Hence, the sample values $f_i$ are $c$-dimensional points. In visualization, the set of sample values of a sampled dataset is usually called *attribute data*. Attribute data can be characterized by their dimension $c$, as well as the semantics of the data they represent. This gives rise to several *attribute types*. These are described in the following sections.