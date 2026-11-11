+   - If $\mathcal{F}(f)(\omega) = 0$ for $|\omega| \ge 1/2$, then $f$ can be recovered from $\tilde{f}$, that is, the map $f \to \tilde{f}$ is invertible once the domain is restricted to the functions strictly band-limited at $1/2$.
+   - For any function $g \in L^2$, there are multiple functions whose samples are given by $g$, so in general, it's impossible to reconstruct an arbitrary $L^2$ function from its samples.

The corresponding statements hold for a function $f \in L^2(H)$, sampled at a collection of $n$ evenly spaced points in the interval; in that case, if the function is band-limited at any frequency below $n/2$, then it's reconstructible from its samples. (Indeed, that's the essence of the sampling theorem.)

We'll actually show exactly *how* to reconstruct a band-limited function from its samples, in that rather than just showing that the sampling process is invertible, we'll explicitly describe an inverse. We'll also describe some approximations to the inverse that are easily computable, that is, functions with the property that if $f$ is band-limited, then sampling $f$, followed by the approximate-reconstruction operation, will yield a function very close to $f$.

We'll start with the easy part: showing there are multiple functions with the same samples. Recall that for a continuous function, “sampling at $x$” simply means “evaluating the function at $x$.” So to show that there are two different functions with the same samples at integer points, consider $f_1(x) = 0$ and $f_2(x) = \sin(\pi x)$. At every integer point, these two have exactly the same value (namely 0). Thus, if you're given the samples of one of the two functions, you cannot possibly tell which one it was. Of course, $f_2$ isn't in $L^2(\mathbf{R})$, because it doesn't approach zero as $x \to \pm\infty$, but this quibble is easily resolved:

> Inline Exercise 18.8: Show that if $f$ is any function in $L^2$, then $x \mapsto f(x)f_2(x)$ is a function whose samples match those of $f_1$, so the sampling operation is a many-to-one map from $L^2(\mathbf{R}) \to \ell^2(\mathbf{Z})$.

Note, however, that the function $f_2$ has frequency $\frac{1}{2}$, so it's *just* above the Nyquist limit. We expect it to produce aliasing.

For the corresponding situation on the interval $H = (-\frac{1}{2}, \frac{1}{2}]$, a similar example suffices. If we consider the $n$ equally spaced sample points $x_j = -\frac{1}{2} + \frac{j}{n}$, $j = 0, 1, \dots, n - 1$, then the function $g_1(x) = 0$ and the function $g_2(x) = \sin(\pi n(x + \frac{1}{2}))$ both take on the value 0 at every $x_j$.

We say that the function $g_2$ is an **alias** of the function $g_1$, because from the point of view of their samples, they appear to be the same. If we had a way to construct a function on the whole interval from a set of samples, then the samples of $g_1$ and $g_2$, being identical, would produce identical results.

Now let's turn to the more difficult part: showing that if a function is **appropriately band-limited**, it can be reconstructed from its samples.

As we saw earlier, if we have a function $f \in L^2(\mathbf{R})$ and multiply it by a “comb-like” function in $L^2$, the Fourier transform of the result starts to look periodic, consisting of multiple copies of the transform of $f$. As we take better and better approximations of the comb, the Fourier transform becomes closer and closer to the convolution of $\tilde{f}$ with a comb. The limit of the comb approximations doesn't exist, of course, but the collection of samples of $f$ *does* exist, and is a function $\tilde{f}$ in $\ell^2$. In the frequency domain, the Fourier transforms of the convolutions of $f$ with more and more comblike approximations of the comb get closer and closer to a