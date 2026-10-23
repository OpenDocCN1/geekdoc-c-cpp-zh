expansion of (ℱ, X). Suppose there exist constants Λ_ij satisfying (2) for ℱ. Then there are constants 	ilde{Λ}_ij satisfying (2) for 𝒳_S ℱ such that ρ(\tilde{Λ}) ≤ ρ(Λ).

# Example 4.

Let (ℱ, X) be the dynamical network given in Example 2 once again considered as a network without local dynamics. That is,

ℱ(x) = [1 − T₁(x₁)T₂(x₂)/α; 1 − T₁(x₁)T₃(x₃)/α; 1 − T₂(x₂)T₃(x₃)/α] for α ≥ 1

where T_i(x_i) = 4x_i(1 − x_i) and X = [0,1]³.

Note that the system (ℱ, X) has the same form as the dynamical network in Example 3. Hence, for S = {v₁, v₃} the expansion (𝒳_S ℱ, X_S) given by Eq. (6) is

𝒳_S ℱ(x) = [𝒳_S ℱ₁; 𝒳_S ℱ₃; 𝒳_S ℱ₁₂₁; 𝒳_S ℱ₁₂₃; 𝒳_S ℱ₃₂₁; 𝒳_S ℱ₃₂₃] = [1 − T₁(x₁)T₂(1 − T₁(x₁₂₁)T₃(x₃₂₁)/c)/c; 1 − T₂(1 − T₁(x₁₂₃)T₃(x₃₂₃)/c)T₃(x₃)/c; x₁; x₁; x₃; x₃] (7)

Letting \tilde{Λ}_{ij} = max_{x∈X_S} |(Dℱ_S)_{ji}(x)| one can compute that

\tilde{Λ} = [16(c−1)/c³ 0 1 1 0 0; 0 16(c−1)/c³ 0 0 1 1; 16/c³ 0 0 0 0 0; 0 16/c³ 0 0 0 0; 16/c³ 0 0 0 0 0; 0 16/c³ 0 0 0 0]

where the rows (and columns) of \tilde{Λ} are numbered as in Eq. (7). The spectral radius of \tilde{Λ} is then given by ρ(\tilde{Λ}) = [8c − 8 + 4√(4 + 2c(c³ + 2c − 4))]/c³

As ρ(\tilde{Λ}) < 1 for c > 6.75 then Theorem 3 implies (ℱ, X) has a globally attracting fixed point for c > 6.75. Note that this is better than the estimate gained by direct (standard) analysis of (ℱ, X) in Example 2.

Importantly, we note that the method of using network expansions generalizes the method used in [1, 2] for determining whether a network has a unique global attractor. As a final observation, in this section, we note that it is possible to sequentially expand a dynamical network and thereby sequentially improve ones estimate of whether the original untransformed network has a globally attracting fixed point.

# 4. Concluding Remarks

The large majority of real world networks are dynamic. Yet most studies consider either only the structure or the dynamics of these networks. As the spectrum is an important dynamical aspect of a network, isospectral graph transformations provide a way of studying the interplay between the topology of a network and its dynamics.

As a tool for investigating networks, isospectral transformations are quite flexible. Isospectral transformations can be used to reduce or expand the size of a network, considered as a graph, while either modifying or maintaining the edge weights of the network [5]. These isospectral graph reductions and isospectral graph expansion have the following useful properties and applications.

Isospectral graph reductions allow one the ability to uniquely reduce a network to any subsets of its vertex set while preserving the network spectrum. This in turn allows for the introduction of new equivalence relations on the space of all networks where two networks are equivalent if they can be reduced to the same network via some rule.

From the point of view of applications, such rules can be designed by experimentalist to compare different networks modulo some specific network structure. However, this requires experts in a particular field (biologist, physicist, etc.) to determine an appropriate set of network elements over which to reduce the network.