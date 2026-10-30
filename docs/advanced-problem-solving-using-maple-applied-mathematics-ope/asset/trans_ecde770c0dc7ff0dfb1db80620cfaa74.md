

> Hf := Hessian(f(x1,x2), [x1,x2]);
  IsDefinite(Hf, query = 'positive_definite');
  IsDefinite(Hf, query = 'negative_definite');
  IsDefinite(Hf, query = 'indefinite');

                         Hf := [ 2  0 ]
                               [ 0  6 ]
                               true
                               false
                               false

> Hg := Hessian(g(x1,x2), [x1,x2]);
  IsDefinite(Hg, query = 'positive_definite');
  IsDefinite(Hg, query = 'negative_definite');
  IsDefinite(Hg, query = 'indefinite');

                         Hg := [ -2   1 ]
                               [  1  -6 ]
                               false
                               true
                               false

> Hh := Hessian(g(x1,x2), [x1,x2]);
  IsDefinite(Hh, query = 'positive_definite');
  IsDefinite(Hh, query = 'negative_definite');
  IsDefinite(Hh, query = 'indefinite');

                         Hh := [ 2   1 ]
                               [ 1  -6 ]
                               false
                               false
                               true

Maple 有多个计算函数 Hessian 的函数。*Hessian* 命令的版本在 *Student[VectorCalculus], Vector-Calculus,* 和 *LinearAlgebra* 包中。查阅 Maple 的帮助页面以帮助您决定在特定情况下使用哪个版本最合适。

在更一般的情况下，如果函数包含幂高于 2 的项或包含超越函数，例如 $x_1x_2^2$ 或 $\sin(x_1x_2)$，Hessian 将包含变量的项。那么将驻点分类为最大值、最小值或鞍点时的 definiteness 分析会稍微复杂一些。

对于两个变量，我们使用 *二次型*

$$Q(x_1,x_2) = [x_1\quad x_2] \times H \times \begin{bmatrix}x_1\\x_2\end{bmatrix}$$

来测试 Hessian 矩阵。一般来说，我们使用 $Q(\vec{x}) = \vec{x}^{T}H\,\vec{x}$。然后定义

## 定义 4.2. 矩阵的 Definiteness。

设 $H$ 为 $f$ 的 Hessian 矩阵。则 $H$ 是

+   1. **正定** iff $H > 0$ 对于 domain$(f)$ 中每个非零向量 $z$，
+   2. **半正定** iff $H \geq 0$ 对于 domain$(f)$ 中每个非零向量 $z$，
+   3. **负定** iff $H < 0$ 对于 domain$(f)$ 中每个非零向量 $z$，
+   4. **半负定** iff $H \leq 0$ 对于 domain$(f)$ 中每个非零向量 $z$，
+   5. **不定** 否则。

我们可以将 definiteness 与主子式的符号联系起来。

**正定：** 所有 leading principal minors 均为正。

**半正定：** 所有 leading principal minors 均非负（某些可能为零）。

**负定：** leading principal minors 遵循 $(-1)^k$ 的符号，其中 $k$ 为 leading principal minor 的阶数。偶数阶 leading principal minors 为正，奇数阶 leading principal minors 为负。

**半负定：** 所有非零 leading principal minors 遵循 $(-1)^k$ 的符号，其中 $k$ 为 leading principal minor 的阶数。偶数阶非零 leading principal minors 为正，奇数阶非零 leading principal minors 为负。某些可能为零。

**不定：** 某些 leading principal minors 不遵循上述任何规则。

如果 Hessian 也是自变量的函数，其 definiteness 可能会从一个点到另一个点变化。要测试点 $x^*$ 处的 Hessian 的 definiteness，将 Hessian 在该点求值。例如，在矩阵

```
$$H(x_1,x_2)=\begin{bmatrix}2x_1 & x_2 \\ x_2 & 4\end{bmatrix},$$
```

中，$x_1$ 和 $x_2$ 的具体值决定了 $H$ 在 $[x_1,x_2]$ 处是正定、半正定、负定、半负定还是不定。**给出每种情况的一个例子！**

*表 4.2* 总结了 Hessian 矩阵 definiteness 与驻点（极值）分类为最大值、最小值、鞍点或“不确定”之间的关系。

## 表 4.2：Hessian Definiteness 摘要

| 行列式：$H_k = k$ 阶 leading principal minors | 结果 | 关于驻点的结论 |
|---|---|---|
| 所有 $H_k > 0$ | 正定，$f$ 为凸 | 最小值 |
| 所有 $H_k \geq 0$ | 半正定，$f$ 为凸 | 局部最小值 |
| $\operatorname{sgn}(H_k)=\operatorname{sgn}((-1)^k)$ | 负定，$f$ 为凹 | 最大值 |
| $\operatorname{sgn}(H_k)=\operatorname{sgn}((-1)^k)$ 或某些，但不是全部，$H_k=0$ | 半负定，$f$ 为凹 | 局部最大值 |
| $H_k$ 不全为 0，但无上述情况 | 不定，$f$ 既非 | 鞍点 |
| $H_k=0$ 对所有 $k$ | 不定 | *不确定* |

## 示例 4.7. 使用摘要表。

+   1. 假设函数 $f(x_1,x_2)$ 的 Hessian 给出为
   
   $$H(x_1,x_2):=\begin{bmatrix}-2 & -1\\-1 & -4\end{bmatrix}$$
   
   1 阶 leading principal minors 为 $-2$ 和 $-4$。2 阶 leading principal minor 为 $|H(x_1,x_2)|=7$。由于一阶为负，二阶为正，leading principal minors 遵循 $(-1)^k$ 的符号。摘要表表明 $f$ 为凹且找到的驻点为最大值。此 Hessian 矩阵为负定。
   
   ```matlab
   >> H := Matrix([-2, -1], [-1, -4]);
   H := [-2  -1
         -1  -4]
   >> IsDefinite(H, query = 'negative_definite');
   true
   ```

+   2. 假设函数 $f$ 的 Hessian 给出为
   
   $$H:=\begin{bmatrix}3 & 2 & 1\\6 & 5 & 4\\9 & 8 & 7\end{bmatrix}$$

1 阶 leading principal minors 为 3、5 和 7。2 阶 leading principal minors 为 3、12 和 3。3 阶 leading principal minor，即 $H$ 的行列式，为 0。所有 leading principal minors 均为正或零。摘要表表明如果 $f$ 为凸且任何对应的驻点将为局部最小值。此 Hessian 矩阵为半正定。

```
> H := Matrix([[3, 2, 1], [6, 5, 4], [9, 8, 7]]);

H :=
\begin{bmatrix}
3 & 2 & 1 \\
6 & 5 & 4 \\
9 & 8 & 7
\end{bmatrix}

> IsDefinite(H, query = 'positive_definite');
        false
> IsDefinite(H, query = 'positive_semidefinite');
        true
```

3. 假设函数 $f$ 的 Hessian 给出为

```
$$H := \begin{bmatrix}-2 & -4 \\ -4 & -3\end{bmatrix}$$
```

1 阶 leading principal minors 为 $-2$ 和 $-3$。2 阶 leading principal minor 为 $|H| = -10$。由于一阶和二阶均为负，摘要表表明 Hessian 为不定且找到的驻点为鞍点。

```
> H := Matrix([[-2, -4], [-4, -3]]);

H :=
\begin{bmatrix}
-2 & -4 \\
-4 & -3
\end{bmatrix}

> IsDefinite(H, query = 'indefinite');
        true
```

## 4.2 无约束优化：示例

上一节的定义和定理被用于解决以下示例中的一组无约束优化问题。在下面的 Maple 会话中，请记住从新文档开始并加载 Student[VectorCalculus] 和 Student[LinearAlgebra] 包。

## 示例 4.8. 寻找极值，I。

求并分类

$$f(x_1,x_2)=55x_1-4x_1^2+135x_2-15x_2^2-100.$$

的所有驻点。

## 深度学习

深度学习是机器学习的一个子集，使用具有多层的人工神经网络来模拟数据中的复杂模式。它推动了计算机视觉、自然语言处理和语音识别方面的突破。

-   - 用于图像数据的卷积神经网络（CNNs）
-   - 用于序列数据的循环神经网络（RNNs）
-   - 用于基于注意力的建模的 Transformer

![](img/0f04050177d82aebd17d3383d7334896_150_0.png)

| 模型 | 精度 |
|-------|----------|
| CNN   | 98.2%    |
| RNN   | 95.7%    |
| Transformer | 99.1% |

```
```python
import torch
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 256),
    nn.ReLU(),
    nn.Linear(256, 10)
)
```
```

> > "深度学习是 21 世纪的电力。" — Andrew Ng

该领域继续快速发展，使生成式 AI、自动驾驶和个性化医疗等新应用成为可能。

