which, by the usual multiplication procedure of polynomials (also known as the Cauchy product of the corresponding coefficients), with

c_m = \sum_{j+k=m} a_j b_k, \quad m \ge 0

is just the discrete version of the convolution theorem.

# 1.7.1 Spectral Analysis and Synthesis

When looking at papers or books on Fourier analysis it is not always clear right away why one should consider things like convolution or the Fourier transform. All too often the nice properties of the (classical) Fourier transform on the classical spaces, in particular on (L^2(\mathbb{R}^d), \| \|_2) (in the form of Plancherel’s Theorem) or its the behaviour on other L^p-spaces (like the Hausdorff–Young Theorem, which only applies for 1 \le p \le 2) are in the center of the presentation, but very unfortunately not so much the goals that would be mentioned by more applied scientists.

Let us try to formulate a few of these goals, in particular those which are related to the questions of spectral analysis and spectral synthesis. We formulate some of these question first in an informal style:

+   1. What are the frequencies in a given signal, respectively can be filtered from the signal in a suitable sense, and, as a counterpart, which ones do not play a role for the given signal?
+   2. How can one recover the signal from the information about the frequencies contained in the signal? In other words, what are the most important or most useful methods to recover a function or distribution from its Fourier transform?
+   3. Can we separate signals from each other in a translation invariant way (i.e. by a so-called filtering process, or moving average)? The answer to this question is of course a clear “yes” if the different signals are concentrated in disjoint frequency bands: such considerations are the basis for modern digital radio techniques which rely on the idea that particular radio stations get certain frequency bands assigned.
+   4. Spectral Analysis should also help us to explain Shannon’s Sampling Theorem for band-limited functions and describe a well-localized series representation of band-limited signals, if they are sampled at least at the Nyquist rate, combined with a possibility to estimate the aliasing errors for the case that the signal is not strictly band-limited to the assumed frequency interval.
+   5. The notion of convolution was not much present in the classical work on Fourier series expansions, so that it does not yet play a prominent role in the classical book of A. Zygmund ([11]). It became however more relevant in Norbert Wiener’s influential work on Generalized Harmonic Analysis published in 1930 [12] and his book [13] (only 7 years before A. Weil’s book [4]). Here, and in particular for the proof of Tauberian Theorems the pointwise inversion of a Fourier transform plays an important role, and thus intensive use of convolution is made. He also clearly indicates that convolutions can be approximated well by linear combinations of shift operators (in the strong operator topology).