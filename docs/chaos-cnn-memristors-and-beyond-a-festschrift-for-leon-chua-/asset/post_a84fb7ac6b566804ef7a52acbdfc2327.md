
subregions

```
$$P_0=\{(p,q):pq<1\},$$

$$P_{IT}=\bigcup_{m>2}P_m,$$

$$P_m=\left\{(p,q):\sum_{i=0}^{m-2}p^{-i}<q<p^{-m+1}\right\},$$

$$P_{ST}=P\setminus(\overline{P_0}\cup\overline{P_{IT}}),$$
```

each is open in $P$. The boundary between the sub-regions is advisable to represent in the form

```
$$G=\bigcup_{m\ge2}G_m^-\cup\bigcup_{m\ge3}G_m^+,$$

$$G_2^- =\{(p,q):pq=1\},$$

$$G_m^- =\{(p,q):q=p^{-m+1}\}\cap\overline{P_m},$$

$$G_m^+ =\left\{(p,q):\sum_{i=0}^{m-2}p^{-i}=q\right\}\cap\overline{P_m},\qquad m=3,4,\ldots$$
```

- Where $(p,q)\in P_0$, the map $g$ has an attracting cycle of period 2, that attracts all the points from $[0,1]$ except the (repelling) fixed point $z=q/(1+q)$.
- Where $(p,q)\in P_m^+$, $m>2$, the map $g$ has an attracting cycle of period $m$; this cycle attracts all the points from $[0,1]$ except the set $D(g)$ formed by the unstable points of $g$ (and including the repelling cycles and their preimages) and is a cantor set of positive Hausdorff dimension $(0<d_H D(g)<1)$. The basin of the attracting cycle consists of a countable number of open intervals (which are the preimages of the $m$ “main” intervals that contain this cycle).
- Where $(p,q)\in P_{ST}$, the map $g$ has no attracting cycles but it has a cycle of intervals $J_1,\ldots,J_s$, $s=s(p,q)$, that “takes up” almost all the points from $[0,1]$. In this case, $g$ is transitive on the set $J=\bigcup_{i=1}^sJ_i$ (i.e. almost each trajectories is dense on $J$) and has a smooth invariant measure concentrated on $J$ (in addition, $g^s$ is probabilistically intermixing on $J_k$, $k=1,\ldots,s$). When $(p,q)$ is in the vicinity of $G_m^-$, then $s=2m$. When $(p,q)$ is in the vicinity of $G_m^+$, then $s=1$ and, moreover, $J=[0,1]$; hence, the support of the smooth invariant measure consists of the unique interval $[0,1]$.

The boundary $G$ is the site of bifurcations of two types.

- At the boundary $G_m^-$, $m\ge2$, we observe a ‘soft’ doubling period bifurcation. The attracting cycle of period $m$, that exists when $(p,q)\in P_m$, transforms, when $(p,q)$ gets on $G_m^-$, into a “taking up” cycle of intervals $J_1,\ldots,J_m$ of exclusive structure: $g^m(z)|_{J_i}=-z$, $i=1,\ldots,m$; therewith the end-points of the intervals $J_1,\ldots,J_m$ are the preimages of the break-point $z=a$. Consequently, every interval $J_i$ is the union of two adjacent intervals which transform one into another under $g^m$. When $(p,q)$ moves away from $G_m^-$ and passes in $P_{ST}$, the adjacent intervals “move apart” and produce a cycle of intervals with period $2m$. It is just the way in which the ‘soft’ doubling period bifurcations happen for piecewise linear maps.
- At the boundary $G_m^+$, $m\ge3$, we deal with a ‘hard’ cycle birth bifurcation. Locally this cycle birth corresponds to a tangential bifurcation for smooth maps: the (repelling or semi-repelling) cycle of period $m$, produced during the transition of $(p,q)$ from $P_{ST}$ at $G_m^+$, splits into two cycles of period $m$, attracting and repelling, when $(p,q)$ moves away from $G_m^+$ and passes in $P_m$.

However, the case $(p,q)\in G_m^+$, $m\ge3$, is the first to give rise a cycle of period $m$, that has the so-called maximal type [2]: if $\gamma_1<\gamma_2<\cdots<\gamma_m$ are the points of the cycle, then $g(\gamma_i)=\gamma_{i+1}$, $i=1,2,\ldots,m-1$, and $g(\gamma_m)=\gamma_1$, which means

![](img/039e7d3c23390584a66737067db8b75b_218_0.png)

![](img/039e7d3c23390584a66737067db8b75b_219_0.png)

![](img/039e7d3c23390584a66737067db8b75b_219_1.png)

Fig. 3. Bifurcation diagram for the family (11) in the plane (z,p) with q = 4 (left) and q = 8 (right).

that all but one points of the cycle are placed on [0,a] (the cycle includes, in particular, the points z = 0,a,1.) Clearly the cycles of period m, that appear when (p,q) transfer into P_m, also are of maximal type. In families of unimodal maps, cycles of maximal type appear last among all the cycles of period m (when (p,q) ∈ P_m and m is large, g has many cycles of period m; for instance, if m is a prime number, there are (2^m − 2)/m such cycles, which is the largest number of cycles of period m, which is possible for the logistic map).

Just this feature of the cycles structure allows to observe in piecewise linear maps the period-adding phenomenon (or the period adding route to chaos), marked already in [5]. For the map (11) we see this phenomenon on the bifurcation diagrams in Fig. 2 and Fig. 3.

To make clear some details, it is useful to note certain differences in the bifurcations for the piecewise linear map (11) and for smooth maps by the example of the logistic map x ↦ λx(1 − x), 3.83 < λ < 4, when the latter already has a cycle with period 3.

With increasing the parameter λ in the logistic map, every cycle is born either as an attracting one (a soft period doubling bifurcation), or together with an attracting one (a hard tangential bifurcation). For λ ≈ 3.83 a cycle of with period 3 appears and thereafter there arise successively cycles of maximal type with periods 4,5,6,… The same sequence of cycles of maximal type realizes

for (11), the only difference being in the following. In both the families, between the birth of a cycle of maximal type with period m and the birth of a cycle of maximal type with period m+1, a countable number of cycles with periods > m + 1 come into being. But for the logistic family, all these cycles appear, as noted, to be attracting or to be paired with a repelling one, and for the family (11), all the appearing cycles are, contrary, repelling (i.e., invisible). Thus, in the family (11) we observe the period-adding phenomenon — the successive appearance of attracting cycles, which is characterized by the increase of period of 1 only, and is alternated by “windows of chaos”.

## 3.3. Ideal turbulence from the lossless transmission line

For any initial condition (4), there corresponds a unique solution

```
(v(x,t), i(x,t))_{φ,ψ} : [0,l] × ℝ⁺ → ℝ²
```

Hence, on the space of continuous, piecewise smooth initial vector-functions (φ,ψ) : [0,l] → ℝ², the BVP induces the dynamical system

```
Sᵗ : (φ(x), ψ(x)) ↦ (v(x,t), i(x,t))_{φ,ψ}. (12)
```

In order to understand which may be the asymptotic dynamics of the system (12), it is reasonable to consider in parallel with (12) the simpler discrete dynamical system (10), which is associated

with (12) via the formulas (5)–(9) and includes the managing map f in an explicit form.

The properties of the model map g lead to the following theorem.

# Theorem 1. Let the conditions (*) be fulfilled. Then if (p,q) ∉ P₀ every initial state φ other than a constant on any interval from [−1,0] generates ideal turbulence in the system (10); therewith for each ζ ∈ ωΔ[φ], 1 < d(ζ) < 2 when (p,q) ∈ P_IT, and d(ζ) = 2 when (p,q) ∈ P_ST. Moreover, if (p,q) ∈ P_ST, every nonsingular initial state φ generates stochastic turbulence in the system (10).

This theorem is a good example to understand why and how turbulence happens in the problems whose dynamics is specified by a 1D map.

- For ideal turbulence, the main factor is the complex topological structure of the set D(f) formed by the unstable points of f. Where f : I → I has a cycle of period other then the powers of 2, the Hausdorff dimension of D(f) is positive. The system (10) “inherits” this property. Schematically, this fact can be explained in the following way. Let D(f,φ) = φ⁻¹(D(f)). With the completion of the phase space via the metric ρΔ, the ω-limit set ωΔ[φ] consists of functions ζ : [−1,0] → 2^I such that ζ(τ*) is a singleton (i.e. a one-point set) when τ* ∉ D(f,φ), and a closed nongenerated interval when τ* ∈ D(f,φ). In typical situations, d(ζ) = d_H D(f,φ) + 1 and d_H D(f,φ) > 0, which implies d(ζ) > 1.

- For stochastic turbulence, of fundamental importance is both the occurrence of a smooth invariant ergodic measure (s.i.e.-measure) for f and the fact that for interval maps, the availability of s.i.e.-measures is not extraordinary point (for ample classes of parameter-dependent maps, the parameter values at which the map possesses a s.i.e.-measure form a set of positive Lebesgue measure).

Where f : I → I possesses a s.i.e.-measure μ, almost every trajectory fⁿ(z), n ∈ ℤ⁺, restores μ:

the residence time of the trajectory in a set A ⊂ I is equal to μ(A). With the completion of the phase space via the metric ρ#, this ‘temporal’ stochasticity of f transforms into ‘spatial-temporal’ stochastization of the system (10). Most simply this fact is possible to explain when the support of μ consists of a single interval. In such a case, for all nonsingularᵃ initial states φ(τ), τ ∈ [−1,0], their ω-limit sets ω#[φ] coincide with the same “point” — a stationary stochastic process ξ#(τ), τ ∈ [−1,0], with mutually independent values,ᵇ whose one-dimensional distribution function is of the form F(y,τ) = μ((−∞, y] ∩ supp μ). With regard to Eq. (7), this means that, given ε* > 0, for any solution β(τ) arising from a nonsingular initial function, and a however small σ > 0 there exists τ* > 0 with the property |F_β^ε(y,τ) − μ((−∞, y] ∩ supp μ)| < σ for τ > τ*, ε > ε*, y ∈ ℝ,

recall that F_β^ε(y,τ) is the ε-averaging of distribution function of the solution β(τ). It follows from the previous section that supp μ = I in the vicinity of “subboundary” ∪_{m≥3} G_m⁺.

We now return to the problem (1), (2) and its associated dynamical system (12). With Theorem 1 and the relationship between the systems (12) and (10), given by S^t[(φ,ψ)](x) = (𝕊^κ[φ](τ−κ) − 𝕊^{κ+1}[φ](τ−κ), 𝕊^κ[φ](τ−κ) + 𝕊^{κ+1}[φ](τ−κ)), τ = (νt/l −1)/2, φ(τ) is as in (9), κ is the integer part of τ, we have every reason to formulate the following theorem.

# Theorem 2. Let the conditions (*) be fulfilled and (p,q) ∉ P₀. Then ideal turbulence occurs in the BVP (1), (2). Moreover, where (p,q) ∈ P_ST, there occurs stochastic turbulence in the BVP.

The former assertion of Theorem 2 is virtually evident: for almost every initial state (φ,ψ) of the system (12), one can find ζ ∈ ωΔ[(φ,ψ)] such that 1 < d(ζ) ≤ 3.
