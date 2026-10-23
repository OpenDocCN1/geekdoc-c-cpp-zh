![](bbox=[0.22, 0.09, 0.75, 0.26])

Fig. 2. The partition in (a) is synchronous while the partition in (b) is not synchronous.

In words, Theorem 1 says that if the state of the network belongs at a given time to manifold (3), characterized by the synchrony of groups of systems, then this synchrony is conserved forever and possibly enhanced because the states of two different groups of systems might asymptotically converge one to each other. This is why partitions satisfying condition (2) have been called synchronous.

In principle, there could exist manifolds preserving synchrony different from those pointed out by Theorem 1. Fortunately, this possibility is ruled out by the following.

# Theorem 2. If a manifold with groups of synchronous systems of the form (3), where Π = {π1, π2, …, πp} is a partition of N, is invariant, then Π is a synchronous partition.

Proof. When the system starts at time t0 in the invariant manifold (3), the state vectors of all the systems of the same group πi are identical, so that two different systems h1 and h2 belonging to the same group πi are described by
\dot{x}_{h1}(t0) = f(x^{(i)}) + D ∑_{j≠i} n_{h1πj} (x^{(j)} − x^{(i)})
\dot{x}_{h2}(t0) = f(x^{(i)}) + D ∑_{j≠i} n_{h2πj} (x^{(j)} − x^{(i)})

But \dot{x}_{h1}(t0) must be equal to \dot{x}_{h2}(t0) because manifold (3) is invariant, so that
∑_{j≠i} (n_{h1πj} − n_{h2πj}) (D x^{(j)} − D x^{(i)}) = 0.

Since this condition must hold for any arbitrary vector (D x^{(j)} − D x^{(i)}) in the range of D, which is at least one-dimensional because D ≠ 0, we must have n_{h1πj} − n_{h2πj} = 0 ∀ j ≠ i which is, indeed, condition (2).

Thus, S represents the number of manifolds in which synchrony is preserved (if not enhanced). S can be computed by an algorithm that checks if the topological condition (2) is satisfied for each partition. A Matlab version of this algorithm that takes advantage of an incremental construction of the possible partitions using a tree structure and a prune strategy which prematurely discards families of partitions that early violate condition (2) is available on request.

# 3. Topological Indicators of Synchronization Propensity

All forms of synchrony of system 1 depend on network topology (matrix [c_{hk}]), local dynamics (function f) and dispersal (matrix D). Functions that depend only on topology and capture the probability that a particular form of synchrony is present, when local dynamics and dispersal belong to a suitably defined admissible class, are called topological indicators of synchronization propensity. In this section we first review the three known topological indicators of synchronization propensity and then present a new one based on the notion of synchronous partitions discussed in the previous section.

The first topological indicator denoted by (a) in the following, has been proposed by Wu and Chua (see [17]) and refers to complete synchrony, namely to the case where all systems in the network behave in unison and return to this peculiar collective behavior after any small perturbation. The topological indicator (a) is theoretically justified when the admissible local dynamics are characterized by Master Stability Functions [10], which