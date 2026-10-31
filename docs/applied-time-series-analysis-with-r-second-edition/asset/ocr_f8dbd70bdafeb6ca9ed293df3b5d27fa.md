$X_t - 0.66 X_{t-1} + 0.02 X_{t-2} - 0.10 X_{t-3} - 0.24 X_{t-4} = a_t, \quad (5.3)$

where, for convenience, we use μ = 0 and σ_a^2 = 1 in the following discussion rather than the corresponding estimates from the temperature data. The factor table for the model in Equation 5.3 is given in Table 5.1. It is important to note that this model does not contain a deterministic component and thus accounts for the trending behavior via the correlation structure in the model. From the factor table, it is clear that the model is stationary since all the roots are greater than one in absolute value (i.e. all the |r_j^{-1}| values are less than one). Table 5.1 shows that the dominant feature of the model is a first-order factor associated with a positive real root quite close to the unit circle. As discussed previously, such a factor is related to aimless wandering behavior in realizations. The other factors contribute less pronounced higher frequency behavior, so we expect the wandering behavior associated with the positive real root to dominate realizations. In Figure 5.1, we show four realizations of length n = 150 from the AR(4) model in Equation 5.3. The wandering/random trending behavior is visible in all realizations as is the presence of more modest high frequency behavior. Figure 5.1a and c shows realizations that trend up and down, respectively, in a manner similar to that of the temperature series. Figure 5.1b and d shows random “trends” that change direction, twice in Figure 5.1b, and several times in Figure 5.1d. Figure 5.1a and c shows that the model in Equation 5.3 is capable of generating realizations that have the appearance of the temperature data, but Figure 5.1b and d shows that these “trends” may turn around abruptly.

# TABLE 5.1

Factor Table for the AR(4) Model in Equation 5.3

| AR Factors | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---|---|---|
| 1 – 0.99B | 1.01 | 0.99 | 0 |
| 1 – 0.2B + 0.455B² | 0.22 ± 1.47i | 0.67 | 0.23 |
| 1 + 0.53B | –1.88 | 0.53 | 0.5 |