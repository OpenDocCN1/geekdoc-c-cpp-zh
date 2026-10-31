following also uses this nomenclature. However, others refer to them as Daublet(k) and Symlet(k) wavelets. That is, the Daublet(4) (shark-fin) wavelet in Figure 12.6a is sometimes referred to as a Daublet(2) wavelet. Check the definition and be careful!

# 12.3.3 Fundamental Wavelet Approximation Result

The fundamental wavelet-based approximation result analogous to the Fourier series approximation is given in Theorem 12.1 that follows.

# Theorem 12.1

Let {ψ_{j,k}} be an orthogonal wavelet basis, and let g ∈ L²(ℝ). Then,

g(x) = Σ_{j=-∞}^{∞} Σ_{k=-∞}^{∞} d_{j,k} ψ_{j,k}(x),  (12.15)

where the equality is in the mean-square sense and the wavelet transform coefficients, d_{j,k}, are given by

d_{j,k} = 1/||ψ||² ∫_{-∞}^{∞} g(t) ψ_{j,k}(t) dt,  (12.16)

where ||ψ||² denotes ∫_{-∞}^{∞} |ψ(x)|² dx.

Proof: See Daubechies (1992) and Ogden (1997). Appendix 12A gives a formal derivation to show that if Equation 12.15 holds, then d_{j,k} is given by Equation 12.16.

Equation 12.15 is analogous to the Fourier series representation in Equation 12A.3. Also, the coefficients, d_{j,k}, in Equation 12.16 correspond to the Fourier series coefficients, α_k in Equation 12A.4. In Fourier analysis large values α_k² of are associated with data (in our setting time series) that have periodic content in the neighborhood of the frequency f = k/n. Similarly, large values of | d_{j,k} | in Equation 12.15 are associated with detail behavior of duration about 2^j, that is, the “frequency” or “1/scale” is about 2^{-j}. In Fourier analysis, α_k’s as defined in