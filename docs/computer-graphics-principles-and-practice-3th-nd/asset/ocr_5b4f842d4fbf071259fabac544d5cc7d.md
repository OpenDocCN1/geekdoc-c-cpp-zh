$x=0$, and the supposed Fourier transform is not in $L^2$, because the integral of its square is not finite. Nonetheless, with some care one can work with the delta function by constantly remembering that the ordinary rules don’t actually apply to it, and it’s really a proxy for a limiting process.

🔶 The only way in which we’ll ever want to use the $\delta$ function, or the comb function defined in the next section, is inside a mapping like

$f\mapsto\int_{\mathbb{R}}\delta(x)f(x)\,dx,$ (18.65)

that is, to define a real-valued function on $L^2$, which is a covector for $L^2$. If we replace $\delta(x)$ in Equation 18.65 with $g(x,a)$, and take a limit as $a\to0$, the resultant sequence of covectors actually does converge, although this requires proof. Thus, the $\delta$ function, at least inside an integral, makes some sense.

![](bbox=[0.707, 0.118, 0.926, 0.319])

# 18.15.2  The Comb Function and Its Transform

In much the same way we just analyzed a sequence of ever-narrower-and-taller box functions, we can consider a sequence of $L^2(\mathbb{R})$ functions that approaches a **comb**, a function with an “infinitely narrow box” at every integer. Figure 18.48 shows how we can do this: We place boxes of width $a$ and height $1/a$ at each integer point, but then multiply their heights by a “tapering” function of width proportional to $1/a$ so that the total area under all the boxes is finite, hence the functions are all in $L^2(\mathbb{R})$.

Figure 18.49 shows the transforms of these functions. Just as with the delta function, the transforms seem to approach a limit, but in this case the limit is again the comb function (i.e., the transform grows larger and larger at integer points, while heading toward zero at all noninteger points).

We’ll use the symbol $\psi$ for the comb; informally, we say that $\mathcal{F}(\psi)=\psi$. If we create a comb with spacing $c$ instead of $1$, its transform is a comb with spacing $1/c$, just as we saw with the box and the sinc.

![](bbox=[0.707, 0.35, 0.926, 0.467])

![](bbox=[0.707, 0.506, 0.926, 0.789])

# 18.16  The Inverse Fourier Transform

We’ve already said that if we take a function $f$ in $L^2(H)$ (or a periodic function of period one) and compute its Fourier transform $c_k=\mathcal{F}(f)(k)$, then we can recover $f$ by writing

$\displaystyle\sum_k c_k e_k(t).$ (18.66)

For a nice function $f$, this sum equals $f$ except at points of discontinuity of $f$, and possibly the endpoints, if $f(\tfrac{1}{2})\ne f(-\tfrac{1}{2})$. Thus, we’ve defined an **inverse transform** that takes a sequence of coefficients and produces an $L^2$ function on the interval (or a periodic function of period one).

There’s a similar “inverse transform” defined for $L^2(\mathbb{R})$:

$\mathcal{F}^{-1}(g)(x)=C\int_{-\infty}^{\infty}g(\omega)e_\omega(x)\,d\omega,$ (18.67)