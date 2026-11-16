can employ quantities such as \(u(v_i)\) in its definition. The finite element solution \(u_h\), on the other hand, is the output of a solution operator whose only inputs are the bilinear form, the linear operator \(V_h\), and the boundary conditions. For linear interpolation derived directly from barycentric or generalized barycentric coordinates, the interpolation error estimate has the form

\(\|u - Iu\|_{H^1(\Omega)} \le C_{\text{IE}} h |u|_{H^2(\Omega)},\) (2.2)

where \(h\) is the maximum diameter of an element in a mesh of \(\Omega\). The constant \(C_{\text{IE}}\) in (2.2) depends both on the interpolation method (i.e., the definition of \(Iu\)) and on the shape of the elements used in the mesh. This dependence is quite subtle and often misunderstood.

Analysis leading to estimate (2.2) can be simplified via two observations. First, the error can be decomposed into individual mesh elements rather than the entire solution domain. Second, assuming that the interpolation method is affine invariant, all estimates can be rescaled to diameter 1 elements. Thus, it is sufficient to establish

\(\|u - Iu\|_{H^1(P)} \le C_{\text{IE}} |u|_{H^2(P)},\) (2.3)

for any polytope \(P\) of diameter 1 that is similar to an element in the mesh of \(\Omega\).

For interpolation via a set of generalized barycentric coordinates \(\phi\), the interpolation operator \(I: H^2(P) \to \text{span}\{\phi\}\) is defined by

\(Iu := \sum_{i=1}^n u(v_i)\phi_i.\) (2.4)

In order to prove (2.3), we may only assume that \(u \in H^2(P)\); however, the formula for \(Iu\) in (2.4) requires point values for \(u\) at vertices of \(P\). We can appeal to the Sobolev embedding theorem [4, 70, 240] to ensure that \(u\) is in fact a continuous function and hence that \(u(v_i)\) is well-defined. We state a special case of the theorem that is also called Morrey’s inequality, which we have tailored to the relevant setting.

# **Theorem 2.1** (Sobolev embedding/Morrey’s inequality). Let \(k > d/2\). For any polygonal or polyhedral domain \(P\), there exists a constant \(C_{\text{SE}}\) depending only on \(k\) and \(d\) such that for any \(u \in H^k(P)\),

\(\|u\|_{L^\infty(P)} \le C_{\text{SE}} \|u\|_{H^k(P)}.\)

Moreover, there is a continuous function in the \(L^\infty(P)\) equivalence class of \(u\).

The constant \(C_{\text{SE}}\) depends, in general, on the geometry of \(P\) and it is possible to find a sequence of polytopes \(\{P_i\}_{i=1}^\infty\) for which the associated sequence of constants grows without bound. In these cases, the sequence of boundaries \(\{\partial P_i\}_{i=1}^\infty\) is typically approaching some kind of cusp, fractal, or other kind of “degenerate” geometry. Accordingly, we require that \(P\) belong to some class of polytopes whose geometry is controlled via shape quality metrics and then seek a uniform bound on \(C_{\text{SE}}\) for this class.