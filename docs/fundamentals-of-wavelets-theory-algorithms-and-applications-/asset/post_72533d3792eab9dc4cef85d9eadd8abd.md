
6. Show that if \(\begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix} \begin{bmatrix} b_1 \\ b_2 \end{bmatrix} = \begin{bmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{bmatrix} \begin{bmatrix} b_1 \\ b_2 \end{bmatrix}\) for all \(b_1\) and \(b_2\) then \(\mathbf{A} = \mathbf{C}\).

\(\mathbf{A} = \begin{bmatrix} 1 & 2 \\ 2 & 4 \end{bmatrix}, \mathbf{B} = \begin{bmatrix} -2 & 1 \\ 1 & 3 \end{bmatrix}\)

Form \((\mathbf{AB})^T\) and \(\mathbf{B}^T \mathbf{A}^T\), and verify that these are the same. Also check if \(\mathbf{AB}\) is equal to \(\mathbf{BA}\).

7. Find the eigenvalues and the eigenvectors for matrix \(A\).

\(A = \begin{bmatrix} 3 & 1 & 0 \\ 1 & 2 & 2 \\ 0 & 2 & 3 \end{bmatrix}\)

Form the transform matrix \(P\) which makes \(P^{-1}AP\) a diagonal matrix.

8. Find the convolution of \(x(n)\) and \(D2(n)\) where

\(x(n) = (1, 3, 0, 2, 4) \text{ for } n = 0, 1, 2, 3, 4\)

and \(D2(n)\) is given in equation (2.45). Plot \(x(n)\) and \(h(n) = x(n) * D2(n)\) as sequences of \(n\).

9. Find the \(z\)-transform of the following sequences and determine the \(ROC\) for each of them:

(a)

$$x(n) = \begin{cases} \cos(n\alpha), & n \ge 0 \\ 0, & n < 0. \end{cases}$$

(b)

$$x(n) = \begin{cases} n, & 1 \le n \le m \\ 2m - n, & m+1 \le n \le 2m-1 \\ 0, & \text{otherwise.} \end{cases}$$

10. Find the z-transform of the system function for the following discrete systems:

(a) \(y(n) = 3x(n) - 5x(n-1) + x(n-3)\)

(b) \(y(n) = 4\delta(n) - 11\delta(n-1) + 5\delta(n-4)\), where

$$\delta(n) = \begin{cases} 1, & n=1; \\ 0, & \text{otherwise.} \end{cases}$$

## 2.10 REFERENCES

- 1. E. A. Guillemin. *The Mathematics of Circuit Analysis*. New York: Wiley, 1949.
- 2. Ben Noble and James W. Daniel. *Applied Linear Algebra*. Upper Saddle River, NJ: Prentice Hall, 1988.
- 3. A. V. Oppenheim and R. W. Schafer. *Discrete-Time Signal Processing*. Upper Saddle River, NJ: Prentice Hall, 1989.

## CHAPTER THREE

### Fourier Analysis

Since the days of Joseph Fourier, his analysis has been used in all branches of engineering science and some areas of social science. Simply stated, the Fourier method is the most powerful technique for signal analysis. It transforms the signal from one domain to another domain in which many characteristics of the signal are revealed. One usually refers to this transform domain as the *spectral* or *frequency* domain, while the domain of the original signal is usually the *time* domain or *spatial* domain. The Fourier analysis includes both the Fourier transform (or Fourier integral) and the Fourier series. The Fourier transform is applicable to functions that are defined on the real line, while the Fourier series is used to analyze functions that are periodic. Since wavelet analysis is similar to Fourier analysis in many aspects, the purpose of this chapter is to provide the reader with an overview of the Fourier analysis from the signal analysis point of view without going into the mathematical details. Most of the mathematical identities and properties are stated without proof.

## 3.1 FOURIER SERIES

Fourier series and Fourier transform are often separately treated by mathematicians since they involve two different classes of functions. However, engineers have always been taught that Fourier transform is an extension of Fourier series by allowing the period \(T\) of a periodic function to approach infinity. We will follow this route by discussing Fourier series first. The Fourier series representation of a real-valued periodic function \(p(t)\), (\(p(t) = p(t + T)\)), is given by

(3.1) \( p(t) = \sum_{k=-\infty}^{\infty} \alpha_k e^{jk\omega_0 t} \)

with

(3.2) \( \alpha_k = \frac{1}{T} \int_{t_0}^{t_0+T} p(t) e^{-jk\omega_0 t} \)

where \(\alpha_k\) are the Fourier coefficients and the period \(T = 2\pi/\omega_0\) with \(\omega_0\) being the *fundamental frequency*. The set of functions \(\{e_k\} = \{e^{jk\omega_0 t}\}\), \(k \in \mathbb{Z}\) forms a complete orthogonal basis in \(L^2 [t_0, t_0 + T]\):

\(\int_{t_0}^{t_0+T} e_k \overline{e_l} dt = T \delta_{k,l}\)

The coefficient \(\alpha_k\) written in the form of an inner product

(3.3) \( \alpha_k = \frac{1}{T} \langle e^{jk\omega_0 t}, p(t) \rangle \)

represents the orthogonal component of the function \(p(t)\) in \(k\omega_0\). Hence the Fourier series is an orthogonal expansion of \(p(t)\) with respect to the basis set \(\{e_k\}\). The representation in (3.1) is exact. However, if we truncate the series to, say ±N terms (k = -N, ..., N) then there will be some error. As described in Section 2.6, the Fourier coefficients, being orthogonal projections, minimize the mean square of such error. A Fourier series may be represented in other forms. Representation using sine and cosine functions is given by

(3.4)
$$p(t) = \frac{a_0}{2} + \sum_{k=1}^{\infty} (a_k \cos k\omega_0 t + b_k \sin k\omega_0 t),$$

in which the $a_k$ and $b_k$ are real quantities. Complex representation using only positive harmonics is written as

(3.5)
$$p(t) = c_0 + \sum_{k=1}^{\infty} c_k \cos(\omega_0 t + \theta_k)$$

with

(3.6)
$$|c_k| = \sqrt{a_k^2 + b_k^2}, \quad \theta_k = \tan^{-1}\left(-\frac{b_k}{a_k}\right),$$

where $c_k = |c_k| e^{i\theta_k}$ are complex quantities. Computation formulas for $a_k$ and $b_k$ are

(3.7)
$$a_k = \frac{2}{T} \int_0^T p(t) \cos k\omega_0 t \, dt,$$

(3.8)
$$b_k = \frac{2}{T} \int_0^T p(t) \sin k\omega_0 t \, dt.$$

## 3.2 EXAMPLES

### 3.2.1 Rectified Sine Wave

Consider a function \( p(t) = |\sin t| \), as shown in Figure 3.1, with the period \( T = \pi \) and \( \omega_0 = 2\pi/T = 2 \, \text{rad/s} \). Since the function \( p(t) \) is an even function with respect to \( t = 0 \), i.e., \( p(-t) = p(t) \), \( b_k = 0 \) for all \( k \). The coefficients \( \{a_k\} \) are computed as

\[
a_k = \frac{2}{\pi} \int_0^\pi \sin t \cos(2kt) dt
= \frac{1}{\pi} \int_0^\pi [\sin(1-2k)t + \sin(1+2k)t] dt
= -\frac{1}{\pi} \left[ \frac{\cos(1-2k)t}{1-2k} \right]_0^\pi + \frac{1}{\pi} \left[ \frac{\cos(1+2k)t}{1+2k} \right]_0^\pi
= -\frac{4}{\pi} \frac{1}{4k^2 - 1}.
\]
(3.9)

FIGURE 3.1: Rectified sine wave.

![](img/f73ae67732328dc36596b27ffe8d0152_83_0.png)

Hence the Fourier series of \( p(t) \) is given as

\( p(t) = \frac{2}{\pi} - \frac{4}{\pi} \sum_{k=1}^{\infty} \frac{1}{4k^2 - 1} \cos 2kt. \)

### 3.2.2 Comb Function and the Fourier Series Kernel \( K_N(t) \)

In this example, we want to find the Fourier series of a periodic impulse train [i.e., a periodic train of delta function] \( \delta(t) \). We write the impulse train with period \( T \) as

\( I_T(t) = \sum_{n=-\infty}^{\infty} \delta(t - nT) = \sum_{k=-\infty}^{\infty} \alpha_k e^{jk\omega_0 t}. \)

(3.10)

The Fourier coefficients are given by

\( \alpha_k = \frac{1}{T} \int_{-T/2}^{T/2} \sum_{n=-\infty}^{\infty} \delta(t - nT) e^{-jk\omega_0 t} dt. \)

(3.11)

Since the only \( n \) that is within the range of integration is \( n = 0 \), we find

\( \alpha_k = \frac{1}{T}, \quad k \in \mathbb{Z}. \)

Therefore, the Fourier series expansion of an impulse train \( I_T(t) \) is written as

(3.12)
\( I_T(t) = \frac{1}{T} \sum_{k=-\infty}^{\infty} e^{jk\omega_0 t} \).

It is instructive to examine the behavior of a truncated version of (3.12). Let \( K_N(t) \) be the \( (2N + 1) \) term finite Fourier sum of \( I_T(t) \):

(3.13)
\( K_N(t) = \frac{1}{T} \sum_{k=-N}^{N} e^{jk\omega_0 t} \).

\( K_N(t) \) is known as the Fourier series kernel. The geometric series sum in (3.13) is carried out to give

\( K_N(t) = \frac{1}{T} \frac{\sin(N + \frac{1}{2})\omega_0 t}{\sin \frac{\omega_0 t}{2}} \).

A graph of \( K_N(t) \) for \( N = 4 \) is given in Figure 3.2. We also compute the kernel for \( N = 10 \) and \( N = 15 \), but find that the shape of the kernel does not change except the oscillation frequency is correspondingly increased for higher value of \( N \). The main lobes (main peaks) of the graph become narrower as the value of \( N \) increases. The oscillation characteristic of \( K_N(t) \) contributes to the Gibb's phenomenon to be discussed later. These oscillation patterns can be modified by weighting the amplitudes of the coefficients in (3.12). This is a common practice in antenna array design [1].
