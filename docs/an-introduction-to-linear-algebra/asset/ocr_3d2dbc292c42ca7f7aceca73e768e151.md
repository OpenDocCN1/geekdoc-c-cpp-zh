(i) if \(\dim V = n\), then \(\dim A(V) = n^2\)
(ii) if \(L, G \in A(V)\), then \(LG = G \circ L \in A(V)\)
(iii) if \(L, G \in A(V)\) and \(LG = I\), then \(L\) is invertible and \(G = L^{-1}\)
(iv) if \(L \in A(V)\), then \(L^n \in A(V)\), \(n = 1, 2, \cdots\)
(v) if \(L, G, H \in A(V)\) and \(c \in F\), then (a) \(L(G + H) = LG + LH\) (b) \((G + H)L = GL + HL\) (c) \(c(GL) = G(cL) = G(cL)\) (d) \((LG)H = L(GH)\).

# 12.15. Let \(L\) and \(G\) be linear mappings given by

\(L(x) = \begin{pmatrix} ax_1 + bx_2 \\ cx_1 + dx_2 \end{pmatrix} \text{ and } G(x) = \begin{pmatrix} \alpha x_1 + \beta x_2 \\ \gamma x_1 + \delta x_2 \end{pmatrix},\)

where \(ad - bc = |A| \neq 0\). Find the matrix \(A\) such that \(L^{-1}(G(x)) = Ax\).

# 12.16. Let \(L: R^2 \to R^2\) be a linear mapping. A *line segment* between two vectors \(u\) and \(v\) in \(R^2\) is defined by \(tu + (1 - t)v\), \(0 \leq t \leq 1\). A set \(S\) in \(R^2\) is called *convex* if for every pair of vectors in \(S\), the line segment between the vectors is in \(S\). Show that

+   (i) the image of a line segment under the map \(L\) is another line segment
+   (ii) if \(L\) is an isomorphism and \(S\) is convex, then \(L(S)\) is a convex set.

# Answers or Hints

**12.1.** Verify directly.
**12.2.** Suppose \(u^1, \cdots, u^n \in V\) are linearly independent, and \(c_1 L(u^1) + \cdots + c_n L(u^n) = 0\). Then, \(L(c_1 u^1 + \cdots + c_n u^n) = 0\). But since, \(\mathcal{N}(L) = \{0\}\) we have \(c_1 u^1 + \cdots + c_n u^n = 0\), which implies \(c_1 = \cdots = c_n = 0\).
**12.3.** (i) Nonsingular.
(ii) Singular.
(ii) Singular.
**12.4.** (i) \(\dim V = 3\), \(n(L) = 0\), \(\dim R(L) = 3\).
(ii) \(\dim V = 4\), \(n(L) = 1\), \(\dim R(L) = 3\).
(iii) \(\dim V = 4\), \(n(L) = 2\), \(\dim R(L) = 2\).
**12.5.** Verify directly.
**12.6.** \(L(V) \subseteq W\), and hence \(G(L(V)) \subseteq G(W)\). Thus, \(\text{rank}(G \circ L) = \dim[G(L(V))] \leq \dim[G(W)] = \text{rank}(G)\). We also have \(\text{rank}(G \circ L) = \dim[G(L(V))] \leq \dim[L(V)] = \text{rank}(L)\).
**12.7.** (i) One-to-one implies \(\mathcal{N}(L) = \{0\}\). Thus \(\dim V = \dim W = \dim R(L)\), and hence \(L\) is onto.
(ii) Onto implies \(R(L) = W\). Thus \(\dim V = \dim W = \dim R(L)\), and hence \(\mathcal{N}(L) = \{0\}\).
**12.8.** (i) In Theorem 12.4, \(\dim R(L) = \dim W\) and \(\dim \mathcal{N}(L) \geq 0\).
(ii) In Theorem 12.4, \(\dim \mathcal{N}(L) = 0\) and \(\dim R(L) \leq \dim W\).