
```
sage: M = matrix([ [p.degree(v) for v in (x,y,z)]
....:                 for p in J.gens()]); M
[2 1 1]
[1 3 1]
[1 1 4]
```

通过计算其行列式

```
sage: M.det()
17
```

我们看到 \(k = 17\) 可行。剩下只需找到一个非零的核元素：

```
sage: M.change_ring(GF(17)).right_kernel()
Vector space of degree 3 and dimension 1 over Finite Field of size 17
Basis matrix:
[1 9 6]
```

### 练习 36，第 198 页。

这几乎是平凡的：

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

因此，例如，对于上面的第五个解，我们有：

\[x = \frac{1}{2}(2-\sqrt{3})^{3/2}-2\sqrt{2-\sqrt{3}},\qquad y = \frac{1}{2}\sqrt{2-\sqrt{3}}.\]

### 练习 37，第 202 页。

我们已经看到如何得到 ℚ-向量空间 \(\mathbb{Q}[x,y]/J_2\) 的一组基 \(B\)：

```
sage: R.<x,y> = QQ[]; J2 = (x^2+y^2-1, 4*x^2*y^2-1)*R
sage: basis = J2.normal_basis(); basis
[x*y^3, x*y^2, x*y, x^2*y, y, x, 1]
```

然后我们计算 \(B\) 在 \(m_x\) 下的像，并推出 \(m_x\) 在基 \(B\) 下的矩阵：

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

多项式 χₓ 及其根则由下式给出（见第 2 章和第 8 章）：

```
sage: charpoly = mat.characteristic_polynomial(); charpoly
x^8 - 2*x^6 + 3/2*x^4 - 1/2*x^2 + 1/16
sage: solve(SR(charpoly), SR(x))
[x == -1/2*sqrt(2), x == 1/2*sqrt(2)]
```

从这个例子我们看到，χ 的根是 V(J₂) 中点的横坐标。

对于任取的一个理想 J，假设 χ(λ) = 0，其中 λ ∈ ℂ。那么 λ 是 mₓ 的一个特征值。设 p ∈ ℚ[x,y]∖J 是与 λ 相关联的特征向量的一个代表：对某个给定的 q ∈ J，我们有 xp = λp + q。由于 p ∉ J，可以找到 (x₀, y₀) ∈ V(J)，使得 p(x₀, y₀) ≠ 0，于是我们有

(x₀ − λ)p(x₀, y₀) = q(x₀, y₀) = 0,

因此 λ = x₀。

### 练习 38，第 211 页。

表达式 sin θ、cos θ、sin(2θ) 和 cos(2θ) 由经典三角公式相联系

sin²θ + cos²θ = 1,   sin(2θ) = 2 sin(θ) cos(θ),   cos(2θ) = cos²θ − sin²θ。

为简化记号，令 c = cos θ，s = sin θ。来自 ℚ[s, c, u, v] 的理想

(u − (s + c), v − (2sc + c² − s²), s² + c² − 1)

表达了练习中 u(θ) 和 v(θ) 的定义，以及正弦与余弦之间的关系。对于先消去 s 和 c 的单项式序，s⁶ 模该理想的标准形给出所需结果。

```
sage: R.<s, c, u, v> = PolynomialRing(QQ, order='lex')
sage: I = ideal(u-(s+c), v-(2*s*c+c^2-s^2), s^2+c^2-1)
sage: I.reduce(s^6)
1/16*u^2*v^2 - 3/8*u^2*v + 7/16*u^2 - 1/8*v^2 - 1/8*v - 1/8
```

## A.10 微分方程与递推关系

### 练习 39，第 221 页。

（*可分离变量方程*）

- 1. 我们使用与 10.1.2 节相同的方法：

```
sage: x = var('x')
sage: y = function('y')(x)
sage: ed = (desolve(y*diff(y,x)/sqrt(1+y^2) == sin(x),y)); ed
sqrt(y(x)^2 + 1) == _C - cos(x)
```

同样的问题出现了。我们要求 _C-cos(x) 为正：

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

- 2. 同样的方法：

```
sage: sol = desolve(diff(y,x)==sin(x)/cos(y), y, show_method=True)
sage: sol
[sin(y(x)) == _C - cos(x), 'separable']
sage: solve(sol[0],y)
[y(x) == -arcsin(-_C + cos(x))]
```

### 练习 40，第 222 页。

（齐次方程）我们验证方程 $xy' = x^2 + y^2$ 在 $]0,+\infty[$ 和 $]-\infty,0[$ 上有定义且为齐次方程，然后尝试用 10.1.2 节所处理例子中给出的未知函数代换来求解它。

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

我们可以用 assume 对 x 添加条件，以记住该方程在 0 处没有定义。

## A.11 浮点数

### 练习 41，第 239 页。

我们提出两种解法。

- 1. 我们不用 `RealField` 类中给出一个数的有效数字和指数的方法来进行计算。首先检查 2⁹⁹ < 10³⁰ < 2¹⁰⁰（注意 10³⁰ = (10³)¹⁰ ≈ (2¹⁰)¹⁰）。

```
sage: R100=RealField(100)
sage: x=R100(10^30)
sage: x>2^99
True
sage: x<2^100
True
```

然后，我们计算有效数字：

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

有效数字中第七十位之后的所有二进制位均为零。因此，我们在有效数字上加 2⁻¹⁰⁰，以得到离 10³⁰ 最近的数，并得到结果：x.ulp() 的值为 2⁻¹⁰⁰ · 2¹⁰⁰ = 1。

- 2. 使用 `RealField` 类的 `sign_mantissa_exponent()` 方法，我们直接得到：

```
sage: R100=RealField(100)
sage: x=R100(10^30)
sage: s,m,e = x.sign_mantissa_exponent()
sage: s,m,e
(1, 1000000000000000000000000000000, 0)
```

命令 `m.binary()` 表明两种情况下得到相同的有效数字。

### 练习 42，第 242 页。

- 1. 我们来计算公式中的 α、β 和 γ 的值：

$$u_n = \frac{\alpha 100^{n+1} + \beta 6^{n+1} + \gamma 5^{n+1}}{\alpha 100^n + \beta 6^n + \gamma 5^n}. \tag{A.1}$$

为什么不用 Sage 来做这件事呢？我们利用 u0、u1 和 u2 的值得到一个以 α、β 和 γ 为未知量的方程组，然后求解它。让我们定义通解：

```
sage: var('u0 u1 u2 alpha beta gamma n')
(u0, u1, u2, alpha, beta, gamma, n)
sage: recurrence = lambda a,b: 111-1130/a+3000/(a*b)
sage: gener1 = lambda n: (alpha*100^n+beta*6^n+gamma*5^n)
sage: solGen = lambda n: gener1(n+1)/gener1(n)
```

我们把 u2 表示为 u1 和 u0 的函数，以得到方程组：

```
sage: u2 = recurrence(u1,u0)
sage: s = [u2==solGen(2),u1==solGen(1),u0==solGen(0)]
sage: t = [s[i].substitute(u0=2,u1=-4) for i in range(0,3)]
```

然后求解它：

```
sage: solve(t,alpha,beta,gamma)
[(alpha == 0, beta == -3/4*r1, gamma == r1)]
```

这表明 γ 可以取任意值。

我们必须验证确实得到了通解，也就是说，方程 (A.1) 对所有 n 都成立：

```
sage: alpha=0
sage: beta = -3/4*gamma
sage: final=solGen(n)-recurrence(solGen(n-1),solGen(n-2))
sage: final.simplify_full()
0
```

由于 γ 可以取任意值，我们取 γ = 4，于是有 β = −3，α = 0。
