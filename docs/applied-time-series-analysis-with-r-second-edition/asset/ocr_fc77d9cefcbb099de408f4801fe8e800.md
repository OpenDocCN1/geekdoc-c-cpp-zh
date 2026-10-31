![](bbox=[0.35, 0.15, 0.6, 0.35])

![](bbox=[0.2, 0.38, 0.45, 0.65])

![](bbox=[0.55, 0.38, 0.8, 0.65])

# FIGURE 3.18

(a) Realization, (b) autocorrelations, and (c) spectral densities for the AR(4) model X_t -1.15 X_{t-1}+0.19 X_{t-2}+0.64 X_{t-3} -0.61 X_{t-4} = (1 -0.95 B)(1 - B +0.8 B^2)(1 +0.8 B) X_t = a_t, in Example 3.12.

NOTE: It is very important to realize that the behavior associated with roots closest to the unit circle tends to be dominant. In this example, the root 1.05 associated with the factor (1 - 0.95 B) is the closest to the unit circle while the root -1.25 associated with (1 + 0.8 B) is the furthest removed from the unit circle. We have already noted that the behavior associated with the factor 1 - 0.95 B is clearly evident in the realization and the autocorrelations while that associated with 1 + 0.8 B is not apparent. In the spectral density, we see peaks close to all three system frequencies, but the peak at f = 0 is much higher than is the peak at f = 0.5 and f = 0.16. We will explore the domination of roots close to the unit circle further in Example 3.14 and in Chapter 5.

# EXAMPLE 3.13: AN AR(4) MODEL WITH ALL ROOTS COMPLEX

We next consider the AR(4) model