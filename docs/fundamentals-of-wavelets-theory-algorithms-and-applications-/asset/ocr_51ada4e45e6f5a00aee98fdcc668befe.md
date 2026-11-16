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

# 5.6.2 Cubic Splines (\( m = 4 \))

In this case

(5.52) 
\( x(t) \mapsto x_M(t) = \sum_k a_{k,M} N_4(2^M t - k) \)

where [4, p. 117]

\( a_{k,M} = \sum_{n=k-2}^{k+6} v_{k+2-2n} x \left( \frac{n}{2^{M-1}} \right), \)

and