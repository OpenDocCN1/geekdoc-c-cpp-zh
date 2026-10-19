

b) 验证对应于 λ₁ = 5 的特征向量与下式成比例

x₁ = 1/√6 ⎛ -1 ⎞
                ⎜ -2 ⎟
                ⎝ +1 ⎠ .  (6.39)

c) 特征值 −3 对应一个二重根。这意味着相应的特征向量是简并的，也就意味着它们不唯一。两个线性无关的特征向量为

x₂ = 1/√5 ⎛ -2 ⎞ ,  x₃ = 1/√10 ⎛ 3 ⎞
                ⎜ +1 ⎟           ⎜ 0 ⎟
                ⎝ +0 ⎠           ⎝ 1 ⎠ .  (6.40)

在这种情况下，你的特征值问题求解器会给出什么样的特征向量并不明确。试着找出你用特征值 −3 计算得到的特征向量与这两个线性无关特征向量之间的关系。

5. 设想你的某个物理系统模型产生了 N = 100 个耦合线性方程，其中有 N 个未知量：

a₀₀ y₀ + a₀₁ y₁ + ⋯ + a₀(N−1) y_{N−1} = b₀ ,
 a₁₀ y₀ + a₁₁ y₁ + ⋯ + a₁(N−1) y_{N−1} = b₁ ,
 ⋮
 a_{(N−1)0} y₀ + a_{(N−1)1} y₁ + ⋯ + a_{(N−1)(N−1)} y_{N−1} = b_{N−1} .

在许多情况下，a 和 b 的值是已知的，因此你的练习是求解所有未知量的值，其中 a 取希尔伯特矩阵，b 取其第一列：

[a_{ij}] = a = [ 1/(i + j − 1) ] = ⎛ 1   1/2  1/3  1/4  …  1/100 ⎞
                                   ⎜ 1/2 1/3  1/4  1/5  …  1/101 ⎟
                                   ⎜ ⋮   ⋮    ⋮    ⋮      ⋮   ⎟
                                   ⎝ 1/100 1/101 …   …   1/199 ⎠ ,

[b_i] = b = [1/i] = ⎛ 1 ⎞
                     ⎜ 1/2 ⎟
                     ⎜ 1/3 ⎟
                     ⎜ ⋮   ⎟
                     ⎝ 1/100 ⎠ .

与解析解比较

⎛ y₁ ⎞   ⎛ 1 ⎞
⎜ y₂ ⎟ = ⎜ 0 ⎟
⎜ ⋮  ⎟   ⎜ ⋮ ⎟
⎝ y_N⎠   ⎝ 0 ⎠ .  (6.41)

6. 狄拉克 γ 矩阵：狄拉克方程将量子力学扩展到包含相对论和自旋 1/2。电子哈密顿算符的推广要求它包含矩阵，而这些矩阵可以用 4 × 4 的 γ 矩阵表示，γ 矩阵又可以用熟悉的 2 × 2 泡利矩阵 σ_i 表示：

γ_i = ( 0   σ_i ; -σ_i  0 ),   i = 1,2,3 ,  (6.42)

σ_1 = ( 0 1 ; 1 0 ),   σ_2 = ( 0 -i ; i 0 ),   σ_3 = ( 1 0 ; 0 -1 ).  (6.43)

验证 γ 矩阵的下列性质：

γ_2^† = γ_2^{-1} = -γ_2 ,  (6.44)

γ_1 γ_2 = -i ( σ_3 0 ; 0 σ_3 ).  (6.45)

## 6.6.1
## 弦问题的矩阵解法

在第 6.1 节中，我们建立了弦上两个质量问题的求解方案。现在我们已经具备了求解所需的矩阵工具。你的任务是检验在各种重量和长度下解的物理合理性。你应该检查推得的张力为正，并且推得的角度对应一个物理几何构型（例如，画一张草图）。由于这是一个基于物理的问题，我们知道正弦和余弦函数的绝对值必须小于 1，而且张力的大小应与球体的重量相近。我们的解在 NewtonNDanimate.py（清单 6.1）中给出，它以图形方式展示了逐步求解搜索过程。

清单 6.1 代码 NewtonNDanimate.py，它通过牛顿–拉弗森搜索逐步展示两质量弦问题的求解过程。

```
# NewtonNDanimate.py:              MultiDimension Newton Search
from visual import *
from numpy.linalg import solve
from visual.graph import *

scene = display(x=0,y=0,width=500,height=500,
                title='String and masses configuration')
tempe = curve(x=range(0,500),color=color.black)

n = 9
eps = 1e-3
deriv = zeros( (n, n), float)
f = zeros( (n), float)

x = array([0.5, 0.5, 0.5, 0.5, 0.5, 0.5, 0.5, 1., 1., 1.])

def plotconfig():
    for obj in scene.objects:
        obj.visible=0                     # Erase previous configuration
    L1 = 3.0
    L2 = 4.0
    L3 = 4.0
    xa = L1*x[3]                         # L1*cos(th1)
    ya = L1*x[0]                         # L1 sin(th1)
    xb = xa+L2*x[4]                      # L1*cos(th1)+L2*cos(th2)
    yb = ya+L2*x[1]                      # L1*sin(th1)+L2*sen(th2)
    xc = xb+L3*x[5]                      # L1*cos(th1)+L2*cos(th2)+L3*cos(th3)
    yc = yb-L3*x[2]                      # L1*sin(th1)+L2*sen(th2)-L3*sin(th3)
    mx = 100.0                           # for linear coordinate transformation
    bx = -500.0                          # from 0<= x <=10
    my = -100.0                          # to    -500 <=x_window>=500
    by = 400.0                           # same transformation for y
    xap = mx*xa+bx                       # to keep aspect ratio
    yap = my*ya+by
    ball1 = sphere(pos=(xap,yap), color=color.cyan,radius=15)
    xbp = mx*xb+bx
    ybp = my*yb+by
    ball2 = sphere(pos=(xbp,ybp), color=color.cyan,radius=25)
    xcp = mx*xc+bx
    ycp = my*yc+by
    x0 = mx*0+bx
    y0 = my*0+by
    line1 = curve(pos=[(x0,y0),(xap,yap)], color=color.yellow,radius=4)
    line2 = curve(pos=[(xap,yap),(xbp,ybp)], color=color.yellow,radius=4)
    line3 = curve(pos=[(xbp,ybp),(xcp,ycp)], color=color.yellow,radius=4)
    topline = curve(pos=[(x0,y0),(xcp,ycp)], color=color.red,radius=4)

def F(x, f):                              # F function
    f[0] = 3*x[3] + 4*x[4] + 4*x[5] - 8.0
    f[1] = 3*x[0] + 4*x[1] - 4*x[2]
    f[2] = x[6]*x[0] - x[7]*x[1] - 10.0
    f[3] = x[6]*x[3] - x[7]*x[4]
    f[4] = x[7]*x[1] + x[8]*x[2] - 20.0
    f[5] = x[7]*x[4] - x[8]*x[5]
    f[6] = pow(x[0], 2) + pow(x[3], 2) - 1.0
    f[7] = pow(x[1], 2) + pow(x[4], 2) - 1.0
    f[8] = pow(x[2], 2) + pow(x[5], 2) - 1.0

def dFi_dXi(x, deriv, n):                # Derivatives
    h = 1e-4
    for j in range(0, n):
        temp = x[j]
        x[j] = x[j] + h/2.
        F(x, f)
        for i in range(0, n): deriv[i, j] = f[i]
        x[j] = temp
    for j in range(0, n):
        temp = x[j]
        x[j] = x[j] - h/2.
        F(x, f)
        for i in range(0, n): deriv[i, j] = (deriv[i, j] - f[i])/h
        x[j] = temp

for it in range(1, 100):
    rate(1)                              # 1 second between graphs
    F(x, f)
    dFi_dXi(x, deriv, n)
    B = array([[-f[0]], [-f[1]], [-f[2]], [-f[3]], [-f[4]], [-f[5]],\
               [-f[6]], [-f[7]], [-f[8]]])
    sol = solve(deriv, B)
    dx = take(sol, (0, ), 1)             # First column of sol

for i in range(0, n):
    x[i] = x[i] + dx[i]
plotconfig()
errX = errF = errXi = 0.0
for i in range(0, n):
    if ( x[i] != 0.): errXi = abs(dx[i]/x[i])
    else: errXi = abs(dx[i])
    if ( errXi > errX ): errX = errXi
    if ( abs(f[i]) > errF ): errF = abs(f[i])
if ( (errX <= eps) and (errF <= eps) ): break
print('Number of iterations = ', it, "\n Final Solution:")
for i in range(0, n):
    print('x[', i, '] = ', x[i])
```

## 6.6.2
## 探索

- 1. 观察你对弦角的初始猜测糟糕到什么程度时，计算机将无法找到物理上合理的解。
- 2. 我们刚刚建立的体系可能有一个问题：将恒等式 sin² θᵢ + cos² θᵢ = 1 纳入方程后，我们可能丢失了关于 sin θ 或 cos θ 符号的一些信息。如果查看图 6.1，你会发现对于某些重量和长度，θ₂ 可能为负，但 cos θ 应保持为正。我们可以通过将 f₇–f₉ 替换为基于以下形式的 f 来将此条件构建到方程中：
- 
- f₇ = x₄ − √(1 − x₁²),   f₈ = x₅ − √(1 − x₂²),   f₉ = x₆ − √(1 − x₃²). (6.46)
- 
- 看看这是否会使得到的解有所不同。
- 3. ⊙ 求解类似的三质量问题。方法相同，但方程数量更多。

# 7
# 试错搜索与数据拟合

在本章中，我们为计算工具箱增加更多工具。首先，我们设计一些方法，通过试错搜索来求方程的解，有时会用到新掌握的数值微分工具。虽然试错搜索听起来可能不太精确，但它实际上广泛用于求解不存在解析解或解析解不实用的问题。在第 6 章中我们已经看过一个这样的例子：弦上两个重物的问题如何导出矩阵方程。在第 8 章中，我们将试错搜索与常微分方程的求解结合起来，以解决一般的量子本征值问题。本章的第二部分介绍数据拟合的一些方面。我们研究如何在数值表中进行插值，以及如何对函数进行最小二乘拟合以匹配数据，后者通常需要搜索。

## 7.1
## 问题1：盒子中量子态的搜索

许多计算机技术都是定义明确的过程集合，能产生确定的结果。相比之下，有些计算技术则是试错算法，它们根据变量的当前值来决定下一步的路径，并且只有在程序认为问题已解决时才会停止。（我们在对幂级数求和直到项变得很小时，已经做过类似的事情。）编写这类程序通常很有趣，因为我们必须预见如何让计算机在所有可能的情况下表现得智能；而运行这类程序非常像做实验，很难预测计算机会得出什么结果。

