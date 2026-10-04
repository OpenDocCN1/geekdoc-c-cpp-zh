# Vector-Valued (Multivariate) Time Series 433

+   a. Prediction: This is the case in which $s < t$. An example would be the one-step ahead forecasts $\hat{\mathbf{X}}_t^1,\hat{\mathbf{X}}_t^2,\dots$,
nb. Filtering: The case in which $s = t$.
nc. Smoothing: The case in which $s > t$. This case is called smoothing, since a time plot of $\hat{\mathbf{X}}_1,\hat{\mathbf{X}}_2,\dots,\mathbf{X}_t$ tends to be smoother than plots of the one-step ahead forecasts $\hat{\mathbf{X}}_t^0,\hat{\mathbf{X}}_t^2,\dots,\hat{\mathbf{X}}_t^{-1}$ or plots of the "filters" $\hat{\mathbf{X}}_t^1,\hat{\mathbf{X}}_t^2,\dots,\hat{\mathbf{X}}_t$.

# 10.6.4 Kalman Filter

The Kalman filter is a very useful iterative procedure for obtaining the estimates $\hat{\mathbf{X}}_t^i$ for the state-space model in Equations 10.48 and 10.49 with initial conditions $\hat{\mathbf{X}}_0=oldsymbol{\mu}$ and $\mathbf{\Gamma}_0=\mathbf{\Gamma}_0$. In the following, we give the Kalman filter recursions for computing predictions, filters, and smoothers of $\mathbf{X}_t$. In Appendix 10A, we give a proof of the prediction and filtering recursion.

# 10.6.4.1 Prediction (Forecasting)

The following equations provide one-step ahead predictions, $\hat{\mathbf{X}}_t^{-1}$ (or equivalently $\hat{\mathbf{X}}_{t+1}$); Specifically, we have observed $\mathbf{Y}_0,\dots,\mathbf{Y}_{t-1}$ and want to use this information to predict $\mathbf{X}_t$. The Kalman recursion is as follows:

```
$$\hat{\mathbf{X}}_t^{-1} = \mathbf{F}\hat{\mathbf{X}}_{t-1}^{-1}$
```

```
$$\mathbf{\Gamma}_t^{-1} = \mathbf{F}\mathbf{\Gamma}_{t-1}^{-1}\mathbf{F}' + \mathbf{\Gamma}_{\mathbf{v}}$
```

# 10.6.4.2 Filtering

The filtering and prediction recursions are run simultaneously. For example, note that the prediction in Equation 10.50 involves the filter term $\hat{\mathbf{X}}_t^{-1}$. The equations in the Kalman recursions for filtering, that is, for estimating $\mathbf{X}_t$ based on $\mathbf{Y}_0,\dots,\mathbf{Y}_t$, are given by

```
$$\hat{\mathbf{X}}_t = \hat{\mathbf{X}}_t^{-1} + \mathbf{K}_t(\mathbf{Y}_t - \mathbf{G}\hat{\mathbf{X}}_t^{-1})$
```

```
$$\mathbf{\Gamma}_t = [\mathbf{I} - \mathbf{K}_t\mathbf{G}]\mathbf{\Gamma}_{t-1}^{-1}$
```

where

```
$$\mathbf{K}_t = \mathbf{\Gamma}_t^{-1}\mathbf{G}'[\mathbf{G}\mathbf{\Gamma}_{t-1}^{-1}\mathbf{G}' + \mathbf{\Gamma}_{\mathbf{v}}]^{-1}$
```

$\mathbf{K}_t$ is called the Kalman gain.