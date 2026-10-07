# Unsteady, Non-Linear, and Chaotic Systems

the context of the general theory (section 9.3) of linear differential equations (4.91b) with periodic coefficients (4.91a).

The exact solutions of the Mathieu differential equation (subsections 4.3.7–4.3.9) suggest (subsection 4.3.10) an approximate method (subsections 4.3.11–4.3.20) suitable to studying parametric resonance (subsections 4.3.1–4.3.6). For example, consider the Mathieu cosine (4.120a–c; 4.137d) = (4.138a–d) [sine (4.122a–c; 4.137f)] a periodic function with period $2\pi$:

```
$w_{2,n}(	heta;q) = A_1 \cos\theta + A_3 \cos(3\theta) + \dots = A_1 \left[ \cos\theta - \frac{a-1}{q} \right] \cos(3\theta) + \dots$
```

```
$= A_1 \left[ \cos\theta + \frac{c_{2,n}(q)-1}{q} \right] \cos(3\theta) = A_1 c_{2n+1}(	heta;q)$,
```

$$(4.138a-d)$

```
$w_{4,n}(	heta;q) = B_1 \sin\theta + B_3 \sin(3\theta) + \dots = B_1 \left[ \sin\theta + \left[ 1 + \frac{a-1}{q} \right] \sin(3\theta) + \dots \right$
```

```
$= B_1 \left[ \sin\theta + \left[ \frac{c_{4,n}(q)-1}{q} \right] \sin(3\theta) + \dots \right] = B_1 s_{2n+1}(	heta;q)$,
```

$$(4.139a-d)$

where: (i) the coefficient $A_2$ ($A_3$) is related to $A_1$ ($B_1$) by (4.125b) ([4.126a]), and $A_{2n+1}$ ($B_{2n+1}$) are proportional to $A_1$ ($B_1$) leading to (4.138a) $\equiv$ (4.139a) ([4.139a] [4.139b]); (ii) the eigenvalues $c_{2,n}$ ($c_{4,n}$) are functions of $q$ specified by the roots of the continued fraction (4.134) ([4.136]) and (iii) each root corresponds to a Mathieu cosine (sine) function of period $2\pi$ in (4.138d) ([4.139d]) by multiplying a constant $A_1$ ($B_1$) that can be set to zero.

The lowest-order approximation to the root of the continued fraction is obtained by truncating the first two terms from (4.140a) with upper (lower) sign q in (4.140b) $\equiv$ (4.140a):

```
$\frac{a-1}{q} = \pm1 \Leftrightarrow a-1 = \pm q \mp ha, \quad (4.140a-c)$
```

where (4.90c) was substituted leading to (4.140c). Substituting (4.90b) in (4.140c) $\equiv$ (4.140d) leads to (4.140e):

```
$a = \left( \frac{2\omega_0}{1 \pm h} \right)^2 \Leftrightarrow \omega_r = 2\omega_0\sqrt{1 \pm h} = 2\omega_0 \omega_0 h + O(\omega_0 h^2), \quad (4.140d-f)$
```