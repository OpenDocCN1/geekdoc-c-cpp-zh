**Lines — into the model.** To add lines to our search for the best fitting circle we need to incorporate them into the parameter scheme. The natural circle parameters $(a, b, R)$, unfortunately do not include lines. Karimäki’s parameters $(\rho, d, \varphi)$ incorporate lines if one allows $\rho = 0$; then $d$ and $\varphi$ are the same as our $C$ and $\varphi$ in equation (2.4). The algebraic parameter scheme (3.8) easily integrates lines, too, by setting $A = 0$, then we recover the linear equation (2.1).

**Noncompactness of the parameter space.** Here we provide a rigorous analysis involving the notion of compactness already employed in Section 2.2. We follow [43], and a similar argument is given by Nievergelt, see page 260 in [138].

The function $\mathscr{F}$ is obviously continuous in the circle parameters $a, b, R$, but the parameter space is not compact as $a, b, R$ may take arbitrarily large values. What is worse, the “reduced” space of circles intersecting any given rectangle $\mathbb{B}$ (“bounding box”) is not compact either, so the remedy we used in the case of lines (Section 2.2) will not save us anymore.

![](bbox=[0.35, 0.39, 0.65, 0.53])

Figure 3.3: *Straightening a circular arc and shrinking a circle to a singleton*.

**Direct geometric argument.** The noncompactness can be again demonstrated geometrically if we introduce an appropriate topology on the space of circles. Following the pattern of (2.7)–(2.8) we say that a sequence of circles $\mathbb{S}_i$ converges to a circle $\mathbb{S}$ (or more generally, to a closed set $\mathbb{S}$) on the plane $\mathbb{R}^2$ if for any closed disk $\mathbb{D} \subset \mathbb{R}^2$ we have

$$\operatorname{dist}_{H}(\mathbb{S}_{i} \cap \mathbb{D}, \mathbb{S} \cap \mathbb{D}) \rightarrow 0 \quad \text{as } i \rightarrow \infty \qquad (3.17)$$

where $\operatorname{dist}_{H}(\cdot,\cdot)$ is again the Hausdorff distance between compact subsets of $\mathbb{R}^2$, see (2.8). Now let us take a circular arc crossing the given bounding box $\mathbb{B}$ and straighten (flatten) it by fixing one of its points and the tangent line at that point, and then increasing the radius steadily. The arc will converge to a straight line, see Fig. 3.3. Also, if one takes a sequence of concentric circles with decreasing radii, they will shrink to a point. These constructions show that if we want the space of circles crossing the box $\mathbb{B}$ be compact, we *must* include lines and singletons in it.