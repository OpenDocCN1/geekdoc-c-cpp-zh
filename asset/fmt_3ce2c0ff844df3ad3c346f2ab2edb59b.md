
对于 $S$ 域。将问题转化为最小化问题并应用 Karush-Kuhn-Tucker 我们扩展问题到 $n$ 维，即

$$S = \{(x_1, \dots, x_n) : x_1^2 + \dots + x_n^2 \le 1, x_1 \ge 0, \dots, x_n \ge 0\}$$

## 12.5. KARUSH-KUHN-TUCKER 条件 (KKT 条件)

```
$f(x_1, x_2, x_3) = 2x_1 + 3x_2 + 3x_3$
```

需要最大化：

```
$g_1(x_1, x_2, x_3) = 60 - 3x_1 - 2x_2 \ge 0$
$g_2(x_1, x_2, x_3) = 10 + x_1 - x_2 - 4x_3 \ge 0$
$g_3(x_1, x_2, x_3) = 50 - 2x_1 + 2x_2 - 5x_3 \ge 0$
$g_4(x_1, x_2, x_3) = x_1 \ge 0$
$g_5(x_1, x_2, x_3) = x_2 \ge 0$
$g_6(x_1, x_2, x_3) = x_3 \ge 0$
```

因此我们需要最小化：

```
$h(x_1, x_2, x_3) = -f(x_1, x_2, x_3) = -2x_1 - 3x_2 - 3x_3$
```

并将约束条件重写为：

```
$$-60 + 3x_1 + 2x_2 \le 0$$
$-10 - x_1 + x_2 + 4x_3 \le 0$
$-50 + 2x_1 - 2x_2 + 5x_3 \le 0$
```

$x_1 \le 0, -x_2 \le 0, -x_3 \le 0$。因此拉格日函数为：

```
$L(\mathbf{x}, \mathbf{\alpha}) = -2x_1 - 3x_2 - 3x_3 + \alpha_1(-60 + 3x_1 + 2x_2) + \alpha_2(10 - x_1 + x_2 + 4x_3)$
$$\alpha_3(-50 + 2x_1 - 2x_2 + 5x_3) + \alpha_4(-x_1) + \alpha_5(-x_2) + \alpha_6(-x_3).$
```

由此我们得到以下条件：

```
$$-2 + 3\alpha_1 - \alpha_2 - 2\alpha_3 - \alpha_4 = 0$
$-3 + 2\alpha_1 + \alpha_2 - 3\alpha_3 - \alpha_5 = 0$
$-3 + 4\alpha_2 + 5\alpha_3 - \alpha_6 = 0$
$-60 + 3x_1 + 2x_2 \le 0$
$-10 - x_1 + x_2 + 4x_3 \le 0$
$-50 + 2x_1 - 2x_2 + 5x_3 \le 0$
$$\alpha_1(-60 + 3x_1 + 2x_2) = 0$$
$$\alpha_2(-10 - x_1 + x_2 + 4x_3) = 0$$
$$\alpha_3(-50 + 2x_1 - 2x_2 + 5x_3) = 0$
```

以及 $-\alpha_4x_1 = 0, -\alpha_5x_2 = 0, -\alpha_6x_3 = 0, \alpha_1 \geq 0, \alpha_2 \geq 0, \alpha_3 \geq 0, \alpha_4 \geq 0, \alpha_5 \geq 0, \alpha_6 \geq 0$。对这些方程和不等式进行案例研究得到了全局最大点 $(x_1, x_2, x_3) = (8, 18, 0)$ 以及 $\alpha_1 = \alpha_2 = \alpha_6 = 1, \alpha_3 = \alpha_4 = \alpha_5 = 0$。全局最大值为 $f(8, 18, 0) = 70$。该程序也可以通过对问题的可能的整数解进行暴力破解来求解：

```cpp
// integeropt.cpp
#include <iostream>
using namespace std;

int main(void)
{
    int x1, x2, x3;
    int max1 = 10;
    int max2 = 30;
    int max3 = 10;

    int f = 0; int f1;
    int t1 = 0; int t2 = 0; int t3 = 0;

    for(x1=0; x1<=max1; x1++)
        for(x2=0; x2<=max2; x2++)
            for(x3=0; x3<=max3; x3++)
            {
                f1 = 2*x1 + 3*x2 + 3*x3;
                if(f1 > f && ((3*x1+2*x2) <= 60) &&
                    (-x1+x2+4*x3) <= 10) &&
                    (-50+2*x1-2*x2+5*x3) <= 50)
                {
                    f = f1; t1 = x1; t2 = x2; t3 = x3;
                }
            }

    cout << "t1 = " << t1 << endl;
    cout << "t2 = " << t2 << endl;
    cout << "t3 = " << t3 << endl;
    cout << "f = " << f << endl;
}
```

如果函数是非线性且约束条件是非线性的，该程序也可以通过核函数扩展来寻找解。

## 支持向量机

### 12.6.1 引言

支持向量机（Vapnik）是一种用于学习分类器的算法，其灵感来自最大化间隔的思想。通过核函数可以扩展到非线性支持向量机。我们在空间 $\mathbb{R}^m$ 中有 $n$ 个向量 $v_0, v_1, \dots, v_{n-1}$ 来自两个类别的训练数据 $(v_j, y_j) : j = 0, \dots, n-1$，其中 $y_j \in \{+1, -1\}$。目标是学习一个分类误差小且泛化良好的分类规则。

### 12.6.2 决策边界

考虑由集合 $(v_0, y_0), (v_1, y_1), \dots, (v_{n-1}, y_{n-1})$ 表示的两类训练集，其中 $v_j (j = 0 \dots, n-1)$ 是 $m$ 维空间 $\mathbb{R}^m$ 中的向量，$y_j \in \{+1, -1\}$。给定权重 $w$ 和偏置 $b$，假设这些类可以通过以下平行超平面进行分离：

```
$$\mathbf{w}^T v_j + b \ge 1, \quad y_j = +1$$
$$\mathbf{w}^T v_j + b \le -1, \quad y_j = -1$$
```

对于 $j = 0, \dots, n-1$。不等式 (1) 和 (2) 可以写成单个不等式：

```
$$y_j(\mathbf{w}^T v_j + b) \ge 1 \quad j = 0, \dots, n-1.$$
```

对于一组训练数据，存在多个分离平面。支持向量机（Vapnik）的目标是确定最优权重 $w^*$ 和最优偏置 $b^*$，使得对应的超平面以最大间隔分离正负训练数据并产生最好的泛化性能。该超平面被称为最优分离平面。任意超平面的方程为：

```
$$\mathbf{w}^Tx + b = 0$$
```

两个分离平面之间的距离为：

```
$$\gamma(\mathbf{w}, b) = \min_{y_j=+1} \frac{\mathbf{w}^T v_j}{\|\mathbf{w}\|} - \max_{y_j=-1} \frac{\mathbf{w}^T v_j}{\|\mathbf{w}\|}$$$
```

在不等式约束 (3) 下，通过最大化距离或最小化范数 $\|\mathbf{w}\|$ 可以获得最优分离平面，且：

```
$$\gamma_{max} = \gamma(\mathbf{w}^*, b^*) = \frac{2}{\|\mathbf{w}^*\|}$$$
```

拉格日函数的鞍点：

```
$L_P(\mathbf{w}, b, \mathbf{\alpha}) = \frac{1}{2}\mathbf{w}^T\mathbf{w} - \sum_{j=0}^{n-1} \alpha_j y_j(\mathbf{w}^T v_j + b)$
```

其中 $\alpha_j \ge 0$ 是拉格日乘子。该二次规划问题的解要求 $L_P(\mathbf{w}, b, \mathbf{\alpha})$ 关于 $\mathbf{w}$ 和 $b$ 的梯度为零，即：

```
$$\frac{\partial L_P}{\partial \mathbf{w}}|_{\mathbf{w}^*} = 0, \quad \frac{\partial L_P}{\partial b}|_{b^*} = 0.$$
```

得到权重向量：

```
$\mathbf{w}^* = \sum_{j=0}^{n-1} \alpha_j y_j \mathbf{v}_j$
```

以及约束条件：

```
$\sum_{j=0}^{n-1} \alpha_j y_j = 0.$
```

将 $\mathbf{w}^*$ 和约束条件代入 $L_P$ 得到拉格日函数：

```
$L_D(\mathbf{\alpha}) = \sum_{i=0}^{n-1} \alpha_i - \frac{1}{2} \sum_{i=0}^{n-1} \sum_{j=0}^{n-1} \alpha_i \alpha_j y_i y_j \mathbf{v}_i^T \mathbf{v}_j$
```

在约束条件下：

```
$\sum_{j=0}^{n-1} \alpha_j y_j = 0$
$\alpha_j \ge 0, j = 0, \dots, n-1.$
```

函数 $L_D(\alpha)$ 是最大化的。注意 $L_P$ 具有不同的系数，$\alpha_j$ 的非零系数点被称为支持向量。通过 Karush-Kuhn-Tucker 条件（即对整数解的最小化）可以得到 $\alpha$。

## 12.6. SUPPORT VECTOR MACHINE (支持向量机)

**示例**。我们将此技术应用于逻辑集（AND 门）：

| 训练集 | $y_j$ |
| :--- | :--- |
| (0,0) | -1 |
| (0,1) | -1 |
| (1,0) | -1 |
| (1,1) | 1 |

对于该数据集，我们得到：

```
$L(\alpha) = \sum_{i=0}^{3} \alpha_i - \frac{1}{2} \sum_{i=0}^{3} \sum_{j=0}^{3} \alpha_i \alpha_j y_i y_j \mathbf{v}_i^T \mathbf{v}_j$
```

由于约束：

```
$\alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 = 0$
$\alpha_j \ge 0, j = 0, 1, 2, 3$
```

通过 Karush-Kuhn-Tucker 条件（即对整数解的最小化）我们得到 $\tilde{L}(\alpha)$：

```
$L(\alpha) = \alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 - \frac{1}{2} (0\alpha_0^2 + 4\alpha_1^2 + 4\alpha_2^2 + 16\alpha_3^2 + 0\alpha_0\alpha_1 + 0\alpha_0\alpha_2 + 0\alpha_0\alpha_3 + 4\alpha_1\alpha_2 + 8\alpha_1\alpha_3 + 8\alpha_2\alpha_3)$
```

注意，这里 $\mathbf{v}_i^T \mathbf{v}_j$ 是点积。求解 $L(\alpha)$ 得到：

```
$L(\alpha) = \alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 - 2\alpha_1^2 - 2\alpha_2^2 - 8\alpha_3^2 - 2\alpha_1\alpha_2 - 4\alpha_1\alpha_3 - 4\alpha_2\alpha_3$
```

由于 $\alpha_0 = \alpha_3 - \alpha_1 - \alpha_2$，代入后：

```
$L(\alpha) = -3\alpha_1^2 - 3\alpha_2^2 - 9\alpha_3^2 + \alpha_1\alpha_2$
```

（此处计算仅为示例）

我们得到拉格日函数：

```
$L(\alpha) = \alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 - \frac{1}{2} \sum_{i=0}^{3} \sum_{j=0}^{3} \alpha_i \alpha_j y_i y_j \mathbf{v}_i^T \mathbf{v}_j$
```

由于约束：

```
$\alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 = 0$
$\alpha_j \ge 0, j = 0, 1, 2, 3$
```

通过 Karush-Kuhn-Tucker 条件（即对整数解的最小化）我们得到 $\tilde{L}(\alpha)$：

```
$L(\alpha) = \alpha_0 + \alpha_1 + \alpha_2 - \alpha_3 - \frac{1}{2} \sum_{i=0}^{3} \sum_{j=0}^{3} \alpha_i \alpha_j y_i y_j \mathbf{v}_i^T \mathbf{v}_j$
```

# 338 第 12 章 优化

对于 $b^*$，我们得到 $b^* = 3$。区分两个类的决策函数给出：

```
$f(\mathbf{x}) = \text{sgn}(\alpha_1y_1\mathbf{v}_1^T\mathbf{x} + \alpha_2y_2\mathbf{v}_2^T\mathbf{x} + \alpha_3y_3\mathbf{v}_3^T\mathbf{x} + b^*)\\
 = \text{sgn}(2x_2 + 2x_1 - 4(x_1 + x_2) + b^*)\\
 = \text{sgn}(-2x_1 - 2x_2 + 3)\\
 = \text{sgn}(-x_1 - x_2 + \frac{3}{2})...
```

因此我们得到了在 $\mathbb{R}^2$ 中的直线：

```
$x_1 + x_2 = \frac{3}{2}$
```

通过观察数据集也可以看出这一解。

### 12.6.3 非线性决策边界

在在上一个问题中，我们考虑了一个可以用超平面划分的数据集。对于非线性决策边界（Vapnik [260], Vapnik [261], Wang [267]），我们可以按照如下方式扩展方法。数据点 $v_i$ 只出现在标量积内部。我们通过映射将数据点映射到另一个高维空间，称为特征空间：

```
$\mathbf{v}_i^T\mathbf{v}_j = \langle\phi(\mathbf{v}_i), \phi(\mathbf{v}_j)\rangle$
```

其中 $\langle , \rangle$ 表示特征空间中的标量积。映射 $\phi(\mathbf{v}_i)$ 不需要知道，因为它通过选择正定核被隐式定义：

```
$K(\mathbf{v}_i, \mathbf{v}_j) = \langle\phi(\mathbf{v}_i), \phi(\mathbf{v}_j)\rangle$.
```

假设 $K(\mathbf{v}_i, \mathbf{v}_j)$ 是径向函数核的示例：

```
$K(\mathbf{v}_i, \mathbf{v}_j) = \text{exp}(-\|\mathbf{v}_i - \mathbf{v}_j||^2/(2\sigma^2))$
```

以及多项式核：

```
$K(\mathbf{v}_i, \mathbf{v}_j) = (1 + \mathbf{v}_i^T\mathbf{v}_j)^d$.
```

因此，对于给定的核选择的二分类，学习任务涉及拉格朗日的最大化：

```
$L_D(\alpha) = \sum_{i=0}^{n-1} \alpha_i - \frac{1}{2}\sum_{i=0}^{n-1}\sum_{j=0}^{n-1} \alpha_i \alpha_j y_iy_j K(\mathbf{v}_i, \mathbf{v}_j)$
```

受限于约束：

```
$\sum_{i=0}^{n-1} \alpha_iy_i = 0, \quad \alpha_i \geq 0, \quad i=0,1,\dots,n-1$.
```

## 12.6 支持向量机

在找到最优值 $\alpha_i^*$ 后，决策函数给出：

```
$$f(\mathbf{x}) = \text{sign} \sum_{i=0}^{n-1} \alpha_i^* K(\mathbf{x}, \mathbf{v}_i) + b.$$
```

偏置 $b$ 从原始约束条件中得到：

```
$$b = \frac{1}{2} \left( \max_{y_i=-1} \sum_{j=0}^{n-1} \alpha_j y_j K(\mathbf{v}_i, \mathbf{v}_j) + \min_{y_i=+1} \sum_{j=0}^{n-1} \alpha_j y_j K(\mathbf{v}_i, \mathbf{v}_j) \right).$$
```

对于 Karush-Tucker 条件，为了最小值我们需要将 $L_D$ 变为 $-L_D$。考虑到约束，我们得到拉格朗日函数：
