

## 问题

量子力学中最标准的¹问题之一是求解质量为 \(m\) 的粒子被限制在 1D 方形阱半径为 \(a\) 时的能量：

\[
V(x)=\begin{cases}
-V_0, & |x|\le a,\\
0, & |x|\ge a.
\end{cases} \tag{7.1}
\]

如量子力学教材所示（Gottfried, 1966），该阱中束缚态 \(E=-E_B<0\) 的能量是超越方程的解

\[
\sqrt{10-E_B}\,\tan\left(\sqrt{10-E_B}\right)=\sqrt{E_B} \quad (\text{even}), \tag{7.2}
\]

\[
\sqrt{10-E_B}\,\cot\left(\sqrt{10-E_B}\right)=\sqrt{E_B} \quad (\text{odd}), \tag{7.3}
\]

其中 even 和 odd 分别指波函数的对称性。这里我们选择单位使得 \(\hbar=1\)，\(2m=1\)，\(a=1\)，且 \(V_0=10\)。

你的问题是

1. 求出偶波函数对应的几个束缚态能量 \(E_B\)，即方程 (7.2) 的解。
2. 看看使势阱加深，例如将 10 改为 20 或 30，是否会产生更多或更深的束缚态。

¹ 我们在第 9.1 节用同样的方法求解此问题，该方法适用于几乎任何势，并且也能给出波函数。本节的方法仅适用于方形阱的本征能量。

## 7.2 算法：通过二分法进行试错求根

试错求根寻找使

\[
f(x)\simeq 0, \tag{7.4}
\]

成立的 \(x\) 值，其中右边的 0 是惯例的（例如方程 \(10\sin x=3x^3\) 可以很容易写成 \(10\sin x-3x^3=0\)）。搜索过程从对 \(x\) 的猜测值开始，将该猜测代入 \(f(x)\)（“试”），然后看左端与零相差多远（“错”）。程序随后根据误差改变 \(x\) 并在 \(f(x)\) 中尝试新的猜测。该过程继续进行，直到 \(f(x)\simeq 0\) 达到所需精度，或 \(x\) 的变化变得不显著，或搜索似乎无止境。

最基本的试错技术是二分算法。它可靠但缓慢。如果你知道 \(f(x)\) 在其中变号的区间，则二分算法总能通过找到零点所在越来越小的区间而收敛到根。其他技术，例如我们接下来描述的牛顿-拉夫逊方法，可能收敛更快，但如果初始猜测不够接近，可能变得不稳定并完全失败。

![Figure 7.1: A graphical representation of the steps involved in solving for a zero of \(f(x)\) using the bisection algorithm. The bisection algorithm takes the midpoint of the interval as the new guess for \(x\), and so each step reduces the interval size by one-half. Four steps are shown for the algorithm.](img/bccda43674e4a93dee81c749eba8d2f7_166_0.png)

二分算法的基础如图 7.1 所示。我们从已知零点出现的两个 \(x\) 值开始。（你可以通过作图或逐步遍历不同的 \(x\) 值并寻找符号变化来确定这些值。）具体来说，假设 \(f(x)\) 在 \(x_-\) 处为负，在 \(x_+\) 处为正：

\[
f(x_-)<0,\qquad f(x_+)>0. \tag{7.5}
\]

（注意，如果函数随 \(x\) 增大而从正变负，可能有 \(x_- > x_+\)。）因此，我们从已知零点出现的区间 \(x_+ \le x \le x_-\) 开始。算法（以 7.1 节清单实现）然后将新的 \(x\) 选为区间的二分点，并将符号变化发生的半区间选为其新的区间：

```
x = ( xPlus + xMinus ) / 2
if ( f(x) * f(xPlus) > 0 ) xPlus = x
else xMinus = x
```

该过程继续进行，直到 \(f(x)\) 的值小于预定义的精度水平，或达到预定义的（较大）细分次数。

**Listing 7.1** `Bisection.py` 是二分算法的简单实现，用于寻找函数的零点，在此例中为 \(2\cos x - x\)。

```python
# Bisection.py                     Find zero via Bisection algorithm

from visual.graph import *

def f(x):                         # Function = 0?
    return 2*cos(x) - x

def bisection(xminus, xplus, Nmax, eps):   # x+, x-, Nmax, error
    for it in range(0, Nmax):
        x = (xplus + xminus)/2.          # Mid point
        print(" it ", it, " x ", x, " f(x) ", f(x))
        if (f(xplus)*f(x) > 0.):         # Root in other half
            xplus = x                    # Change x+ to x
        else:
            xminus = x                   # Change x- to x
        if (abs(f(x)) < eps):            # Converged?
            print("\n Root found with precision eps = ", eps)
            break
        if it == Nmax-1:
            print("\n Root NOT found after Nmax iterations\n")
    return x

eps = 1e-6                         # Precision of zero
a = 0.0;        b = 7.0              # Root in [a,b]
imax = 100                         # Max no. iterations
root = bisection(a ,b, imax, eps)
print(" Root =", root)
```

图 7.1 中的示例显示第一个区间从 \(x_- = x_-^{(1)}\) 延伸到 \(x_+ = x_+^{(1)}\)。我们在 \(x\) 处二分该区间，由于中点处 \(f(x)<0\)，我们设 \(x_- \equiv x_-^{(2)} = x\) 并将其标记为 \(x_-^{(2)}\) 以表示第二步。然后我们使用 \(x_+^{(2)} \equiv x_+^{(1)}\) 和 \(x_-^{(2)}\) 作为下一个区间并继续该过程。我们看到在此示例中前三步只有 \(x_-\) 发生变化，但在第四步 \(x_+\) 最终发生变化。随后变化变得太小而无法显示。

### 7.2.1 实现：二分算法

1. 实现任何搜索算法的第一步是了解你的函数是什么样子的。对于当前问题，你通过绘制 \(f(E)=\sqrt{10-E_B}\,\tan\left(\sqrt{10-E_B}\right)-\sqrt{E_B}\) 对 \(E_B\) 的图来做到这一点。从你的图中注意 \(f(E_B)=0\) 的近似值。你的程序应该能够找到这些零点的更精确值。

2. 编写一个实现二分算法的程序，并用它来寻找 (7.2) 的一些解。

3. 警告：由于 tan 函数有奇点，你必须小心。事实上，你的图形程序（或 Maple）可能在这些奇点附近不能准确工作。一个补救措施是使用不同但等价的形式来表示方程。证明 (7.2) 的等价形式是

\[
\sqrt{E}\,\cot\left(\sqrt{10-E}\right)-\sqrt{10-E}=0. \tag{7.6}
\]

4. 绘制 (7.6) 的第二张图，它也有奇点但在不同位置。从该图中选择零点的近似位置。

5. 评估 \(f(E_B)\)，从而直接确定解的精度。

6. 将你找到的根与 Maple 或 Mathematica 给出的结果进行比较。

## 7.3 改进算法：牛顿-拉夫逊搜索

牛顿-拉夫逊算法比二分法更快地找到方程 \(f(x)=0\) 的近似根。如图 7.2 所示，该算法等价于在 \(f(x)\simeq 0\) 的 \(x\) 值处画一条与曲线相切的直线 \(f(x)\simeq mx+b\)，然后使用该直线与 \(x\) 轴的交点 \(x=-b/m\) 作为根的改进猜测。如果“曲线”是一条直线，答案就是精确的；否则，如果猜测足够接近根使得 \(f(x)\) 近似线性，则是很好的近似。该过程继续进行直到达到设定的精度水平。如果猜测位于 \(f(x)\) 近似线性的区域（图 7.2），则收敛速度比二分算法快得多。

牛顿-拉夫逊算法的解析表述从旧猜测 \(x_0\) 开始，将新猜测 \(x\) 表示为对旧猜测的修正 \(\Delta x\)：

\[
x_0 = \text{old guess}, \qquad \Delta x = \text{unknown correction}
\]

\[
\Rightarrow \quad x = x_0 + \Delta x = \text{(unknown) new guess}.
\]

![Figure 7.2: A graphical representation of the steps involved in solving for a zero of \(f(x)\) using the Newton–Raphson method. The Newton–Raphson method takes the new guess as the zero of the line tangent to \(f(x)\) at the old guess. Two guesses are shown.](img/bccda43674e4a93dee81c749eba8d2f7_168_0.png)

我们接下来在 \(x_0\) 附近对已知函数 \(f(x)\) 进行泰勒展开并只保留线性项：

\[
f(x=x_0+\Delta x)\approx f(x_0)+\left.\frac{df}{dx}\right|_{x_0}\Delta x. \tag{7.10}
\]

我们然后通过计算该线性近似与 \(x\) 轴相交的点来确定修正 \(\Delta x\)：

\[
f(x_0)+\left.\frac{df}{dx}\right|_{x_0}\Delta x=0, \tag{7.11}
\]

\[
\Rightarrow \quad \Delta x = -\frac{f(x_0)}{\left.\frac{df}{dx}\right|_{x_0}}. \tag{7.12}
\]

该过程重复进行，从改进的 \(x\) 开始，直到获得设定的精度。

牛顿-拉夫逊算法 (7.12) 要求在每个 \(x_0\) 值处求值导数 \(df/dx\)。在许多情况下，你可能有导数的解析表达式并可将其构建到算法中。然而，尤其对于更复杂的问题，使用数值前向差分近似导数更简单且不易出错²：

\[
\frac{df}{dx}\approx \frac{f(x+\delta x)-f(x)}{\delta x}, \tag{7.13}
\]

其中 \(\delta x\) 是你选择的 \(x\) 的微小变化（与 (7.12) 中用于搜索的 \(\Delta\) 不同）。虽然中心差分近似对导数更准确，但它需要额外求值 \(f\)，一旦找到零点，你得到零点的方式并不重要。在清单 7.2 中，我们给出了程序 `NewtonCD.py`，它使用中心差分导数实现搜索。

**Listing 7.2** `NewtonCD.py` 使用牛顿-拉夫逊方法搜索函数 \(f(x)\) 的零点。中心差分近似用于确定 \(df/dx\)。

```python
# NewtonCD.py   Newton Search with central difference

from math import cos

x = 4.;        dx = 3.e-1;        eps = 0.2;                # Parameters
imax = 100;                                      # Max no of iterations

def f(x):                                         # Function
    return 2*cos(x) - x

for it in range(0, imax + 1):
    F = f(x)
    if ( abs(F) <= eps ):
        # Check for convergence
        print("\n Root found, F =", F, ", tolerance eps = ", eps)
```

² 我们在第 5 章讨论数值微分。

