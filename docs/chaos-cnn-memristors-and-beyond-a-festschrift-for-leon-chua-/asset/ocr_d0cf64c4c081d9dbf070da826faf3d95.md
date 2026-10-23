the automata act on a finite ring. Using symmetries and introducing new criteria, he sifted each rule in order to understand globally this family.

Chua studied 1-D Wolfram’s cellular automata on finite words (called “bit-strings” in the Chua language) on a circle C_l of length l, that is, the ring of integers modulo l, (Z/lZ). They are finite dynamical systems X = (X, f) such that the configuration space X = S^{C_l}, S = {0,1} and f : X → X is a transformation defined by

(fx)_n = F(x_{n−r},…,x_{n+r}),
 x = (x_i) ∈ X, n ∈ C_l.

F is called the local rule and r is called the range of the cellular automaton map f. In the case r = 1, there are 256 possible rules numbered using the well known binary Wolfram numbering. Apart from f, consider the left shift transformation σ : X → X defined as follows.

(σx)_n = x_{n+1},   x ∈ X,  n ∈ C_l.

Studying the attractors of each rule, Chua observed that, in some large class of rules, the dynamical map f^n acts ultimately as a shift σ, or more generally as a k-step shift σ^k. He called such rules Bernoulli shifts. This investigation meets another investigation on the existence of traveling waves in cellular automata on Z in [5,8,9], where a method allowing the identification of those initial configurations x ∈ S^Z such that f(x) = σ^k(x) showed that those configurations are spatially periodic for all k greater than r. When k ≤ r there are many non periodic traveling waves [20]. Using the isomorphism between {0,1}^Z and the interval [0,1], Chua et al. associated to each cellular automaton a map of this interval into itself. Their explicit study of the basins of the Wolfram CA-maps is the most complete updated investigation providing an exhaustive classification including invariance and fractal properties, abundance of Isles of Eden in most rules, scale-free properties and some new empirical quasi-ergodicity.

# 2. Cellular Automata as Dynamical Systems

From now on, we extend the above definition substituting C_l by Z. The CA-map is an example of a toy spatially extended system, since physical extended dynamical systems are given by PDE’s in large space. However some notions here used may be generalized to Lattice Dynamical Systems.

The complex dynamics of spatial patterns of the extended dynamical system is very rich compared with the dynamics of systems with few degrees of freedom. Concepts of Lyapunov exponents and topological and Kolmogorov-Sinai entropy are reformulated in order to take into account the space-time interplay. One of these new concepts is the spatial density of entropy (cf. [3]) which is associated to the two parameters group of space translation and temporal evolution. In general, when this density of entropy is non zero, the entropy of the temporal evolution group is infinite.

The cellular automata dynamical systems are the simplest spatially extended toy systems on an infinite lattice with finite entropy. In order to distinguish the trivial CAs like shifts from those more complex CAs, Milnor ([15,16]) introduced a concept of directional entropy, showing a class of CAs that unlike shifts, have positive entropy in many directions. Recently, a concept of directional Lyapunov exponents has also been introduced ([7]). Let us start with Lyapunov exponents. M. A. Shereshevsky has introduced a rigorous definition of the so-called Lyapunov exponents ([17]) after Wolfram ([21]). According to Wolfram these exponents aim to describe a velocity of propagation to the right or to the left of the “local perturbations” of initial patterns in one-dimensional CAs. In fact, modifying locally a spatial configuration, may lead either to an infinite expansion of the perturbation or to its containment. In the first case, to the instability of the initial configuration corresponds a positive Lyapunov exponent. Viewing a Lyapunov exponent in a space-time diagram is the best way to observe the intrinsic instability of such systems.

Let us first introduce some notations following Shereshevsky. For a given configuration x = (x_i) denote by W_s^+(x) the set of all configurations y obtained from x in modifying it only at the left of the site s ∈ Z. In other words y_i = x_i for all i ≥ s, and arbitrary otherwise. W_s^-(x) is similarly the set of perturbed configurations at the right of the site (−s). Let us compute the evolution of a perturbed configuration y ∈ W_0^+(x) at the left of the site 0 that will start to differ from x under the action of the CA-map, f(y), f^2(y), etc. By using the formula

f(y)_0 = F(y_{−1}, y_0, y_1)   (1)

and the fact: y_0 = x_0, y_1 = x_1, we see that

f(y)_0 = F(y_{−1}, x_0, x_1)   (2)