
## 10.4.2 Dual formulation as vertex weights

Instead of examining equilibrium through the lens of edge weights, one may instead attack the problem from the perspective of the discrete Airy stress surface S. Here we can make an important observation: when a thrust network top view M is simply connected and has purely triangular faces, then all discrete convex functions S on M are valid discrete Airy stress surfaces on M, since S automatically has planar faces. To each such S must be associated a reciprocal diagram, which in this case is the power diagram [19] (see Section 9.2.1) with vertex weight $r_i$ at $\bar{\mathbf{v}}_i$ given by

$$r_i = \frac{1}{2} \| \mathbf{v}_j \|^2 - \frac{1}{2} s_i.$$

Some sets of edge weights do not correspond to valid reciprocal diagrams, and hence Airy stress surfaces (if they do not satisfy (10.2)) and many sets of edge weights can give the same Airy stress surface. On the other hand, the vertex weights $s_i$ form a reduced basis for the valid Airy stress surfaces, an observation that de Goes et al. [113] and Liu et al. [255] leveraged into efficient algorithms for finding equilibrium thrust networks $M'$ approximating a designed network M.

Given M, the algorithm seeks $S_i$ and heights $z_i$ satisfying the vertical equilibrium condition (10.3) while keeping the $z_i$ as close as possible to their designed values; de Goes et al. [113] propose to penalize displacements of $z_i$ more for vertices initially closer to equilibrium. The compression-only constraint, that S is convex, becomes a set of linear inequality constraints encoding that every edge of S is a convex edge. The algorithm can be easily modified to handle the more general case where M has holes, and S exists only locally. It can also be augmented to allow sliding of the top view vertices, using edge flips to keep M a regular triangulation [255].

## 10.4.3 Perfect Laplacian optimization

Recall that equilibrium of M is equivalent to the existence of a perfect Laplacian (10.2) on the top view $\bar{M}$ for which vertical heights of the network vertices satisfy a Poisson equation (10.3). Herholz et al. [187] studied perfect Laplacians on polygonal meshes and developed a different approach to finding an equilibrium thrust network $M'$ given a guess M. The key insight is that a current guess for the weights $w_{ij}$, together with the specified supported boundary vertex positions and the external loads, uniquely determine heights $z_i$ of a thrust network $M'$ in equilibrium, with $\bar{M} = \bar{M}'$, via (10.3). Comparing edge lengths of $M'$ to M suggests that the edge weights should be updated as

$$u_{ij}^{k+1} = u_{ij}^k \frac{\| \mathbf{v}_i^k - \mathbf{v}_j^k \|}{\| \mathbf{v}_i - \mathbf{v}_j \|},$$

where $u_{ij}^k$ and $\mathbf{v}_i^k$ are the edge weights and vertex positions at the k-th iteration of the algorithm. This process is repeated until convergence of $M'$.

![](img/4913dd83a2a14bc205a0a92cce102c82_209_0.png)

Figure 10.8. Left: Direct optimization of the thrust network can cause “spikes” to appear where the stresses change rapidly over the surface. Optimizing for constant dual-isotropic mean curvature yields a better-behaved thrust network. (Data for this image courtesy of Yang Liu and Hao Pan.) Right: Laying out blocks on a thrust surface by staggered grouping of quadrilateral faces, as a final step of the design process. (Image courtesy of Daniele Panozzo, used by permission.)

Remarkably, this optimization works well even in cases where the top view \(\tilde{M}\) has challenging geometry, such as sliver triangles or non-convex polygonal faces, which is far from admitting a perfect Laplacian. Moreover, the update rules for \(M\) and \(w_{ij}\) do not require the constrained optimization of the alternating algorithm in Section 10.4.1, instead needing only the solution of sparse linear systems. On the other hand, the forms \(M'\) to which this approach converges can differ substantially from the initial design \(M\).

## 10.4.4 Relative-curvature-based smoothing

One drawback of the optimization methods presented so far is that they do not guarantee the quality of the final, equilibrium thrust network \(M'\); indeed, a common problem is the presence of “spikes” in the equilibrium network, caused by edge weights that vary wildly over the star of a vertex (or equivalently, stresses that do not change smoothly over a small neighborhood). See Figure 10.8, left. Liu et al. [255] developed a method for addressing this problem by insisting that \(M\) has constant dual-isotropic relative mean curvature relative to its Airy stress surface \(S\): \(H_{ij}^r = H\) for a constant \(H\) (taken to be the median value of \(H_{ij}^r\) in the input network). If this assumption were to hold, equilibrium, as understood in terms of curvatures in (10.8), would reduce to

$$-F_i = 2A_i K_g^h H = 24 A_i (S^*, S^*) H,$$

where the dual cell areas \(A_i(S^*, S^*)\) depend on the stress surface heights \(s_i\). Liu et al. solve for these using Newton's method, taking care that \(S\) remains convex (this is done by computing the convex hull and projecting any violating vertices down to the convex hull in between Newton iterations). This curvature-smoothing operation dramatically improves the fairness of the thrust network.

![](img/4913dd83a2a14bc205a0a92cce102c82_210_0.png)

Figure 10.9. Left: Initial thrust network and Airy stress surface. Middle: Eigenvectors of [H₁]⁻¹[H₂] trace out curve networks conjugate to both surfaces. Right: Simultaneous remeshing of both thrust network and stress surface as planar quadrilateral meshes. (Images courtesy of Mathias Höbinger, used by permission.)

## 10.4.5 Steel-glass structures and PQ faces

A popular alternative to masonry for realizing freeform structures are steel-glass constructions, made out of glass panels supported inside a steel skeleton. Under the assumption that the glass panels are not structural and carry no load, equilibrium of steel-glass structures is identical to equilibrium of thrust networks, with the exception that the steel beams can carry only bounded compressive load, and do support some tension.

Steel-glass structures introduce new aesthetic considerations, however. Quadrilateral glass panels are preferred to triangular ones, as the nodes where beams meet in the former case have lower valence and are thus easier to manufacture, and the structure requires fewer steel beams, making the structure more permeable to light. Planar glass panels are much preferred to curved panels, as it is much easier to cut planar panels from a large glass sheet, than it is to hot-bend custom panel shapes.

We are thus left with a geometry problem: given a thrust network M in equilibrium, it can be approximated by a thrust network N with planar quadrilateral faces? Let S be the Airy stress surface certifying M’s stability. One could simply remesh M, and then resample S to yield Ψ with Ψ = N. While Ψ would still be convex, there is no guarantee that the faces of Ψ are planar, and thus Ψ is no longer necessarily a valid stress surface. One thus needs to simultaneously remesh both M and S so that both remeshed surfaces have an identical top view, and planar quadrilateral faces (see Figure 10.9).

The edges of any planar quadrilateral mesh approximating M follow conjugate curve networks [347] on M. More specifically, if M approximates a smooth surface $z: \bar{M} \to \mathbb{R}$. $M$ can be remeshed as a planar quadrilateral mesh by first finding two families of curves $\mathbf{a}(s,t), \mathbf{b}(s,t)$ in the plane with $a^T[\mathbf{H}_s]\mathbf{b} = 0$. Since the same must hold for $S$ approximating $s$, we need families of curves satisfying
$a^T[\mathbf{H}_s]\mathbf{b} = a^T[\mathbf{H}_s]\mathbf{b} = 0$,

which we can find by taking $\mathbf{a}$ and $\mathbf{b}$ to be streamlines following the eigenvectors of $[\mathbf{H}_s]^{-1}[\mathbf{H}_s]$. A new top view can be traced along these lines, and then lifted to planar quadrilateral remeshings $N$ and $\Psi$ of $M$ and $S$, using the procedure of Schifter [347]. Since remeshing does not alter the surface's coarse geometry, $\Psi$ is close to being convex and to satisfying the curvature equilibrium equation (10.8); $N$ and $\Psi$ can be further polished using Newton's method to exactly satisfy equilibrium and face planarity.

The unexpected consequence of the above is the following theorem [405].

**Theorem 10.4.** If a surface $z(x,y)$ can be approximated by a thrust network $M$ in compressive equilibrium, it can also be approximated by a thrust network $N$ in compressive equilibrium and with planar quadrilateral faces.

However, there is no guarantee about the quality of the faces, which can vary dramatically in scale across the surface.

## 10.4.6 Block layouts from stable surfaces

Once a thrust network in equilibrium has been found, a masonry structure can be constructed around it that is guaranteed to be stable by the safe theorem, as discussed in Section 10.3.2. However, a practical issue remains: blocks arranged directly by dualing the thrust network tend to lie in long “chains” or “strips” that easily come apart under weathering or horizontal load. Panozzo et al. [301] developed a post-processing algorithm that remeshes the thrust network into blocks that are rectangular and staggered, much as is seen in a regular brick wall. The algorithm first remeshes the surface into a quadrilateral mesh. If the quad mesh has no singularities, one can find a staggered block pattern by simply deleting every other “vertical” edge. Generally speaking, a nontrivial freeform surface has complex geometry with several singularities present after remeshing, so edges are instead removed by solving a 2-coloring problem, which guarantees that blocks are staggered and are composed of at most two quads (see Figure 10.8, right).

## 10.5 CONCLUSION AND OPEN PROBLEMS

Although computational analysis and form-finding of stable freeform masonry structures is by now a thoroughly studied topic, there remain several open questions that have not been addressed by any previous work. Answering them will require significantly expanding our understanding of the mathematics of stable masonry, and its connections to discrete and smooth geometry.
