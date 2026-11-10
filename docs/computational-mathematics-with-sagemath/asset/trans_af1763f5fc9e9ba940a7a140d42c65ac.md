
$$
\begin{aligned}
I_5 &= \int_0^1 \sin(\sin(x))\,dx, \quad I_6 = \int_0^\pi \sin(x)\exp(\cos(x))\,dx = e - \frac{1}{e},\\
I_7 &= \int_0^1 \frac{1}{1+10^{10}x^2}\,dx = 10^{-5}\arctan(10^5), \quad I_8 = \int_0^{1.1} \exp(-x^{100})\,dx,\\
I_9 &= \int_0^{10} x^2\sin(x^3)\,dx = \frac{1}{3}(1-\cos(1000)), \quad I_{10} = \int_0^1 \sqrt{x}\,dx = \frac{2}{3}.
\end{aligned}
$$

我们不会详尽描述积分函数——这些可在在线帮助中找到——而只介绍它们更常见的用法。

### N(integrate(...))

可与 Sage 一起使用的第一种数值方法是 N(integrate(...))：

```python
sage: N(integrate(exp(-x^2)*log(x), x, 17, 42))
2.5657285006962035e-127
```

这种方式并不保证积分会真正以数值方式计算。实际上，`integrate` 命令要求进行符号积分；如果符号积分成功，那么 Sage 只会对得到的符号表达式进行数值求值：

```python
sage: integrate(log(1+x)*x, x, 0, 1)
1/4
sage: N(integrate(log(1+x)*x, x, 0, 1))
0.250000000000000
```

### numerical_integral

相反，`numerical_integral` 函数明确要求对给定函数进行数值积分。它调用 GSL 库（GNU Scientific Library），该库对固定数量 n 的积分点实现 Gauss-Kronrod 方法。积分点和权重是预先计算好的，精度限于机器浮点数的精度（53 位有效数字）。结果是一个包含计算近似值和误差估计的二元组：

```python
sage: numerical_integral(exp(-x^2)*log(x), 17, 42)
(2.5657285006962035e-127, 3.3540254049238093e-128)
```

误差估计并不是误差的保证上界，而只是对逼近给定积分难易程度的简单指示。在上面的例子中，误差估计如此之大，以至于结果中除最高有效位之外的所有数字都可能是错误的。

`numerical_integral` 的参数尤其允许：

- 选择求值点的数量（有六种选择，从 rule=1 对应 15 个点到 rule=6 对应 61 个点，后者为默认值）；
- 请求自适应细分（默认选择），或要求在积分区间上直接应用复合方法（使用选项 algorithm='qng'）；
- 限制被积函数的求值次数。

禁止 GSL 执行自适应积分可能会导致精度损失：

```python
sage: numerical_integral(exp(-x^100), 0, 1.1)
(0.99432585119150..., 4.0775730...e-09)
sage: numerical_integral(exp(-x^100), 0, 1.1, algorithm='qng')
(0.994327538576531..., 0.016840666914688864)
```

当 integrate 命令找不到所请求积分的解析表达式时，它会原样返回输入的积分：

```python
sage: integrate(exp(-x^2)*log(x), x, 17, 42)
integrate(e^(-x^2)*log(x), x, 17, 42)
```

而使用 N 进行的数值求值会调用 numerical_integral。这尤其解释了为什么在这种情况下精度参数被忽略：

```python
sage: N(integrate(exp(-x^2)*log(x), x, 17, 42), digits=60)
2.5657285006962035e-127
```

但我们得到：

```python
sage: N(integrate(sin(x)*exp(cos(x)), x, 0, pi), digits=60)
2.350402387287602913764763701191201630311435962628190174045913
```

因为在这种情况下符号积分成功了。

### sage.calculus.calculus.nintegral

对于符号函数，可以向 Maxima 请求积分的数值近似：

```python
sage: sage.calculus.calculus.nintegral(sin(sin(x)), x, 0, 1)
(0.430606103120690..., 4.78068810228705...e-15, 21, 0)
```

也可以直接在 Expression 类型的对象上调用 nintegral 方法：

```python
sage: g = sin(sin(x))
sage: g.nintegral(x, 0, 1)
(0.430606103120690..., 4.78068810228705...e-15, 21, 0)
```

Maxima 调用 QUADPACK 数值求积库，该库与 GSL 一样限于机器浮点数。nintegral 方法对积分区间使用自适应细分策略，并且我们可以指定：

- 结果所需的相对精度；
- 计算的最大子区间数。

输出是一个元组：

- 1. 积分的近似值；
- 2. 绝对误差的估计；
- 3. 被积函数的求值次数；
- 4. 错误代码（如果未遇到问题则为 0；关于其他可能值的更多细节，读者应使用 `sage.calculus.calculus.nintegral?` 查阅参考手册）。

### gp('intnum(...)')

Sage 中可用的 PARI/GP 计算器也实现了一个名为 intnum 的数值积分命令：

```python
sage: gp('intnum(x=17, 20, exp(-x^2)*log(x))')
2.5657285005610514829173563961304785900 E-127
```

intnum 命令使用双指数方法，但请注意，它不保证结果有任何正确的有效数字！

我们可以通过修改 PARI/GP 解释器的全局精度来请求结果的给定精度：

```python
sage: gp('intnum(x=0, 1, sin(sin(x)))')
0.43060610312069049123773552484578643
sage: old_prec = gp.set_precision(50)
sage: gp('intnum(x=0, 1, sin(sin(x)))')
0.430606103120690490123773552484578643360804182200
```

一个主要瓶颈是被积函数必须以字符串形式按照 PARI/GP 语法给出，因此无法通过这种方式对任意函数进行积分。

intnum 命令允许我们指明被积函数在区间边界处的行为。下面的例子演示了对结果精度的相应影响。让我们在没有任何指示的情况下对 $x \mapsto x^{-99/100}$ 进行积分：

```python
sage: p = gp.set_precision(old_prec) # we reset the default precision
sage: gp('intnum(x=0, 1, x^(-99/100))')
73.62914262423378365
```

如果我们给出奇点的性质，即该函数在 0 处行为类似于 $x \mapsto x^{-99/100}$：

```python
sage: gp('intnum(x=[0, -99/100], 1, x^(-99/100))')
100.0000000000000000000000000000000000
```

用户要对所给行为的准确性负责；如果我们错误地说该函数在 0 处行为类似于 $x \mapsto x^{-1/42}$，误差将仍然很大：

```python
sage: gp('intnum(x=[0, -1/42], 1, x^(-99/100))')
74.47274932026288503
```

### mpmath.quad

mpmath 库是一个用 Python 编写的任意精度数值库。它能够处理浮点实数和复数、矩阵以及浮点实数区间。

它提供数值求积函数（其中主要的是 quad），并在导入后可在 Sage 中使用：

```python
sage: import mpmath
sage: mpmath.mp.prec = 53
sage: mpmath.quad(lambda x: mpmath.sin(mpmath.sin(x)), [0, 1])
mpf('0.43060610312069059')
```

mpmath 的浮点数 mpf(...) 可以转换为 Sage 浮点数，反之亦然：

```python
sage: a = RDF(pi); b = mpmath.mpf(a); b
mpf('3.1415926535897931')
sage: c = RDF(b); c
3.141592653589793
```

用户可以以十进制位数（mpmath.mp.dps）或以比特位数（mpmath.mp.prec）指定所需精度，就像使用 Sage 的 N 命令一样：N(...,53) 或 N(..., digits=17)。

```python
sage: mpmath.mp.prec = 113
sage: mpmath.quad(lambda x: mpmath.sin(mpmath.sin(x)), [0, 1])
mpf('0.430601063109062904912377355248465809')
```

mpmath.quad 函数可以使用 Gauss-Legendre 方法，或双指数方法（后者默认使用）。要使用的方法可以通过函数 mpmath.quadgl 和 mpmath.quadts 固定。²

Sage 中 mpmath 积分函数的一个重要限制是它们不能操作任意的 Sage 表达式：

```python
sage: mpmath.quad(sin(sin(x)), [0, 1])
Traceback (most recent call last):
...
TypeError: no canonical coercion from <type 'sage.libs.mpmath.ext_main.
    mpf'> to Symbolic Ring
```

然而，情况不像限于自身语法的 PARI/GP 那样严重。确实可以定义求值和转换过程，以便通过 mpmath.quad 对任意函数进行积分³：

```python
sage: g(x) = max_symbolic(sin(x), cos(x))
sage: mpmath.mp.prec = 100
sage: mpmath.quadts(lambda x: g(N(x, 100)), [0, 1])
mpf('0.873912416263038435957979086252')
```

不规则函数（如上面的 J₄ 例子）的积分可能导致显著的精度损失，即使请求很大的精度：

```python
sage: mpmath.mp.prec = 170
sage: mpmath.quadts(lambda x: g(N(x, 190)), [0, 1])
mpf('0.873910975740075205393005981962476344054148354188794')
sage: N(eqtr2(-cos(1), 100))
0.87391125650495533140075211677
```

这里我们只得到 5 位正确数字。尽管如此，我们无法通过建议对区间域进行细分（这里是在不规则点处，参见图 14.5）来帮助 mpmath：

² 这让人想起上面见过的变换 φ : t ↦ tanh(π/2 sinh(t)) 的名称。

³ 想知道我们为什么使用 max_symbolic 的读者可以改用 max 试试，并查看 max_symbolic 的在线帮助。
