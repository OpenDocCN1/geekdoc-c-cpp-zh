$$\alpha_1 = \frac{a - bi}{a^2 + b^2}$$ $$\alpha_2 = \frac{a + bi}{a^2 + b^2},$$

where $b \neq 0$. Now letting $R = \sqrt{a^2 + b^2}$, then $\alpha_1 = R^{-1} e^{-i\theta}$ and $\alpha_2 = R^{-1} e^{i\theta}$, where $\theta = \text{arc tan}(b / a)$. Then,

$$\alpha_2 - \alpha_1 = 2R^{-1}\left[\frac{e^{i\theta} - e^{-i\theta}}{2}\right] = 2iR^{-1} \sin \theta,$$

and

$$\psi_k(2) = R^{-k-1}\left[\frac{e^{i\theta(k+1)} - e^{-i\theta(k+1)}}{2iR^{-1} \sin \theta}\right] = R^{-k}\frac{\sin \theta(k + 1)}{\sin \theta}.$$

Therefore,

$$X_t = \sum_{k=0}^{\infty} R^{-k} \frac{\sin \theta(k + 1)}{\sin \theta} a_{t-k}. \tag{3.67}$$

# **EXAMPLE 3.6: AR(2) MODELS**

+   1. *Characteristic equation has two positive real roots:* In Figures 3.4a and 3.5a, the autocorrelations and a realization from the process

$$\left(1 - 0.95B\right)X_t = a_t, \tag{3.68}$$

were given. In considering the AR(2) process, it is interesting to examine the effect of introducing an additional first-order factor to the model in Equation 3.68. Figure 3.9 shows autocorrelations for the models