# 7.2.2 Ideals and Quotients

**Ideals of $A[x]$.** The ideals of polynomial rings, and the quotients by these ideals, are represented by Sage objects built from the polynomial ring by the methods ideal and quo. The product of a tuple of polynomials by a polynomial ring is interpreted as an ideal:

```
~~~
sage: R.<x> = QQ[]
sage: J1 = (x^2 - 2*x + 1, 2*x^2 + x - 3)*R; J1
Principal ideal (x - 1) of Univariate Polynomial Ring in x
over Rational Field
~~~
```

We can multiply ideals, and reduce a polynomial modulo an ideal:

```
~~~
sage: J2 = R.ideal(x^5 + 2)
sage: (3*x+5)*J1*J2 .reduce(x^10)
421/81*x^6 - 502/81*x^5 + 842/81*x - 680/81
~~~
```

The reduced polynomial remains in this case an element of QQ['x']. Another way is to construct the quotient by an ideal and project the elements on it. The parent of the projected element is then in the quotient ring. The lift method of the quotient elements converts them back into the initial ring.

```
~~~
sage: B = R.quo((3*x+5)*J1*J2)  # quo automatically names 'xbar' which is
sage: B(x^10)                   # the generator of B image of x
421/81*xbar^6 - 502/81*xbar^5 + 842/81*xbar - 680/81
sage: B(x^10).lift()
421/81*x^6 - 502/81*x^5 + 842/81*x - 680/81
~~~
```

If $K$ is a field, then the ring $K[x]$ is principal: the ideals are represented during computations by a generator, all this being an algebraic language for the operations seen in §7.1. Its principal advantage is that quotient rings can be easily used in new constructions, here that of $(F_5[t]/(t^2+3))[x]$:

```
~~~
sage: R.<t> = GF(5)[]; R.quo(t^2+3)['x'].random_element()
(3*tbar + 1)*x^2 + (2*tbar + 3)*x + 3*tbar + 4
~~~
```

Sage also allows building non principal ideals like in $Z[x]$, where the available operations are then limited — except in case of multivariate polynomials over a field, which are the subject of Chapter 9.

**Exercise 27.** We define the sequence $(u_n)_{n∈N}$ with the initial conditions $u_n = n + 7$ for $0 ≤ n < 1000$, and the linear recurrence relation

$$u_{n+1000} = 23u_{n+729} - 5u_{n+2} + 12u_{n+1} + 7u_n  (n ≥ 0).$$

Compute the last five digits of $u_{10^{10000}}$. *Hint:* we might look at the algorithm from §3.2.4. However, this algorithm is too expensive when the order of the recurrence is large. Introduce a clever quotient of polynomial rings to avoid this issue.