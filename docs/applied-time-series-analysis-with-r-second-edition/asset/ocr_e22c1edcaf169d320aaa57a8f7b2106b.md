homogeneous difference equation with constant coefficients for k > q. The Box–Jenkins procedure is based on the fact that the functional form of the solution is satisfied by ρ_k for k > q − p. Unfortunately these types of patterns do not provide perfect identification even when true quantities are known, and model identification is even more difficult when only the sample autocorrelations and sample partial autocorrelations are available.

# EXAMPLE 8A.4: BOX–JENKINS MODEL IDENTIFICATION FOR ARMA(1,2) AND ARMA(4,3) MODELS

+   1. In Figure 8A.4a–d, we show true autocorrelations, sample autocorrelations, true partial autocorrelations, and sample partial autocorrelations for the ARMA(1,2) model

# TABLE 8A.1

# Patterns Used for Box–Jenkins Model Identification

AR(p)
φ_kk = 0,  k > p (φ_pp = φ_p ≠ 0)
ρ_k is a damped { exponential (p = 1) 
 sinusoid and / or exponential (p > 1) }
MA(q)
ρ_k = 0,  k > q (ρ_q ≠ 0)
φ_kk is a dominated by damped { exponential (q = 1) 
 sinusoid and / or exponential (q > 1) }
ARMA(q,p)
ρ_k is a damped exponential or sinusoid after first q−p
φ_kk is dominated by damped exponential or sinusoid after first p−q