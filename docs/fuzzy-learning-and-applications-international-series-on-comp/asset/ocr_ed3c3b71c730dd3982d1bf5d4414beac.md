is also assigned using a uniform distribution with parameters U[200, 500] milliseconds.

For a given point in the multi-dimensional problem space spanned by vectors (NAC, PAR, NCD) and (κ, δ), the overall performance of an algorithm is defined in terms of the number of times it outperforms the other algorithms. For this purpose we simulated F-ECT, B-ECT, JIT, AUS-F and the proposed neuro-fuzzy scheduler algorithms for each problem instance. For each simulation run, i, the value for ∑ₖ(Iₖℒ_d^k + Iₖℒ_b^k + Iₖℱ_k)(i) is recorded. Here, ∑ₖ Iₖℒ_d^k(i), ∑ₖ Iₖℒ_b^k(i) and ∑ₖ Iₖℱ_k(i) represent the total weighted number of AUS losses due to deadline misses, destination buffer overflow and AUS-filtering, respectively. Note that, in order to use a unified performance measure, the importance factor is also associated with deadline miss and buffer overflow objective. Let 𝒜 denote the set of algorithms considered here, i.e., 𝒜 = { F-ECT, B-ECT, JIT, AUS-F, NFS}. Performance comparison is based on the QOP factor Q(j), j ∈ 𝒜 defined as follows:

Q(j) = ∑_{i=1}^{100} 𝒲(j), (10.12)

where i refers to the ith simulation run for a given fixed point of the multi-dimensional problem space. The winner function, 𝒲(j), is defined as follows:

𝒲(j) = { 1 if ∑(ℒ_d + ℒ_b + ℱ)(j) ≤ ∑(ℒ_d + ℒ_b + ℱ)(k) ∀k ∈ 𝒜, 0 otherwise. 

In order words, QOP factor Q(j) represents the number of times algorithm j outperformed the other algorithms.

In the following we study the effect of various parameters on the performance of the proposed neuro-fuzzy scheduler. The performance comparison is based on the QOP factor defined in Equation 10.12.

# Effect of Amortized Capacity

In this section, we investigate the performance of the neuro-fuzzy scheduler under various setting of the NAC parameter. Fig. 10.13 depicts the performance results for four different types of SI work-loads. Fig. 10.13(a) uses SI work-load trace depicted in Fig. 10.6(b) while Fig. 10.13(b) uses the example SI profile of Fig. 10.6(a). Notice that the SI of Fig. 10.6(b) is computed by observing the reverse playout of SI of Fig. 10.6(a). Hence, arithmetic means of the capacity requirement profiles for both SIs are the same. However, as can be noticed from Fig. 10.13 (a) and (b), the performance of various algorithms for the two profiles varies significantly. Specifically, the work-load of