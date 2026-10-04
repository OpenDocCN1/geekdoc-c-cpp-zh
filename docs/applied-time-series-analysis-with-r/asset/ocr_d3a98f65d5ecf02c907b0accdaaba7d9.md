the data less than or equal to the cutoff frequency $f_c = 0.2$ and removes fre-
encies greater than $f_c = 0.2$. The result in Equation 2.3 says that ideally, wendesign our filter, so that

```
$|H(e^{-2\pi f})|^2=1, \quad f \leq 0.2\n= 0, \quad f > 0.2, \qquad (2.10)$
```

since according to Theorem 2.2, this would eliminate frequency behavior
from the spectrum of the output for $f > 0.2$ and leave it unchanged for $f \leq 0.2$.
Figure 2.1a shows the squared frequency response for this ideal (brickwall)
filter, and Figure 2.1b shows the ideal squared frequency response for a
band-pass filter that passes frequencies $0.1 \leq f \leq 0.2$.

# **EXAMPLE 2.1: FIRST DIFFERENCE FILTER**

Consider a time series realization $x_t, t=1, \dots, n$, and suppose we compute
the first difference $y_t = x_t - x_{t-1}$. In order to see the effect of this differencing
operation, we note that the first difference is a linear filter of the form
Equation 2.1 where $h_1=1, h_j=0, j \neq 0$ or 1. We can thus
H$H(e^{-2\pi f})-1$ is given by $2-\cos(2\pi f)$ and $|H(e^{-2\pi f})|^2=2(1-\cos(2\pi f))$.
The plot of $|H(e^{-2\pi f})|^2$ is given in Figure 2.2b where it can be seen that
a difference is a high-pass filter, but that it is not a sharp filter in that we
show the realization previously shown in Figure 1.3a, which shows a
wandering behavior associated with low-frequency behavior, along with
some higher frequency oscillation. The first difference data are shown
in Figure 2.2c where it can be seen that the low-frequency wandering
behavior has been removed with only the higher frequency behavior
remaining. The first difference is widely used in time series analysis, but
if the goal is to remove a specific range of low frequencies from the data,
there are better approaches.

![](bbox=[0.185, 0.725, 0.8, 0.882])

**FIGURE 2.1**
Squared frequency response function, $|H(e^{-2\pi f})|^2$, for ideal (a) low-pass and (band-pass) filters.