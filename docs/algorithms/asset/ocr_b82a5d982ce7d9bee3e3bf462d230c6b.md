# Chapter 2

# Algorithms 77

+   * For $k>0, H_k$ is the $2^k 	imes 2^k$ matrix

```
$H_k = \begin{bmatrix} H_{k-1} & H_{k-1} \ H_{k-1} & -H_{k-1} \end{bmatrix}$
```

Show that if $v$ is a column vector of length $n=2^k$, then the matrix-vector product $H_kv$ can be calculated using $O(n \log n)$ operations. Assume that all the numbers involved are small enough that basic arithmetic operations like addition and multiplication take unit time.

2.29. Suppose we want to evaluate the polynomial $p(x) = a_0 + a_1x + a_2x^2 + \dots + a_nx^n$ at point x.

+   (a) Show that the following simple routine, known as Horner's rule, does the job and leaves the answer in z.

```
$z = a_n\nfor i = n-1 \text{ downto } 0:\nz = z + a_i$
```

+   (b) How many additions and multiplications does this routine use, as a function of $n$? Can you find a polynomial for an alternative method that is substantially better?

2.30. This problem illustrates how to do the Fourier Transform (FT) in modular arithmetic, for example, modulo 7.

+   (a) There is a number $\omega$ such that all the powers $\omega, \omega^2, \dots, \omega^6$ are distinct (modulo 7). Find this $\omega$, and show that $\omega + \omega^2 + \dots + \omega^6 = 0$. (Interestingly, for any prime modulus there is such a number.)

+   (b) Using the matrix form of the FT, produce the transform of the sequence $(0, 1, 1, 1, 5, 2)$ modulo 7; then multiply by the vector for the value of $\omega$ found earlier. In the matrix multiplication, $M_\omega(\omega)$, all calculations should be performed modulo 7.

+   (c) Write down the matrix necessary to perform the inverse FT. Show that multiplying by this matrix returns the original sequence. (Again all arithmetic should be performed modulo 7)

+   (d) Now show how to multiply the polynomials $x^2 + x + 1$ and $x^3 + 2x - 1$ using the FT modulo 7.

2.31. In Section 1.2.3, we studied Euclid's algorithm for computing the greatest common divisor (gcd) of two positive integers: the largest integer which divides both them. Here we will look at an alternative algorithm based on divide-and-conquer.

+   (a) Show that the following rule is true:

```
$gcd(a, b) = \begin{cases} 2 gcd(a/2, b/2) & \text{if } a, b$ are even \n gcd(a, b/2) & \text{if } a$ is odd, $b$ is even \n gcd((a-b)/2, b) & \text{if } a, b are odd \end{cases}$
```