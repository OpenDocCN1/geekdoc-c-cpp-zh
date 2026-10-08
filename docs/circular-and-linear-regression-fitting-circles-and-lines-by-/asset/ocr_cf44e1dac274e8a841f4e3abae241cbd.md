it has a bell-shaped density on the circumference, and its spread over the circle is controlled by a “concentration parameter” $\kappa \geq 0$, see [18, 16]. Its density on the circle (parameterized by an angular variable $\varphi \in [0, 2\pi)$) is

```
$$f(\varphi) = \frac{\exp[\kappa \cos(\varphi - \mu)]}{2\pi I_0(\kappa)}$$
```

where $\mu$ is the center of the distribution and $I_0(\kappa)$ is the modified Bessel function of order 0. When $\kappa = 0$, it turns to a uniform distribution on the entire circle; and when $\kappa$ grows the density peaks at $\varphi = \mu$.

![](bbox=[0.08, 0.25, 0.9, 0.49])

Simulated examples. Fig. 6.1 shows $n = 100$ points (crosses) generated on the unit circle with a von Mises distribution centered at $\mu = 0$ and having the concentration $\kappa = 1$. We see that the points mostly cluster near the right end (where $\varphi = 0$), but occasionally appear on the left side, too. Perhaps such distributions describe some practical applications, but not such a common situation where the observed points are evenly spread along an arc, with the rest of the circle (ellipse) totally invisible, see Fig. 6.2. In the last case, a uniform distribution on the arc seems much more appropriate, but every statistician knows how inconvenient uniform densities are in theoretical analysis.

Thus it appears that there is no probability distributions concentrated on a circle or an ellipse that would adequately represent the majority of practical applications and be acceptable in theoretical studies. For these reasons practitioners prefer to rely on the functional model almost exclusively. We will restrict our further studies to the functional model (except for the end of Section 6.3).

# ## 6.3 Maximum Likelihood Estimators (MLE)

MLE in the functional model. In the previous section we described two models, which are the most appropriate for the studies of fitting geometric curves