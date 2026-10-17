
如果线性电机如图 5.5b 所示安装在地面上，则 `θ` 和 `dotθ` 都将为零。可以使用之前的方程 `5.9` 和 `5.13` 计算 B 点和 A 点的坐标，它们的速度和加速度的标量分量如下：

```
$$\dot{xA}=\dot{xB}=\dot{s}\cdot\cos\theta$$
$$\dot{yA}=\dot{yB}=\dot{s}\cdot\sin\theta$$
```

以及

```
$$\ddot{xA}=\ddot{xB}=\ddot{s}\cdot\cos\theta$$
$$\ddot{yA}=\ddot{yB}=\ddot{s}\cdot\sin\theta$$
```

### 5.2.4 滑块 Slider 和 gSlider 程序

方程 `5.9`、`5.11` 至 `5.13`、`5.15` 和 `5.16` 已在程序 `Slider` 中编写，该程序在直线执行器的气缸连接在 `P` 和 `Q` 处的移动元件上时，计算 `A` 点和 `B` 点的位置、速度和加速度。必须提供 `P` 点和 `Q` 点的位置、速度和加速度作为输入，以及活塞位移及其一、二阶导数 `dot s` 和 `ddot s`。程序 `Slider` 定义如下：

```procedure Slider (Color: Integer; xP, yP, vxP, axP, ayP, xQ, yQ, vxQ, vyQ, axQ, ayQ, AB, s, ds, ds: double; var xB, yB, vxB, vyB, axB, ayB, xA, yA, double);
```

其形式参数与之前符号的对应关系列：

`Slider` 的输入参数：

| -16...16 | xP | yP | vxP | axP | ayP | xQ | yQ | vxQ | vyQ | axQ | ayQ |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Color | xP | yP | vxP | vyP | axP | ayP | xQ | vxQ | vyQ | axQ | ayQ |

| AB | s | ds | ds |

| :--- | :--- | :--- | :--- |

`Slider` 的输出参数：

| fB | yB | xB | yB | xB | yB | xA | yA | xA | yA | xA | yA |

| fB | yB | vxB | vyB | axB | ayB | xA | yA | vxA | vyA | axA | ayA |

在图形系统中，程序 `Slider` 将以 `Color` 颜色（如果为 0 则为常量 BGI Black）绘制活塞和气缸，类似于图 5.5a。如果距离 `AB` 或距离 `PQ` 小于关节尺寸的五倍，程序将在 B 处绘制滑块及其滑轨 `PQ`。如果 `Color` 为负数，则仅绘制滑块，不绘制轴。

辅助程序 `gSlider` 计算气缸固定在地面上时活塞 A 点和 B 点的位置、速度和加速度。该程序实现了方程 `5.9`、`5.10`、`5.17` 和 `5.18`，其定义如下：

```
procedure gSlider(Color:Word; xP,yP,xQ,yQ, PQ, s,ds:double; xB,yB, vxB,vyB, axB,ayB, xA,yA, vxA,vyA, axA,ayA:double);
```

其形式参数与之前符号的对应关系为：

`gSlider` 的输入参数：

| -16...16 | xP | yP | xQ | yQ | PQ | s | ds |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Color | xP | yP | xQ | yQ | s | ds |

`gSlider` 的输出参数：

| fB | yB | xB | yB | xB | yB | xA | yA | xA | yA | xA | yA | yA |

| fB | yB | vxB | vyB | axB | ayB | xA | yA | vxA | vyA | axA | ayA |

# AutoCAD 用户的计算机辅助绘图与仿真工具

![](img/fe0d0bb9b123aa34fc70ee5a03e0d0dd_191_0.png)

参考系 `O,X,Yi` 的 `O,Xi` 轴从 A 指向 B 定向，其原点与 A 点重合，而偏移点 P 则通过局部坐标 `(xI,P, yI,P)` 进行指定。

如果指定了长度 `AP` 和 `BP`，则点 P 的位置可以确定为以 A 和 B 为中心、半径分别为 `AP` 和 `BP` 的两个圆的交点。为了区分这两个圆的两个交点，必须额外指定三角形回路 `APB` 的方向。第二种方法可以使用第 6 章讨论的程序 `Int2CirPVA` 方便地解决，此处详细阐述其在程序 `OffsetV` 中的计算机实现。

在任何时刻，假设以下参数已知：

- 点 P 相对于固定参考系 `OXY` 的坐标 `xA` 和 `yA`。
- 点 A 的速度在固定参考系上的投影 `xA` 和 `yA`。
- 点 A 的加速度在固定参考系上的投影 `xA` 和 `yA`。
- 点 B 相对于固定参考系 `OXY` 的坐标 `xB` 和 `yB`。
- 点 B 的速度在固定参考系上的投影 `xB` 和 `yB`。
- 点 B 的加速度在固定参考系上的投影 `xB` 和 `yB`。
- 相对于移动参考系 `O,Xi,Yi`，连接在运动杆上的感兴趣点 P 的局部坐标 `xi,P` 和 `yi`（图 5.7a），或距离 `AP` 和 `BP` 加上三角形回路 `ABP` 的方向（图 5.7b）。

未知的运动学参数为：

- 点 P 相对于固定参考系 `OXY` 的坐标 `xP` 和 `yP`。
- 点 P 的线速度在固定参考系上的投影 `xP` 和 `yP`。
- 点 P 的加速度在固定参考系上的投影 `xP` 和 `yP`。

# 平面机械系统的运动仿真程序

对于图 5.7a 所示的情况，我们将矢量方程 `OP = OA + AP` 投影到固定参考系的坐标轴上，得到：

```
$$\begin{aligned}xP&=xA+x_iP\cdot\cos\theta+y_iP\cdot\cos\left(\theta+\frac{\pi}{2}\right)=xA+x_iP\cdot\cos\theta-y_iP\cdot\sin\theta\\\yP&=yA+x_iP\cdot\sin\theta+y_iP\cdot\sin\left(\theta+\frac{\pi}{2}\right)=yA+x_iP\cdot\sin\theta-y_iP\cdot\cos\theta\end{aligned}$$
```

其中角 `θ` 是在 `OX` 轴和矢量 `AB` 之间角的（见图 5.7a），由公式给出：

```
$$\theta=\tan^{-1}\left[\frac{yB-yA}{xB-xA}\right]
```

注意，通过对坐标为 `x_iP` 和 `y_iP` 的点 P 应用角度 `θ` 的旋转，然后从 `(0, 0)` 平移到 `(xA, yA)`，也可以得到相同的方程 `5.20`。

对方程 `5.20` 关于时间求导，得到点 P 的速度在固定参考系坐标轴上的投影：

```
$$\begin{aligned}\dot{xP}&=\dot{xA}-\dot{\theta}\cdot(x_iP\cdot\sin\theta+y_iP\cdot\cos\theta)\\dot{yP}&=\dot{yA}+\dot{\theta}\cdot(x_iP\cdot\cos\theta-y_iP\cdot\sin\theta)\end{aligned}$$
```

等价于：

```
$$\begin{aligned}\dot{xP}&=\dot{xA}-\dot{\theta}\cdot(yB-yA)\\dot{yP}&=\dot{yA}+\dot{\theta}\cdot(xB-xA)\end{aligned}$$
```

运动部件 `AB` 的角速度 `dotθ` 可以通过为点 B（代替 P）编写类似于 `(5.23)` 的方程来确定，点 B 的速度是知的：

```
$$\begin{aligned}\dot{xB}&=\dot{xA}-\dot{\theta}\cdot(yB-yA)\\dot{yB}&=\dot{yA}+\dot{\theta}\cdot(xB-xA)\end{aligned}$$
```

产生以下两个等价方程：

```
$$\dot{\theta}=-\frac{\dot{xB}-\dot{xA}}{yB-yA}\quad or\quad=\frac{\dot{yB}-\dot{yA}}{xB-xA}$$
```

# AutoCAD 用户的计算机辅助绘图与仿真工具

点 P 加加速度的 x 和 y 分量通过对方程 `5.23` 求导得到，即：

```
$$\ddot{x} = \ddot{x} - \dot{\theta} \cdot (x_P\sin\theta + y_P\cos\theta) - \ddot{\theta}^2 \cdot (x_P\cos\theta - y_P\sin\theta)$$
$$\ddot{y} = \ddot{y} + \dot{\theta} \cdot (x_P\cos\theta - y_P\sin\theta) - \ddot{\theta}^2 \cdot (x_P\sin\theta + y_P\cos\theta) (5.26)$$
```

等于：

```
$$\ddot{x} = \ddot{x} - \dot{\theta} \cdot (y_P - y_A) - \ddot{\theta}^2 \cdot (x_P - x_A)$$
$$\ddot{y} = \ddot{y} + \dot{\theta} \cdot (x_P - x_A) - \ddot{\theta}^2 \cdot (y_P - y_A) (5.27)$$
```

注意，方程 `5.23` 和 `27` 是 2D 刚体速度和加速度的欧拉方程标量形式（Goldstein 等）。`AB` 的角加速度通过从方程 `5.26` 中点 P 与 B 重合的特殊情况提取 `ddotθ` 得到：

```
$$\ddot{\theta} = \frac{\ddot{x}-\dot{\theta}(yB-yA)}{xB-xA} \text{ or } \ddot{\theta} = \frac{\ddot{y}-\dot{\theta}(xB-xA)}{yB-yA} (5.28)$$
```

为了避免取决于 `(y_B-y_A)` 和 `(x_P-x_A)` 的值导致除以零，在计算 `dotθ` 和 `ddotθ` 时，应使用方程 `5.23` 和 `28` 中的第一个或第二个。

## 5.3.1 程序 Offset 和 OffsetV

方程 `5.20`、`23` 和 `27` 已在 `LibMemD` 的程序 `Offset0` 中实现，该程序计算连接在运动杆上的点 P 的位置、速度和加速度，给出相对坐标 `x_P` 和 `y_P`。程序 `Offset0` 在 `LibMemD` 外部可见，但被程序 `Offset` 使用。伴侣程序 `OffsetV` 基于使用 `LibMemD` 的程序 `Int2CirPVA`，使用点 P 的距离 `AP` 和 `BP`。两个程序都有图形输出且易于更改。它们的头部如下：

```
procedure Offset(Color:Integer; Style:char; xA, yA, vxA, vyA, vxP, vyP, axP, ayP:double; var xP, yP, xB, yB, axB:double);
```

以及

```
procedure OffsetV(Color:Integer; Style:char; xA, yA, vxA, vyA, xB, yB, vxB, vyB, AP, BP, APB:double; var xP, yP, axP, ayP:double);
```

# 平面机械系统运动仿真程序

这两个程序的形式参数与方程 `5.20` 到 `5.28` 以及图 `5.4` 中的符号对应关系如下：

程序 `Offset` 的输入参数：

| | |

| :--- | :--- |

| -16.16 T, I/,V,A | xA yA xA yA xB yB xB yB x_P y_P |

| Color Style | xA yA vXA vA axA yB xB vB vB axB yB ay xP yP |

程序 `OffsetV` 的输入参数：

| | |

| :--- | :--- |

| -16.16 T, I/,V,A | xA yA xA yA xB yB yB xB yB xB AP BP ABP |

| Color Style | xA yA vXA vA axA yB xB vB vB axB yB ay BP ABP |

程序 `Offset` 和 `OffsetV` 的输出参数：

| | |

| :--- | :--- |

| xP yP | xP yP yP |

| xP vXP vYP ayP | |

如果图形系统，这些程序在返回点 P 及其一阶、二阶导数后，将在计算机屏幕上绘制，当前 DXF 文件的分析图形有助于定位 P（见图 5.8 和附录 B 中的 `P5_08A.PAS` 和 `P5_08B.PAS`）。如果 `Style` 等于 `"/"` 或 `"\"`, 程序将分别连接 A 和 P 或 B 和 P。如果参数 `Style` 等于 `"I"` 或 `"T"`，将绘制一条从点 P 垂直于 `AB` 的线，而 `Style` 等于 `"T"`，还会额外绘制连接 A 和 B 的线。如果 `Style` 等于 `"v"`，则绘制多折线 `APB`，而 `Style` 等于 `"A"`，则绘制完整的三角形 `ABP`。如果参数 `Color` 为正且调用 `SetJoinSize` 时带有正参数（即关节为全视图），则三角形 `ABP` 将填充颜色。否则，将绘制一个透明三角形

![](img/fe0d0bb9b123aa34fc70ee5a03e0d0dd_194_0.png)

`ABP`。如果参数 `Color` 设置为 0，或 `Style` 被分配为空字符，则没有线或三角形角。

## 5.3.2 程序 AngVA, Ang3VA 和 Ang4VA

可以使用方程 `21`、`25` 和 `28` 计算连接有 A、B 点的刚性杆的角位置、速度和加速度。这些方程已在程序 `AngVA` 中实现，头部为：

```
procedure AngVA (xA, yA, vxA, vyA, xA, ayA, xB, yB, vxB, vyB, xB, ayB:double; var yD, dTheta, ddTheta:double);
```

用户必须提供 A、B、C 和 D 点的 x 和 y 坐标以及速度和加速度的标量分量。关于角 Theta 带有初始意义值或上一个值的要求也适用于程序 `Ang3PVA` 和 `Ang4VA`。

# 平面机械系统的运动仿真程序

**重要：** `LibMec2D` 单元中的程序假设所有角度均为弧度 `rad`，角速度为 `rad/s`，角加速度为 `rad/s²`。

**重要：** 在程序 `Offset`、`OffsetV`、`AngPVA`、`Ang3PVA` 和 `Ang4PVA` 中，距离 `AB` 和 `BC` 保持不变，否则这些程序返回的时间导数将是不正确的。距离不保持不变的情况将在下一节讨论。

## 5.4 相对运动中的位置、速度和加速度：程序 VarDist

比之前讨论的更一般的情况是 A 点和 B 点之间的距离不保持不变（见图 5.9）。给定这两个点相对于 `OXY` 坐标系的坐标 `x_A, y_A` 和 `x_B, y_B`，以及它们的速度和加速度在 `OX` 和 `OY` 轴上的投影（即 `x_A, y_A, x_B, y_B, x_A, y_A, x_B, y_B`），我们想要找到它们之间的距离 `r`，以及 `AB` 线与 `OX` 轴构成的角 `θ`。我们感兴趣的可变距离 `r` 和角度 `θ` 的一阶和二阶时间导数，分别为 `r, r', r''` 和 `θ, θ'`。

距离 `r` 可以可以使用公式计算：

```
r = \sqrt{(xB-xA)^2+(yB-yA)^2} \quad (5.29)
```

为了确定速度和加速度分量，我们将向量方程 `AB = OB - OA` 投影到固定参考系 `OXY` 的坐标轴上，并得到：

```
r\cosθ = xB-xA
r\sinθ = yB-yA \quad (5.30)
```

![](img/fe0d0bb9b123aa34fc70ee5a03e0d0dd_196_0.png)

图 5.9 计算由运动点 A 和 B 决定的可变距离 `r` 和角度 `θ`，以及时间导数 `r, r', r'', θ` 和 `θ'` 的示意图。虚线还显示了相对于导轨移动的滑块科里力加速度矢量。

## 170 AutoCAD 用户的计算机辅助绘图和仿真工具

其中角度 `θ` 可以用方程 `5.21` 计算。对方程 `5.30` 关于时间求导，得到一个关于未知数 `hat r` 和 `θ` 的两个线性方程组：

```
$\begin{aligned}&\hat{r}\cdot\cos\theta-\dot{\hat{r}}\cdot\sin\theta &= \dot{x}B-\dot{x}A\\\dot{\hat{r}}\cdot\sin\theta+\dot{\hat{r}}\cdot\cos\theta &= \dot{y}B-\dot{y}A\end{aligned}$
```

将其与方程 `5.30` 结合，变为：
