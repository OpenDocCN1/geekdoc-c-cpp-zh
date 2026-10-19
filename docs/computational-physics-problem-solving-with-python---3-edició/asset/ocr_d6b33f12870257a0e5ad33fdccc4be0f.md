# 13.5

**The Wavelet Transform**

The wavelet transform of a time signal $y(t)$ is defined as

$$Y(s,\tau)=\int_{-\infty}^{+\infty}dt\,\psi^*_{s,\tau}(t)y(t)\quad\text{(wavelet transform)},$$  (13.14)

and is similar in concept and notation to a short-time Fourier transform. The difference is rather than using $\exp(i\omega t)$ as the basis functions, here we are using wave packets or wavelets $\psi_{s,\tau}(t)$ localized in time, such as the those shown in Figure 13.2. Because each wavelet is localized in time, each acts as its own window function. Because each wavelet is oscillatory, each contains its own small range of frequencies.

Equation 13.14 says that the wavelet transform $Y(s,\tau)$ is a measure of the amount of basis function $\psi_{s,\tau}(t)$ present in the signal $y(t)$. The $\tau$ variable indicates the time portion of the signal being decomposed, while the $s$ variable is equivalent to the frequency present during that time:

$$\omega=\frac{2\pi}{s},\qquad s=\frac{2\pi}{\omega}\quad\text{(scale-frequency relation)}.$$  (13.15)

Because it is key to much that follows, it is a good idea to think about (13.15) for a while. If we are interested in the time *details* of a signal, then this is another way of saying that we are interested in what is happening at small values of the *scale* $s$. Equation 13.15 indicates that small values of $s$ correspond to high-frequency components of the signal. That being the case, the time details of the signal are in the high-frequency, or low-scale, components.

# 13.5.1

**Generating Wavelet Basis Functions**

The conceptual discussion of wavelets is over, and it is time to get down to work. We first need a technique for generating wavelet basis functions, and then we need to discretize this technique. As is often the case, the final formulation will turn out to be simple and short, but it will be a while before we get there.

Just as the expansion of an arbitrary function in a complete set of orthogonal functions is not restricted to any particular set, so too is the wavelet transform not restricted to any particular wavelet basis, although some might be better than others for a given signal. The standard way to generate a family of wavelet basis functions starts with $\Psi(t)$, a *mother* or *analyzing* function of the real variable $t$, and then to use this to generate *daughter* wavelets. As a case in point, we start with the mother wavelet

$$\Psi(t)=\sin(8t)e^{-t^2/2}.$$  (13.16)