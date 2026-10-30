
## Multivariable Optimization

- 1. Compute the following Hessian matrices:
  - (a) $H=\begin{bmatrix}2&3\\3&5\end{bmatrix}$
  - (b) $H=\begin{bmatrix}4&3\\3&2\end{bmatrix}$
  - (c) $H=\begin{bmatrix}-2&1\\1&-2\end{bmatrix}$
  - (d) $H=\begin{bmatrix}-3&4\\4&-5\end{bmatrix}$
  - (e) $H=\begin{bmatrix}6x&0\\0&2x\end{bmatrix}$
  - (f) $H=\begin{bmatrix}x^2&0\\0&2y\end{bmatrix}$
  - (g) $H=\begin{bmatrix}2&2&3\\2&6&4\\3&4&4\end{bmatrix}$
  - (h) $H=\begin{bmatrix}1&2&2\\2&1&2\\2&2&1\end{bmatrix}$
  - (i) $H=\begin{bmatrix}12x&2&2\\2&-12y&-1\\2&-1&18z\end{bmatrix}$

- 2. Determine the convexity of the given function using the Hessian matrix $H$. Find and classify the function’s critical points.
  - (a) $f(x,y)=x^2+3xy-y^2$
  - (b) $f(x,y)=x^2+y^2$
  - (c) $f(x,y)=-x^2-xy-2y^2$
  - (d) $f(x,y)=3x+5y-4x^2+y^2-5xy$
  - (e) $f(x,y,z)=2x+3y+3z-xy+xz-yz-x^2-3y^2-z^2$

- 3. Determine the values of $a$, $b$, and $c$ such that $g(x,y)=ax^2+bxy+cy^2$ is convex. Determine the values where $g$ is concave.

- 4. Find and classify all the extreme points for the following functions.
  - (a) $f(x,y)=x^2+3xy-y^2$
  - (b) $f(x,y)=x^2+y^2$
  - (c) $f(x,y)=-x^2-xy-2y^2$
  - (d) $f(x,y)=3x+5y-4x^2+y^2-5xy$
  - (e) $f(x,y)=3x^3+7x^2+2x+3y^3+7y^2-y-5$
  - (f) $f(x,y,z)=2x+3y+3z+xy+xz-yz-x^2-3y^2-z^2$

- 5. Find and classify all critical points of $f(x,y)=e^{(x-y)}+x^2+y^2$.

- 6. Find and classify all critical points of $f(x,y)=(x^2+y^2)^{1.5}-4(x^2+y^2)$.

- 7. Three oil wells are located at coordinates $(0,0)$, $(12,6)$, and $(10,20)$. Each well produces an equal amount of oil. A pipeline is to be laid from each oil well to a central refinery located at $(a,b)$. Where should the refinery be located to minimize the total squared Euclidean distance?

$$d^2=\sum_{i=1}^{3}\left[(a-x_i)^2+(b-y_i)^2\right]$$

That is, determine the optimal location $(a,b)$.

In many problems (*most real problems*), it is quite difficult to find the stationary or critical points, and then use them to determine the nature of the stationary point. In this section, we’ll discuss numerical techniques to maximize or minimize a multivariable function.

### Gradient Search Methods

We want to solve the *unconstrained nonlinear programming problem* (NLP) given in Equation 4.1 above. Calculus tells us that if a function $f$ is concave, then the optimal solution—if there is one—will occur at a stationary point $x^*$; i.e., at a point $x^*$ where

$$\frac{\partial f}{\partial x_1}(x^*)=\frac{\partial f}{\partial x_2}(x^*)=\cdots=\frac{\partial f}{\partial x_n}(x^*)=0$$

Finding the stationary points in many problems is quite difficult. The methods of *Steepest Ascent* (maximization) and *Steepest Descent* (minimization) offer an alternative by finding an approximation to a stationary point. We’ll focus on the gradient method, the Steepest Ascent.

Examine the function shown in Figure 4.9.

![](img/0f04050177d82aebd17d3383d7334896_160_0.png)

Figure 4.9: A Surface Defined by a Function

We want to find the maximum point on the surface. If we started at the bottom of the hill, we might proceed by finding the gradient vector, since the gradient is the vector that points “up the hill” in the direction of maximum

## 1. 引言

本文档旨在介绍一种基于深度学习的图像识别方法，该方法在多个标准数据集上取得了优异的性能表现。

## 2. 相关工作

近年来，卷积神经网络（CNN）在计算机视觉领域取得了显著进展。本文方法基于ResNet架构，并引入了注意力机制。

- 方法一：基于区域提议的检测方法
- 方法二：基于回归的检测方法
- 方法三：基于Transformer的检测方法

## 3. 方法

我们提出了一种端到端的训练框架，整体流程如下图所示。

![](img/0f04050177d82aebd17d3383d7334896_161_0.png)

> 注意：训练过程中需要调整学习率，并采用数据增强策略以避免过拟合。

```python
model = ResNet50()
model.train()
```

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局的文档中提取结构化信息。该方法结合了深度学习与传统的规则匹配技术，在准确率和召回率上均取得了显著提升。

在当今信息爆炸的时代，从海量文档中快速、准确地提取关键信息已成为一项至关重要的技术。无论是学术研究、商业分析还是法律文书处理，都依赖于对文档内容的深度理解。

## 2. 相关工作

近年来，基于Transformer的模型在自然语言处理领域取得了巨大成功。然而，将这些模型直接应用于文档解析任务时，往往会忽略文档的视觉布局信息。为此，研究者们提出了多种多模态文档解析模型。

- LayoutLMv3：通过统一文本和图像掩码策略，有效融合了视觉与文本信息。
- Donut：采用端到端的OCR-free架构，直接对文档图像进行理解。
- UDOP：将文档解析任务统一为序列生成问题，简化了模型设计。

## 3. 方法

我们提出了一种基于图神经网络（GNN）的文档解析框架。该框架首先利用视觉特征提取器获取文档图像的区域特征，然后构建区域间的空间关系图，最后通过GNN进行信息传播与聚合，实现精确的语义角色标注。

> 核心思想：将文档解析视为图节点分类问题，充分利用文档的二维空间结构。

## 4. 实验与结果

我们在公开数据集PubLayNet和DocBank上进行了大量实验。实验结果表明，我们的方法在多个评估指标上均优于现有的基线模型。

SAf := SteepestAscent(f, (0, 0), 0.01, graph);

![](img/0f04050177d82aebd17d3383d7334896_163_0.png)

SAf =

|   | Pts | Gradient | Fcn | Grad_Step |
|---|---|---|---|---|
| 1 | [0.; 0.] | [0.; 2.] | 0. | 0.2500 |
| 2 | [0.; 0.5000] | [1.000; 0.] | 0.5000 | 0.5000 |
| 3 | [0.5000; 0.5000] | [0.; 1.000] | 0.7500 | 0.2500 |
| 4 | [0.5000; 0.7500] | [0.500; 0.] | 0.8750 | 0.5000 |
| 5 | [0.7500; 0.7500] | [0.; 0.500] | 0.9375 | 0.2500 |
| 6 | [0.7500; 0.8750] | [0.250; 0.] | 0.9699 | 0.5000 |
| 7 | [0.8750; 0.8750] | [0.; 0.250] | 0.9844 | 0.2500 |
| 8 | [0.8750; 0.9375] | [0.125; 0.] | 0.9922 | 0.5000 |
| 9 | [0.9375; 0.9375] | [0.; 0.125] | 0.9961 | 0.2500 |
| 10 | [0.9375; 0.9688] | [0.063; 0.] | 0.9980 | 0.5000 |
| ⋮ | ⋮ | ⋮ | ⋮ | ⋮ |

14 × 4 DataFrame

To see the list of points generated, use $SAf['Pts'][-1]$; to see just the last point and its function value, use $SAf['Pts'][-1]$, $SAf['Fcn'][-1]$.

```text
SAf['Pts'][-1], SAf['Fcn'][-1];
[[0.9844], [0.9922]], 0.9999
```

The multivariable calculus solution is straightforward to compute by solving the system $\{\partial f/\partial x_1=0,\partial f/\partial x_2=0\}$, and checking $f$'s Hessian at the critical point.

$\frac{\partial f}{\partial x_1}=2x_2-2x_1=0$

$\frac{\partial f}{\partial x_2}=2x_1+2-4x_2=0 \quad\Longrightarrow\quad x^*=\langle x_1,x_2\rangle=\langle1,1\rangle$

The Hessian

$\begin{bmatrix}-2 & 2 \\ 2 & -4\end{bmatrix}$

is negative definite, so the point $x^*=\langle1,1\rangle$ is a maximum with $f(x^*)=1$.

To get a closer approximation with the steepest ascent method, we would make our tolerance smaller. A look at $f$’s contour plot confirms a hill at approximately $(1,1)$ in Figure 4.10.

![](img/0f04050177d82aebd17d3383d7334896_164_0.png)

FIGURE 4.10: Contour Plot of $f$

### Example 4.14. Steepest Ascent Example, II.

Maximize \(g(x) = 55x_1 - 4x_1^2 + 135x_2 - 15x_2^2 - 100\) using the Steepest Ascent method starting at the point \(\{1,1\}\) to within a tolerance of \(\epsilon = 0.01\).

Figure 4.11 provides a visual reference for the maximum.

![](img/0f04050177d82aebd17d3383d7334896_165_0.png)

FIGURE 4.11: Surface Plot of \(g\) Showing Contours

The gradient is \(\nabla g(x) = \langle 55 - 8x_1, 135 - 30x_2\rangle\).

### Iteration 1.

We begin with \(x_0 = \{1,1\}\). Then \(\nabla g(x_0) = \langle 47,105\rangle\). From \(\{1,1\}\), we move in the direction of \(\langle 47,105\rangle\). How far do we go along the line \(L(t) = \{1,1\} + t\langle 47,105\rangle\)? We need to maximize the function

\[g(L(t)) = g(x_0 + t\cdot\nabla g(x_0))\]
\[= -4(1+47t)^2 - 15(1+105t)^2 + 55(1+47t) + 135(1+105t) - 100\]
\[= -174211t^2 + 13234t + 71.\]

This function can also be maximized by simple single-variable calculus:

\[\frac{d}{dt}g(L(t)) = 0 \quad\Longrightarrow\quad t^* = 0.03798\]

The new point \(x_1\) is found by evaluating \(L(t^*) = x_0 + t^*\cdot\nabla g(x_0)\).

\[x_1 = \{1,1\} + t^*\cdot\langle 47,105\rangle = \langle 2.785, 4.988\rangle\]

Since \(|x_1-x_0| > 0.01\), iterate again.

### Iteration 2

Now compute ∇g(x₁) = (32.719, −14.645). We move from (2.785, 4.988) in the direction of (32.719, −14.645). How far do we go along the line L(t) = (2.785, 4.988) + (32.719, −14.645)t? We need to maximize the function

$$g(L(t)) = g(x_1 + t \cdot \nabla g(x_1))$$

$$= 322.33 + 1285.0t - 7499.3t^2.$$

This function can also be maximized by simple single-variable calculus:

$$\frac{d}{dt}g(L(t)) = 0 \quad\Longrightarrow\quad t^* = 0.08567$$

The new point x₂ is found by evaluating L(t*) = x₁ + t* · ∇g(x₁).

$$x_2 = (5.588, 3.733)$$

Since ‖x₂ − x₁‖ > 0.01, we must iterate again.

Use our *SteepestAscent* function to have Maple finish the iterations. Define g as a function of the vector x.

```text
g := x → −4x₁² − 15x₂² + 55x₁ + 135x₂ − 100:
```
