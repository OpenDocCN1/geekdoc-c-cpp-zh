# Applied Time Series Analysis with R

of generating realizations that have the appearance of the temperature data, by Figure 5.1b and d shows that these “trends” may turn around abruptly.

The point of this example is to illustrate the fact that trending behavior can be produced by the autocorrelation alone, and as a consequence, the problem of testing for the existence of a real or deterministic trend in the form of Equation 5.2 is quite difficult, for example, Woodward and Gray (1993, 1995) and Woodward et al. (1997). We return to this problem in Chapter 9. Another important point is that forecasts (to be studied in Chapter 6) from the model predicting the increasing trend to continue because subsequent observations are just as likely to going down as they are going up as Figure 5.1b and d. However, forecasts using the model in Equation 5.2 with nonzero b will forecast an existing trend to continue. We will refer to trends produced by models of type in Equation 5.2 as deterministic trends while those produced by stationary models, such as Equation 5.3, will be called random trends.

# 5.1.2 Harmonic Component Models

In this section, we consider the case where s is a function of the form s= C (2πft + U). In Chapters 1 and 4, we have discussed models with harmonic components and studied them as a type of stationary process. The stationarity requires that the phase, U, is a random variable. However, in physical situations in which one realization is available, the phase is constant throughout the only realization observed. For this reason, it is often the case that signal-plus-noise models with harmonic components, the harmonic component, such as s= C (2πft + U) is considered to be a deterministic signal in the case of the trend-plus-noise examples.

Consider the case of the signal-plus-noise model with one harmonic component

```
X_i = C cos(2πft + U) + Z_i,
```

which is written as

```
X_i = A cos(2πft) + B sin(2πft) + Z_i,
```

where A=C cos U and B=-C sin U using trigonometric identities. In practice, if X satisfies Equation 5.5, then it is analyzed as if it a nonstationary process, in which the parameters A, B, and f fare often estimated as a first step, and then the process

```
Z_i = X_i - A cos(2πft) - B sin(2πft),
```