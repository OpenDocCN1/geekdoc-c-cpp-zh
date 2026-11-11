+   - First, if \(f\) is an even function, then each \(c_k\) is a real number (i.e., its imaginary part is 0). For even functions, we can therefore actually plot \(c_k\) rather than \(|c_k|\); that’s what we did in Figure 18.35, although we only plotted it for \(k \geq 0\).
+   - Second, if \(f\) is real-valued (as are all the functions we care about, the real value being something like “the intensity of light arriving at this point”), then its Fourier transform is even, that is, \(c_k = c_{-k}\) for every \(k\). That’s why we showed the plot of \(c_k\) for \(k \geq 0\) in Figure 18.35: The values for \(k < 0\) would have added no information.

We have one example of the Fourier transform already: We wrote the square-wave function \(s\), as a sum of cosines in Equation 18.35. From that sum, we can read off

\[\hat{s}(k)=\begin{cases}0 & k\text{ even}\\(-1)^{\frac{k-1}{2}}\frac{4}{\pi k} & k=2n+1\end{cases}\qquad (18.50)\]

The plot of \(\hat{s}\) is shown in Figure 18.38.

![](bbox=[0.742, 0.2, 0.93, 0.351])

*Figure 18.38: The Fourier transform of the square wave.*

# 18.11.1 Sampling and Band Limiting in an Interval

Now suppose that we have a function \(f\) on the interval \(H\) with \(\mathcal{F}(f)(k)=0\) for all \(|k|>k_0\). Such a function is said to be **band-limited** at \(k_0\). The function \(f\) can be written as a sum of sinusoidal functions, all of frequency less than or equal to \(k_0\). Since the “features” of a sinusoidal function of frequency \(k\) (the “bumps”) are of size \(\frac{1}{2k}\), the features of \(f\) must be no smaller than \(\frac{1}{2k_0}\). We can say that the function \(f\) is “smooth at the scale \(\frac{1}{2k_0}\).” In a technical sense, \(f\) is completely smooth, but what we mean is that \(f\) has no bumpiness smaller than \(\frac{1}{2k_0}\).

Turning this notion around, suppose that the graph of \(f\) has a sharp corner, or a discontinuity. Then \(f\) cannot be band-limited—it must be made up of sinusoids of arbitrarily high frequencies! This is important: A function that’s discontinuous, or nondifferentiable, cannot be band-limited. The converse is false, however—there are plenty of smooth functions that contain arbitrarily high frequencies.

The set of all functions band-limited at \(k_0\) is a vector space—if we add two band-limited functions, we get another band-limited function, etc. The dimension of this vector space is \(2k_0+1\), with coordinates provided by the numbers \(c_0,c_{\pm1},\ldots,c_{\pm k_0}\). (This is the dimension as a **real** vector space; each number \(c_j\) has a real and an imaginary part, contributing two dimensions, except for \(c_0\), which is pure real.)

If we evaluate the function \(f\) at \(k_0+1\) equally spaced points in the interval \(H=\left(-\frac{1}{2},\frac{1}{2}\right)\), we get \(k_0+1\) complex numbers, which we can treat as \(2k_0+2\) real numbers. If we ignore any one of these, we’re left with \(2k_0+1\) real numbers. That is to say, we’ve defined a linear mapping from the band-limited functions to \(\mathbf{R}^{2k_0+1}\). This mapping turns out to be bijective. (The proof involves lots of trigonometric identities and some complex arithmetic.) What that tells us is somewhat remarkable:

> If \(f\) is band-limited at \(k_0\), then any \(k_0+1\) equally spaced samples of \(f\) determine \(f\) uniquely. Conversely, if you are given values for \(k_0+1\) equally spaced samples (except for either the real or complex part of one value), then there’s a unique function \(f\), band-limited at \(k_0\), that takes on those values at those points.