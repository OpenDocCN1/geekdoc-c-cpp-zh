So C has dimension at most k and

```
{g(x), xg(x), ..., x^{k-1}g(x)}
```

spans C. Since these k polynomials are of different degrees, they are independent in F_q[x]. Since they are of degree at most n - 1, they remain independent in R_n, yielding (iv) and (v). The codewords in this basis, written as n-tuples, give G in part (vi). Part (vii) follows from Theorem 4.1.1.

We remark that part (ii) shows that R_n is a principal ideal ring. Also parts (i) through (vi) of Theorem 4.2.1 hold even if gcd(n, q) != 1. However, part (vii) requires that gcd(n, q) = 1. A parity check matrix for a cyclic code will be given in Theorem 4.2.7.

# Corollary 4.2.2 Let C be a nonzero cyclic code in R_n. The following are equivalent:

+   (i) g(x) is the monic polynomial of minimum degree in C.

+   (ii) C = <g(x)>, g(x) is monic, and g(x) | (x^n - 1).

Proof: That (i) implies (ii) was shown in the proof of Theorem 4.2.1. Assume (ii). Let g_1(x) be the monic polynomial of minimum degree in C. By the proof of Theorem 4.2.1(i) and (ii), g_1(x) | g(x) in F_q[x] and C = <g_1(x)>. As g_1(x) in C = <g(x)>, g_1(x) = g(x)a(x) (mod x^n - 1) implying g(x) = g(x)(a(x) + (x^n - 1)b(x)) in F_q[x]. Since g(x) != (x^n - 1), g(x) | g(x)a(x) + (x^n - 1)b(x) or g(x) | g_1(x). As both g_1(x) and g(x) are monic and divide one another in F_q[x], they are equal.

Theorem 4.2.1 shows that there is a monic polynomial g(x) dividing x^n - 1 and generating C. Corollary 4.2.2 shows that the monic polynomial dividing x^n - 1 which generates C is unique. This polynomial is called the generator polynomial of the cyclic code C. By the corollary, this polynomial is both the monic polynomial in C of minimum degree and the monic polynomial dividing x^n - 1 which generates C. So there is a one-to-one correspondence between the nonzero cyclic codes and the divisors of x^n - 1, not equal to x^n - 1. In order to have a bijective correspondence between all the cyclic codes in R_n, and all the monic divisors of x^n - 1, we define the generator polynomial of the zero cyclic code {0} to be x^n - 1. (Note that x^n - 1 equals 0 in R_n.) This bijective correspondence leads to the following corollary.

# Corollary 4.2.3 The number of cyclic codes in R_n equals 2^m, where m is the number of q-cyclotomic cosets modulo n. Moreover, the dimensions of cyclic codes in R_n are all possible sums of the sizes of the q-cyclotomic cosets modulo n.

# Example 4.2.4 In Example 4.1.2, we showed that, over F_2, x^9 - 1 = (1 + x)(1 + x + x^3)(1 + x^2 + x^6), and so there are eight binary cyclic codes C_i of length 9 with generator polynomial g_i(x) given in the following table.