
![](img/d9a4cc12c48f7466f309cbd3c4549c73_237_0.png)

**图 6.3：** 集合“非常矮”“中等”和“非常高”由“矮”和“高”派生而来

## 示例 2：（论域）

- (a) “人”这个集合可以以世界上所有人类作为其论域。或者，它也可以是 4 到 6 英尺之间的数值；这些数值将表示人的身高，如图 6.3 所示。

当我们处理非数值量时，例如味道，它无法用数值尺度来衡量，我们就不能使用数值论域。此时称这些元素取自一个*心理连续统*；这种论域的一个例子可以是{苦、甜、酸、咸、辣，……}。

## 6.6 隶属函数

隶属函数 μ_A(x) 描述基础集 X 的元素 x 在模糊集 A 中的隶属情况，其中 μ_A(x) 可以取一大类函数。合理的函数通常是分段线性函数，例如三角形函数或梯形函数。

隶属函数 μ_A(x) 的隶属度 μ_A(x₀) 描述了对于特殊元素 x=x₀，它属于模糊集 A 的程度等级。该值位于单位区间 [0,1] 内。当然，x₀ 可以同时属于另一个模糊集 B，从而 μ_B(x₀) 表征 x₀ 对 B 的隶属度。这种情况如图 6.4 所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_238_0.png)

**图 6.4：** x₀ 在集合 A 和 B 中的隶属度：μ_A(x₀)=0.75，μ_B(x₀)=0.25

一个50岁的人在“年轻”集合中的隶属情况取决于个人观点。隶属度是一种精确但主观的度量，取决于上下文。模糊隶属函数不同于统计概率分布。下面的吃鸡蛋示例说明了这一点。

## 示例 3：（概率与可能性）

```
Consider the statement “Hans ate X eggs for breakfast”, where X ∈ U = {1,2,3,...,8}. We may associate a probability distribution p by observing Hans eating breakfast for 100 days.

U={1, 2, 3, 4, 5, 6, 7, 8}
p={.1, .8, .1, 0, 0, 0, 0, 0}

A fuzzy set expressing the grade of ease with which Hans can eat eggs may be the following possibility distribution Π

U={1, 2, 3, 4, 5, 6, 7, 8}
Π={1, 1, 1, 1, .8, .6, .4, .2}

Where the possibility for X = 3 is 1, the probability is only 0.1. The example shows, that a possible event does not imply that it is probable. However, if it is probable it must also be possible. You might view a fuzzy membership function as the personal distribution, in contrast with a statistical distribution based on observations.
```

### 6.6.1 隶属函数的类型

原则上，任何形如 A:X→[0,1] 的函数都描述一个与模糊集 A 相关联的隶属函数，该函数不仅取决于所要表示的概念，还取决于其使用情境。函数图形可以具有不同形状，并可能具有特定性质。某个特定形状是否合适，只能在应用情境中确定。然而，在某些情况下，模糊集所捕捉的语义含义对形状变化不太敏感，因而简单函数较为方便。在许多实际情形中，模糊集可以通过参数化函数族显式表示，最常见的是以下几种：

- 1. 三角函数
- 2. Γ函数
- 3. S函数
- 4. 梯形函数
- 5. 高斯函数
- 6. 指数函数

上述常见隶属函数的隶属函数定义在以下各节中给出：

### 三角函数

三角函数的隶属定义如下：

$$
A(x) = \begin{cases}
0, & \text{if } x \le a \\
\frac{x-a}{m-a}, & \text{if } x \in [a,m] \\
\frac{b-x}{b-m}, & \text{if } x \in [m,b] \\
0, & \text{if } x \ge b
\end{cases} \tag{6.3}
$$

其中 m 是模态值，a 和 b 分别表示 A(x) 非零值的下界和上界。有时使用显式突出隶属函数参数的记号更方便；在这种情况下，

$$
A(x; a, m, b) = \max\{\min[(x-a)/(m-a), (b-x)/(b-m)], 0\} \tag{6.4}
$$

### Γ函数

Γ函数的隶属定义如下：

$$
A(x) = \begin{cases}
0, & \text{if } x \le a \\
1 - e^{-k(x-a)^2}, & \text{if } x > a
\end{cases} \quad (6.5)
$$

或

$$
A(x) = \begin{cases}
0, & \text{if } x \le a \\
\frac{k(x-a)^2}{1+k(x-a)^2}, & \text{if } x > a
\end{cases}
$$

其中 k>0。

### S函数

S函数的隶属定义如下：

$$
A(x) = \begin{cases}
0, & \text{if } x \le a \\
2\left(\frac{x-a}{b-a}\right)^2, & \text{if } x \in [a,m] \\
1-2\left(\frac{x-b}{b-a}\right)^2, & \text{if } x \in [m,b] \\
1, & \text{if } x > b
\end{cases} \quad (6.6)
$$

点 \(m=(a+b)/2\) 称为 S 函数的交叉点。

### 梯形函数

梯形函数的隶属定义如下：

$$
A(x) = \begin{cases}
0, & \text{if } x \le a \\
\frac{x-a}{b-a}, & \text{if } x \in [a,b] \\
1, & \text{if } x \in [b,c] \\
\frac{d-x}{d-c}, & \text{if } x \in [c,d] \\
0, & \text{if } x \ge d
\end{cases} \quad (6.7)
$$

使用等价记号，可得

$$
A(x;a,m,n,b)=\max\{\min[(x-a)/(m-a),1,(b-x)/(b-n)],0\} \quad (6.8)
$$

### 高斯函数

高斯函数的隶属定义如下：

$$
A(x) = e^{-\frac{(x-c)^2}{2\sigma^2}}, \text{ where } 2\sigma^2 > 0. \quad (6.9)
$$

![](img/d9a4cc12c48f7466f309cbd3c4549c73_241_0.png)

**图 6.5：** 隶属函数

### 指数函数

指数函数的隶属定义如下：

$$
A(x)=\frac{1}{1+k(x-m)^2},\quad k>1
$$

或

$$
A(x)=\frac{k(x-m)^2}{1+k(x-m)^2},\quad k>0
$$

图 6.5 展示了几个隶属函数。

## 6.6.2 MATLAB 模糊逻辑工具箱中的隶属函数

隶属函数真正必须满足的唯一条件是其取值必须在 0 和 1 之间变化。函数本身可以是任意曲线，其形状可以定义为从简单性、便利性、速度和效率角度适合我们的函数。经典集合可以表示为

$$
A=\{x\mid x>6\}
$$

模糊集是经典集合的扩展。如果 X 是论域，其元素用 x 表示，那么 X 中的模糊集 A 定义为有序对的集合。

$$
A=\{(x,\mu_A(x))\mid x\in X\}
$$

μ_A(x) 称为 x 在 A 中的隶属函数（或 MF）。隶属函数将 X 的每个元素映射为 0 到 1 之间的隶属值。

模糊逻辑工具箱包括 11 种内置隶属函数类型，如图 6.6 所示。这 11 个函数又由若干基本函数构建：分段线性函数、高斯分布函数、S 形曲线，以及二次和三次多项式曲线。按惯例，所有隶属函数名称末尾都带有字母 mf。最简单的隶属函数由直线构成。其中最简单的是三角隶属函数，其函数名为 trimf，它由三个点组成一个三角形。梯形隶属函数 trapmf 具有平顶，只是一个截断的三角形曲线。这些直线型隶属函数的优点是简单。

有两个隶属函数建立在高斯分布曲线上：一个简单高斯曲线，以及两个不同高斯曲线的双侧复合。这两个函数是 gaussmf 和 gauss2mf。广义钟形隶属函数由三个参数指定，函数名为 gbellmf。钟形隶属函数比高斯隶属函数多一个参数，因此如果调整自由参数，它可以逼近非模糊集。由于平滑且记号简洁，高斯和钟形隶属函数是指定模糊集的常用方法。高斯和钟形隶属函数都具有在所有点表示平滑且非零输出的优点。尽管这些曲线具有平滑性，但它们不能指定非对称隶属函数，而非对称隶属函数在某些关键应用中起着至关重要的作用。

S 形隶属函数要么向左开放，要么向右开放。非对称且闭合（即不向左或向右开放）的隶属函数可以用两个 S 形函数合成。除基本的 sigmf 外，还提供两个 S 形函数之差 dsigmf，以及两个 S 形函数之积 psigmf。

模糊逻辑工具箱中的各种隶属函数是基于多项式的曲线。三个相关的隶属函数是 Z、S 和 Pi 曲线，均因其形状而得名。函数 zmf 是向左开放的非对称多项式曲线，smf 是向右开放的镜像函数，pimf 在两端为零、中间上升。在这方面，挑选首选隶属函数有非常大的选择余地。用户也可以使用模糊逻辑工具箱创建自己的隶属函数。

