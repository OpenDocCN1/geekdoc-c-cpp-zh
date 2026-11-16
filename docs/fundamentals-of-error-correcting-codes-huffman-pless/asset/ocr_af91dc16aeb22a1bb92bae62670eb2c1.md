**Corollary 12.3.14** With the notation as in Theorem 12.3.13, if \( g(x) = 1 \), then \( \mathcal{C} = \langle f(x) \rangle \), and \( \mathcal{C} \) has type \( 4^{n-\deg f} \). If \( h(x) = 1 \), then \( \mathcal{C} = \langle 2f(x) \rangle \), and \( \mathcal{C} \) has type \( 2^{n-\deg f} \).

**Exercise 720** Prove Corollary 12.3.14.

**Corollary 12.3.15** Let \( n \) be odd. Assume that \( x^n - 1 \) is a product of \( k \) irreducible polynomials in \( \mathbb{Z}_4[x] \). Then there are \( 3^k \) cyclic codes over \( \mathbb{Z}_4 \) of length \( n \).

**Proof:** Let \( x^n - 1 = g_1(x)g_2(x) \cdots g_k(x) \) be the factorization of \( x^n - 1 \) into monic irreducible polynomials. If \( \mathcal{C} \) is a cyclic code, by Theorem 12.3.13, \( \mathcal{C} = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle \) where \( x^n - 1 = f(x)g(x)h(x) \). Each \( g_i(x) \) is a factor of exactly one of \( f(x) \), \( g(x) \), or \( h(x) \). The result follows.

**Example 12.3.16** By Example 12.3.8, \( x^7 - 1 = g_1(x)g_2(x)g_3(x) \), where \( g_1(x) = x - 1 \), \( g_2(x) = x^3 + 2x^2 + x + 1 \), and \( g_3(x) = x^3 + x^2 + 2x - 1 \) are the monic irreducible factors of \( x^7 - 1 \). By Corollary 12.3.15, there are \( 3^3 = 27 \) cyclic codes over \( \mathbb{Z}_4 \) of length 7. In Table 12.1 we give the generator polynomials of the 25 nontrivial cyclic codes of length 7 as described in Theorem 12.3.13. Each generator is given as a product of some of the \( g_i(x) \)s. If a single generator \( a \) is given, then the code is \( \langle a \rangle \); these are the codes that come from Corollary 12.3.14. If a pair \( \langle a, 2b \rangle \) of generators is given, then the code is \( \langle a \rangle \oplus \langle 2b \rangle \). The information on idempotent generators and duality is discussed later.

**Exercise 721** Verify that all the nontrivial cyclic codes of length 7 over \( \mathbb{Z}_4 \) have been accounted for in Table 12.1, and show that the codes with given generator polynomials have the indicated types.

If \( \mathcal{C} = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle \) as in Theorem 12.3.13, we can easily write down a generator matrix \( G \) for \( \mathcal{C} \). The first \( \deg h \) rows of \( G \) correspond to \( x^i f(x)g(x) \) for \( 0 \le i \le \deg h - 1 \). The last \( \deg g \) rows of \( G \) correspond to \( 2x^i f(x)h(x) \) for \( 0 \le i \le \deg g - 1 \).

**Example 12.3.17** Consider code No. 22 in Table 12.1. Since \( g_1(x)g_3(x) = 1 + x + 3x^2 + 2x^3 + x^4 \) and \( 2g_2(x) = 2 + 2x + 2x^3 \), one generator matrix for this code is

```
[ 1 1 3 2 1 0 0 ]
[ 0 1 1 3 2 1 0 ]
[ 0 0 1 1 3 2 1 ]
[ 2 2 0 2 0 0 0 ]
[ 0 2 2 0 2 0 0 ]
[ 0 0 2 2 0 2 0 ]
[ 0 0 0 2 2 0 2 ]
```

As with cyclic codes over \( \mathbb{F}_q \), we can find generator polynomials of the dual codes. Let \( f(x) = a_d x^d + a_{d-1} x^{d-1} + \cdots + a_0 \in \mathbb{Z}_4[x] \) with \( a_d \neq 0 \). Define the reciprocal polynomial \( f^*(x) \) to be \( f^*(x) = \pm x^d f(x^{-1}) = \pm (a_0 x^d + a_1 x^{d-1} + \cdots + a_d) \).