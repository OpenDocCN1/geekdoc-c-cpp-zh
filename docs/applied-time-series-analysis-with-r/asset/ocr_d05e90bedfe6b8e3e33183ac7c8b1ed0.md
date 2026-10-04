# Applied Time Series Analysis with R

$X(g^{-1}(g(t) + g(	au))) = Y(g(t) + g(	au)) = Y(u + \xi). \quad (13.2)$

From Equations 13.1 and 13.2, it follows that

```
$R_X(\tau) = E[(X(t) - \mu)(X(g^{-1}(g(t) + g(\tau))) - \mu)]\n= E[(Y(u) - \mu)(Y(u + \xi) - \mu)]. \quad (13.3)$
```

Consequently, Definition 13 gives the conditions on $X(t)$ and $g(t)$ for the dual process $Y(u)$, to be stationary in the usual sense (of Definition 1.5). That is, although $X(t)$ may not be stationary on the original index set $(t)$, it can be mapped onto a new index set on which is stationary. We will refer to this process as the dual of $X(t)$. We use the notation $C_Y(\tau) = E[(Y(u) - \mu)(Y(u + \tau) - \mu)]$ to denote the autocovariance of $Y(u)$, and $R_X(\tau)$ is called the $G$-stationary autocovariance. Clearly, $C_Y(\tau) = R_X(\tau)$.

Note that stationarity is a special case of $G$-stationarity since a process is stationary if and only the dual process based on linear time transformation $u=g(t)=a+b$ is stationary. Again, although in general, a $G$-stationary process is not stationary, the corresponding dual process is. The basic idea is that in order to analyze a $G$-stationary process you should use the time transformation, $u=g(t)$, for which the dual process, $Y(u)$, is stationary. The dual process, $Y(u)$, can then be analyzed using the techniques discussed in the first 11 chapters.

# 13.1.1 General Strategy for Analyzing G-Stationary Processes

The following is an outline of the general procedure we will use for analyzing $G$-stationary processes.

+   1. Transform the axis to obtain a stationary dual realization
2. Analyze the transformed (dual) realization using methods for stationary time series. For example
   a. Fit an $AR(p)$ or an $ARMA(p,q)$ model to the dual data using model identification techniques discussed in Chapter 8 and estimation methods covered in Chapter 7
   b. Compute forecasts, spectral estimates, etc., as desired, for the problem at hand
3. Transform back to original timescale

In the next few sections, we will discuss the multiplicative (M)-stationary, $G(\lambda)$-stationary, and linear chirp processes that are special cases of $G$-stationary processes. In Section 13.3, we will give further discussion of the aforementioned procedure for the case of $G(\lambda)$-stationary processes.