

## 1.5.2 VPython 的动画

使用 Visual 创建动画本质上就是一遍又一遍地绘制相同的 2D 图，每次都在略有不同的时间点上，然后将这些图叠加在一起。操作得当的话，这会给人以运动的印象。我们的大多数示例代码都生成了动画，例如 HarmosAnimate.py 和 3DAnimate.py。图 1.3b 显示了由 HarmosAnimate.py 产生的三个帧。这些代码的主要部分处理的是 PDE 的求解，这暂时与我们无关。使动画生效的部分很简单：

```python
PlotObj= curve(x=xs, color=color.yellow, radius=0.1)
...
while True:
    rate(500)                # Runs forever
    psr[1:-1] = ...
    psi[1:-1] = ...
    PlotObj.y = 4*(psr**2 + psi**2)
```

这里 PlotObj 是一个曲线，它不断地在 while 循环内部构建，因此看起来在移动。注意，能够在不将所有时间点都存储在数组中的情况下逐个绘制点，可以使程序的内存需求保持很小，从而实现快速的程序。

### Listing 1.4 EasyMatPlot.py 使用 Matplotlib 包生成 2D x–y 绘图（该包包含 NumPy 包）。

```python
# EasyMatPlot.py: Simple use of matplotlib's plot command
from pylab import *                     # Load Matplotlib
Xmin = -5.;  Xmax = +5.;  Npoints= 500
DelX = (Xmax - Xmin) / Npoints
x = arange(Xmin, Xmax, DelX)
y = sin(x) * sin(x*x)                   # function of x array
print ('arange => x[0], x[1],x[499]=%8.2f %8.2f %8.2f' %(x[0],x[1],x[499]))
print ('arange => y[0], y[1],y[499]=%8.2f %8.2f %8.2f' %(y[0],y[1],y[499]))
print ('\n Now doing the plotting thing, look for Figure 1 on desktop' )
xlabel('x'); ylabel('f(x)'); title(' f(x) vs x')
text(-1.75, 0.75, 'MatPlotLib \n Example')     # Text on plot
plot(x, y, '-', lw=2)
grid(True)                              # Form grid
show()
```

## 1.5.3 Matplotlib 的 2D 绘图

Matplotlib 是一个功能强大的绘图包，可让你直接在 Python 程序中制作 2D 和 3D 图形、直方图、功率谱、条形图、误差图、散点图等。Matplotlib 是免费的，使用了 NumPy 和 LAPACK 的复杂数值计算（Anderson et al., 2013），而且，令人难以置信的是，易于使用。具体来说，Matplotlib 使用 NumPy 数组（向量）对象来存储要绘制的数据。在第 6 章中，我们将更详细地讨论 NumPy 数组，因此你可能想尽快去那里更好地理解数组。

Matplotlib 命令的设计与 MATLAB 的绘图命令相似，MATLAB 是一个在工程领域特别流行的商业问题求解环境。与 MATLAB 一样，Matplotlib 假设你已将要绘制的 x 和 y 值放入 1D 数组（向量）中，然后一次性绘制这些向量。这与 Visual 不同，Visual 首先创建一个绘图对象，然后逐点向对象添加点。因为 Matplotlib 不是 Python 的标准部分，所以你必须将整个 Matplotlib 包或你使用的单个方法导入到你的程序中。例如，在 Listing 1.4 的 EasyMatPlot.py 的第 2 行（行号在右侧的深色阴影中），我们将 Matplotlib 导入为 pylab 库：

```python
from pylab import *        # Load Matplotlib
```

然后，在第 6 行和第 7 行我们计算并输入 x 和 y 值的数组

```python
x = arange(Xmin, Xmax, DelX)    # Form x array in range with increment
y = -sin(x)*cos(x)               # Form y array as function of x array
```

正如你所见，NumPy 的 arange 方法构造了一个从 Xmax 到 Xmin 以 DelX 为步长的数组。因为限制是浮点数，所以 x_i 也将是浮点数。因为 x 是一个数组，所以 y = -sin(x)*cos(x) 也会自动成为一个数组！实际的绘图在第 14 行执行，使用破折号 "-" 表示线条，lw = 2 设置其宽度。结果如图 1.5a 所示，并带有所需的标签和标题。show() 命令在你的桌面上生成图形。更多命令在表 1.3 中给出。我们建议你尝试一些选项和可能的绘图类型。

![](img/bccda43674e4a93dee81c749eba8d2f7_41_0.png)

图 1.5 Matplotlib 绘图。 (a) EasyMatPlot.py 的输出，显示一个简单的 x–y 绘图。 (b) GradesMatPlot.py 的输出，将两组数据点、两条曲线和不相等的上下误差条全部放在一个绘图上。

### 表 1.3 一些常见的 Matplotlib 命令。

| Command | Effect | Command | Effect |
|---|---|---|---|
| plot(x, y, '-', lw=2) | x−y curve, line width 2 | myPlot.setYRange(-8., 8.) | Set y range |
| show() | Show output graph | myPlot.setSize(500, 400) | Size in pixels |
| xlabel('x') | x-axis label | pyplot.semilogx | Semilog x plot |
| ylabel('f(x)') | y-axis label | pyplot.semilogy | Semilog y plot |
| title('f vs x') | Add title | grid(True) | Draw grid |
| text(x, y, 's') | Add text s at (x, y) | myPlot.setColor(false) | Black and White |
| myPlot.addPoint(0,x,y,true) | Add (x, y) to set 0 connect | myPlot.setButtons(true) | For zoom button |
| myPlot.addPoint(1,x,y, false) | Add (x, y) to 1, no connect | myPlot.fillPlot() | Fit ranges to data |
| pyplot.errorbar | Point + error bar | myPlot.setImpulses(true,0) | Vertical lines, set 0 |
| pyplot.clf() | Clear current figure | pyplot.contour | Contour lines |
| pyplot.scatter | Scatter plot | pyplot.bar | Bar charts |
| pyplot.polar | Polar plot | pyplot.gca | For current axis |
| myPlot.setXRange(-1., 1.) | Set x range | pyplot.acorr | Autocorrelation |

### Listing 1.5 GradesMatPlot.py 使用 Matplotlib 包生成 2D x–y 绘图。

```python
# Grade.py: Using Matplotlib's plot command with multi data sets & curves
import pylab as p                     # Matplotlib
from numpy import *

p.title('Grade Inflation')            # Title and labels
p.xlabel('Years in College')
p.ylabel('GPA')

xa = array([-1, 5])                   # For horizontal line
ya = array([0, 0])                    # "   "
p.plot(xa, ya)                        # Draw horizontal line

x0 = array([0, 1, 2, 3, 4])
y0 = array([-1.4, +1.1, 2.2, 3.3, 4.0]) # Data set 0 points
p.plot(x0, y0, 'bo')                  # Data set 0 = blue circles
p.plot(x0, y0, 'g')                   # Data set 0 = line

x1 = arange(0, 5, 1)                  # Data set 1 points
y1 = array([4.0, 2.7, -1.8, -0.9, 2.6])
p.plot(x1, y1, 'r')

errTop = array([1.0, 0.3, 1.2, 0.4, 0.1])   # Asymmetric error bars
errBot = array([2.0, 0.6, 2.3, 1.8, 0.4])
p.errorbar(x1, y1, [errBot, errTop], fmt = 'o')  # Plot error bars

p.grid(True)                          # Grid line
p.show()                              # Create plot on screen
```

在 Listing 1.5 中，我们给出了代码 GradesMatPlot.py，并在图 1.5b 中展示了其输出。这不是一个简单的绘图。这里我们多次重复 plot 命令，以便在同一张图上绘制多组数据集，并绘制数据

![](img/bccda43674e4a93dee81c749eba8d2f7_44_0.png)

(a) (b)

图 1.6 (a,b) 列显示了由 MatPlot2figs.py 产生的两个单独的输出，每个输出包含两个图形。 （我们使用滑块按钮在绘图之间添加了一些空间。）

放置了两条曲线在一个绘图上，然后输出两个不同的图形，每个图形包含两个绘图。关键在于 subplot 命令的重复：

```python
figure(1)               # The 1st figure
subplot(2,1,1)          # 2 rows, 1 column, 1st subplot
subplot(2,1,2)          # 2 rows, 1 column, 2nd subplot
```

该列表是自解释的，其中包含设置绘图限制的部分、创建每个图形的部分，然后创建网格。

### Listing 1.7 PondMatPlot.py 生成图 5.5 中第 5 章所示的散点图和曲线。

```python
# PondMatPlot.py: Monte-Carlo integration via vonNeumann rejection
import numpy as np
import matplotlib.pyplot as plt

N = 100
x1 = np.arange(0, 2*np.pi+2*np.pi/N,2*np.pi/N)
fig,ax = plt.subplots()
y1 = x1 * np.sin(x1)**2                # Integrand
ax.plot(x1, y1, 'c-', linewidth=4)
ax.set_xlim((0, 2*np.pi))
ax.set_ylim((0, 5))
ax.set_xticks([0, np.pi, 2*np.pi])
ax.set_xticklabels(['0', '$\uppi$', '2$\uppi$'])
ax.set_ylabel('$f(x) = x\sin^2 x$', fontsize=20)
ax.set_xlabel('x', fontsize=20)
fig.patch.set_visible(False)
xi=[]; yi=[]; xo=[]; yo=[]

def fx(x):                             # Integrand
    return x*np.sin(x)**2

j = 0                                  # Inside curve counter
Npts = 3000
analyt = np.pi**2
xx = 2.* np.pi * np.random.rand(Npts)  # 0 <= x <= 2pi
yy = 5*np.random.rand(Npts)           # 0 <= y <= 5
for i in range(1,Npts):
```

