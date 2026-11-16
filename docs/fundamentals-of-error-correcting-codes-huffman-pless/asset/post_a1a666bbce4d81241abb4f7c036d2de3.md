
coefficient. We will usually write polynomials with terms in either increasing or decreasing degree order, e.g. \(a_0 + a_1x + a_2x^2 + \cdots + a_nx^n\) or \(a_nx^n + a_{n-1}x^{n-1} + \cdots + a_1x + a_0\).

### Exercise 153 Prove that \(\mathbb{F}_q[x]\) is a commutative ring with unity and an integral domain as well. \(\diamond\)

### Exercise 154 Multiply \((x^3 + x^2 + 1)(x^3 + x + 1)(x + 1)\) in the ring \(\mathbb{F}_2[x]\). Do the same multiplication in \(\mathbb{F}_3[x]\). \(\diamond\)

### Exercise 155 Show that the degree of the product of two polynomials is the sum of the degrees of the polynomials. \(\diamond\)

A polynomial is monic provided its leading coefficient is 1. Let \(f(x)\) and \(g(x)\) be polynomials in \(\mathbb{F}_q[x]\). We say that \(f(x)\) divides \(g(x)\), denoted \(f(x) | g(x)\), if there exists a polynomial \(h(x) \in \mathbb{F}_q[x]\) such that \(g(x) = f(x)h(x)\). The polynomial \(f(x)\) is called a divisor or factor of \(g(x)\). The greatest common divisor of \(f(x)\) and \(g(x)\), at least one of which is nonzero, is the monic polynomial in \(\mathbb{F}_q[x]\) of largest degree dividing both \(f(x)\) and \(g(x)\). The greatest common divisor of two polynomials is uniquely determined and is denoted by \(\gcd(f(x), g(x))\). The polynomials \(f(x)\) and \(g(x)\) are relatively prime if \(\gcd(f(x), g(x)) = 1\). Many properties of the ring \(\mathbb{F}_q[x]\) are analogous to properties of the integers. One can divide two polynomials and obtain a quotient and remainder just as one can do with integers. In part (i) of the next theorem, we state this fact, which is usually called the Division Algorithm.

### Theorem 3.2.1 Let \(f(x)\) and \(g(x)\) be in \(\mathbb{F}_q[x]\) with \(g(x)\) nonzero.

- (i) (Division Algorithm) There exist unique polynomials \(h(x), r(x) \in \mathbb{F}_q[x]\) such that \(f(x) = g(x)h(x) + r(x), \quad \text{where } \deg r(x) < \deg g(x) \text{ or } r(x) = 0.\)

- (ii) If \(f(x) = g(x)h(x) + r(x)\), then \(\gcd(f(x), g(x)) = \gcd(g(x), r(x))\).

We can use the Division Algorithm recursively together with part (ii) of the previous theorem to find the gcd of two polynomials. This process is known as the Euclidean Algorithm. The Euclidean Algorithm for polynomials is analogous to the Euclidean Algorithm for integers. We state it in the next theorem and then illustrate it with an example.

### Theorem 3.2.2 (Euclidean Algorithm) Let \(f(x)\) and \(g(x)\) be polynomials in \(\mathbb{F}_q[x]\) with \(g(x)\) nonzero.

- (i) Perform the following sequence of steps until \(r_n(x) = 0\) for some \(n\):

\(f(x) = g(x)h_1(x) + r_1(x), \quad \text{where } \deg r_1(x) < \deg g(x),\)
\(g(x) = r_1(x)h_2(x) + r_2(x), \quad \text{where } \deg r_2(x) < \deg r_1(x),\)
\(r_1(x) = r_2(x)h_3(x) + r_3(x), \quad \text{where } \deg r_3(x) < \deg r_2(x),\)
\(\vdots\)
\(r_{n-3}(x) = r_{n-2}(x)h_{n-1}(x) + r_{n-1}(x), \quad \text{where } \deg r_{n-1}(x) < \deg r_{n-2}(x),\)
\(r_{n-2}(x) = r_{n-1}(x)h_n(x) + r_n(x), \quad \text{where } r_n(x) = 0.\)

Then \(\gcd(f(x), g(x)) = c r_{n-1}(x)\), where \(c \in \mathbb{F}_q\) is chosen so that \(c r_{n-1}(x)\) is monic.

- (ii) There exist polynomials \(a(x), b(x) \in \mathbb{F}_q[x]\) such that

```
a(x)f(x) + b(x)g(x) = gcd(f(x), g(x)).
```

The sequence of steps in (i) eventually terminates because at each stage the degree of the remainder decreases by at least 1. By repeatedly applying Theorem 3.2.1(ii), we have that \(c r_{n-1}(x) = \gcd(r_{n-2}(x), r_{n-1}(x)) = \gcd(r_{n-3}(x), r_{n-4}(x)) = \dots = \gcd(f(x), g(x))\). This explains why (i) produces the desired gcd.

Technically, the Euclidean Algorithm is only (i) of this theorem. However, (ii) is a natural consequence of (i), and seems to possess no name of its own in the literature. As we use (ii) so often, we include both in the term "Euclidean Algorithm." Part (ii) is obtained by beginning with the next to last equation \(r_{n-1}(x) = r_{n-3}(x)q_{n-1}(x) + r_{n-2}(x)\) in the sequence in (i) and solving for \(r_{n-1}(x)\) in terms of \(r_{n-2}(x)\) and \(r_{n-3}(x)\). Using the previous equation, solve for \(r_{n-2}(x)\) and substitute into the equation for \(r_{n-1}(x)\) to obtain \(r_{n-1}(x)\) as a combination of \(r_{n-3}(x)\) and \(r_{n-4}(x)\). Continue up through the sequence until we obtain \(r_{n-1}(x)\) as a combination of \(f(x)\) and \(g(x)\). We illustrate all of this in the next example.

### Example 3.2.3 We compute \(\gcd(x^5 + x^4 + x^2 + 1, x^3 + x^2 + x)\) in the ring \(\mathbb{F}_2[x]\) using the Euclidean Algorithm. Part (i) of the algorithm produces the following sequence.

```
x^5 + x^4 + x^2 + 1 = (x^3 + x^2 + x)(x^2 + 1) + x + 1
x^3 + x^2 + x = (x + 1)(x^2 + 1) + 1
x + 1 = 1(x + 1) + 0.
```

Thus \(1 = \gcd(x + 1, 1) = \gcd(x^3 + x^2 + x, x + 1) = \gcd(x^5 + x^4 + x^2 + 1, x^3 + x^2 + x)\). Now we find \(a(x)\) and \(b(x)\) such that \(a(x)(x^5 + x^4 + x^2 + 1) + b(x)(x^3 + x^2 + x) = 1\) by reversing the above steps. We begin with the last equation in our sequence with a nonzero remainder, which we first solve for. This yields

```
1 = (x^3 + x^2 + x) - (x + 1)(x^2 + 1). (3.1)
```

Now \(x + 1\) is the remainder in the first equation in our sequence; solving this for \(x + 1\) and plugging into (3.1) produces

```
1 = (x^3 + x^2 + x) - [(x^5 + x^4 + x^2 + 1) - (x^3 + x^2 + x)(x^2 + 1)](x^2 + 1)
= (x^2 + 1)(x^5 + x^4 + x^2 + 1) + x^4(x^3 + x^2 + x).
```

So \(a(x) = x^2 + 1\) and \(b(x) = x^4\).

### Exercise 156 Find \(\gcd(x^9 + x^7 + x^4 + x^3 + x + 1, x^5 + x^3 + x^2 + x)\) in \(\mathbb{F}_2[x]\). Find \(a(x)\) and \(b(x)\) such that \(\gcd(x^9 + x^7 + x^4 + x^3 + x + 1, x^5 + x^3 + x^2 + x) = a(x)(x^9 + x^7 + x^4 + x^3 + x + 1) + b(x)(x^5 + x^3 + x^2 + x)\).

### Exercise 157 Find \(\gcd(x^5 - x^4 + x + 1, x^3 + x)\) in \(\mathbb{F}_3[x]\). Find \(a(x)\) and \(b(x)\) such that \(\gcd(x^5 - x^4 + x + 1, x^3 + x) = a(x)(x^5 - x^4 + x + 1) + b(x)(x^3 + x)\).

### Exercise 158 Let \(f(x)\) and \(g(x)\) be polynomials in \(\mathbb{F}_q[x]\).

- (a) If \(k(x)\) is a divisor of \(f(x)\) and \(g(x)\), prove that \(k(x)\) is a divisor of \(a(x)f(x) + b(x)g(x)\) for any \(a(x), b(x) \in \mathbb{F}_q[x]\).

- (b) If \(k(x)\) is a divisor of \(f(x)\) and \(g(x)\), prove that \(k(x)\) is a divisor of \(\gcd(f(x), g(x))\).

### Exercise 159 Let \(f(x)\) be a polynomial over \(\mathbb{F}_q\) of degree \(n\).

- (a) Prove that if \(a \in \mathbb{F}_q\) is a root of \(f(x)\), then \(x - a\) is a factor of \(f(x)\).

- (b) Prove that \(f(x)\) has at most \(n\) roots in any field containing \(\mathbb{F}_q\).

## 3.3 Primitive elements

When working with a finite field, one needs to be able to add and multiply as simply as possible. In Theorem 3.1.1(ii), we stated that \(\mathbb{F}_q\) is a vector space over \(\mathbb{F}_p\) of dimension \(m\). So a simple way to add field elements is to write them as \(m\)-tuples over \(\mathbb{F}_p\) and add them using ordinary vector addition, as we will see in Section 3.4. Unfortunately, multiplying such \(m\)-tuples is far from simple. We need another way to write the field elements so that multiplication is easy; then we need a way to connect this form of the field elements to the \(m\)-tuple form. The following theorem will assist us with this. Recall that the set \(\mathbb{F}_q^*\) of nonzero elements in \(\mathbb{F}_q\) is a group.

### Theorem 3.3.1 We have the following:

- (i) The group \(\mathbb{F}_q^*\) is cyclic of order \(q - 1\) under the multiplication of \(\mathbb{F}_q\).

- (ii) If \(\gamma\) is a generator of this cyclic group, then
\(\mathbb{F}_q = \{0, 1, \gamma, \gamma^2, ..., \gamma^{q-2}\}\),
and \(\gamma^i = 1\) if and only if \((q - 1) | i\).

Proof: From the Fundamental Theorem of Finite Abelian Groups [130], \(\mathbb{F}_q^*\) is a direct product of cyclic groups of orders \(m_1, m_2, ..., m_r\), where \(m_i | m_{i+1}\) for \(1 \le i < r\) and \(m_1 m_2 ... m_r = q - 1\). In particular \(a^{m_r} = 1\) for all \(a \in \mathbb{F}_q^*\). Thus the polynomial \(x^{m_r} - 1\) has at least \(q - 1\) roots, a contradiction to Exercise 159 unless \(r = 1\) and \(m_r = q - 1\). Thus \(\mathbb{F}_q^*\) is cyclic giving (i). Part (ii) follows from the properties of cyclic groups.

Each generator \(\gamma\) of \(\mathbb{F}_q^*\) is called a primitive element of \(\mathbb{F}_q\). When the nonzero elements of a finite field are expressed as powers of \(\gamma\), the multiplication in the field is easily carried out according to the rule \(\gamma^u \gamma^v = \gamma^{u+v} = \gamma^t\), where \(0 \le t \le q - 2\) and \(u + v \equiv t \pmod{q - 1}\).

### Exercise 160 Find all primitive elements in the fields \(\mathbb{F}_2, \mathbb{F}_3, \text{and } \mathbb{F}_4\) of Examples 1.1.1, 1.1.2, \text{and } 1.1.3. Pick one of the primitive elements \(\gamma\) of \(\mathbb{F}_4\) and rewrite the addition and multiplication tables of \(\mathbb{F}_4\) using the elements \(\{0, 1 = \gamma^0, \gamma, \gamma^2\}\).

Let \(\gamma\) be a primitive element of \(\mathbb{F}_q\). Then \(\gamma^{q-1} = 1\) by definition. Hence \((\gamma^i)^{q-1} = 1\) for \(0 \le i \le q - 2\) showing that the elements of \(\mathbb{F}_q^*\) are roots of \(x^{q-1} - 1 \in \mathbb{F}_p[x]\) and hence of \(x^q - x\). As \(0\) is a root of \(x^q - x\), by Exercise 159 we now see that the elements of \(\mathbb{F}_q\) are precisely the roots of \(x^q - x\) giving this important theorem.
