

因此，必要条件为

$\partial L/\partial x \Rightarrow 2(x-14)+2\lambda_1(x-11)+2\lambda_2x=0$  
$\partial L/\partial y \Rightarrow 2(y-11)+2\lambda_1(y-13)+2\lambda_2y=0$  
$\partial L/\partial \lambda_1 \Rightarrow (x-11)^2+(y-13)^2+\mu_1^2-49=0$  
$\partial L/\partial \lambda_2 \Rightarrow x+y+\mu_2^2-19=0$  
$\partial L/\partial \mu_1 \Rightarrow 2\lambda_1\mu_1=0$  
$\partial L/\partial \mu_2 \Rightarrow 2\lambda_2\mu_2=0$

在 Maple 中定义函数，然后研究 $\lambda_i$ 和 $\mu_i$ 为零或非零的情况。我们将使用常数的十进制形式来强制浮点运算以简化计算。请记住加载 *Student[MultivariateCalculus]* 包以使 *Gradient* 函数可用。

```
g := (x, y) → (x − 14)^2 + (y − 11)^2:
g₁ := (x, y) → (x − 11)^2 + (y − 13)^2:
g₂ := (x, y) → x + y:
L := (x, y, λ₁, λ₂, μ₁, μ₂) → f(x, y) + λ₁ · (g₁(x, y) + μ₁² − 49.0) + λ₂ · (g₂(x, y) + μ₂² − 19.0):
grad := Gradient(L(x, y, λ₁, λ₂, μ₁, μ₂), [x, y, λ₁, λ₂, μ₁, μ₂]):
NecessaryConditions := [seq(G = 0, G in grad)]:
```

在每种情况下，我们将求解变量 $\mu_i$ 而不是 $\mu_i$ 以降低复杂度。我们还将使用 *RealDomain:-solve* 以避免复数解。将变量列表定义为 *vars* 可减少输入并使命令结构更简洁、更易读。

```
vars := [x, y, λ₁, λ₂, μ₁², μ₂²]:
```

CASE 1.  λ₁ = 0 且 λ₂ = 0。则 μ₁² ≠ 0 且 μ₂² ≠ 0。

```
Case1 := λ₁ = 0, λ₂ = 0:
subs(Case1, NecessaryConditions):
s1 := RealDomain:-solve(%, vars):
Matrix(subs(Case1, s1));
[2x − 28 = 0, 2y − 22 = 0, (x − 11)^2 + (y − 13)^2 + μ₁² − 49.0 = 0,
x + y + μ₂² − 19.0 = 0, μ₁ = 0, μ₂ = 0]
[x = 14, y = 11, 0 = 0, 0 = 0, μ₁² = 36, μ₂² = −6.]
```

此情况不可行，因为 $\mu_2^2=-6$，这表明条件 2，$g_2(x,y)\leq 19$，被违反。通过手工求解该必要条件系统很容易。第一个必要条件给出 $x=14$ 和 $y=11$，然后将 $x$ 和 $y$ 的值代入两个约束很容易得到 $\mu_1^2=36$ 和 $\mu_2^2=-6$。使用 Maple，提供了求解全部四种情况的模板。

## Case 2. $\lambda_1 = 0$ 且 $\lambda_2 \ne 0$。则 $\mu_1^2 \ne 0$ 且 $\mu_2^2 = 0$。

```
Case2 := λ₁ = 0, μ₂ = 0;
subs(Case2, NecessaryConditions);
s2 := RealDomain:-solve(%, vars);
Matrix(subs(Case2, s2));

[2x − 28 + λ₂ = 0, 2y − 22 + λ₂ = 0, (x − 11)² + (y − 13)² + μ₁² − 49.0 = 0,
x + y − 19.0 = 0, 0 = 0]

[x = 11.   y = 8.   0 = 0   λ₂ = 6   μ₁² = 24.   0 = 0.]
```

所有必要条件在点 $(x^*, y^*) = (11, 8)$ 处均得到满足，其中 $\lambda_1 = 0$，$\lambda_2 = 6$，$\mu_1^2 = 24$，且 $\mu_2^2 = 0$。 （请验证！）该点处 $f$ 的值为 18。将 $(11, 8)$ 证明为最优点作为练习留给读者。

## Case 3. $\lambda_1 \ne 0$ 且 $\lambda_2 = 0$。则 $\mu_1^2 = 0$ 且 $\mu_2^2 \ne 0$。

```
Case3 := λ₁ = 0, μ₂ = 0;
subs(Case3, NecessaryConditions);
s3 := RealDomain:-solve(%, vars);
fnormal(Matrix(subs(Case3, s3)), 4);

[2x − 28 + λ₁(2x − 22) = 0, 2y − 22 + λ₁(2y − 26) = 0, (x − 11)² + (y − 13)²
− 49.0 = 0, x + y − 19.0 = 0, 0 = 0]

[x = 5.176   y = 16.88   λ₁ = −1.515   0. = 0.   0. = 0.   μ₂² = −3.059]
[x = 16.892  y = 9.117   λ₁ = −0.4849  0. = 0.   0. = 0.   μ₂² = −6.941]
```

此情况也不可行，因为两种情况下 $\mu_2^2$ 均为负值，这表明条件 2，$g_2$，被违反。

## Case 4. $\lambda_1 \ne 0$ 且 $\lambda_2 \ne 0$。则 $\mu_1^2 = 0$ 且 $\mu_2^2 = 0$。

```
Case4 := μ₁ = 0, μ₂ = 0;
subs(Case4, NecessaryConditions);
s4 := RealDomain:-solve(%, vars);
fnormal(Matrix(subs(Case4, s4)), 4);

[2x − 28 + λ₁(2x − 22) + λ₂ = 0, 2y − 22 + λ₁(2y − 26) + λ₂ = 0,
(x − 11)² + (y − 13)² − 49.0 = 0, x + y − 19.0 = 0, 0 = 0]

[x = 12.77   y = 6.228   λ₁ = −0.4148   λ₂ = 3.926   0. = 0.   0. = 0.]
[x = 4.228   y = 14.77   λ₁ = −1.585    λ₂ = −1.926  0. = 0.   0. = 0.]
```

此情况再次不可行。函数值为 $f(12.77, 6.228) = 24.284$ 且 $f(4.228, 14.77) = 109.720$。这些不是最优值，因为它们不满足局部相对最小值的充分条件。证明 $f(4.228, 14.77)$ 是相对最大值。为什么会发生这种情况？

使用 **Figure 4.21**，该图显示了 $f$ 的等高线、约束条件以及上述情况中发现的六个点，从几何上解释为什么每个点都作为潜在解出现。

```
> Case$_4$: \mu_1^2 = 0, \mu_2^2 = 0 :
> 
> subs(Case$_4$, NecessaryConditions);
> 
> s4 := RealDomain:-solve(%, vars) :
> 
> Matrix(subs(Case$_4$, s4));
> 
> [4x - 8 + \lambda_1 = 0, 2y - 6 + \lambda_1 + \lambda_2 = 0, x + y - 4.0 = 0, y - 2.0 = 0]
> 
> [x = 2.  y = 2.  0 = 0  \lambda_2 = 2.  \mu_1 = 0.  0 = 0.]
```

Case IV 得到了与 Case II 相同的解。

使用 Figure 4.22，该图显示了 $f$ 的等高线、约束条件以及上述情况中发现的点，从几何上解释每个点为何作为潜在解出现。

![](img/0f04050177d82aebd17d3383d7334896_210_0.png)

FIGURE 4.22: Infeasible Solutions and the Real Solution Redux

# Applications Using the Kuhn-Tucker Conditions Method

# Example 4.28. Maximizing Profit from Perfume Manufacturing.

一家公司生产香水。他们最多可按每盎司 $10 的价格购买 1,925 盎司的主要化学原料。一盎司化学原料可生产一盎司香水 #1，加工成本为每盎司 $3。另一方面，化学原料可生产售价更高的香水 #2，加工成本为每盎司 $5。分析部门利用历史数据估计，如果生产 $x$ 盎司，香水 #1 将以 $(30 - 0.01x)$ 美元/盎司的价格出售，而香水 #2 如果生产 $y$ 盎司，则可售价为 $(50 - 0.02y)$ 美元/盎司。公司希望最大化利润。

# MODEL FORMULATION. Let

$x$ = 生产的香水 #1 盎司数  
$y$ = 生产的香水 #2 盎司数  
$z$ = 购买的主要化学原料盎司数

Then

Maximize $P(x,y,z)=x\cdot(30-0.01x)+y\cdot(50-0.02y)-(3x+5y+10z)$  
subject to  
$x+y\le z$  
$z\le 1925$

Solution. 建立模型，定义拉格朗日函数 $L$，并使用前面的示例中的技术。

```
P := (x,y,z) -> x·(30 − 0.01x) + y·(50 − 0.02y) − (3x + 5y + 10z):
g1 := (x,y,z) -> x + y − z:
g2 := (x,y,z) -> z:
L := (x,y,z,λ1,λ2,μ1,μ2) -> P(x,y,z) + λ1·g1(x,y,z) + μ1² − 0.0
    + λ2·(g2(x,y,z) − 1925.0):
grad := Gradient(L(x,z,λ1,λ2,μ1,μ2), [x,y,z,λ1,λ2,μ1,μ2]):
vars := [x,y,z,λ1,λ2,μ1,μ2]:
NecessaryConditions := [seq(G = 0, G in grad)]:
    {NecessaryConditions};
    [
      27 − 0.02x + λ1 = 0
      45 − 0.04y + λ1 = 0
      −10 − λ1 + λ2 = 0
      μ1² + x + y − z = 0
      z + μ2² − 1925.0 = 0
    ]
```

再次，我们准备开始处理四种情况。Maple 的结果摘要如表 4.9 所示。

# TABLE 4.9: Perfume Application’s Four Cases

| Case | x | y | z | λ₁ | λ₂ | μ₁² | μ₂² |
|---|---:|---:|---:|---:|---:|---:|---:|
| I. | — | — | — | 0 | 0 | — | — |
| II. | 1350 | 1125 | 1925 | 0 | 10 | −550 | 0 |
| III. | 850 | 875 | 1725 | −10 | 0 | 0 | 200 |
| IV. | 983.33 | 941.67 | 1925 | −7.333 | 2.667 | 0 | 0 |

*Remarks:*

**Case I.** ∂L/∂z = 0 变为 −10 = 0；此情况不可行。

**Case II.** μ₁² 为负值违反约束 1。

**Case III.** λᵢ ≤ 0 且 μᵢ ≥ 0：**候选解。**

**Case IV.** λᵢs 符号不同因此不是最优点。

我们有一个凹利润函数 P，线性约束，且 λᵢ（λ₁ = −10）对所有绑定约束为负。因此，我们满足了点 (850,875) 为最优解的充分条件。最优生产策略是购买 z = 1725 盎司化学原料并生产 x = 850 盎司香水 #1 和 y = 875 盎司香水 #2，利润为 P = $22,537.50。

考虑 λ₁ 影子价格的意义。我们如何在此场景中解释影子价格？如果我们能以零成本获得额外一盎司（Δ = 1）主要化学原料，利润将提高到约 $22,537.50 + $10。额外一盎司主要化学原料的最大成本是多少仍能带来更高利润？

# Example 4.29. Minimum Variance of Expected Investment Returns.

一家新公司有 $5,000 用于投资以产生计划项目的资金；公司需要赚取约 12% 的利息。一位股票专家建议了三只共同基金 A、B 和 C，公司可投资于其中。基于往年的回报，这些基金似乎相对稳定。预期回报、回报方差以及基金之间的协方差如表 4.10 所示。
