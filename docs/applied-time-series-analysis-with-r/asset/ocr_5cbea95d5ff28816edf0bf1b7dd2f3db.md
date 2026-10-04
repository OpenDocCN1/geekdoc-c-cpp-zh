# # 13

# ## G-Stationary Processes

# ### 13.1 Generalized-Stationary Processes

In Chapter 12, we considered window-based methods for analyzing nonstationary processes with time-varying frequencies (TVF). These include short-term Fourier transforms (Gabor), along with Wigner-Ville and wave-representations. In this chapter, we introduce an altogether different approach for analyzing TVF data in which we extend the definition of stationarity to cover of generalized-stationary (or G-stationary) processes. This approach allows us to transform the time index of many nonparametric processes to an index set upon which they are stationary.

The presentation will be introductory in nature, and no effort will be made to cover this topic in detail. Our approach is to include sufficient information to give the reader a basic understanding of this methodology. Most of the developments in this area have only recently appeared in the literature, and these references are given here as a source of further details.

# #### Definition 13.1

Let $X(t): t \in S$ be a stochastic process defined on $S \subset \mathbb{R}$, let $u=g(t)$ be a mapping onto a set $R_u \subset \mathbb{R}$, and let $g^{-1}$ denote a specified inverse. $X(t)$ is a G-stationary process if

+   i. $E[X(t)] = \mu$.
ii. $Var[X(t)] = \sigma^2 < \infty$.
iii. $E[(X(t) - \mu)(X(g^{-1}(g(t)) + g(\tau))) - \mu)] = R_X(\tau)$.

The usefulness of this definition may not be immediately apparent. In order to better understand its implications, suppose $g$ is a transformation of the time axis and let $u=g(t)$ with $t=g^{-1}(u)$, so that $X(t)=X(g^{-1}(u))=Y(u)$. Letting $\xi=g(t)$, then