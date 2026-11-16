

(5.42) \(\hat{N}_1(\omega) = \int_0^1 e^{-j\omega t} dt = \frac{1 - e^{-j\omega}}{j\omega}\)

The important property of splines for our purposes is the fact that they are scaling functions. That is, there exists a sequence \(\{g_0[m, k]\} \in \mathbb{Z}^2\) such that

(5.43) \(N_m(t) = \sum_k g_0[m, k] N_m(2t - k)\)

In Chapter 6, we will derive an expression for \(g_0[m, k]\).

### 5.5.1 Properties of Splines

Some important properties of splines, relevant to the topics discussed in this book, are discussed in this section without giving any proof. Proofs of some of the properties are left as exercises.

- 1. Support \(N_m = [0, m]\) with \(N_m(0) = N_m(m) = 0\)

- 2. \(N_m(t) \in C^{m-2}\); \(C^k\) is the space of functions that are \(k\)-times continuously differentiable.

- 3. \(N_m|_{[k-1, k]} \in \pi_{m-1}\); \(k \in \mathbb{Z}\), \(\pi_k\) is the polynomial space of degree \(k\) (order \(k + 1\)).

- 4. \(\int_{-\infty}^{\infty} N_m(t) dt = 1\)

- 5. \(N'_m(t) = N_{m-1}(t) - N_{m-1}(t - 1)\)

- 6. \(N_m(t)\) is symmetric with respect to the center \(t^* = m/2\):

\(N_m\left(\frac{m}{2} + t\right) = N_m\left(\frac{m}{2} - t\right) ; \quad t \in \mathbb{R}\)

(5.44)

- 7. \(N_m(t)\) behaves as a lowpass filter [\(\hat{N}_m(0) = 1\); see Figure 5.7].

- 8. \(N_m(t)\) has \(m\)th order of approximation in the sense that \(\hat{N}_m(\omega)\) satisfies the Strang-Fix condition

(5.45)

\(\begin{cases} \hat{N}_m(0) = 1, \text{ and} \\ D^j \hat{N}_m(2\pi k) = 0, \quad k \in \mathbb{Z} \setminus \{0\} \quad \text{and} \quad j = 1, ..., m-1, \end{cases}\)

where \(D^j\) denotes the \(j^{\text{th}}\) order derivative. Consequently, \(N_m(t)\) locally reproduces all polynomials of order \(m\) [8, pp. 114–121].

- 9. \(N_m(t - k) \equiv 1\); for all \(t\). This property is referred to as the *partition of unity* property.

- 10. *Total positivity*: \(N_m(t) \ge 0\), for \(t \in [0, m]\). By virtue of the total positivity [6, p. 7] property of \(B\)-splines, coefficients of a \(B\)-spline series follow the shape of the data. For instance, if \(g(t) = \sum_j \alpha_j N_m(t - j)\), then

\(\alpha_j \ge 0 \quad \forall j \Rightarrow g(t) \ge 0\)

\(\alpha_j \uparrow (\text{increasing}) \Rightarrow g(t) \uparrow, \text{and}\)

\(\alpha_j (\text{convex}) \Rightarrow g(t) \text{ convex.}\)

Furthermore, the number of sign changes of \(g(t)\) does not exceed that of the coefficient sequence \(\{\alpha_j\}\). The latter property can be used to identify the zero crossing of a signal.

- 11. As the order \(m\) increases, \(N_m(t)\) approaches a Gaussian function (\(\Delta N_m / \Delta_n \to 0.5\)). For instance, in the case of a cubic spline (\(m=4\)), the r.m.s. in time-frequency window product is 0.501.

## 5.6 MAPPING A FUNCTION INTO MRA SPACE

As discussed in Section 5.2, before a signal \(x(t)\) can be decomposed, it must be mapped into an MRA subspace \(A_M\) for some appropriate scale \(M\), that is,

(5.46) \(x(t) \mapsto x_M(t) = \sum_k a_{k,M} \phi(2^M t - k).\)

Once we know \(\{a_{k,M}\}\) we can use fast algorithms to compute \(\{a_{k,s}\}\) for \(s < M\). Fast algorithms will be discussed in later chapters. Here we are concerned with the evaluation of the coefficients \(\{a_{k,M}\}\).

If \(x(t)\) is known at every \(t\), then we can obtain \(\{a_{k,M}\}\) by the orthogonal projection (\(L^2\) projection) of the signal:

$$a_{k,M} = 2^M \int_{-\infty}^{\infty} x(t) \bar{\phi}(2^M t - k) dt.$$

However, in practice the signal $x(t)$ is known at some discrete points. The given time step determines the scale \(M\) to which the function can be mapped. For representation such as (5.46), we want it to satisfy two important conditions: (1) interpolatory and (2) polynomial reproducibility. By *interpolatory representation* we mean that the series should be exact, at least at the points at which the function is given, meaning \(x(k/2^M) = x_M(k/2^M)\). As pointed out before, *polynomial reproducibility* means that the representation is exact at every point for polynomials of order \(m\) if the basis \(\phi(t)\) has the approximation order \(m\). In other words, \(x(t) \equiv x_M(t)\) for \(x(t) \in \pi_{m-1}\). Cardinal \(B\)-splines have \(m\) order of approximation. In addition, since they are a local basis, the representation (5.46) is also local. By *local* we mean that to obtain the coefficient \(a_{kM}\) for some \(k\), we do not need all the function values; only a few, determined by the support of the splines, will suffice. The coefficients when \(\phi(t) = N_2(t)\) and \(\phi(t) = N_4(t)\) are derived below.

### 5.6.1 Linear Splines (m = 2)

Suppose a function $x(t)$ is given at \(t = k 2^{-M}, k \in \mathbb{Z}\). Then to obtain the spline coefficients \(\{a_{k,M}\}\) for the representation

$$x(t) \mapsto x_M(t) = \sum_k a_{k,M} N_2(2^M t - k).$$

we apply the interpolation condition, namely

(5.49)
\( x \left( \frac{\ell}{2^M} \right) = x_M \left( \frac{\ell}{2^M} \right). \)

By using equation (5.49), along with the fact that

(5.50)
\( N_2(1) = 1, \text{ and } N_2(k) = 0, k \in \mathbb{Z} \setminus \{0\}, \)

we get

(5.51)
\( a_{k,M} = x \left( \frac{k+1}{2^M} \right). \)

The representation (5.48) preserves all polynomials of degree at most 1.

### 5.6.2 Cubic Splines (\(m = 4\))

In this case

(5.52)
\( x(t) \mapsto x_M(t) = \sum_k a_{k,M} N_4(2^M t - k) \)

where [4, p. 117]

\( a_{k,M} = \sum_{n=k-2}^{k+6} v_{k+2-2n} x \left( \frac{n}{2^{M-1}} \right), \)

and

| \(n\) | \(V_n\) |
|-------|---------|
| 0 | \(\frac{29}{24}\) |
| \(\pm 1\) | \(\frac{7}{12}\) |
| \(\pm 2\) | \(-\frac{1}{8}\) |
| \(\pm 3\) | \(-\frac{1}{12}\) |
| \(\pm 4\) | \(\frac{1}{48}\) |
| otherwise | 0 |

The representation (5.52) preserves all polynomials of degree at most 3.

## 5.7 EXERCISES

- 1. For a given \(j \in \mathbb{Z}\), a projection \(P_{2j}f(t)\) of any given function \(f(t) \in L^2(-\infty, \infty)\) onto the “hat function space”

\(V_j = \left\{ \sum_{k=-\infty}^{\infty} c_k N_2(2^j t - k) : \{c_k\}_{k \in Z} \in \ell_2 \right\}\)

can be determined by the interpolation conditions \(P_{2j}f(k/2^j) = f(k/2^j)\) for all \(k \in Z\). Find the formulas for the coefficients \(\{a_n\}\) if \(P_{2j}f\) is written as

\(P_{2j}f(t) = \sum_{n=-\infty}^{\infty} a_n N_2(2^j t - n).\)

- 2. For the Haar wavelet

\(\psi_H(t) := \begin{cases} 1 & \text{for } t \in [0, \frac{1}{2}) \\ -1 & \text{for } t \in [\frac{1}{2}, 1) \\ 0 & \text{otherwise.} \end{cases}\)

define

\(\psi_{H, k, s}(t) = 2^{\frac{s}{2}} \psi_H(2^s t - k), \quad k, s \in \mathbb{Z}\)

Show the orthogonality relations

\(\int_{-\infty}^{\infty} \psi_{H, k, s}(t) \psi_{H, m, p}(t) dt = \delta_{m,k} \delta_{s,p} \quad m, k, p, s \in \mathbb{Z}.\)

Due to these relations, we say that the set \(\{\psi_{H, k, s}\}_{k, s \in Z}\) forms an orthonormal family in \(L^2(-\infty, \infty)\).

- 3. Show that the Gaussian function \(\phi(t) = e^{-t^2}\) cannot be the scaling function of a multiresolution analysis. (Hint: assume that \(e^{-t^2}\) can be written as \(e^{-t^2} = \sum_{k=-\infty}^{\infty} a_k e^{-(2t-k)^2}\) for a sequence \(\{a_k\}_{k \in \mathbb{Z}}\) in \(l_2\), which has to be true if \(e^{-t^2} \in V_0 \subset V_1\). Then show that this leads to a contradiction by taking Fourier transforms on both sides of the equation and comparing the results.)

- 4. Show that the \(m\)th order \(B\)-spline \(N_m(t)\) and its integer translates form a partition of unity:

\(\sum_{k=-\infty}^{\infty} N_m(t-k) = 1 \quad \text{for all } t \in \mathbb{R}.\)

(Hint: use Poisson sum formula.)

- 5. Show the following symmetry property of \(N_m(t)\):

\(N_m\left(\frac{m}{2} + t\right) = N_m\left(\frac{m}{2} - t\right), \quad t \in \mathbb{R}.\)

- 6. Use exercise 5 to show that

\(\int_{-\infty}^{\infty} N_m(t+k) N_m(t) dt = N_{2m}(m+k)\)

for any \(k \in \mathbb{Z}\).

- 7. Show that the hat function

$$N_2(t) = \begin{cases} t & t \in [0, 1] \\ 2-t & t \in [1, 2] \\ 0, & \text{otherwise} \end{cases}$$
(5.53)

and the function \(N_1(t)\) are related by convolution: \(N_2(t) = N_1(t) * N_1(t)\). Find the defining equations (the polynomial expression) for the functions given by

\(N_3(t) := N_2(t) * N_1(t)\)

\(N_4(t) := N_3(t) * N_1(t)\).

## 5.8 COMPUTER PROGRAMS

### 5.8.1 B-Splines

```
%
% PROGRAM Bspline.m
%
% Computes uniform Bsplines
function y = Bspline(m,x)
y = 0;
% Characteristic function
if m == 1
if x >= 0.0 & x < 1.0
y = 1.0;
else
```

