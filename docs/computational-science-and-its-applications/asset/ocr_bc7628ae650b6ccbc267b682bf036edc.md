F(x, K) = {k ∈ K : d(x, k) = δ(x, K)}.

The collection of all such points of K for which farthest distance of some x from K is attained is denoted by FarK, i.e

FarK = {k ∈ K : k ∈ F(x, K) for some x ∈ X}.

# Definition 21.7 A center c of a subset M of a metric space (X, d) is an element c ∈ X such that

δ(c, M) = inf{δ(x, M) : x ∈ X}.

A space X is said to admit centers if every non-empty bounded subset of X has a center.

Centers of sets have played a major role in the study of uniquely remottal sets (see [Astaneh 1983], [Astaneh 1986] and [Baronti 1993]). Whether a set has a center or not, is another question. However, in inner product spaces, any closed bounded set does have a center(see [Astaneh 1983]).

# Definition 21.8 A subset V of a metric space (X, d) is said to be M-compact if for every x ∈ X and every sequence < v_n > in V with

lim d(x, v_n) = δ(x, V) (21.3)

there exists a subsequence < v_{n_j} > converging to an element of V. Any sequence satisfying Equation (21.3) is called a maximizing sequence for x in V.

Clearly every compact set is M-compact.

# Definition 21.9 Let (X, d) be a metric space. A mapping W : X × X × [0,1] → X is said to be a convex structure on X if for all x, y ∈ X and λ ∈ [0,1]

d(u, W(x, y, λ)) ≤ λ d(u, x) + (1 − λ) d(u, y) (21.4)

holds for all u ∈ X. A metric space (X, d) together with a convex structure is called a convex metric space [Takahashi 1970] and is denoted by (X, d, W).

The following properties (see [Takahashi 1970]) are direct consequences of Equation (21.4):

W(x, y, 1) = x,   W(x, y, 0) = y,   d(W(x, y, λ), y) = λ d(x, y),

d(W(x, y, λ), x) = (1 − λ) d(x, y), d(x, y) = d(x, W(x, y, λ)) + d(W(x, y, λ), y).

Every normed linear space is a convex metric space, however there are plenty of convex metric spaces which are not normed linear spaces (see [Takahashi 1970]).

# Definition 21.10 A metric space (X, d) is called a linear metric space if (i) X is a linear space (ii) addition and scalar multiplication in X are continuous, and (iii) d is translation invariant i.e. d(x + z, y + z) = d(x, y) for all x, y, z ∈ X. A complete locally convex linear metric space is called a Fréchet space.

# Example 21.2 Let X be the collection of all sequences of scalars made into a vector space with the usual vector space operations. Define d : X × X → [0,1] by d(x, y) = Σ_n 1/2^n min