# 528 Applied Time Series Analysis with R

![](bbox=[0.128, 0.126, 0.857, 0.442])

**FIGURE 12.14**
(a) DWT and (b) the time-scale plot for 256 point linear chirps signal.

is hardly visible in the time-scale plot. The problem relates back to the poor localization associated with higher levels of 1/scale (frequency). A schematic diagram of the DWT calculated using the pyramid algorithm is shown in Figure 12.15. The pyramid algorithm begins by down-sampling the data to obtain two sets containing $n/2$ coefficients each. As mentioned previously, $s_{1,k}$ and $d_{1,k}$ coefficients are the results of applying a low pass

| $s_0 (=data)$ | |
| $s_{1,k}$ (low freq) | $d_{1,k}$ (high freq) |
| $s_{2,k}$ (low freq) | $d_{2,k}$ (high freq) |
| $s_{3,k}$ (lf) | $d_{3,k}$ (hf) |
| $s_{4,k}$ | $d_{4,k}$ |

**FIGURE 12.15**
Diagram of the pyramid algorithm for $J = 4$.