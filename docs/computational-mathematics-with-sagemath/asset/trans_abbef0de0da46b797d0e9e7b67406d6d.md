
![](img/99840d73c45ee58b635c4eedc727fd9a_96_0.png)

(a) 情形 \(u_n = n\sqrt{2}\)。

(b) 情形 \(u_n = n\ln(n)\sqrt{2}\)。

(c) 情形 \(u_n = \ln\ln(n)\sqrt{2}\)。

(d) 情形 \(u_n = p_n\sqrt{2}\)。

图 4.9 — 均匀分布序列。

desolve 函数将在第 10 章中更详细地研究。为了数值求解微分方程，Sage 提供了几种工具：`desolve_rk4`（使用与 `desolve` 相同的语法，足以求解本科水平的微分方程）、`odeint`（调用 SciPy 包），最后是 `ode_solver`（调用 GSL 库，其用法在第 14.2 节中详述）。`desolve_rk4` 和 `odeint` 函数返回点列表，使用 `line` 命令很容易绘制；本节将用它们绘制数值解。

**示例。**（*一阶线性微分方程*）我们来绘制微分方程 \(xy' - 2y = x^3\) 的积分曲线。

```sage
sage: x = var('x'); y = function('y')
sage: DE = x*diff(y(x), x) == 2*y(x) + x^3
sage: desolve(DE, [y(x),x])
(_C + x)*x^2
sage: sol = []
sage: for i in srange(-2, 2, 0.2):
....:     sol.append(desolve(DE, [y(x), x], ics=[1, i]))
....:     sol.append(desolve(DE, [y(x), x], ics=[-1, i]))
sage: g = plot(sol, x, -2, 2)
sage: y = var('y')
sage: g += plot_vector_field((x, 2*y+x^3), (x,-2,2), (y,-1,1))
sage: g.show(ymin=-1, ymax=1)
```

为了减少计算时间，这里更好的做法是“手工”定义方程的通解，并创建一个特解列表（如习题 14 的解答中所做的那样），而不是用不同的初始条件多次求解微分方程。我们也可以计算该方程的数值解（使用 `desolve_rk4` 函数）来绘制其积分曲线：

```sage
sage: x = var('x'); y = function('y')
sage: DE = x*diff(y(x), x) == 2*y(x) + x^3
sage: g = Graphics()                         # creates an empty graph
sage: for i in srange(-2, 2, 0.2):
....:     g += line(desolve_rk4(DE, y(x), ics=[1, i]), \
....:         step=0.05, end_points=[0,2])
....:     g += line(desolve_rk4(DE, y(x), ics=[-1, 1]), \
....:         step=0.05, end_points=[-2,0]))
sage: y = var('y')
sage: g += plot_vector_field((x, 2*y + x^3), (x,-2,2), (y,-1,1))
sage: g.show(ymin=-1, ymax=1)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_97_0.png)

(a) 符号解。　　　　　　　　　(b) 数值解。

图 4.10 — \(xy' - 2y = x^3\) 的积分曲线。

如上例所示，desolve_rk4 函数接受一个微分方程（或显式形式 \(y' = f(y,x)\) 中方程的右端 \(f\)）、未知函数的名称、初始条件、步长以及求解区间作为输入。可选参数 output 使我们能够指定输出类型：默认值 'list' 返回列表（如果像我们的示例那样要组合图形，这很有用），'plot' 输出解的图形，'slope_field' 添加积分曲线斜率图。

**习题 14.** 绘制方程 \(x^2 y' - y = 0\) 的积分曲线，其中 \(-3 \le x \le 3\) 且 \(-5 \le y \le 5\)。

现在给出 SciPy 包中 `odeint` 函数的一个示例。

**示例。**（一阶非线性微分方程）我们来绘制方程 \(y'(t)+\cos(y(t)\cdot t)=0\) 的积分曲线。

```sage
sage: import scipy; from scipy import integrate
sage: f = lambda y, t: -cos(y * t)
sage: t = srange(0, 5, 0.1); p = Graphics()
sage: for k in srange(0, 10, 0.15):
....:     y = integrate.odeint(f, k, t)
....:     p += line(zip(t, flatten(y)))
sage: t = srange(0, -5, -0.1); q = Graphics()
sage: for k in srange(0, 10, 0.15):
....:     y = integrate.odeint(f, k, t)
....:     q += line(zip(t, flatten(y)))
sage: y = var('y')
sage: v = plot_vector_field((1, -cos(x*y)), (x,-5,5), (y,-2,11))
sage: g = p + q + v; g.show()
```

![](img/99840d73c45ee58b635c4eedc727fd9a_98_0.png)

**图 4.11** — \(y'(t)+\cos(y(t)\cdot t)=0\) 的积分曲线。

odeint 函数接受微分方程 \(y' = f\) 的右端 \(f\)（假定为显式形式）、一个或多个初始条件，以及求解区间作为参数；它返回一个类型为 `numpy.ndarray` 的数组，可用已在 §3.3.2 中见过的 `flatten` 命令¹转换。得到的列表随后使用 `zip` 命令与数组 \(t\) 组合，并显示近似解。为了添加与积分曲线相切的向量场，我们使用了 `plot_vector_field` 命令。

**示例。**（Lotka–Volterra 捕食者-猎物模型）我们希望用图形表示一组猎物和捕食者根据 Lotka–Volterra 方程组演化时的数量变化：

$$
\begin{cases}
\dfrac{du}{dt} = au - buv,\\[4pt]
\dfrac{dv}{dt} = -cv + dbuv,
\end{cases}
$$

其中 \(u\) 是猎物数量（例如兔子），\(v\) 是捕食者数量（例如狐狸）。此外，参数 \(a\)、\(b\)、\(c\)、\(d\) 描述种群演化：\(a\) 是在没有狐狸捕食时兔子的自然增长，\(b\) 是狐狸捕杀兔子时兔子的减少量，\(c\) 是没有兔子可吃时狐狸的减少量，最后 \(d\) 表示每出现一只新狐狸需要多少只兔子。

```sage
sage: import scipy; from scipy import integrate
sage: a, b, c, d = 1, 0.1, 1.5, 0.75
sage: def dX_dt(X, t=0):                      # returns the population variation
....:     return [a*X[0] - b*X[0]*X[1], -c*X[1] + d*b*X[0]*X[1]]
sage: t = srange(0, 15, .01)                  # time scale
sage: X0 = [10, 5]                            # initial conditions: 10 rabbits and 5 foxes
sage: X = integrate.odeint(dX_dt, X0, t)      # numerical solution
sage: rabbits, foxes = X.T                    # short cut for X.transpose()
sage: p = line(zip(t, rabbits), color='red')  # number of rabbits graph
sage: p += text("Rabbits", (12,37), fontsize=10, color='red')
sage: p += line(zip(t, foxes), color='blue')  # idem for foxes
sage: p += text("Foxes", (12,7), fontsize=10, color='blue')
sage: p.axes_labels(['time', 'population']); p.show(gridlines=True)
```

上面的指令显示了兔子和狐狸数量随时间的变化（图 4.12，左），下面的指令显示了向量场（图 4.12，右）：

```sage
sage: n = 11;  L = srange(6, 18, 12 / n); R = srange(3, 9, 6 / n)
sage: CI = zip(L, R)              # list of initial conditions
sage: def g(x,y):
....:     v = vector(dX_dt([x, y]))   # for a nicer grid, we
....:     return v/v.norm()          # normalise the vector field
sage: x, y = var('x, y')
sage: q = plot_vector_field(g(x, y), (x, 0, 60), (y, 0, 36))
sage: for j in range(n):
....:     X = integrate.odeint(dX_dt, CI[j], t)       # resolution
....:     q += line(X, color=hue(.8*float(j)/(1.8*n))) # graph plot
sage: q.axes_labels(["rabbits","foxes"]); q.show()
```

![](img/99840d73c45ee58b635c4eedc727fd9a_100_0.png)

图 4.12 — 捕食者-猎物系统的研究。

**习题 15**（捕食者-猎物模型）。使用 `desolve_system_rk4` 而不是 `odeint` 重新绘制图 4.12 的左图。

**习题 16**（一个自治微分系统）。绘制以下微分系统的积分曲线：

$$
\begin{cases}
\dot{x}=y,\\
\dot{y}=0.5y-x-y^2.
\end{cases}
$$

**习题 17**（带马格努斯效应的圆柱绕流）。我们将半径为 \(a\) 的圆柱周围的简单流动与参数为 \(\alpha\) 的涡旋叠加，后者会改变周向速度分量。我们在以圆柱为中心的坐标系中工作，使用平面 \(z=0\) 中的柱坐标，即极坐标。速度分量于是为：

$$v_r=v_0\cos(\theta)\left(1-\frac{a^2}{r^2}\right)\qquad\text{and}\qquad v_\theta=-v_0\sin(\theta)\left(1+\frac{a^2}{r^2}\right)+\frac{2\alpha a v_0}{r}.$$

流线（由于流动是定常的，因此与轨迹相同）平行于速度。我们寻找流线的参数表达式；因此必须求解微分方程组：

$$\frac{dr}{dt}=v_r\qquad\text{and}\qquad\frac{d\theta}{dt}=\frac{v_\theta}{r}.$$

通过使用以圆柱半径 \(a\) 缩放的坐标，我们可以假设 \(a=1\)。绘制 \(\alpha\in\{0.1,0.5,1,1.25\}\) 时的流线。

