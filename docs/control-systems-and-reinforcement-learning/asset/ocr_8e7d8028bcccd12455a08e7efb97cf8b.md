# B.2 Computational Aspects of MDPs

where $c_n(x) = c(x, \phi_n(x))$ for each $x$, $\eta_n$ is the steady-state cost using the policy $\Phi_n$, and $P_n$ is the transition matrix obtained when the chain is controlled by $\Phi_n$;

+   (ii) construct a policy:
$$\phi_{n+1}(x) \in \arg \min \{c(x,u) + P_u h_n(x)\}, \quad x \in X. \quad (B.14)$

The PIA is in a special case of the Newton-Raphson method, in which the function $T$ appearing in (B.8) is replaced by its linearization $\hat{T}_n$ to obtain a sequence of approximations to $h^*$.

Given some $h_n$, the mapping $\hat{T}_n$ is defined as a first-order Taylor expansion,
$$\hat{T}_n(h_n) \approx T(h_n) + D_n(h-h_n). \quad (B.15)$

where $D_n = \nabla T(h_n)$ is a $d \times d$ matrix when $X$ consists of $d$ elements. The Newton-Raphson method then defines $h_{n+1}$ as a solution of the equation,
$$h_n = T(h_n) + D_n(h-h_n). \quad (B.16)$

This is illustrated in Figure B.1
The functional $T$ may not be differentiable, but we can always find a subgradient $D_n$. This means that for any $h_n$ and any other function $g$,
$$T(h_n) \le T(h_n) + D_n(g),

The function $h-T(h)$ is convex, as illustrated in Figure B.1.
The following lemma shows how to obtain the gradient of $T(h)$.

+   **Lemma B.2** For any function $h: X \to \mathbb{R}$, let $\phi+$ denote a policy satisfying
$$\phi_+(x) \in \arg \min \{c(x,u) + P_u h(x)\}, \quad x \in X.$$

Let $P_+ = P_{\phi_+}$ and let $S$, the substitution operator, for any function $g: X \to \mathbb{R}$ by
$$S,g(x)=g(x^*), \quad x \in X.$

![](bbox=[0.313, 0.755, 0.683, 0.874])

**Figure B.1** PIA interpreted as an application of Newton-Raphson. The functional $T$ is piecewise linear for a finite-state/finite-action MDP.