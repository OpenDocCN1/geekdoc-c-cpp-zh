behaviors: exponential or sinusoidal decay. This permits to determine if a series is stationary or not.

The most general model is the model ARIMA (p, d, q) (AutoRegressive Integrated Moving Average processes) that includes not stationary series for which apply differences of order d to stationarize it:

$$\phi_p(B)\nabla^d z_t = \delta + \theta_q(B)a_t$$

Where φ_p(B), θ_q(B) and B are operators that satisfy the following relations:

$$\phi_p(B)z_t = (1 - \phi_1 B - \phi_2 B^2 - \cdots - \phi_p B^p)z_t = z_t - \phi_1 z_{t-1} - \cdots - \phi_p z_{t-p}$$

and

$$\theta_q(B)a_t = (1 - \theta_1 B - \theta_2 B^2 - \cdots - \theta_q B^q)a_t = a_t - \theta_1 a_{t-1} - \cdots - \theta_q a_{t-q}$$

$$B^k z_t = z_{t-k}$$

$$\nabla^d z_t = (1 - B)^d z_t$$

Similarly, there is a general model that considers the presence of stationarity or cyclic movement of short term of longitude s modeled by the expression:

$$\phi_p(B^s)\phi_p(B)\nabla^d z_t = \delta + \theta_Q(B^s)\theta_q(B)a_t$$

Where φ_p(B^s) y θ_Q(B^s) are polynomial operators similar to the above mention, but its powers are multiples of s, {a_t} are residuals in the moment t and θ_i are its components in the part of moving averages.

BJ methodology satisfies the following stages:

+   - (a). Identification of a possible model among the ARIMA type models. To accomplish this first is necessary to determine if the series is stationary or not. When an observed series is not stationary the difference operator is applied:
+   
+   $$\nabla z_t = z_t - z_{t-1}$$
+   
+     as many times as it will be necessary up to stationarity. To avoid overdifferentiation it is calculated the variances of the new obtained series choosing the one with the smallest value.
+   
+     When a series is stationary in its mean, but its variance is increasing or decreasing according to BJ methodology it should be applied a transformation (generally logarithmic) for the stability of the variance. It is important to notice that this is not necessary in our proposal.
+   
+     Given a stationary series the behavior pattern of the autocorrelation function and the partial autocorrelation indicate the possible number of parameters i and j that the model should have.
+   
+     Besides the presence of stationarity in a temporal series there is other property that is required in the ARIMA models denominated invertibility, which permits to represent the series as an autoregressive model of infinite extension that satisfy the condition: