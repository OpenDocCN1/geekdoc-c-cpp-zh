# 2

# Preliminary Notions

Two sets of basic notions are studied in this chapter, which is mainly based upon [1, 125]:

+   - the first ones are related to the objects we are interested in: *subdivisions* of geometric objects. They are illustrated by following Griffith’s approach about surface classification [125], and then extended for higher dimensions;
+   - the second ones are related to the *representations* of these subdivisions. Here we are interested in defining data structures which can be handled in geometric softwares: such representations are algebraic ones, based upon well-known discrete structures equivalent to graphs.

Some notions are not formally defined, since the goal of this chapter is to give an intuition about (*subdivisions of*) quasi-manifolds, and about *identification*, which is the basic construction operation. Quasi-manifolds are formally defined in chapter 8. See [1, 196, 180, 133] for introductions to topology.

# 2.1 Basic Topological Notions

Some classical vocabulary is introduced here.

# 2.1.1 Basic Elements

*Balls:* cf. Figs. 2.1(a), (b) and (c).

Let ℝⁿ = {x = (x₁, …, xₙ)|xᵢ ∈ ℝ, 1 ≤ i ≤ n} be the usual *n-dimensional* space. Let r ∈ ℝ.

+   - *Bᵣⁿ(x) = {y ∈ ℝⁿ|d(x, y) < r}*, where *d(x, y)* denotes the usual Euclidean distance between *x* and *y*, is the *n-dimensional open ball of radius r around x in ℝⁿ*;
+   - *B̄ᵣⁿ(x) = {y ∈ ℝⁿ|d(x, y) ≤ r}* is the *n-dimensional closed ball of radius r around x in ℝⁿ*;