![](bbox=[0.28, 0.11, 0.72, 0.32])

Figure 4.6 Construction of the intermediate polygon $\Omega^{t_k}$ using the paths $\psi_i$.

with $M = M_1 + \cdots + M_n$ and $d = \max_{1 \le i \le n} \|u_i\|$. Overall, this implies that the mapping $f$ is injective if
$$d < \frac{\sqrt{5}-1}{2M}.$$

# 4.3 BIJECTIVE COMPOSITE BARYCENTRIC MAPPING

Section 4.2.1 suggests that if source and target polygon are sufficiently close, the mapping is close to the identity and hence bijective. Therefore, by “splitting” the barycentric mapping from source to target polygon into a finite number of intermediate steps, where each step perturbs the vertices only slightly, it should be possible to obtain a bijective composite mapping.

To this end, suppose that $\psi_i: [0, 1] \to \mathbb{R}^2, i = 1, \dots, n$ are a set of continuous vertex paths between each source vector $v_i^0 = \psi_i(0)$ and its corresponding target vector $v_i^1 = \psi_i(1)$, as shown in Figure 4.6. Let $\tau = (t_0, t_1, \dots, t_m)$ with $t_0 = 0, t_m = 1$, let $t_k < t_{k+1}$ for $k = 0, \dots, m-1$ be a partition of $[0, 1]$ and let $f_k$ be the barycentric mapping from $\Omega^{t_k}$ to $\Omega^{t_{k+1}}$, based on the barycentric coordinates $\phi_i^{t_k}$.

![](bbox=[0.17, 0.73, 0.82, 0.89])

Figure 4.7 Construction of a composite barycentric mapping for $\tau = [0, 0.5, 1]$.