
## 参考文献和建议进一步阅读

Abramowitz, M. and I. A. Stegun (Eds.). 1972. Handbook of Mathematical Functions: With Formulas, Graphs, and Mathematical Tables. New York: Dover Publications.

Beu, T. A. 2004. Numerical Calculus in C (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.

Boole, G. and J. F. Moulton. 2003. A Treatise on the Calculus of Finite Differences (2nd ed.). New York: Dover Publications.

Burden, R. and J. Faires. 2010. Numerical Analysis (9th ed.). Boston: Brooks/Cole, Cengage Learning.

Demidovich, B. and I. Maron. 1987. Computational Mathematics (4th ed.). Moscow: MIR Publishers.

Fitts, D. 2002. *Principles of Quantum Mechanics: As Applied to Chemistry and Chemical Physics.* Cambridge: Cambridge University Press.

Guenther, R. D. 1990. *Modern Optics.* New York: John Wiley & Sons.

Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. *Numerical Recipes: The Art of Scientific Computing* (3rd ed.). Cambridge: Cambridge University Press.

Ralston, A. and P. Rabinowitz. 2001. *A First Course in Numerical Analysis* (2nd ed.). New York: Dover Publications.

Romberg, W. 1955. Vereinfachte numerische Integration (Simplified Numerical Integration (in German)). *Det Kongelige Norske Videnskabers Selskab Forhandlinger (Trondheim)* 28, 30–36.

Stroud, A. 1971. *Approximate Calculation of Multiple Integrals.* Englewood Cliffs: Prentice-Hall.

Stroud, A. and D. Secrest. 1966. *Gaussian Quadrature Formulas.* Englewood Cliffs: Prentice-Hall.

# 11 蒙特卡洛方法

## 11.1 引言

求解数值分析问题的经典方法依赖于严格的算法，该算法对于给定的输入，在预定数量的步骤内提供明确的解。这种方法本质上是确定性的，因为其实现在重复运行、完成相同数量的操作后预期会得到相同的结果。然而，对于应用科学和工程中的众多前沿问题，确定性算法的复杂性使得在合理的时间内进行计算变得不可行。

现代科学的某些领域关注由大量耦合组件组成的系统，这些组件有时还容易受到波动的影响。这种复杂系统可以像自旋集合、生物种群或星系一样不同。它们的表征通常通过高维积分来完成。一个典型例子是 N 个相互作用粒子的经典正则配分函数，

Z = ∫ ⋯ ∫ d³r₁ ⋯ d³r_N exp[ − 1/(k_B T) E(r₁ ⋯ r_N) ] ,

其中 E(r₁ ⋯ r_N) 是系统的总能量，r_i 为粒子 i 的位置，T 是系统温度，k_B 为玻尔兹曼常数。即使对于实际感兴趣的最低粒子数，通过任何经典求积方法对这个 3N 维积分进行求值也是完全不可行的。事实上，考虑到适中的值 N = 20 且每个维度仅有 10 个积分点，所需的基本运算次数将达到 10⁶⁰ 的数量级。即使使用最新的百亿亿次超级计算机，其每秒可执行超过 10¹⁶ 次浮点运算，计算也需要大约 3 · 10³⁶ 年！

对于复杂的高维问题，确定性方法的一种有益替代方案是所谓的随机方法，其基于概率论中的大数定律。在这里，感兴趣的量被定义为随机变量的期望值，或者换句话说，在某些概率假设下，考虑大量随机变量的平均值以获得所求量的概率估计。这些技术通常被称为蒙特卡洛方法，具有内在的非确定性特征，因为它们使用随机实验的结果，并且在统计误差范围内，在不同运行中表现出不同的行为。本质上，与确定性地覆盖所涉及函数的域相比，蒙特卡洛方法随机地采样这些域。一般而言，随机技术不需要真正的随机数，而是使用伪随机序列，但具有高度的均匀性和低的序列相关性。

开创性的蒙特卡洛方法由 Stanislaw Ulam、Nicholas Metropolis 和 John von Neumann 于 1940 年代末在洛斯阿拉莫斯国家实验室开发，并因其赌博般的底层原理而以著名的蒙特卡洛赌场命名。随着高性能计算机的出现，蒙特卡洛方法开始展现其优势，因为获得足够精确的结果通常意味着需要进行大量的运算并传递海量数据。与确定性数值方法相比，蒙特卡洛方法的成功主要归功于计算工作量随问题规模增大时更有利的缩放。在事实上，虽然它是单维积分最无效的求积方法，但随着维度的增加，蒙特卡洛方法逐渐超过了确定性方法。

蒙特卡洛方法的主要用途大致可分为优化、数值积分和从概率分布中生成样本。在应用数学中，蒙特卡洛方法的效率在诸如具有复杂边界的多维积分的求值、大型线性系统的求解或微分方程狄利克雷问题的求解等应用中最为明显。本章我们特别关注函数的积分。

## 11.2 函数的积分

在蒙特卡洛方法中，函数 *f* 在多维域 𝒟 上的积分简单地通过函数算术平均值与域体积 *V* 的乘积来估计，

$$\int_{\mathcal{D}} f\,dV \approx V\langle f\rangle \pm \sigma,$$  (11.1)

其中平均值 ⟨*f*⟩ 是针对 *n* 个随机点 **x**₁, …, **x**ₙ 计算的，这些点 *随机* 且 *均匀* 地采样域 𝒟。与积分结果相关的统计不确定性由 *标准偏差* σ 指定，

$$\sigma = V\sqrt{\frac{\langle f^2\rangle-\langle f\rangle^2}{n}}=\frac{V}{\sqrt n}\sigma_f,$$  (11.2)

或其平方 σ²，称为 *方差*。标准偏差，

$$\sigma_f=\sqrt{\left\langle(f-\langle f\rangle)^2\right\rangle}=\sqrt{\langle f^2\rangle-\langle f\rangle^2},$$

出现在上述表达式中，衡量被积函数 *f* 在积分域内与其均值 ⟨*f*⟩ 的偏差。平均值 ⟨*f*⟩ 和 ⟨*f*²⟩ 分别由

$$\langle f\rangle=\frac{1}{n}\sum_{i=1}^{n}f(\mathbf{x}_i),\qquad \langle f^2\rangle=\frac{1}{n}\sum_{i=1}^{n}f^2(\mathbf{x}_i).$$  (11.3)

给出。

标准偏差 σ 的表达式 11.2 说明了蒙特卡洛积分的两个重要特征。第一个涉及不确定性 σ 的 *n*⁻¹ᐟ² 缩放。正如预期的那样，采样点数越大，积分结果越精确，即使 σ 的减小相当缓慢。相比之下，基本梯形公式的误差——牛顿-科茨求积族中最原始的公式——具有 *n*⁻² 依赖性，并且在 *一维* 积分中实现相同精度所需的数值工作量明显低于蒙特卡洛方法。然而，经典求积公式运算计数更有利的缩放优势在多维情况下消失。可以很容易看出，基于常规一维积分器、每个维度有 *n* 次函数求值的 *d* 维积分方案的余项随 *n*⁻²ᐟᵈ 增大。相反，不确定性 σ 的 *n*⁻¹ᐟ² 依赖性与维度无关，因此，对于 *d* > 4，蒙特卡洛方法变得更有效。

在 C/C++ 编译器的任何标准实现中至少为 32,767。为了在标准区间 [0,1) 中生成实随机数，`rand()` 返回的值只需除以 `(RAND_MAX+1)`：

```
// Generates random floating point numbers in the range [0,1)

#define random() ((double)rand()/(RAND_MAX+1))
```

以下将假设宏 `seed()` 和 `random()` 已包含在头文件 `random.h` 中。

作为蒙特卡洛求积的第一个、初等的例子，我们考虑积分

∫₀¹ x e⁻ˣ dx = 1 − 2e⁻¹ ≈ 0.26424. (11.7)

相应的程序（列表 11.1）实际上并未将蒙特卡洛方法作为独立过程实现，因为此类例程缺乏实际兴趣，正如使用蒙特卡洛方法进行一维积分的整个想法一样。相反，主程序保持简单，旨在强调一般概念。这里，`n` 表示采样点数，`s` 是积分估计值，`sigma` 表示相关的标准偏差。变量 `f1` 和 `f2` 分别用于存储平均值 ⟨f⟩ 和平均平方函数 ⟨f²⟩。

程序执行结果针对不同的积分点数 `n` 编译在表 11.1 的前三列中。随着 `n` 的增加，积分估计值趋向于精确值，并且相关的不确定性估计 σ 明显减小。正如下一节所示，标准偏差 σ 确实按 n⁻¹/² 缩放，并且与任何经典一维求积公式的比较证明了后者明显更有效。

### 列表 11.1 函数的蒙特卡洛积分（Python 编码）

```
# One-dimensional Monte Carlo quadrature

from math import *

from random import *

def func(x): return x * exp(-x)                     # integrand

#### main

n = eval(input("n = "))                           # number of sampling points

seed()

f1 = f2 = 0e0                                      # quadrature with uniform sampling

for i in range(1,n+1):

    x = random()                                   # RNG with uniform distribution

    f = func(x)                                    # integrand

    f1 += f; f2 += f * f                           # sums

f1 /= n; f2 /= n                                   # averages

s = f1                                             # integral

sigma = sqrt((f2-f1*f1)/n)                         # standard deviation

print("s = ",s,"+/-",sigma)
```

**表 11.1** 蒙特卡洛估计的积分 \(I=\int_0^1 xe^{-x}\,dx\) 及其相关标准偏差 \(\sigma\)，使用分布 \(w(x)=1\) 和分别 \(w(x)=(3/2)x^{1/2}\) 的随机序列计算

| \(n\) | \(w(x)=1\): \(I\) | \(w(x)=1\): \(\sigma\) | \(w(x)=(3/2)x^{1/2}\): \(I\) | \(w(x)=(3/2)x^{1/2}\): \(\sigma\) |
|---:|---:|---:|---:|---:|
| 10 | 0.25108 | 0.03855 | 0.26860 | 0.00727 |
| 100 | 0.26252 | 0.01085 | 0.26397 | 0.00285 |
| 1000 | 0.26622 | 0.00336 | 0.26458 | 0.00089 |
| 10,000 | 0.26544 | 0.00105 | 0.26423 | 0.00027 |

经典一维求积公式的比较证明了后者明显更有效。虽然蒙特卡洛积分仍可改进，但其全部潜力只有在多维积分的求值中才显现出来。

## 11.3 重要性采样

鉴于蒙特卡洛求积的不确定性 \(\sigma\)（11.2）与衡量被积函数与其平均值偏差的被积函数方差 \(\sigma_f\) 直接相关，为了提高求积的精度和效率，可以应用一种广为人知的策略，即 *方差缩减*。更精确地说，我们讨论一种称为 *重要性采样* 的技术。

本质上，引入一个正的 *权重函数*，\(w(x)\)，在区间 \([0,1]\) 上归一化为 1，

$$\int_0^1 w(x)\,dx=1,\tag{11.8}$$

用它乘以并除以被积函数（11.5）：

$$I=(b-a)\int_0^1\frac{f((b-a)x+a)}{w(x)}w(x)\,dx.$$

执行变量变换 \(d\xi=w(x)dx\) 或以积分形式，

$$\xi(x)=\int_0^x w(x')\,dx',\tag{11.9}$$

边界条件为 \(\xi(0)=0\) 且 \(\xi(1)=1\)（以符合归一化（11.8）），积分变为

$$I=(b-a)\int_0^1\frac{f((b-a)x(\xi)+a)}{w(x(\xi))}\,d\xi.\tag{11.10}$$

在变量变换下积分域的保持是 \(w(x)\) 归一化的直接结果。为了求值该积分，可以直接应用前一节描述的蒙特卡洛方法，通过对一组来自区间 \([0,1]\) 的 *均匀分布* 采样点 \(\xi_i\) 的新被积函数 \(f/w\) 取平均：

$$I\approx\frac{b-a}{n}\sum_{i=1}^{n}\frac{f((b-a)x(\xi_i)+a)}{w(x(\xi_i))}.\tag{11.11}$$

所执行的变量变换乍一看似乎使求积变得更复杂。这种技术的优点只有在选择权重函数 \(w(x)\) 时才变得明显，即尽可能多地，类似于函数 f((b − a)x + a)。在这种情况下，被积函数 f/w 变得光滑且变化缓慢（在理想情况下 w ≡ f，甚至为常数）。由于被积函数相对于其平均值的波动减小，因此积分本身的方差也随之减小。显然，这种好处直接取决于选择合适的权重函数 w(x) 以及通过求逆积分关系 11.9 表示依赖关系 x = x(ξ) 的可能性。

通过注意到随机点 ξi 的均匀分布对应于自变量 xi ≡ x(ξi) 的、通常是非均匀分布，即根据权重函数 w(x)。换句话说，变换后的横坐标 xi 位于区间 (x, x + dx) 内的概率为 w(x)dx。这意味着自变量 xi 是以最大概率生成的，因此集中在 w 较大的区域。对于 w 的合适选择，采样点因此主要集中在原被积函数 f 具有显著值的区域。通过这种方式，可以实现对积分域的最优采样（重要性采样），减少在求和式 (11.11) 中对统计意义较小的点上评估被积函数所“浪费”的工作。

为了说明重要性采样带来的方差降低，我们再次考虑积分

$$\int_0^1 x e^{-x} dx \approx 0.26424.\tag{11.12}$$ 

被积函数在区间 [0,1] 内单调上升，从 0 上升到 e⁻¹，同时保持负的二阶导数。函数 e⁻¹x¹/² 也表现出类似的行为，最重要的是，积分变换 (11.9) 可逆。在这种情况下，适当归一化的权重函数为

$$w(x) = (3/2)x^{1/2}.\tag{11.13}$$ 

通过求逆变量变换 (11.9)，可得到

$$x = \xi^{2/3}.\tag{11.14}$$ 

列表 11.2 显示了基于公式 11.11 的重要性采样蒙特卡洛求积 11.12 的实现。函数 `seed()` 和 `random()`（在模块 `random.py` 和 `random.h` 中定义）被调用以初始化并分别生成均匀随机序列。对于具有分布 w(x) = (3/2)x¹/² 的变量，程序定义了例程 `ranSqrt()`，它反过来调用例程 `random()` 来产生底层均匀分布的随机数 ξ。

程序执行的结果列在表 11.1 的最后两列中，并明显显示出相对于不依赖方差降低（对于 w(x) = 1）的结果的显著改进。事实上，对于相同数量的采样点，标准偏差通常减小超过 4 倍。

图 11.1 中描绘的图也可以用来判断重要性采样带来的改进。左面板绘制了采样点数在 n = 100 到 30,000 之间的积分估计值，可以立即注意到使用重要性采样得到的值的离散程度明显更低，尽管两种方法都收敛到相同的结果。这种行为也在右面板中反映出来，即标准偏差 σ。虽然 σ 的缩放（通过回归得到）对于两种方法都是理论上预测的，即 σ ∼ n⁻¹/²，但可以看出，由重要性采样产生的误差被下移了大约 3.7 倍。

当被积函数本身是两个函数的乘积时，方差降低尤其有效，F(x) = w(x)f(x)。在这种情况下，如果因子 w(x) 可以根据方程 11.9 进行解析积分以得到依赖关系 ξ = ξ(x)，并且后者可以进一步求逆，则因子 w(x) 可以被视为分布函数。基于均匀分布的随机序列

### Listing 11.2 Monte Carlo integration of a Function with Importance Sampling (Python Coding)

```
# One-dimensional Monte Carlo quadrature with variance reduction

from math import *
```
