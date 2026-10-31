# 2

# *Linear Filters*

Many of the time series that we will study can be viewed as the output of a linear operator or filter. In this chapter, we introduce the basic concepts and terminology of linear filter theory. We also discuss the general linear process, which is a linear filter with white noise input that plays a fundamental role in the study of stationary processes. Finally, we discuss the application of linear filters for purposes of removing or retaining certain types of frequency behavior from a time series realization.

# 2.1 Introduction to Linear Filters

Consider the process \(\{X_t-\mu;\ t=0,\ \pm1,\ \pm2,\ \ldots\}\) given by

$$X_t-\mu=\sum_{j=-\infty}^{\infty}h_jZ_{t-j} \tag{2.1}$$

where

$h_j$ are constants  
$Z_t$ is a random variable with $E[Z_t]=0$ for each $t$

The process $X_t$ is referred to as the output of a linear filter, and $Z_t$ is the input. If $h_j=0$ for $j<0$, then this is called a *causal linear filter*, since $X_t$ only depends on present and past values of the input $Z_t$. In this book, we focus on causal filters, and, thus, although Theorems 2.1 and 2.2 and Definition 2.1, which follow, have noncausal analogs, we state them here only for causal filters. We will find it convenient to use the backshift operator $B$, defined by $B^kZ_t=Z_{t-k}$, to write (the causal version of) [Equation 2.1](#equation-2.1) as