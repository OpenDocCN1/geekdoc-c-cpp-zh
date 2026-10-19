

```
if (pp < prob):
    if (r>0 and r<(npoints - 1)):
        if ((hit[r] >= hit[r - 1]) and (hit[r] >= hit[r + 1])):
            hit[r] = hit[r] + 1
        else:
            if (hit[r - 1] > hit[r + 1]):
                hit[r] = hit[r - 1]
            else: hit[r] = hit[r + 1]
    oldx = r
    oldy = hit[r]
    olc = oldx*2 - 200                 # TF for plot
    olyc = oldy*4 - 200
    pts.append((pos=(olc, olyc)))
```

- 1. 编写一个生成高斯分布随机数的子程序。³)
- 2. 定义一个由数组 `grid[400,400]` 表示的二维点阵，所有元素初始为零。
- 3. 将种子置于点阵中心；即设 `grid[199,199]=1`。
- 4. 想象一个以 `grid[199,199]` 为中心、半径为 180 个点阵间距的圆。这是我们释放粒子的圆。
- 5. 通过生成 0 到 2π 之间的均匀随机角度来确定新粒子在圆周上的角度位置。
- 6. 计算新粒子在圆上的 *x* 和 *y* 位置。
- 7. 通过生成均匀随机数 `0 < r_xy < 1` 并应用以下规则来确定粒子是水平移动还是垂直移动：

if  \(\begin{cases} r_{xy}<0.5, & \text{motion is vertical},\\ r_{xy}>0.5, & \text{motion is horizontal}.\end{cases}\)  (16.28)

- 8. 生成区间 [−∞, ∞] 内的高斯加权随机数。这是步长的大小，正负号表示方向。
- 9. 我们现在知道了粒子将移动的总距离和方向。它每次跳跃一个点阵间距，直到覆盖该总距离。
- 10. 在跳跃前，检查最近邻位点是否被占据：
    - a) 如果被占据，粒子停留在当前位置且行走结束。
    - b) 如果未被占据，粒子跳跃一个点阵间距。
    - c) 继续检查和跳跃，直到总距离被覆盖、粒子粘住或它离开圆为止。
- 11. 一次随机行走结束后，可以释放另一个粒子并重复该过程。这就是簇的生长方式。

由于许多粒子丢失，你可能需要生成数十万个粒子才能形成包含数百个粒子的簇。

³) 我们在第 5.22.1 节中说明了如何做到这一点。

## 16.7.2

## DLA 或波洛克画作的分形分析

使用 DLA 技术生成的簇如图 16.7 所示。我们希望分析它以查看结构是否为分形，如果是，则确定其维数。 （作为替代，你可以分析图 16.8 中波洛克画作的分形性质，这是一种用于确定此类艺术品真实性的技术。）作为对照，*同时* 分析一个几何图形，例如正方形或圆，其维数已知。分析是用于确定英国海岸线长度的方法的一种变体。

- 1. 如果尚未进行，请使用盒计数法确定简单正方形的分形维数。
- 2. 在种子粒子周围画一个长度为 *L* 的正方形，相对于簇的大小很小。 （小可能是指边长为七个点阵间距。）
- 3. 统计正方形内的粒子数。
- 4. 通过将粒子数除以盒中可用的位点数来计算密度 ρ （在我们的例子中为 49）。
- 5. 使用越来越大的正方形重复该过程。
- 6. 直到簇被覆盖时停止。
- 7. （盒计数）分形维数 *d_f* 可从密度 ρ 与 *L* 的对数-对数图估计得出。如果簇是分形，则 (16.2) 告诉我们 ρ ∝ *L*^{*d_f*−2}，图应为斜率为 *d_f* − 2 的直线。

我们生成的图斜率为 −0.36，这对应于 1.66 的分形维数。由于涉及随机数，你生成的图会不同，但分形维数应相似。 （实际上，该结构是多重分形，因此维数也随位置变化。）

![](img/bccda43674e4a93dee81c749eba8d2f7_422_0.png)

**图 16.8** 美国画家杰克逊·波洛克的《数字 8》。 （经许可使用，纽约州立大学 Neuberg 博物馆。）一些研究者声称波洛克的画作表现出特征性的分形结构，而另一些研究者对此提出质疑（Kennedy, 2006）。 看看你能否确定这幅画中的分形维数。

## 16.8

## 分岔图中的分形（问题 7）

回想一下涉及 logistic 映射的项目，我们在其中绘制了稳定人口数与生长参数 μ 的值。 取你制作的分岔图之一，并使用与英国海岸线所应用的相同技术确定图中不同部分的分形维数。

## 16.9

## 细胞自动机产生的分形

我们已经在多处指出统计模型可能导致分形。 有一类称为细胞自动机的统计模型，它们能从非常简单的系统中产生复杂的行为。这里我们研究其中的一些。

细胞自动机由 von Neumann 和 Ulam 于 1940 年代初期开发（von Neumann 当时也在从事现代计算机背后的理论）。 尽管非常简单，细胞自动机已在科学的许多分支中找到应用（Peitgen et al., 1994; Sipper, 1996）。 它们的经典定义是（Barnsley and Hurd, 1992）：

> 细胞自动机是一种离散动力系统，其中空间、时间和系统的状态都是离散的。 规则空间格子中的每个点，称为细胞，可以具有有限数量的状态中的任意一个，并且格子中细胞的状态根据局部规则更新。 也就是说，给定时间下细胞的状态仅取决于其上一时间步的状态，以及上一时间步附近邻居的状态。 格子上的所有细胞同步更新，因此整个格子的状态以离散时间步推进。

二维细胞自动机由多个彼此生长的方形细胞组成。 一个著名的是康威的生命游戏，我们在列表 16.3 中实现。 在其中，值为 1 的细胞为活细胞，而值为 0 的细胞为死细胞。 细胞按以下规则生长：

- 1. 如果一个细胞存活并且其八个邻居中有两个或三个存活，则该细胞保持存活。
- 2. 如果一个细胞存活并且其八个邻居中有超过三个存活，则该细胞因过度拥挤而死亡。
- 3. 如果一个细胞存活并且只有其八个邻居中的一个存活，则该细胞因孤独而死亡。
- 4. 如果一个细胞死亡并且其邻居中有超过三个存活，则该细胞复活。

生命游戏的一个变体是加入“八分之一规则”，即如果恰好有一个邻居存活，则细胞将存活，否则细胞保持不变。

**列表 16.3  Gameoflife.py** 是康威生命游戏的扩展，其中如果八分之一的邻居存活，细胞总是复活。

```python
# Gameoflife.py:        Cellular automata in 2 dimensions

'''* Rules: a cell can be either dead (0) or alive (1)
   * If a cell is alive:
   * On next step will remain alive if
   * 2 or 3 of its closer 8 neighbors are alive.
   * If > 3 of 8 neighbors are alive, cell dies of overcrowdedness
   * If less than 2 neighbors are alive the cell dies of loneliness
   * A dead cell will be alive if 3 of its 8 neighbors are alive,'''

from visual import *
from visual.graph import * ; import random

scene = display(width=500,height=500, title='Game of Life')
cell  = zeros((50,50));        cellu = zeros((50,50))
curve(pos=[(-49,-49),(-49,49),(49,49),(49,-49),(-49,-49)],color=color.white)
boxes = points(shape='square', size=8, color=color.cyan)

def drawcells(ce):
    boxes.pos = []                              # Erase previous cells
    for j in range(0,50):
        for i in range(0,50):
            if ce[i,j] == 1:
                xx = 2*i-50
                yy = 2*j-50
                boxes.append(pos=(xx,yy))

def initial():
    for j in range (20,28):
        for i in range(20, 28):
            r = int(random.random()*2)
            cell[j,i] = r
    return cell

def gameoflife(cell):
    for i in range(1,49):
        for j in range(1,49):
            sum1 = cell[i-1,j-1] + cell[i,j-1] + cell[i+1,j-1] # neighb
            sum2 = cell[i-1,j] + cell[i+1,j] + cell[i-1,j+1] \
                   + cell[i,j+1] + cell[i+1,j+1]
            alive = sum1+sum2
            if cell[i,j] == 1:
                if alive == 2 or alive == 3:                  # Alive
                    cellu[i,j] = 1                              # Lives
                if alive > 3 or alive < 2:        # Overcrowded or solitude
                    cellu[i,j] = 0                              # dies
            if cell[i,j] == 0:
                if alive == 3:
                    cellu[i,j] = 1                              # Revives
                else:
                    cellu[i,j] = 0                              # Remains dead
    alive = 0
    return cellu
temp = initial()
drawcells(temp)
while True:
```
