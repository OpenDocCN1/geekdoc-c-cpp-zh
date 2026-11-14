Performing calculations we obtain

```
(14.3.2) \( u(x) \leq K + \inf_{q \geq 0} \left[ cq + \frac{h}{\alpha} \left( x \left( 1 - \exp -\alpha \frac{q}{r} \right) + \frac{r - \lambda}{\alpha} \right. \right. \\
\left. \left. \cdot \left( 1 - \exp -\alpha \frac{q}{r} - \alpha \frac{q}{r} \exp -\alpha \frac{q}{r} \right) \right) + \exp -\alpha \frac{q}{r} u \left( x + q - \frac{\lambda}{r} \right) \right] \).
```

We proceed as in the EQO case and consider \( s = 0 \) and that the equation is verified for \( x > 0 \) and use the boundary condition

```
(14.3.3) \( u(0) = K + \inf_{q \geq 0} \left[ cq + \frac{h(r - \lambda)}{\alpha^2} \left( 1 - \exp -\alpha \frac{q}{r} - \alpha \frac{q}{r} \exp -\alpha \frac{q}{r} \right) \right. \\
\left. + \exp -\alpha \frac{q}{r} u(q - \frac{\lambda}{r} q) \right] \).
```

**Exercise 14.6.** We compute the optimal \(\hat{S} = \hat{q}\) by differentiating the right hand side and equaling it to 0. We get

```
(14.3.4) \( c + \frac{r - \lambda}{r} \exp -\alpha \frac{S}{r} \frac{S}{r} \left( S + u' \left( S \frac{r - \lambda}{r} \right) \right) - \frac{\alpha}{r} \exp -\alpha \frac{S}{u} u \left( S \frac{r - \lambda}{r} \right) = 0 \).
```

**Exercise 14.7.** Show that \(\hat{S}\) is a solution of

```
(14.3.5) \( \left( \exp -\alpha \frac{S}{r} + \frac{\alpha c}{h} \right) \left( \exp \frac{\alpha}{\lambda} S - 1 \right) - \frac{r}{\lambda} \left( 1 - \exp -\frac{S\alpha}{r} \right) - S \frac{\alpha^2 c}{\lambda h} \frac{\alpha^2 K}{\lambda h} = 0 \).
```

**Exercise 14.8.** Check that equation (14.3.5) reduces to (14.1.12) as \( r \to \infty \), and to the transformed EOQ formula of section 14.3.1 as \( \alpha \to 0 \).

# 14.4. LEAD TIME

# 14.4.1. NO SHORTAGE ADMITTED.

We consider now a situation with discount rate. We complement section 2.6.1. If we implement an \( s, q \) policy with \( s = \lambda L \), the optimal \( q \) will be different from the EOQ formula. Indeed, we recall the differential function for \( u_s(x) \) with \( s = \lambda L \), which we write \( u(x) \) to simplify the notation, although it is not the value function. We have

```
\( u(x) = \frac{h}{\alpha} \left( x - \frac{\lambda}{\alpha} \right) + \left( u(\lambda L) - \frac{L \lambda h}{\alpha} + \frac{\lambda h}{\alpha^2} \right) \exp -\frac{\alpha}{\lambda} (x - L \lambda), \).
```

then we must write

```
\( u'(q) = -c \exp \alpha L, \).
```

where we expect \(\hat{q} > \lambda L\). We can then apply the equation to obtain

```
\( u(q) \exp -\alpha L = \frac{\lambda c + h \hat{q} \exp -\alpha L}{\alpha}. \).
```

We deduce

```
\( u(\lambda L) = K + c\hat{q} + \frac{L \lambda h}{\alpha} - \frac{\lambda h}{\alpha} + \frac{h \lambda}{\alpha} \exp -\alpha L + \frac{\lambda c + h \hat{q} \exp -\alpha L}{\alpha}. \).
```

Collecting results, we obtain that \(\hat{q}\) is the solution of the equation

```
(14.4.1) \( \left( \exp -\alpha L + \frac{\alpha c}{h} \right) \frac{\exp \alpha \hat{q}}{\lambda} \frac{\alpha}{q} \hat{q} \left( \exp -\alpha L + \frac{\alpha c}{h} \right) - \exp -\alpha L - \frac{\alpha c}{h} - \frac{\alpha^2 K}{\lambda h} = 0. \).
```

**Exercise 14.9.** Check that when \(\alpha\) is small, the solution of equation (14.4.1) converges to the EOQ formula, independent of \( L \), provided it is larger than \(\lambda L\).