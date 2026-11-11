It then turns out that for a continuous $L^2$ function $f$ satisfying $f(\frac{1}{2})=f(-\frac{1}{2})$,

$$f(x)=\sum_k c_k e_k(x), \qquad (18.47)$$

that is, computing the inner product of $f$ with each basis element $e_k$ lets us write $f$ as a linear combination of the $e_k$’s. This is exactly analogous to the situation in $\mathbf{R}^3$, where a vector is the sum of its projections onto the three coordinate axes. The only difference here is that the sum is infinite, and so a proof is needed to establish that it converges.

The **Fourier transform** of $f$ is now defined to be the sequence $\{c_k : k \in \mathbf{Z}\}$. With this revised definition, we see that the Fourier transform of $f$ is just the list of coefficients of $f$ when it’s written in a particular orthonormal basis. Such “lists of coefficients” form a vector space under term-by-term addition and scalar multiplication, and the Fourier transform is a linear transformation from $L^2$ to this new vector space. Be sure you understand this: *The Fourier transform is just a change of representation.* It’s a very important one, though, because of the multiplication-convolution property.

The function $f \in L^2(H)$ is often referred to as being in the **time domain**, while its Fourier transform is said to be in the **frequency domain**. Since one is a function on an interval and the other is a function on the integers, the distinction between the two is quite clear. But for functions in $L^2(\mathbf{R})$, the Fourier transform is also in $L^2(\mathbf{R})$, and so being able to talk about the two domains is helpful. We’ll sometimes use “value domain” or “value representation” for the original function, and “frequency representation” for its Fourier transform, because $f(x)$ tells us the *value* of $f$ at $x$, while $c_k$ tells us how much frequency-$k$ content there is in $f$.

We mostly won’t care about the particular values $c_k$ in what follows, but we’ll want to be able to take a big-picture look at these numbers and say things like “For this function, it turns out that $c_k=0$ whenever $|k|>200$,” or “The complex numbers $c_k$ get smaller and smaller as $k$ gets larger.” (Recall that the “size” of a complex number $z=a+bi$ is called its **modulus**, and is $|z|=\sqrt{a^2+b^2}$.) Because of this big-picture interest, rather than trying to plot $c_k$ for $k\in\mathbf{Z}$, we instead plot $|c_k|$. The advantage is that $|c_k|$ is a real number rather than a complex one, so it’s easier to plot. The plot of these absolute values is called the **spectrum** of $f$, and it tells us a lot about $f$. (The word “spectrum” arises from a parallel with light being split into all the colors of the spectrum.)

The Fourier transform takes a function in $L^2(H)$ and produces the sequence of coefficients $c_k$. It’s useful to think of this sequence as a function defined on the integers, namely $k\mapsto c_k$. In fact, the sum

$$\sum_k |c_k|^2 \qquad (18.48)$$

turns out to be the same as $\int_{-1/2}^{1/2}|f(x)|^2\,dx$, which is finite because $f$ is an $L^2$ function. This means that $k\mapsto c_k$ is an $\ell^2$ function, and thus the Fourier transform takes $L^2(H)$ to $\ell^2(\mathbf{Z})$.

$$\mathcal{F}: L^2(H)\to \ell^2(\mathbf{Z}): f\mapsto \mathcal{F}(f). \qquad (18.49)$$

Notice that $\mathcal{F}(f)$ is a *function*: $\mathcal{F}(f)(k)$ is defined to be $c_k$, the $k$th Fourier coefficient for $f$. For simplicity, we’ll sometimes denote the Fourier transform of $f$ by $\hat{f}$.

We’ll often use two properties of the Fourier transform.