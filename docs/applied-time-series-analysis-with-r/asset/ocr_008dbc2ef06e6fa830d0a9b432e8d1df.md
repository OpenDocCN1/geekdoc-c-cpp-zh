# Applied Time Series Analysis with R

of AR(2) models in Chapter 3. However, in Figure 8A.3c it is clear that the associated model is AR(3) since the true partial autocorrelation at k=3 is nonzero while for k>3 are zero. The sample partial auto-correlations in Figure 8A.3d clearly show the AR(3) behavior, and the model identification of the process is an AR(3).

# 8A.3 Box–Jenkins Procedure for ARMA Model Identification

The classical Box-Jenkins procedure (see Box et al., 2008) for identifying the patterns p and q of an ARMA(p,q) process identifies patterns exhibited by autocorrelations and partial autocorrelations. While these functions provide perfect identification for MA(q) and AR(p) models when true quantities are known, the identification of ARMA(p,q) processes is more problematic. The Box-Jenkins identification patterns are shown in Table 8A.1, and their use recognizing behavior exhibited by solutions to difference equations. For example, the autocorrelations, $ho_k$, of an ARMA(p,q) process satisfy a linear difference equation with constant coefficients for k>q. The Box-Jenkins procedure is based on the fact that the functional form of the solution is satisfied by $ho_k$ for k>q-p. Unfortunately these types of patterns do not provide perfect identification even when true quantities are known, and model identification is even more difficult when only the sample autocorrelations and sample partial autocorrelations are available.

# EXAMPLE 8A.4: BOX-JENKINS MODEL IDENTIFICATION FOR ARMA(1,2) AND ARMA(4,3) MODELS

+   1. In Figure 8A.4a–d, we see true autocorrelations, sample autocorrelations, and sample partial autocorrelations, for the ARMA(1,2) model

# TABLE 8A.1

Patterns Used for Box-Jenkins Model Identification

AR(p)
$\phi_k = 0, k > p$ ($\phi_p 
eq 0$)
$ho_k$ is damped exponential ($p = 1$)

MA(q)
$ho_k = 0, k > q$ ($ho_q 
eq 0$)
$\phi_k$ is dominated by damped sinusoidal and/or exponential ($q > 1$)

ARMA(p,q)
$ho_k$ is a damped exponential or sinusoid after first $p - q$ lags
$\phi_k$ is dominated by damped exponential or sinusoid after first $p - q$ lags