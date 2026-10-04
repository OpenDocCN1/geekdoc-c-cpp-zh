
# Wavelets

# EXERCISES

12.1 This problem involves analysis of the following time series data sets:

+   a. lynx (recall that we typically analyze the logarithm of this series). See Example 5.2
b. hadley (global temperature data)
c. prob12.1c (simulated data)
ni. Plot the data
ii. Plot the periodogram
iii. Plot the Parzen window spectral estimator with the default lag window
iv. Plot the AR spectral estimator
v. Plot the Gabor (use cgt in Rwave) and Wigner–Ville spectra
In each case, discuss the information in the plots with regard to whether or not there is an indication of stationarity, TVFs, etc. If the process appears to be stationary, describe the frequency behavior. If the process has TVFs, discuss the resulting effect on the plots.

12.2 Consider the following wavelet:

$\psi(x)=x, \quad -1\leq x\leq1$
$$=0, \quad \text{elsewhere}$$

Find and plot the following dilations and translations, $\psi_{j,k}(x)$:

+   a. $j=2, k=0$
b. $j=2, k=3$
c. $j=-1, k=3$
d. $j=-2, k=3$

12.3 This problem involves the analysis of the following three data sets:

+   1. prob12.3a
2. prob12.3b
3. prob12.1c

For these data sets:
a. Plot the following related to the DWT:
ni. MRA
iii. Time scale plot (scalogram)
For each of these plots, discuss the information that the plot conveys.

12.4 Consider the three data sets in Problem 12.3. For each of these data sets plot the Wigner–Ville spectrum and compare it with the three

wavelet-based plots produced in Problem 12.3b. Compare the plots with regard to the time–frequency spectral information.

12.5 Using Equation 12.24 and the matrix **M** given in Equation 12.26, show that

+   a. $x_1 = -\frac{1}{\sqrt{2}}d_{1,1} - \frac{1}{2}d_{2,1} - \frac{1}{\sqrt{8}}d_{3,1} + \frac{1}{\sqrt{8}}s_{3,1}$.
b. Find a similar expression for $x_2$.

12.6 Analyze the following data sets using wavelet analysis and the Wigner–Ville plot. Describe any TVF behavior, abrupt changes, etc. that are identified by these analyses.

+   a. bat (echolocation signal of a big brown bat)
b. doppler (a Doppler signal)
c. prob12.6c (simulated data set)

# 13

## G-Stationary Processes

### 13.1 Generalized-Stationary Processes

In Chapter 12, we considered window-based methods for analyzing nonstationary processes with time-varying frequencies (TVF). These include short-term Fourier transforms (Gabor), along with Wigner-Ville and wave-representations. In this chapter, we introduce an altogether different approach for analyzing TVF data in which we extend the definition of stationarity to cover of generalized-stationary (or G-stationary) processes. This approach allows us to transform the time index of many nonparametric processes to an index set upon which they are stationary.

The presentation will be introductory in nature, and no effort will be made to cover this topic in detail. Our approach is to include sufficient information to give the reader a basic understanding of this methodology. Most of the developments in this area have only recently appeared in the literature, and these references are given here as a source of further details.

#### Definition 13.1

Let $X(t): t \in S$ be a stochastic process defined on $S \subset \mathbb{R}$, let $u=g(t)$ be a mapping onto a set $R_u \subset \mathbb{R}$, and let $g^{-1}$ denote a specified inverse. $X(t)$ is a G-stationary process if

+   i. $E[X(t)] = \mu$.
ii. $Var[X(t)] = \sigma^2 < \infty$.
iii. $E[(X(t) - \mu)(X(g^{-1}(g(t)) + g(\tau))) - \mu)] = R_X(\tau)$.

The usefulness of this definition may not be immediately apparent. In order to better understand its implications, suppose $g$ is a transformation of the time axis and let $u=g(t)$ with $t=g^{-1}(u)$, so that $X(t)=X(g^{-1}(u))=Y(u)$. Letting $\xi=g(t)$, then

$X(g^{-1}(g(t) + g(\tau))) = Y(g(t) + g(\tau)) = Y(u + \xi). \quad (13.2)$

From Equations 13.1 and 13.2, it follows that

$R_X(\tau) = E[(X(t) - \mu)(X(g^{-1}(g(t) + g(\tau))) - \mu)]$
$= E[(Y(u) - \mu)(Y(u + \xi) - \mu)]. \quad (13.3)$

Consequently, Definition 13 gives the conditions on $X(t)$ and $g(t)$ for the dual process $Y(u)$, to be stationary in the usual sense (of Definition 1.5). That is, although $X(t)$ may not be stationary on the original index set $(t)$, it can be mapped onto a new index set on which is stationary. We will refer to this process as the dual of $X(t)$. We use the notation $C_Y(\tau) = E[(Y(u) - \mu)(Y(u + \tau) - \mu)]$ to denote the autocovariance of $Y(u)$, and $R_X(\tau)$ is called the $G$-stationary autocovariance. Clearly, $C_Y(\tau) = R_X(\tau)$.

Note that stationarity is a special case of $G$-stationarity since a process is stationary if and only the dual process based on linear time transformation $u=g(t)=a+b$ is stationary. Again, although in general, a $G$-stationary process is not stationary, the corresponding dual process is. The basic idea is that in order to analyze a $G$-stationary process you should use the time transformation, $u=g(t)$, for which the dual process, $Y(u)$, is stationary. The dual process, $Y(u)$, can then be analyzed using the techniques discussed in the first 11 chapters.

### 13.1.1 General Strategy for Analyzing G-Stationary Processes

The following is an outline of the general procedure we will use for analyzing $G$-stationary processes.

+   1. Transform the axis to obtain a stationary dual realization
2. Analyze the transformed (dual) realization using methods for stationary time series. For example
   a. Fit an $AR(p)$ or an $ARMA(p,q)$ model to the dual data using model identification techniques discussed in Chapter 8 and estimation methods covered in Chapter 7
   b. Compute forecasts, spectral estimates, etc., as desired, for the problem at hand
3. Transform back to original timescale

In the next few sections, we will discuss the multiplicative (M)-stationary, $G(\lambda)$-stationary, and linear chirp processes that are special cases of $G$-stationary processes. In Section 13.3, we will give further discussion of the aforementioned procedure for the case of $G(\lambda)$-stationary processes.

# G-Stationary Processes

### 13.2 M-Stationary Processes

The first type of G-stationary processes we will discuss is the M-stationary process, which is based on a logarithmic time transformation.

#### 13.2.1 Continuous M-Stationary Process

Continuous M-stationary processes were first introduced and studied by Gray and Zhang (1988). The M-stationary process is defined in Definition 13.2.

# Definition 13.2

X(t) is a continuous M-stationary process for $t \in (0,\infty)$ if for any $t \in (0,\infty)$ and $t\tau \in (0,\infty)$

+   1. $E[X(t)] = \mu$
2. $Var[X(t)] = \sigma^2 < \infty$
3. $E[(X(t) - \mu)(X(t\tau) - \mu)] = R_x(\tau)$

Where $R_x(\tau)$ is referred to as the M-covariance of $X(t)$.

Now let $g(t) = u = \ln t / \ln h$. In this, $g^{-1}(u) = h^u$, and

$g^{-1}(g(t) + g(\tau)) = g^{-1}\left(\frac{\ln t + \ln \tau}{\ln h}\right)$
$= h^{\ln t/\ln h}h^{\ln \tau/\ln h} = t\tau.$

Let $\xi = g(\tau) = \ln \tau/ln h$, then $R_x(\tau)$ is defined in part (3) of Definition 13.1 becomes

$R_x(\tau) = E[(X(t) - \mu)(X(g^{-1}(g(t) + g(\tau)))) - \mu)]$
$= E[(X(t) - \mu)(X(t\tau) - \mu)]$
$= E[[Y(u) - \mu)(Y(u + \xi) - \mu)]$
$= C_y(u).$

From Equation 13.3. Thus, a G-stationary process with $u = g(t) = \ln t / \ln h$ is M-stationary. For the development and application of continuous M-stationary processes, see Gray and Zhang (1988).

Remark: We have taken $u = \ln t / \ln h$ for convenience. We could let $u = C \ln t$ where C is any real constant.

# EXAMPLE 13.1: AN M-STATIONARY COSINE PROCESS

A simple example of an M-stationary process is the cosine with argument ln(t) and random phase shift given by

$$X(t) = A \cos(2\pi\beta \ln(t) + \psi). \quad (13.4)$$

where $t \in (0, \infty)$, and $\psi \sim \text{Uniform}(0, 2\pi)$. In Figure 13.1a, we show a typical realization from Equation 13.4 with the circled values illustrating the evaluation of the curve at equally spaced points. Figure 13.1b shows the same curve evaluated at the points $t_i = ch^k$ for $c > 0$, and then Figure 13.1c displays the dual realization where the circled points represent the circled values indexed on $k$. Note that the curves shown in Figure 13.1b go through about three cycles. The effect of evaluating the curve in Figure 13.1a at equally spaced points is to oversample the first (longest) cycle and take very few samples in the last (shortest) cycle. Evaluating the curve at $ch^k$ (Figure 13.1b) has the effect of sampling more rapidly for shorter cycles and slower for longer cycles, resulting in an equal number of observations in each of

![](img/41dcbfb9af56fa48895afde322197b0b_566_0.png)

**Figure 13.1**
M-stationary cosine process in Equation 13.4 with $\psi = 0$. (a) Showing 50 equally spaced points, (b) showing the values of the process at $ch^k$, and in (c) the circled values in (b) are plotted against the index $k$.
