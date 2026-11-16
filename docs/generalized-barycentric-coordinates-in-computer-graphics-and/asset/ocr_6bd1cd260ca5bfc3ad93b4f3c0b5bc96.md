# 12.6 CONFORMING GALERKIN APPROXIMATIONS

Consider $\Omega_h$ to be a finite element decomposition of the domain $\Omega$ into non-overlapping polygons or polyhedra, where $h$ is the average element size. The boundary of the mesh, denoted as $\Gamma_h$, is assumed to be compatible with the applied boundary condition. In other words, $\Gamma_h^u$ and $\Gamma_h^t$ are both unions of edges of the mesh.

We define the numerical integration $\oint_{\Omega_h}$ on $\Omega_h$ as the summation of the contributions from numerical integrals $\oint_P$ from each element $P$ following the standard assembly rule, namely, $\oint_{\Omega_h} = \sum_{P \in \Omega_h} \oint_P$, and $\oint_{\Gamma_h^t}$ as the numerical integration on $\Gamma_h^t$. Similarly, we define the gradient correction map on the global level, $\nabla_{h,k} : \mathcal{K}_{h,k} \to [L^2(\Omega_h)]^{d \times d}$, such that it coincides with the gradient correction map $\nabla_{P,k}$ at the element level,

$(\nabla_{h,k} \mathbf{v}_h)|_P = \nabla_{P,k} \otimes (\mathbf{v}_h|_P) \quad \forall P \in \Omega_h \quad \text{and} \quad \mathbf{v}_h \in \mathcal{K}_{h,k}.$

The Galerkin approximation of the displacement-based formulation then consists of finding $\mathbf{u}_h \in \mathcal{K}_{h,k}$, such that

$G_h(\mathbf{u}_h, \delta \mathbf{v}_h) = 0 \quad \forall \delta \mathbf{v}_h \in \mathcal{K}_{h,k}^0,$

where $\mathcal{K}_{h,k}^0 = \mathcal{K}_{h,k} \cap \mathcal{K}^0$ and $G_h(\mathbf{u}_h, \delta \mathbf{v}_h)$ is the discretization and quadrature evaluation of $G(\mathbf{u}, \delta \mathbf{w})$ in (12.3) with the exact gradient operator $\nabla$ replaced by $\nabla_{h,k}$, which takes the form

$G_h(\mathbf{u}_h, \delta \mathbf{v}_h) = \int_{\Omega_h} \frac{\partial W}{\partial \mathbf{F}}(\mathbf{x}, \mathbf{I} + \nabla_{h,k} \mathbf{u}_h) : \nabla_{h,k}(\delta \mathbf{v}_h) \, d\mathbf{x} - \oint_{\Omega_h} \mathbf{f}_h \cdot \delta \mathbf{v}_h \, d\mathbf{x} - \oint_{\Gamma_h^t} \mathbf{t}_h \cdot \delta \mathbf{v}_h \, ds, \quad (12.13)$

and terms $\mathbf{f}_h$ and $\mathbf{t}_h$ are the approximated body force and boundary traction, respectively.

For the two-field mixed formulation, if we introduce the additional finite element space $\mathcal{Q}_{h,k}^D$- (or $\mathcal{Q}_{h,k-1}^C$-) $\subseteq \mathcal{Q}$, the Galerkin approximation consists of finding $(\mathbf{u}_h, \widehat{p}_h) \in \mathcal{K}_{h,k} \times \widehat{\mathcal{Q}}_{h,k-1}^C$ (or $\mathcal{Q}_{h,k-1}^C$), such that

$G_h^R(\mathbf{u}_h, \widehat{p}_h, \delta \mathbf{v}_h) = 0 \quad \forall \delta \mathbf{v}_h \in \mathcal{K}_{h,k}^0, \quad G_h^R(\mathbf{u}_h, \widehat{p}_h, \delta \widehat{q}_h) = 0 \quad \forall \delta \widehat{q}_h \in \widehat{\mathcal{Q}}_{h,k-1}^C \text{ (or } \mathcal{Q}_{h,k-1}^C),$

with $G_h^R(\mathbf{u}_h, \widehat{p}_h, \delta \mathbf{v}_h)$ and $G_h^R(\mathbf{u}_h, \widehat{p}_h, \delta \widehat{q}_h)$ being of the form

$G_h^R(\mathbf{u}_h, \widehat{p}_h, \delta \mathbf{v}_h) = \int_{\Omega_h} \left[ -\frac{\partial \widehat{W}^*}{\partial \mathbf{F}}(\mathbf{x}, \mathbf{I} + \nabla_{h,k} \mathbf{u}_h, \widehat{p}_h) + \widehat{p}_h \text{adj}(\mathbf{I} + (\nabla_{h,k} \mathbf{u}_h)^T) \right] : \nabla_{h,k}(\delta \mathbf{v}_h) \, d\mathbf{x} - \oint_{\Omega_h} \mathbf{f}_h \cdot \delta \mathbf{v}_h \, d\mathbf{x} - \oint_{\Gamma_h^t} \mathbf{t}_h \cdot \delta \mathbf{v}_h \, ds, \quad (12.14)$