synthetic image, which has sharp edges (e.g., a checkerboard), you might expect a $1/\omega$ falloff, as we saw in the case of a square wave. In general, we’ll plot signals in blue and their transforms in magenta, although on a few occasions we’ll plot several signals on one axis and their transforms on another axis, using the same color for each signal and its transform. We’ll plot discrete signals—ones whose domain is $\mathbb{Z}$—using stemplots.

# 18.13.2  The Transform of a Box Is a Sinc

Let

$$b(x)=\begin{cases}1 & -0.5\le x\le 0.5\\0 & \text{otherwise,}\end{cases}\tag{18.55}$$

be a box function defined on the real line. Because it’s an even function and it’s real-valued, its Fourier transform will be even and real-valued. We can evaluate $\mathcal{F}(b)(\omega)$ directly from the definition.

$$\mathcal{F}(b)(\omega)=\int_{-\infty}^{\infty} b(x)e_\omega(x)\,dx \tag{18.56}$$

$$=\int_{-1/2}^{1/2}e_\omega(x)\,dx \qquad\text{because }b(x)=0\text{ for }|x|>\frac12 \tag{18.57}$$

$$=\int_{-1/2}^{1/2}\cos(2\pi\omega x)\,dx-i\int_{-1/2}^{1/2}\sin(2\pi\omega x)\,dx \tag{18.58}$$

$$=\int_{-1/2}^{1/2}\cos(2\pi\omega x)\,dx \qquad\text{because sin is odd} \tag{18.59}$$

$$=\left.\frac{\sin(2\pi\omega x)}{2\pi\omega}\right|_{-1/2}^{1/2} \tag{18.60}$$

$$=\frac{\sin(\pi\omega)}{\pi\omega}. \tag{18.61}$$

The calculation above works for all $\omega\ne 0$; for $\omega=0$, we have $\mathcal{F}(b)(0)=1$, which you should verify by writing out the integral.

This computation is shown pictorially in Figure 18.39, which is adapted from Bracewell [Bra99], an excellent reference for those interested in practical signal processing.

**Inline Exercise 18.6:** Repeat the preceding computation to compute the Fourier transform of a box of width $a$, that is, a function that’s one on the interval $[-a/2,a/2]$ and zero elsewhere. Hint: Substitute $u=x/a$ in the integral to avoid doing any further work at all.

This is the only Fourier transform of a function on the real line that we’ll actually compute directly like this. The resultant function is so important that it gets its own name:

$$\operatorname{sinc}(x)=\begin{cases}\dfrac{\sin(\pi x)}{\pi x} & x\ne 0\\1 & x=0\end{cases}. \tag{18.62}$$