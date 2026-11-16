# 15.2.7 Extension to three dimensions

We now briefly consider the situation when \(\Omega\) is a subset of \(\mathbb{R}^3\). In this case, \(\Omega_h\) is assumed to be a mesh consisting of very general shaped polyhedra with planar faces and straight edges, and the virtual space (15.13) is defined by taking

```
\(V_h^P := \left\{ v_h \in H^1(P) : \Delta v_h \in \mathbb{P}_{k-2}(P); \right.\)
\(\left. v|_e \in V_h^f \text{ for each face } f \text{ of } P; \right.\)
\(\left. v_h|_{\partial P} \in C^0(\partial P) \right\},\)
(15.13)
```

where \(V_h^f\) is the two-dimensional discrete space on the face \(f\), introduced in Section 15.2.3 (with the convention that \(\mathbb{P}_{-1}(P) = \{0\}\)).

As for the two-dimensional case, two equivalent bases for this space can be considered: the natural basis, defined through a set of Dirichlet problems from the space definition (15.13); a virtual basis, defined through the degrees of freedom associated with the vertex values and the moments on the edges, the faces, and the interior of element \(P\). However, in the 3D case the orthogonal projections of Section 15.2.5 cannot be computed directly using these degrees of freedom, since this would require the knowledge of the moments of order up to \(k-1\) and \(k\) on the element faces, which are not available from (15.13).

To get around this problem, the space must be modified in such a way that these extra moments are available. One approach is to simply expand the space by relaxing the conditions required in its definition such that the extra moments can be taken as degrees of freedom. However, this results in a significant increase in the dimension of the space and therefore the size of the final matrix. Instead, a process known as _VEM enhancement_ has been developed (see [6, 82]) to produce a space with the same virtual degrees of freedom as \(V_h^P\), but in which these moments may be computed. We point out that although the virtual degrees of freedom remain unchanged, the natural basis for \(V_h^P\) is no longer valid for the enhanced space.

# 15.3 VIRTUAL ELEMENT METHOD FOR ELLIPTIC PDES

# 15.3.1 Model problem

Consider the diffusion of the scalar variable \(u\), which satisfies the following Poisson problem (we refer to [29, 82] for a treatment of more general elliptic problems):

```
\(-\text{div}(K\nabla u) = f \text{ in } \Omega,\) (15.14)
\(u = g \text{ on } \partial\Omega,\) (15.15)
```

where \(K\) is the diffusion tensor, \(f\) is the forcing term, and \(g\) defines the (typically non-homogeneous) Dirichlet boundary condition. We assume that:

+   (H1) \(\Omega\) is a bounded, open, polytopal subset of \(\mathbb{R}^2\);