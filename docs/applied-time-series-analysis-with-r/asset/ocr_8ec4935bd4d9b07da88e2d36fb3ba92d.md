80 Applied Time Series Analysis with R

2.4 Verify the frequency response functions given in the text for 2-point, 3-point, and 7-point moving averages. Find the frequency response function for a 5-point moving average. In each case, derive $|H(e^{-itm})|^2$. Plot the squared frequency response for the 5-point moving average using a program or language of your choice.

# Theoretical Problems

2.5 Suppose that for each $t$, the sequence $\{X_t^{(m)} : m=1,2,...\}$ of random variables converges to $X_t$, in mean square for each $t$ as $m 	o \infty$. Similarly, let $Y_t^{(m)}$ converge to $Y_t$, in mean square as $m 	o \infty$; $a_1X_t^{(m)} + b_1Y_t^{(m)} \to a_1X_t + b_1Y_t$ in mean square as $m 	o \infty$, where $a_1$ and $b_1$ are constants. You may assume that each of these random variables is in $L^2$, that is, that each random variable, $X$, is such that $E[|X|^2] < \infty$.

2.6 Let $\{X_t\}$ be a sequence of independent random variables with $E(X_t) = \sigma_t^2 < \infty$. Show that $\sum_{t=1}^\infty X_t = Y$ exists as a limit in the mean-square with $Y \in L^2$ and only if $\sum_{t=1}^\infty \sigma_t^2 < \infty$.

2.7 Let $X_t^{(k)}, k=1,2,...$ be a stationary linear process given by

![](bbox=[0.418, 0.503, 0.582, 0.566])

where $a_t$ is zero white noise and $\sum_{j=0}^\infty |h_j^{(k)}| < \infty, k=1,2,...,m$. Show that the process $X_t = \sum_{k=1}^\infty b_k X_t^{(k)}$ is stationary where the $b_k$ are finite constants.

2.8 Let $\{h_k\}$ and $\{b_k\}$ be sequences of real numbers and that $\sum_{k=0}^\infty |h_k| < \infty$ and $\sum_{k=0}^\infty |b_k| < \infty$. Furthermore, let $Z_t$, be a zero-mean stationary process with $M < \infty$ such that $E[|Z_t|^2] \le M$ for $t = \pm1, \pm2$, and define

![](bbox=[0.418, 0.726, 0.582, 0.824])

Show the following:

+   a. $E(X_t) = \lim_{m \to \infty} \sum_{k=0}^m h_k E(Z_{t-k})$

+   b. $E(X_t Y_t) = \lim_{m \to \infty} \sum_{k=0}^m \sum_{j=0}^m h_k b_j E(Z_{t-k} Z_{t-j})$.