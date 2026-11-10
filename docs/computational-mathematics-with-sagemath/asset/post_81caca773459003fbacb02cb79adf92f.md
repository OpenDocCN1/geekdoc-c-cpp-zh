
```
sage: M = matrix([ [p.degree(v) for v in (x,y,z)]
....:                 for p in J.gens()]); M
[2 1 1]
[1 3 1]
[1 1 4]
```

By computing its determinant

```
sage: M.det()
17
```

we see that \(k = 17\) works. It just remains to find a non-zero kernel element:

```
sage: M.change_ring(GF(17)).right_kernel()
Vector space of degree 3 and dimension 1 over Finite Field of size 17
Basis matrix:
[1 9 6]
```

### Exercise 36 page 198.

It is almost trivial:

```
sage: L.<a> = QQ[sqrt(2-sqrt(3))]; L
Number Field in a with defining polynomial x^4 - 4*x^2 + 1
sage: R.<x,y> = QQ[]
sage: J1 = (x^2 + y^2 - 1, 16*x^2*y^2 - 1)*R
sage: J1.variety(L)
[{y: 1/2*a^3 - 2*a, x: -1/2*a}, {y: 1/2*a^3 - 2*a, x: 1/2*a},
 {y: -1/2*a, x: 1/2*a^3 - 2*a}, {y: -1/2*a, x: -1/2*a^3 + 2*a},
 {y: 1/2*a, x: 1/2*a^3 - 2*a}, {y: 1/2*a, x: -1/2*a^3 + 2*a},
 {y: -1/2*a^3 + 2*a, x: -1/2*a}, {y: -1/2*a^3 + 2*a, x: 1/2*a}]
```

Thus, for example, we have for the fifth solution above:

\[x = \frac{1}{2}(2-\sqrt{3})^{3/2}-2\sqrt{2-\sqrt{3}},\qquad y = \frac{1}{2}\sqrt{2-\sqrt{3}}.\]

### Exercise 37 page 202.

We have seen how to obtain a basis \(B\) of the ℚ-vector space \(\mathbb{Q}[x,y]/J_2\):

```
sage: R.<x,y> = QQ[]; J2 = (x^2+y^2-1, 4*x^2*y^2-1)*R
sage: basis = J2.normal_basis(); basis
[x*y^3, x*y^2, x*y, x^2*y, y, x, 1]
```

We then compute the image of \(B\) by \(m_x\), and we deduce the matrix of \(m_x\) in the basis \(B\):

```
sage: xbasis = [(xp).reduce(J2) for p in basis]; xbasis
[1/4*y, x*y^3, 1/4, x*y^2, -y^3 + y, x*y, -y^2 + 1, x]
sage: mat = matrix([ [xp@q for q in basis]
                     for xp in xbasis])
sage: mat
[ 0 0 0 0 0 1/4 0 0]
[ 1 0 0 0 0 0 0 0]
[ 0 0 0 0 0 0 0 1/4]
[ 0 0 1 0 0 0 0 0]
[ 0 -1 0 0 0 1 0 0]
[ 0 0 0 0 0 1 0 0]
[ 0 0 0 -1 0 0 0 1]
[ 0 0 0 0 0 0 1 0]
```

The polynomial χₓ and its roots are then given by (see Chapters 2 and 8):

```
sage: charpoly = mat.characteristic_polynomial(); charpoly
x^8 - 2*x^6 + 3/2*x^4 - 1/2*x^2 + 1/16
sage: solve(SR(charpoly), SR(x))
[x == -1/2*sqrt(2), x == 1/2*sqrt(2)]
```

We see on this example that the roots of χ are the abscissas of the points of V(J₂).

For a random ideal J, let us assume χ(λ) = 0 with λ ∈ ℂ. Then λ is an eigenvalue of mₓ. Let p ∈ ℚ[x,y]∖J a representative of an eigenvector associated to λ: we have xp = λp + q for a given q ∈ J. Since p ∉ J, we can find (x₀, y₀) ∈ V(J) such that p(x₀, y₀) ≠ 0, and we have then

(x₀ − λ)p(x₀, y₀) = q(x₀, y₀) = 0,

thus λ = x₀.

### Exercise 38 page 211.

The expressions sin θ, cos θ, sin(2θ) and cos(2θ) are related by the classical trigonometric formulas

sin²θ + cos²θ = 1,   sin(2θ) = 2 sin(θ) cos(θ),   cos(2θ) = cos²θ − sin²θ.

To simplify the notations, let us write c = cos θ and s = sin θ. The ideal

(u − (s + c), v − (2sc + c² − s²), s² + c² − 1)

from ℚ[s, c, u, v] translates the definitions of u(θ) and v(θ) from the exercise, together with the relation between sine and cosine. For a monomial order which eliminates s and c first, the canonical form of s⁶ modulo this ideal gives the wanted result.

```
sage: R.<s, c, u, v> = PolynomialRing(QQ, order='lex')
sage: I = ideal(u-(s+c), v-(2*s*c+c^2-s^2), s^2+c^2-1)
sage: I.reduce(s^6)
1/16*u^2*v^2 - 3/8*u^2*v + 7/16*u^2 - 1/8*v^2 - 1/8*v - 1/8
```

## A.10 Differential Equations and Recurrences

### Exercise 39 page 221.

(*Separable variable equations*)

- 1. Let us use the same method as in Section 10.1.2:

```
sage: x = var('x')
sage: y = function('y')(x)
sage: ed = (desolve(y*diff(y,x)/sqrt(1+y^2) == sin(x),y)); ed
sqrt(y(x)^2 + 1) == _C - cos(x)
```

The same problem appears. We impose that _C-cos(x) is positive:

```
sage: c = ed.variables()[0]
sage: assume(c-cos(x) > 0)
sage: sol = solve(ed,y) ; sol
[y(x) == -sqrt(_C^2 - 2*_C*cos(x) + cos(x)^2 - 1),
y(x) == sqrt(_C^2 - 2*_C*cos(x) + cos(x)^2 - 1)]
```

```
sage: P = Graphics()
sage: for j in [0,1]:
....:    for k in range(0,20,2):
....:        P += plot(sol[j].substitute(c==2+0.25*k).rhs(),x,-3,3)
sage: P
```

![](img/99840d73c45ee58b635c4eedc727fd9a_446_0.png)

- 2. Same method:

```
sage: sol = desolve(diff(y,x)==sin(x)/cos(y), y, show_method=True)
sage: sol
[sin(y(x)) == _C - cos(x), 'separable']
sage: solve(sol[0],y)
[y(x) == -arcsin(-_C + cos(x))]
```

### Exercise 40 page 222.

(Homogeneous equations) We verify that the equation $xy' = x^2 + y^2$ defined on $]0,+\infty[$ and on $]-\infty,0[$ is homogeneous, then we try to solve it by the change of unknown function indicated in the example treated in Section 10.1.2.

```
sage: x = var('x')
sage: y = function('y')(x)
sage: id(x) = x
sage: u = function('u')(x)
sage: D = diff(u*id,x)
sage: DE = (x*D == x*x+y*y).substitute(y == u*id)
sage: eq = desolve(DE,u)
```

```
sage: sol = solve(eq,u)
sage: sol
[u(x) == -sqrt(2*_C + 2*log(x)), u(x) == sqrt(2*_C + 2*log(x))]
sage: Y = [x*sol[0].rhs(), x*sol[1].rhs()]
sage: Y[0]
-sqrt(2*_C + 2*log(x))*x
```

We can add conditions on x (with assume) to remember that the equation is not defined in 0.

## A.11 Floating-Point Numbers

### Exercise 41 page 239.

We propose two solutions.

- 1. Let us make the calculation without the methods of the class `RealField` which give the significand and the exponent of a number. We first check that 2⁹⁹ < 10³⁰ < 2¹⁰⁰ (we remark that 10³⁰ = (10³)¹⁰ ≈ (2¹⁰)¹⁰).

```
sage: R100=RealField(100)
sage: x=R100(10^30)
sage: x>2^99
True
sage: x<2^100
True
```

Then, we compute the significand:

```
sage: e=2^100
sage: s1=10^30
sage: significand=[]
sage: nbdigits=0 # number of significant digits
sage: while s1>0:
....:     e/=2
....:     if e<=s1:
....:         significand.append(1)
....:         s1-=e
....:     else:
....:         significand.append(0)
....:     nbdigits+=1
sage: print(significand)
[1, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0,
 1, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0,
 0, 1, 0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1,
 1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1]
sage: print("number of significant digits: " + str(nbdigits))
number of significant digits: 70
```

All the binary digits of the significand beyond the seventieth are zero. Thus we add 2⁻¹⁰⁰ to the significand to obtain the nearest number from 10³⁰, and we get the result: the value of x.ulp() is 2⁻¹⁰⁰ · 2¹⁰⁰ = 1.

- 2. Using the method sign_mantissa_exponent() of the class RealField, we obtain directly:

```
sage: R100=RealField(100)
sage: x=R100(10^30)
sage: s,m,e = x.sign_mantissa_exponent()
sage: s,m,e
(1, 1000000000000000000000000000000, 0)
```

The command `m.binary()` reveals that we get the same significand in both cases.

### Exercise 42 page 242.

- 1. Let us calculate the values of α, β and γ in the formula:

$$u_n = \frac{\alpha 100^{n+1} + \beta 6^{n+1} + \gamma 5^{n+1}}{\alpha 100^n + \beta 6^n + \gamma 5^n}. \tag{A.1}$$

Why not use Sage for this? We use the values of u0, u1 and u2 to obtain a system of equations where the unknowns are α, β and γ and then, we solve it. Let us define the general solution:

```
sage: var('u0 u1 u2 alpha beta gamma n')
(u0, u1, u2, alpha, beta, gamma, n)
sage: recurrence = lambda a,b: 111-1130/a+3000/(a*b)
sage: gener1 = lambda n: (alpha*100^n+beta*6^n+gamma*5^n)
sage: solGen = lambda n: gener1(n+1)/gener1(n)
```

We calculate u2 as a function of u1 and u0 to get the system:

```
sage: u2 = recurrence(u1,u0)
sage: s = [u2==solGen(2),u1==solGen(1),u0==solGen(0)]
sage: t = [s[i].substitute(u0=2,u1=-4) for i in range(0,3)]
```

then, we solve it:

```
sage: solve(t,alpha,beta,gamma)
[(alpha == 0, beta == -3/4*r1, gamma == r1)]
```

This shows that γ can have any value.

We must verify that we really got the general solution, that is to say that equation (A.1) is verified for all n:

```
sage: alpha=0
sage: beta = -3/4*gamma
sage: final=solGen(n)-recurrence(solGen(n-1),solGen(n-2))
sage: final.simplify_full()
0
```

Since we can take any value for γ, let us take γ = 4 and then we have β = −3 and α = 0.
