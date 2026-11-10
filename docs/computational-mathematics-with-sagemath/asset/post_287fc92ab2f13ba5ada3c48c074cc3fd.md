
```sage
sage: p_cheb.substitute_function(T, chebyshev_T).expand()
4*x^6 + 4*x^5 + 1/9*x^4 - 2*x^3 + 2/19*x^2 + 1
```

### Exercise 26 page 135.

A direct translation of the algorithm in Sage gives something like:

```sage
sage: def mydiv(u, v, n):
....:     v0 = v.constant_coefficient()
....:     quo = 0; rem = u
....:     for k in xrange(n+1):
....:         c = rem[0] / v0
....:         rem = (rem - c*v) >> 1  # shifting the coefficients
....:         quo += c*x^k
....:     return quo, rem
```

(One can apply this function to larger examples and measure the execution time and try to make the code more efficient, keeping the same algorithm.)

But the division by increasing powers up to order \(n\) is the series expansion of the rational function \(u/v\) truncated at order \(n+1\). Using the division of formal power series (see §7.5), we can compute the division by increasing powers like in the following function.

```sage
sage: def mydiv2(u, v, n):
....:     x = u.parent().gen()
....:     quo = (u / (v + O(x^(n+1)))).polynomial()
....:     rem = (u - quo*v) >> (n+1)
....:     return quo, rem
```

The line `quo = ...` uses the fact that, if we add \(O(x^{n+1})\) to a polynomial, it is converted into a truncated series and that the default precision used when dividing a polynomial by a series is that of the divisor.

### Exercise 27 page 136.

First of all, \(u_{10^{10000}}\) has about \(10^{10000}\) expected digits. Computing it entirely is absolutely out of reach. But as we are only interested by the last five digits, it is not a real problem: we will compute everything modulo \(10^5\). The fast exponentiation method as presented in §3.2.4 needs tens of thousands of matrix multiplications, the matrix size being 1000 × 1000, with coefficients in \(\mathbb{Z}/10^5\mathbb{Z}\). Each of these matrix products costs about one billion multiplications, or less with a fast algorithm. It is not impossible, but a test with only one multiplication suggests that the full computation with Sage would take at least one hour:

```sage
sage: Mat = MatrixSpace(IntegerModRing(10^5), 1000)
sage: m1, m2 = (Mat.random_element() for i in (1,2))
sage: %time p = m1*m2
CPU times: user 48 ms, sys: 4 ms, total: 52 ms
Wall time: 54.3 ms
```

It is possible to do much better from the algorithmic point of view. Let us denote \(S\) the shift operator \((a_n)_{n\in\mathbb{N}} \mapsto (a_{n+1})_{n\in\mathbb{N}}\). The equation satisfied by \(u = (u_n)_{n\in\mathbb{N}}\) can be rewritten as \(P(S)\cdot u = 0\), with \(P(x) = x^{1000} - 23x^{729} + 5x^2 - 12x - 7\). For all \(N\) (especially \(N = 10^{10000}\)), the \(u_N\) term is the first one in the sequence \(S^N \cdot u\). Let \(R\) be the remainder of the Euclidean division of \(x^N\) by \(P\). As \(P(S)\cdot u = 0\), we have \(S^N \cdot u = R(S)\cdot u\). Thus it is only necessary to compute the image of \(x^N\) in \((\mathbb{Z}/10^5\mathbb{Z})[x]/(P(x))\). We obtain the following code which, on the same machine, computes the result in less than twenty seconds:

```sage
sage: Poly.<x> = Integers(10^5)[]
sage: P = x^1000 - 23*x^729 + 5*x^2 - 12*x - 7
sage: Quo.<s> = Poly.quo(P)
sage: op = s^(10^10000)
sage: add([op[n]*(n+7) for n in range(1000)])
63477
```

The last five digits are 63477. The difference in computing time between both methods grows rapidly with the order of the recurrence.

### Exercise 28 page 147.

- 1. Let us assume that \(a_s u_{n+s} + a_{s-1}u_{n+s-1} + \cdots + a_0u_n = 0\) for all \(n \ge 0\), and let us denote \(u(z) = \sum_{n=0}^{\infty} u_n z^n\). Let \(Q(z) = a_s + a_{s-1}z + \cdots + a_0 z^s\). Then

  \[
  S(z) = Q(z) u(z) = \sum_{n=0}^{\infty} (a_s u_n + a_{s-1}u_{n-1} + \cdots + a_0u_{n-s}) z^n,
  \]

  with the convention that \(u_n = 0\) for \(n < 0\). The coefficient of \(z^n\) in \(S(z)\) is zero for \(n \ge s\), thus \(S(z)\) is a polynomial and \(u(z) = S(z)/Q(z)\). The denominator \(Q(z)\) is the reciprocal polynomial of the characteristic polynomial of the recurrence, and the numerator encodes the initial conditions.

- 2. The first coefficients are enough to guess an order-3 recurrence satisfied by the given coefficients. Using rational_reconstruct we obtain a rational function. By computing a series expansion of this rational function we recover all given coefficients and the possible next ones:

```sage
sage: p = previous_prime(2^30); ZpZx.<x> = Integers(p)[]
sage: s = ZpZx([1, 1, 2, 3, 8, 11, 34, 39, 148, 127, 662, 339])
sage: num, den = s.rational_reconstruct(x^12, 6, 6)
sage: S = ZpZx.completion(x)
sage: map(lift_sym, S(num)/S(den))
[1, 1, 2, 3, 8, 11, 34, 39, 148, 127, 662, 339, 3056, 371,
 14602, -4257, 72268, -50489, 369854, -396981]
```

(The lift_sym function is defined in the chapter of the book. All of the first 20 coefficients of the sequence are much lower than \(2^{29}\), so that we can allow us to unroll the recurrence modulo a prime near \(2^{30}\), then lift up the result in \(\mathbb{Z}\), rather than the converse.)

With berlekamp_massey, we directly obtain the characteristic polynomial of the recurrence with coefficients in \(\mathbb{Z}\):

```sage
sage: berlekamp_massey([1, 1, 2, 3, 8, 11, 34, 39, 148, 127])
x^3 - 5*x + 2
```

Then we verify that all coefficients satisfy \(u_{n+3} = 5u_{n+1} - 2u_n\), and from there we guess the missing coefficients \(72268 = 5 \cdot 14602 - 2 \cdot 371\), \(-50489 = 5 \cdot (-4257) - 2 \cdot 14602\) and so forth.

### Exercise 29 page 147.

We first construct a polynomial of degree 3 which satisfies the given interpolation conditions:

```sage
sage: R.<x> = GF(17)[]
sage: pairs = [(0,-1), (1,0), (2,7), (3,5)]
sage: s = R(QQ['x'].lagrange_polynomial(pairs)); s
6*x^3 + 2*x^2 + 10*x + 16
sage: [s(i) for i in range(4)]
[16, 0, 7, 5]
```

We reduce the exercise to a problem of rational reconstruction:

\[
p/q \equiv s \pmod{(x-1)(x-2)(x-3)}.
\]

As \(s\) cannot be inverted modulo \(x(x-1)(x-2)(x-3)\) (recall that \(s(1)=0\)), there is no solution with a constant \(p\). With \(\deg p=1\), we find:

```sage
sage: s.rational_reconstruction(prod(x-i for i in range(4)), 1, 2)
(15*x + 2, x^2 + 11*x + 15)
```

### Exercise 30 page 150.

We proceed as in the example: we rewrite the equation \(\tan x = \int_0^x (1 + \tan^2 t)\,dt\) and we search for a fixed point, starting from the initial condition \(\tan(0) = 0\).

```sage
sage: S.<x> = PowerSeriesRing(QQ)
sage: t = S(0)
sage: for i in range(7): # here t is correct up to degree 2i+1
....:     # with O(x^15) we prevent the truncation order to grow
....:     t = (1+t^2).integral() + O(x^15)
sage: t
x + 1/3*x^3 + 2/15*x^5 + 17/315*x^7 + 62/2835*x^9 + 1382/155925*x^11 + 21844/6081075*x^13 + O(x^15)
```

## A.8 Linear Algebra

### Exercise 31 page 171. (*Minimal polynomial of a vector*)

- 1. \(\varphi_A\) is an annihilating polynomial for all vectors \(e_i\) of the canonical basis. It is therefore a multiple of all \(\varphi_{A,e_i}\). Let \(\psi\) be the least common multiple of the \(\varphi_{A,e_i}\). It verifies \(\psi|\varphi_A\). Moreover, \(\psi(A) = [\psi(A)e_1\ \ldots\ \psi(A)e_n] = 0\) is annihilating the matrix \(A\). Hence \(\varphi_A|\psi\). Since these polynomials are both monic, they are equal.

- 2. In this case all \(\varphi_{A,e_i}\) are of the form \(\chi^{\ell_i}\), where \(\chi\) is an irreducible polynomial. From the previous question, \(\varphi_A\) coincides with the polynomial \(\chi^\ell\) having the largest multiplicity \(\ell_i\).

- 3. Let \(\varphi\) be an annihilating polynomial for the vector \(e = e_i + e_j\) and let \(\varphi_1 = \varphi_{A,e_i}\), \(\varphi_2 = \varphi_{A,e_j}\). We have \(\varphi_2(A)\varphi(A)e_i = \varphi_2(A)\varphi(A)e - \varphi(A)\varphi_2(A)e_j = 0\). Hence \(\varphi_2\varphi\) is annihilating the vector \(e_i\), and is therefore divisible by \(\varphi_1\). Now since \(\varphi_1\) and \(\varphi_2\) are coprime, we have \(\varphi_1 | \varphi_2\varphi\), thus \(\varphi\) is a multiple of \(\varphi_1\varphi_2\). Now \(\varphi_1\varphi_2\) is annihilating \(e\), thus \(\varphi = \varphi_1\varphi_2\).

- 4. \(P_1\) and \(P_2\) being coprime, there exist two polynomials \(\alpha\) and \(\beta\) such that \(1 = \alpha P_1 + \beta P_2\). Thus for any vector \(x\), we have \(x = \alpha(A)P_1(A)x + \beta(A)P_2(A)x = x_2 + x_1\), where \(x_1 = \beta(A)P_2(A)x\) and \(x_2 = \alpha(A)P_1(A)x\). As \(\varphi_A = P_1P_2\), \(P_1\) is annihilating \(x_1 = \beta(A)P_2(A)x\) (similarly \(P_2\) is annihilating \(x_2\)). If for any vector \(x\), \(x_1 = 0\), then \(\beta P_2\) is annihilating \(A\) and is therefore a multiple of \(P_1P_2\), hence \(1 = P_1(\alpha + \gamma P_2)\), which implies \(\deg P_1 = 0\). Therefore, there exists a nonzero \(x_1\) such that \(P_1\) is an annihilating polynomial of \(x_1\). We will now show that \(P_1\) is minimal for \(x_1\): let \(\tilde P_1\) be an annihilating polynomial of \(x_1\). Then \(\tilde P_1(A)P_2(A)x = P_2(A)\tilde P_1(A)x_1 + \tilde P_1(A)P_2(A)x_2 = 0\), hence \(\tilde P_1P_2\) is a multiple of \(\varphi_A = P_1P_2\). Hence \(P_1 | \tilde P_1\), and \(P_1\) is therefore the minimal polynomial of \(x_1\). The reasoning is identical for \(x_2\).

- 5. For each factor \(\varphi_i^{m_i}\), there exists a vector \(x_i\) for which \(\varphi_i^{m_i}\) is the minimal polynomial and the vector \(x_1 + \cdots + x_k\) has minimal polynomial \(\varphi_A\).

- 6. One first computes the minimal polynomial of the matrix \(A\).

```sage
sage: A = matrix(GF(7),[[0,0,3,0,0],[1,0,6,0,0],[0,1,5,0,0],
....:                  [0,0,0,0,5],[0,0,0,1,5]])
sage: P = A.minpoly(); P
x^5 + 4*x^4 + 3*x^2 + 3*x + 1
sage: P.factor()
(x^2 + 2*x + 2) * (x^3 + 2*x^2 + x + 4)
```

It has maximal degree.

```sage
sage: e1 = identity_matrix(GF(7),5)[0]
sage: e4 = identity_matrix(GF(7),5)[3]
sage: A.transpose().maxspin(e1)
[(1, 0, 0, 0, 0), (0, 1, 0, 0, 0), (0, 0, 1, 0, 0)]
sage: A.transpose().maxspin(e4)
[(0, 0, 0, 1, 0), (0, 0, 0, 0, 1)]
sage: A.transpose().maxspin(e1 + e4)
[(1, 0, 0, 1, 0), (0, 1, 0, 0, 1), (0, 0, 1, 5, 5),
 (3, 6, 5, 4, 2), (1, 5, 3, 3, 0)]
```

The method `maxspin` iterates a vector on the left. We therefore apply it on the transpose of the matrix so as to produce the list of linearly independent Krylov iterates from the vectors \(e_1\) and \(e_4\). The minimal polynomial of \(e_1\) thus has degree 3, that of \(e_4\) has degree 2, and that of \(e_1 + e_4\) has degree 5. Note that the shape of the matrix implies that the vectors \(e_1\) and \(e_4\) produce iterates that are also vectors of the canonical basis. This form is also called the Frobenius normal form (see §8.2.3). It describes how the
