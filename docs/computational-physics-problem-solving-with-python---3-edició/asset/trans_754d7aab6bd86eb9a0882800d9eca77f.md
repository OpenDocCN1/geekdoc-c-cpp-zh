
![](img/bccda43674e4a93dee81c749eba8d2f7_449_0.png)

图17.6 我们在二维Ising模型的WLS实现中使用的编号方案，自旋格点为8 × 8。

熵S(T)和能量直方图H(E_i)如图17.5所示。其他热力学函数可以通过将(17.21)中的E替换为相应变量来获得。结果类似于图17.4中的结果。

计算这些变量时可能遇到的一个问题是，(17.21)中的求和可能变得足够大而导致溢出，尽管比值不会溢出。你可以通过提出一个公共大因子来解决这个问题，例如：

```
∑_{E_i} X(E_i) g(E_i) e^{-E_i / k_B T} = e^{λ} ∑_{E_i} X(E_i) e^{ln g(E_i) - E_i / k_B T - λ} , (17.39)
```

其中λ是每个温度下ln g(E_i) − E_i / k_B T的最大值。实际上，在计算变量时不需要包括因子e^{λ}，因为它同时出现在分子和分母中，最终会抵消。

## 清单17.2 WangLandau.py 使用Wang–Landau采样模拟二维Ising模型，计算态密度，并由此得到内能。

```
# WangLandau.py: Wang Landau algorithm for 2D spin system
""" Author in Java: Oscar A. Restrepo,
Universidad de Antioquia, Medellin, Colombia
Each time fac changes, a new histogram is generated.
Only the first Histogram plotted to reduce computational time"""
from visual import *
import random;
from visual.graph import *

L = 8; N = (L*L)

# Set up graphics
entgr = gdisplay(x=0,y=0,width=500,height=250,title='Density of States',\
    xtitle='E/N', ytitle='log g(E)', xmax=2., xmin=-2.,ymax=45,ymin=0)
```

```
entrp  = gcurve(color = color.yellow, display = entgr)
energygr = gdisplay(x=0, y=250, width=500, height=250, title='E vs T',\
           xtitle = 'T', ytitle='U(T)/N', xmax=8.,xmin=0, ymax =0.,ymin=-2.)
energ  = gcurve(color = color.cyan, display = energygr)
histogr = display(x = 0, y = 500, width = 500, height = 300,\
           title = '1st histogram: H(E) vs. E/N, corresponds to log(f) = 1')
histo  = curve(x = list(range(0, N+1)), color=color.red, display=histogr)
xaxis = curve(pos = [( - N, -10), (N, -10)])
minE  = label(text = '-2', pos = ( - N + 3, -15), box = 0)
maxE  = label(text = '2', pos = (N - 3, -15), box = 0)
zeroE = label(text = '0', pos = (0, -15), box = 0)
ticm  = curve(pos = [( - N, -10), ( - N, -13)])
tic0  = curve(pos = [(0, -10), (0, -13)])
ticM  = curve(pos = [(N, -10), (N, -13)])
enr   = label(text = 'E/N', pos = (N/2, -15), box = 0)

sp    = zeros( (L, L) )                     # Grid size, spins
hist  = zeros( (N + 1) )
prhist = zeros( (N + 1) )                   # Histograms
S     = zeros( (N + 1), float)             # Entropy = log g(E)

def iE(e):  return int((e + 2**N)/4)

def intEnergy():
    exponent = 0.0
    for T in arange(0.2, 8.2, 0.2):         # Select lambda max
        Ener = -2**N
        maxL = 0.0                          # Initialize
        for i in range(0, N + 1):
            if S[i]!= 0 and (S[i] - Ener/T)>maxL:
                maxL = S[i] - Ener/T
                Ener = Ener + 4
        sumdeno = 0
        summume = 0
        Ener = -2**N
        for i in range(0, N):
            if S[i] != 0:
                exponent = S[i] - Ener/T - maxL
                summume += Ener*exp(exponent)
                sumdeno += exp(exponent)
                Ener = Ener + 4.0
        U = summume/sumdeno/N                 # internal energy U(T)/N
        energ.plot(pos = (T, U) )

def WL():
    Hinf  = 1.e10                           # Wang - Landau sampling
    Hsup  = 0.                              # initial values for Histogram
    tol   = 1.e-3                           # tolerance, stops the algorithm
    ip    = zeros(L)
    im    = zeros(L)                        # BC R or down, L or up
    height = abs(Hsup - Hinf)/2.            # Initialize histogram
    ave = (Hsup + Hinf)/2.                  # about average of histogram
    percent = height / ave
    for i in range(0, L):
        for j in range(0, L): sp[i, j] = 1  # Initial spins
    for i in range(0, L):
        ip[i] = i + 1
        im[i] = i - 1                       # Case plus, minus
    ip[L - 1] = 0
    im[0]    = L - 1                        # Borders
    Eold = -2**N                            # Initialize energy
    for j in range(0, N + 1): S[j] = 0      # Entropy initialized
    iter = 0
    fac  = 1
    while fac > tol:
        i = int(N*random,random())          # Select random spin
```

```
xg = i%L
# Must be i//L, not i/L for Python 3:
yg = i//L                # Localize x, y, grid point
Enew = Eold + 2*(sp[ip[xg],yg] + sp[im[xg],yg] + sp[xg,ip[yg]]
        + sp[xg, im[yg]] ) * sp[xg, yg]      # Change energy
deltaS = S[iE(Enew)] - S[iE(Eold)]
if deltaS <= 0 or random.random() < exp( - deltaS):
    Eold = Enew;
    sp[xg, yg] *= -1      # Flip spin
    S[iE(Eold)] += fac;   # Change entropy
if iter%10000 == 0:       # Check flatness every 10000 sweeps
    for j in range(0, N + 1):
        if j == 0:
            Hsup = 0
            Hinf = 1e10      # Initialize new histogram
        if hist[j] == 0 : continue      # Energies never visited
        if hist[j] > Hsup: Hsup = hist[j]
        if hist[j] < Hinf: Hinf = hist[j]
    height = Hsup - Hinf
    ave = Hsup + Hinf
    percent = 1.0* height/ave      # 1.0 to make it float number
    if percent < 0.3 :      # Histogram flat?
        print(" iter ", iter, " log(f) ", fac)
        for j in range(0, N + 1):
            prhist[j] = hist[j]          # to plot
            hist[j] = 0                 # Save hist
        fac *= 0.5                      # Equivalent to log(sqrt(f))
iter += 1
hist[iE(Eold)] += 1      # Change histogram, add 1, update
if fac >= 0.5:           # just show the first histogram
    # Speed up by using array calculations:
    histo.x = 2.0*arange(0,N+1) - N
    histo.y = 0.025*hist-10
deltaS = 0.0
print("wait because iter > 13 000 000")      # not always the same
WL()
deltaS = 0.0
for j in range(0, N + 1):
    rate(150)
    order = j*4 - 2*N + log(2)
    deltaS = S[j] - S[0] + log(2)
    if S[j] != 0 : entrp.plot(pos = (1.*order/N, deltaS))   # plot entropy
IntEnergy();
print("Done")
```

## 17.6.2

## WLS Ising模型评估

重复第17.4.2节中对Ising模型热力学性质进行的评估，但使用WLS代替Metropolis算法。

## 17.7

## 费曼路径积分量子力学 ⊙

问题 众所周知，连接在线性弹簧上的经典粒子做简谐运动，其位置作为时间的函数为x(t) = A sin(ω₀ t + φ)。你的问题是取这条经典的时空轨迹x(t)，并用它来生成束缚在谐振子势中的粒子的量子波函数ψ(x, t)。

## 17.8

## 费曼的时空传播（理论）

费曼在寻找一种量子力学的表述，使其比薛定谔理论更直接地联系到经典力学，并且从一开始就让量子力学的统计性质变得明显。他遵循狄拉克的建议，即哈密顿的最小作用量原理（可用于推导经典动力学）也可能是量子最小作用量原理的ℏ → 0极限。看到哈密顿原理处理的是粒子在时空中的路径，费曼假设描述自由粒子从时空点a = (xₐ, tₐ)传播到点b = (x_b, t_b)的量子力学波函数可以表示为（Feynman和Hibbs，1965；Mannheim，1983）

ψ(x_b, t_b) = ∫ dx_a G(x_b, t_b; x_a, t_a) ψ(x_a, t_a) , (17.40)

其中G是格林函数或传播子

G(x_b, t_b; x_a, t_a) ≡ G(b, a) = √[m / (2πi (t_b − t_a))] exp[ i m (x_b − x_a)² / (2 (t_b − t_a)) ] . (17.41)

方程17.40是惠更斯子波原理的一种形式，其中波前ψ(x_a, t_a)上的每个点都发出一个球面子波G(b; a)，该子波在空间和时间中向前传播。它表明新的波前ψ(x_b, t_b)是由所有其他子波求和并干涉而产生的。

费曼设想，(17.40)的另一种解释方式是作为一种哈密顿原理的形式，其中粒子处于B点的概率幅度，即波函数ψ，等于从时间A出发并在B点结束的所有时空路径之和（图17.7）。这种观点通过赋予不同路径不同的传播概率，体现了量子力学的统计性质。所有路径都是可能的，但有些路径比其他路径更可能。（当你意识到薛定谔理论是求解波函数，并把路径视为经典概念时，你就能体会到它与费曼的观点有多么不同。）路径概率的值来自哈密顿的经典最小作用量原理：

> 一个物理粒子沿经典轨迹x̄(t)从时间t_a运动到t_b的最一般运动，是沿着一条使得作用量S[x̄(t)]是一个

