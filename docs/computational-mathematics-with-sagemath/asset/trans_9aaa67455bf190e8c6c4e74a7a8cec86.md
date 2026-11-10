
![](img/99840d73c45ee58b635c4eedc727fd9a_89_0.png)

-   alpha：线条透明度；
-   thickness：线条粗细；
-   linestyle：线条样式，可以用 `':'` 表示点线，用 `'-.'` 表示点划线，或用默认值 `'-'` 表示实线。

为了可视化图形，我们将图形对象赋给一个变量，比如 `g`，然后使用 `show` 命令；此外，我们还可以给定 y 轴的边界（`g.show(ymin=-1, ymax=3)`），或选择纵横比（`g.show(aspect_ratio=1)`），使 `x` 和 `y` 的刻度相等。

得到的图形可以用 `save` 命令导出为多种格式，这些格式由后缀 `.pdf`、`.png`、`.ps`、`.eps`、`.svg` 和 `.sobj` 定义：`g.save(name, aspect_ratio=1, xmin=-1, xmax=3, ymin=-1, ymax=3)`

要在 LaTeX 文档中使用 `includegraphics` 命令包含这样的图形，如果文档要用 `latex` 编译，则应使用 `eps` 后缀（封装 PostScript）；如果文档要用 `pdflatex` 编译，则应使用 `pdf` 后缀（为了获得更好的分辨率，应优先于 `png`）。

让我们在同一幅图上绘制正弦函数及其在 0 处的首批 Taylor 多项式。

```sage
sage: def p(x, n):
....:     return(taylor(sin(x), x, 0, n))
sage: xmax = 15 ; n = 15
sage: g = plot(sin(x), x, -xmax, xmax)
sage: for d in range(n):
....:     g += plot(p(x, 2 * d + 1), x, -xmax, xmax,\
....:     color=(1.7*d/(2*n), 1.5*d/(2*n), 1-3*d/(4*n)))
sage: g.show(ymin=-2, ymax=2)
```

我们还可以创建动画，以观察当 Taylor 多项式的次数增加时，它们如何越来越好地逼近正弦函数。要保留动画，只需将其保存为 `gif` 格式。

### 4.1.2 参数曲线

参数曲线 \((x = f(t),\ y = g(t))\) 可以使用命令 `parametric_plot((f(t), g(t)), (t, a, b))` 可视化，其中 \([a, b]\) 是参数 \(t\) 的取值范围。

让我们展示由以下方程定义的参数曲线：

\[
\begin{cases}
x(t)=\cos(t)+\frac{1}{2}\cos(7t)+\frac{1}{3}\sin(17t),\\
y(t)=\sin(t)+\frac{1}{2}\sin(7t)+\frac{1}{3}\cos(17t).
\end{cases}
\]

```sage
sage: t = var('t')
sage: x = cos(t) + cos(7*t)/2 + sin(17*t)/3
sage: y = sin(t) + sin(7*t)/2 + cos(17*t)/3
sage: g = parametric_plot((x, y), (t, 0, 2*pi))
sage: g.show(aspect_ratio=1)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_91_0.png)

图 4.4 – 方程 \(x(t)=\cos(t)+\frac{1}{2}\cos(7t)+\frac{1}{3}\sin(17t)\)、\(y(t)=\sin(t)+\frac{1}{2}\sin(7t)+\frac{1}{3}\cos(17t)\) 的参数曲线。

### 4.1.3 极坐标中的曲线

极坐标 \(\rho = f(\theta)\) 中的曲线，其中参数 \(\theta\) 在区间 \([a, b]\) 上变化，可以用命令 `polar_plot(rho(theta), (theta,a,b))` 绘制。例如，让我们用图形观察极坐标方程为 \(\rho(\theta)=1+e\cdot\cos(n\theta)\) 的玫瑰线，其中 \(n=20/19\)，\(e\in\{2,1/3\}\)。

```sage
sage: t = var('t'); n = 20/19
sage: g1 = polar_plot(1+2*cos(n*t),(t,0,n*36*pi),plot_points=5000)
sage: g2 = polar_plot(1+1/3*cos(n*t),(t,0,n*36*pi),plot_points=5000)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_92_0.png)

```python
sage: g1.show(aspect_ratio=1); g2.show(aspect_ratio=1)
```

**练习 12.** 当参数 $a$ 从 0 到 2 以 0.1 为步长变化时，绘制极坐标方程 $\rho(\theta)=a+\cos\theta$ 的帕斯卡蜗线族。

### 4.1.4 由隐式方程定义的曲线

要绘制由隐式方程给出的曲线，需要调用函数 `implicit_plot(f(x, y), (x, a, b), (y, c, d))`；不过也可以使用 `complex_plot` 命令，它使我们能够用颜色绘制二元函数的水平集。让我们绘制由隐式方程 $C=\{z\in\mathbb{C},\ |\cos(z^4)|=1\}$ 给出的曲线。

```python
sage: z = var('z')
sage: g1 = complex_plot(abs(cos(z^4))-1,
                       (-3,3), (-3,3), plot_points=400)
sage: f = lambda x, y : (abs(cos((x + I * y) ** 4)) - 1)
sage: g2 = implicit_plot(f, (-3, 3), (-3, 3), plot_points=400)
sage: g1.show(aspect_ratio=1); g2.show(aspect_ratio=1)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_93_0.png)

图 4.6 – 由方程 |cos(z^4)| = 1 定义的曲线 g2。

### 4.1.5 数据绘图

要构造条形图，有两种不同的函数可用。一方面，`bar_chart` 接收一个整数列表作为输入，并绘制竖直条，其高度由列表元素给出（按给定顺序）。width 选项使我们能够选择条宽。

```python
sage: bar_chart([randrange(15) for i in range(20)])
sage: bar_chart([x^2 for x in range(1,20)], width=0.2)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_93_1.png)

图 4.7 – 条形图。

另一方面，要根据浮点数列表绘制随机变量的直方图，我们使用 `plot_histogram` 函数。列表中的值首先被排序并分组到区间中（区间数量由选项 bins 给出，其默认值为 50），每个条的高度与对应值的数量成正比。

```sage
sage: liste = [10 + floor(10*sin(i)) for i in range(100)]
sage: bar_chart(liste)
sage: finance.TimeSeries(liste).plot_histogram(bins=20)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_93_2.png)

(a) 使用 bar_chart 绘图。

(b) 使用 plot_histogram 绘图。

我们想要研究的数据值列表经常以电子表格格式存储。Python 的 csv 包使我们能够导入以 csv 格式存储的这类数据。例如，假设我们想绘制一个班级成绩的直方图，这些成绩位于文件 exam01.csv 的第 3 列。要从这一列提取成绩，我们将使用以下指令（通常，这类文件的前几行包含文本，因此我们用 try 关键字处理可能不匹配的行）：

```python
sage: import csv
sage: reader = csv.reader(open("exam01.csv"))
sage: grades = []; list = []
sage: for line in reader:
....:     grades.append(line[2])
....: for i in grades:
....:     try:
....:         f = float(i)
....:     except ValueError:
....:         pass
....:     else:
....:         list.append(f)
sage: finance.TimeSeries(list).plot_histogram(bins=20)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_94_0.png)

要绘制一组相连的点（或不相连的点），我们使用 `line(p)`（或 `point(p)` 或 `points(p)`）命令，其中 p 是一个由二元素列表（或元组）组成的列表，给出各点的横坐标和纵坐标。

**例。（随机游走）** 从原点 O 出发，一个粒子每 t 秒沿随机方向移动距离 ℓ，且与之前的移动无关。让我们绘制一个粒子轨迹的示例。红线从初始位置延伸到最终位置。

```python
sage: n, l, x, y = 10000, 1, 0, 0; p = [[0, 0]]
sage: for k in range(n):
....:     theta = (2 * pi * random()).n(digits=5)
....:     x, y = x + l * cos(theta), y + l * sin(theta)
....:     p.append([x, y])
sage: g1 = line([p[n], [0, 0]], color='red', thickness=2)
sage: g1 += line(p, thickness=.4); g1.show(aspect_ratio=1)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_95_0.png)

图 4.8 – 随机游走。

**例。（均匀分布序列）** 给定实数序列 \((u_n)_{n\in\mathbb{N}}\)，我们构造折线，其连续顶点是复平面中的点

$$z_N = \sum_{n\leq N} e^{2i\pi u_n}.$$

如果该序列模 1 均匀分布，则折线应表现得像随机游走，因而不会离原点太远。因此，我们可以从折线的图形外观推测其模 1 均匀分布。让我们研究以下情形：

- \(u_n = n\sqrt{2}\) 且 \(N = 200\)，
- \(u_n = n\ln(n)\sqrt{2}\) 且 \(N = 10000\)，
- \(u_n = [n\ln(n)]\sqrt{2}\) 且 \(N = 10000\)，
- \(u_n = p_n\sqrt{2}\) 且 \(N = 10000\)（这里 \(p_n\) 是第 \(n\) 个素数）。

图 4.9 按如下方式得到（这里以 \(u_n = n\sqrt{2}\) 为例）：

```
sage: length = 200; n = var('n')
sage: u = lambda n: n * sqrt(2)
sage: z = lambda n: exp(2 * I * pi * u(n)).n()
sage: vertices = [CC(0, 0)]
sage: for n in range(1, length):
....:     vertices.append(vertices[n - 1] + CC(z(n)))
sage: line(vertices).show(aspect_ratio=1)
```

我们看到，曲线 4.9a 惊人地规则，这表明 \(n\sqrt{2}\) 模 1 的均匀分布是确定性的。在 \(u_n = n\ln(n)\sqrt{2}\) 的情形中，这些值模 1 看起来似乎是随机的。然而，相关曲线 4.9b 却结构分明。曲线 4.9c 具有与第二条曲线相同类型的结构。最后，曲线 4.9d 显示了素数模 \(1/\sqrt{2}\) 的完全不同性质：螺旋消失了，外观看起来非常类似于随机游走 \(u_n\)（图 4.8）。因此，看起来“素数利用了赋予它们的所有随机性……”

关于这些曲线的详细解释，我们请读者参阅 Gérald Tenenbaum 和 Michel Mendès France 的书（法文）*Les nombres premiers* [TMF00]。

**练习 13**（绘制递推序列的项）。我们考虑由下式定义的序列 \((u_n)_{n\in\mathbb{N}}\)：

$$u_0 = a, \qquad \forall n \in \mathbb{N},\; u_{n+1} = \left|u_n^2 - \frac{1}{4}\right|.$$

通过构造点列表 \([(u_0, 0), (u_0, u_1), (u_1, u_1), (u_1, u_2), (u_2, u_2), \ldots]\) 来图形化表示该序列的行为，其中 \(a \in \{-0.4, 1.1, 1.3\}\)。

### 4.1.6 显示微分方程的解

我们可以组合上述命令来表示微分方程或方程组的解。要符号求解一个常微分方程，需要调用
