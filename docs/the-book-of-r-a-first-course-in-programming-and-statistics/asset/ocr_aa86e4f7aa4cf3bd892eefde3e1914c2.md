outcome" that you can expect many realizations. This is expressed mathematically as follows:

$$\mu_W = \mathbb{E}[W] = \int_{-\infty}^{\infty} wf(w) dw$ (15.7)$

This equation represents the continuous analogue of Equation (15.3) and can be read as "the total area underneath the function given by multiplication of $f(w)$ with the value of w itself.\nFor W, the variance $\sigma_W^2$, also written as $Var[W]$, quantifies the variability inherent in calculations of W. Calculation of the continuous random variable depends on its mean $\mu_W$ and is given as follows:

$$\mu_W = Var[W] = \int_{-\infty}^{\infty} (w - \mu_W)^2 f(w) dw$ (15.8)$

Again, the procedure is to find the area under the density function multiplied—in this case, the squared difference of w with the expected value $\mu_W$.\nEvaluation of the mean and variance of the picnic temperature variable must follow (15.7) and (15.8), respectively. These calculations become rather complex, so I won't reproduce them here. However, Figure 15-2 shows that the mean of w must be $\mu_W = 65$; it is the perfect center of the symmetric density function $f(w)$.

In terms of the required integrals, you can therefore use the previously stored w and $fw$ objects to view the two functions, $wf(w)$ and $(w-\mu_W)^2 f(w)$, by executing the following, which produces two images in Figure 15-4:

```
plot(w,w*fw,type="1",lab="wf(w)")\nplot(w,(w-65)^2*fw,type="1",lab="(w-65)^2 f(w)")
```

![](bbox=[0.238, 0.606, 0.88, 0.831])

Figure 15-4: Integrands for the expected value (left) and variance (right) of the probability density function for the temperature example