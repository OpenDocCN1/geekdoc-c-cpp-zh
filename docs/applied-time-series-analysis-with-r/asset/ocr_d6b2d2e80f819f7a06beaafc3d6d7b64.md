# ARMA Time Series Models

AR(1) components obtained using the state-space approach to be discussed in Section 10.6.7.
We note the following:

+   - The ARMA(2,1) component in Figure 3.26b contains the pseudocyclic portion of the realization associated with the complex conjugate root in the first row of the factor table in Table 3.1.
- The wandering behavior root listed on the second row of the factor table in Table 3.1 is captured by the AR(1) component shown in Figure 3.26c.

These types of decompositions are an instructive aide for visualizing the underlying structure of AR(p) models as well as understanding the associated phenomena.

# EXAMPLE 3.21: ADDITIVE COMPONENTS OF THE SUNSPOT DATA

We previously examined the sunspot data shown in Figure 1.23 (≈08 to today) and noted the pseudo-cyclic behavior with cycles of 9–11 years. Also, there tends to be a hint of a pattern in the peaks of the cycles. That is, the peaks tended to be high in the 1700s, again and more recently since 1940. In Figure 3.27a we replot the sunspot data, and in which we show the first additive components of an AR(9) model fit to the sunspot data. In Chapters 8 and 9 we will discuss the topic of finding an appropriate model for a set of data. The factor table, not shown here, of the AR(9) model fit not surprisingly shows the wandering behavior to be associated with a system frequency of $f=0.95$ and this is illustrated by the first component. The second component is a wandering behavior (associated with a factor of 1–0.95) and further examination of the wandering behavior shows that it seems to track the heights of the peaks through time. The third component, in Figure 3.27d, shows some high frequency behavior associated with system frequency $f=0.19$ is barely visible in the original plot.

Using R: Decompositions of AR realizations into additive components can be achieved using the twage function factor.comp.wge. This function prints the factor table associated with the AR model fit to a time series realization using Burg estimates (Chapter 7). The function calculates ncomp (nfactors) additive components where nfactors is the number of factors in the factor table for the fitted model. See Appendix 10A for more details.

# Seasonal ARMA($p,q$), $(P_sQ_s)_s$ Models

Several modifications of the ARMA($p,q$) model have been found to be useful. In Chapter 5, we will discuss ARMA-type models that are nonstationary