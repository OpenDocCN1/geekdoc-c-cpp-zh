Likelihood term corresponds to the fidelity of the data and prior estimates r_{i,m}=r_{j,m} validity when f_g^m i.e. guidance image-value is given. It is assumed that distribution of p(f_g^m) is uniform. Thus it can be concluded that

p_{llhd} ∝ Θ^{2N-1}, where Θ = [ v_{i,m} v_{j,m} / (v_{i,m}^2 + v_{j,m}^2) ] (8.27)

p_{pr} ∝ exp(-A·Φ), where Φ = ( | (f_{i,m}^g)^2 - (f_{j,m}^g)^2 | / [ (f_{i,m}^g)^2 (f_{j,m}^g)^2 ] ) (8.28)

Using the idea of Nakagami and Rayleigh distribution, for N-look image [30] to represent image i with amplitude A:

p(i | f) = 2 (N / r)^N 1 / Γ(N) exp( - N i^2 / r ) i^{2N-1} (8.29)

Let i and f be speckled and guidance images. C, D are constants for normalization to calculate these images relatively. Thus GGF kernel weight for nonlinear system becomes

W_{i,j}(i, f^g) = exp( -1/C Σ_m 1/Θ + N/D Σ_m Φ ) (8.30)

Proper choice of the guidance image is crucial to remove speckle noise for a nonlinear guided filter. Now analyzing Equation (8.30) it can be observed that by tuning N, C, D, one can decide about the proportional effects of i or f^g on the final filtering output through various ranges of weight kernel values.

# 8.2.4.3 Guidance Image Construction

It is known from the literature that guidance image plays a crucial role in image filtering, actually considered as the prior value estimation of f. An idea is proposed for construction of a guidance image from the original image which approximates the original image as closely as possible. Based upon the analysis of local-region homogeneity, variance of pixel intensities could be used for the homogeneity metric [8]. Original images are divided into various regions as described in [31] and [32]. Three variances are calculated as:

ζ₁ = √[ (4/π -1) / N ] (8.31)

ζ₂ = √3·ζ₁ (8.32)

ζ₃ = √var(c_i) / M[ζ_i] (8.33)