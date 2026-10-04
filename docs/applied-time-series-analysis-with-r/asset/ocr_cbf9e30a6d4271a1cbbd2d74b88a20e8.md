# Definition 13.8

If the data are sampled from a continuous G($\lambda$)-stationary process, X(t), at $t_k$ defined in Equation 13.18, then $f_n^G(\Delta;\lambda)=1/(2\Delta)$ is called the G($\lambda$)-Nyquist frequency.

NOTE: When $\lambda=1$, the G($\lambda$)-Nyquist frequency is the usual Nyquist frequency. When $\lambda=0$, the G($\lambda$)-stationary frequency is $f_0(\Delta;0)=1/(2\Delta)=1/(2\ln h)$. This follows from the fact that in the transformed time,

```
$u_k - u_{k-1} = \ln h^k - \ln h^{k-1}\n=\ln \left(\frac{h^k}{h^{k-1}}\right)\n=\ln h.$
```

# 13.3.2.1 Equally Spaced Sampling from G(p; $\lambda$) Processes

As noted in the case of M-stationary processes, the desirable points at which to sample a G($\lambda$)-stationary process (the $t_k$'s given in Equation 13.18) are equally spaced (unless $\lambda=1$), which can cause difficulties since data taken at equally spaced points. Just as in the case of Euler processes or M-stationary processes, in this general, difficulty can be overcome by over-sampling or interpolation. When data are only available at equally spaced points and are not sufficiently over-sampled, interpolation can be used to obtain values at the $t_k$ in Equation 13.18 required for G($\lambda$) processes. Wang et al. (2009) give a Kalman filtering-based approach to avoid the need for interpolation. Haney (2011) discusses a Fourier interpolation technique that can be preferable to linear interpolation for data having cyclic behavior. However, in the applications considered here, linear interpolation will be satisfactory.

Using R: The tswge function gen.glambda.w can be used to generate a realization from a specified G($\lambda; p$) process. Note that a realization from an M-stationary process can be generated using gen.glambda.w with lambda=0.

# EXAMPLE 13.6: G(2; $\lambda$) MODELS FOR A VARIETY OF VALUES

Figure 13.6 shows several realizations from G(2; $\lambda$) models associated with the dual process

```
$(1-1.9B+0.99B^2)Y_k = a_k,$
```

with offset 25, n=500, and a different set of $\lambda$ values than those used in Figure 13.5 to further emphasize that the direction of frequency changes occurs at $\lambda=1$.