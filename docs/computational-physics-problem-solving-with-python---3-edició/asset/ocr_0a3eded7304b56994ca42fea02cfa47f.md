# 12

# Fourier Analysis: Signals and Filters

We start this chapter with a discussion of Fourier series and Fourier transforms, the standard tools for decomposing periodic and nonperiodic motions, respectively. We find that, as implemented for numerical computation, both the series and the transform become the same discrete Fourier transform (DFT) algorithm, which has a beautiful simplicity in its realization as a program. We then show how Fourier tools can be used to reduce noise in measured or simulated signals. We end the chapter with a discussion of the fast Fourier transform (FFT), a technique so efficient that it permits nearly instantaneous evaluations of DFTs on various devices.

# 12.1

# Fourier Analysis of Nonlinear Oscillations

Consider a particle oscillating either in the nonharmonic potential of (8.5):

```
$$V(x) = \frac{1}{p} k |x|^p \ , \quad p \neq 2 \tag{12.1}$$
```

or in the perturbed harmonic oscillator potential (8.2),

```
$$V(x) = \frac{1}{2} k x^2 \left(1 - \frac{2}{3} a x\right) \ . \tag{12.2}$$
```

While free oscillations in these potentials are always periodic, they are not sinusoidal. Your problem is to take the solution of one of these nonlinear oscillators and expand it in a Fourier basis:

```
$$x(t) = A_0 \sin(\omega t + \phi_0) \ . \tag{12.3}$$
```

For example, if your oscillator is sufficiently nonlinear to behave like the sawtooth function (Figure 12.1a), then the Fourier spectrum you obtain should be similar to that shown in Figure 12.1b.

In general, when we undertake such a spectral analysis we want to analyze the steady-state behavior of a system. This means that we have waited for the initial