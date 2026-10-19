
我们在前面已经看到，(22.60) 式表明，减小时间步长可以提高精度并保持稳定性；但减小空间步长则必须同时减小时间步长，才能维持稳定性（你应该自行验证这一点）。

### 清单 22.2 FDTD.py 通过 FDTD 时间步进（时域有限差分）求解自由空间中沿 z 方向传播的线偏振波的麦克斯韦方程组。

```
# FDTD.py  FDTD solution of Maxwell's equations in 1D

from visual import *
xmax=201
ymax=100
zmax=100
scene = display(x=0,y=0,width= 800, height= 500, \
    title='E: cyan, H: red. Periodic BC',forward=(-0.6,-0.5,-1))
Efield = curve(x=list(range(0,xmax)),color=color.cyan,radius=1.5,display=scene)
Hfield = curve(x=list(range(0,xmax)),color=color.red,
    radius=1.5,display=scene)
vplane= curve(pos=[(-xmax,ymax),(xmax,ymax),(xmax,-ymax),(-xmax,-ymax),
    (-xmax,ymax)],color=color.cyan)
zaxis=curve(pos=[(-xmax,0),(xmax,0)],color=color.magenta)
hplane=curve(pos=[(-xmax,0,zmax),(xmax,0,zmax),(xmax,0,-zmax),
    (-xmax,0,-zmax),(-xmax,0,zmax)],color=color.magenta)
ball1 = sphere(pos = (xmax+30, 0,0), color = color.black, radius = 2)
ts = 2
# time switch
beta = 0.01
Ex = zeros((xmax,ts),float)      # init E
Hy = zeros((xmax,ts),float)      # init H
Exlabel1 = label( text = 'Ex', pos = (-xmax-10, 50), box = 0 )
Exlabel2 = label( text = 'Ex', pos = (xmax+10, 50), box = 0 )
Hylabel  = label( text = 'Hy', pos = (-xmax-10, 0,50), box = 0 )
zlabel  = label( text = 'Z',  pos = (xmax+10, 0), box = 0 )
ti=0

def inifields():
    k = arange(xmax)
    Ex[:xmax,0] = 0.1*sin(2*pi*k/100.0)
    Hy[:xmax,0] = 0.1*sin(2*pi*k/100.0)

def plotfields(ti):
    # screen coordinates
    k = arange(xmax)
    Efield.x = 2*k-xmax
    # world to screen coords
    Efield.y = 800*Ex[k,ti]
    Hfield.x = 2*k-xmax
    Hfield.z = 800*Hy[k,ti]

inifields()
plotfields(ti)
# initial field
while True:
    rate(600)
    Ex[1:xmax-1,1] = Ex[1:xmax-1,0] + beta*(Hy[0:xmax-2,0]-Hy[2:xmax,0])
    Hy[1:xmax-1,1] = Hy[1:xmax-1,0] + beta*(Ex[0:xmax-2,0]-Ex[2:xmax,0])
    Ex[0,1] = Ex[0,0] + beta*(Hy[xmax-2,0] -Hy[1,0]) # BC
    Ex[xmax-1,1] = Ex[xmax-1,0] + beta*(Hy[xmax-2,0] -Hy[1,0])
    Hy[0,1] = Hy[0,0] + beta*(Ex[xmax-2,0] -Ex[1,0]) # BC
    Hy[xmax-1,1] = Hy[xmax-1,0] + beta*(Ex[xmax-2,0] - Ex[1,0])
    plotfields(ti)
    Ex[:xmax,0] = Ex[:xmax,1]               # New->old
    Hy[:xmax,0] = Hy[:xmax,1]
```

![](img/bccda43674e4a93dee81c749eba8d2f7_553_0.png)

(a)

(b)

图 22.9  E 场（亮）与 H 场（暗）在初始时刻 (a) 和稍后时刻 (b) 的分布。空间区域两端采用周期性边界条件，这意味着大 z 处的波会继续进入 z = 0 处的波。

### 22.7.1 实现

在清单 22.2 中，我们给出了一个简单的 FDTD 算法实现，用于包含 200 个格点的 z 方向网格；图 22.9 展示了一些结果。初始条件对应于 E 场和 H 场在 0 ≤ z ≤ 200 范围内所有 z 值上的正弦变化：

$$E_x(z, t = 0) = 0.1 \sin \frac{2\pi z}{100}, \quad H_y(z, t = 0) = 0.1 \sin \frac{2\pi z}{100}. \quad (22.61)$$

随后，该算法按照用户需要的时间步数逐步向前推进。所使用的麦克斯韦方程组离散形式为：

```
Ex[k, 1] = Ex[k, 0] + beta * (Hy[k-1, 0] - Hy[k+1, 0])
Hy[k, 1] = Hy[k, 0] + beta * (Ex[k-1, 0] - Ex[k+1, 0])
```

其中 1 ≤ k ≤ 200，beta 为常数。第二个索引取值为 0 和 1，0 代表旧时刻，1 代表新时刻。每次迭代结束时，整个空间中的新场变为旧场，然后计算新的场。在该算法中，空间端点 k=0 和 k=xmax-1 未被定义。我们通过假设周期性边界条件来定义它们：

```
Ex[0, 1] = Ex[0, 0] + beta* (Hy[xmax-2, 0] - Hy[1,0])
Ex[xmax-1, 1] = Ex[xmax-1, 0] + beta* (Hy[xmax-2, 0] - Hy[1,0])
Hy[0, 1] = Hy[0, 0] + beta* (Ex[xmax-2, 0] - Ex[1,0])
Hy[xmax-1, 1] = Hy[xmax-1, 0] + beta* (Ex[xmax-2, 0] - Ex[1,0])
```

### 22.7.2 评估

- 1. 施加边界条件，使所有场在边界处为零。将这样得到的解与没有显式边界条件的解进行比较，分别在脉冲到达边界之前和之后的时间进行。
- 2. 考察不同 Δz 和 Δt 取值下解的稳定性，并据此检验 Courant 条件 (22.60)。
- 3. 扩展算法，使其包含电磁波进入、穿过并离开置于 z 积分区域内的介电材料的效果。
- 4. 确保你在边界处同时观察到透射和反射。
- 5. 研究改变介质折射率带来的影响。
- 6. 脉冲的传播方向为 E × H 的方向，这取决于 E 场和 H 场之间的相对相位。（若没有初始 H 场，我们会得到向左和向右两个方向的脉冲。）
- 7. 修改程序，使初始时刻同时存在 H 脉冲和 E 脉冲，两者都具有高斯函数乘以正弦函数的形状。
- 8. 验证当 E 场和 H 场的相对相位为 0 或 π 时，传播方向是否会改变。
- 9. 通过选取边界处具有节点的平面波作为初始条件，研究波导的谐振模式。
- 10. 研究波长比积分区域尺寸更长的驻波。
- 11. 通过在算法中内置周期性边界条件，模拟无界传播。
- 12. 在积分体积内放置具有周期性介电常数的介质。这应起到频率相关滤波器的作用，某些频率完全无法传播。

### 22.7.3 扩展：圆偏振波

我们现在将处理方法扩展到 E 场和 H 场仍然横向且沿 z 方向传播，但不限于仅沿一个轴线性偏振的电磁波。为此，我们在 (22.46) 和 (22.47) 的基础上增加：

$$\frac{\partial H_x}{\partial t} = \frac{1}{\mu_0} \frac{\partial E_y}{\partial z}, \quad (22.62)$$

$$\frac{\partial E_y}{\partial t} = \frac{1}{\varepsilon_0} \frac{\partial H_x}{\partial z}. \quad (22.63)$$

按照与 (22.51) 和 (22.52) 相同的方式进行离散化后，我们得到

$$H_x^{k+1/2,n+1} = H_x^{k+1/2,n} + \frac{\Delta t}{\mu_0 \Delta z} \left(E_y^{k+1,n+1/2} - E_y^{k,n+1/2}\right), \quad (22.64)$$

$$E_y^{k,n+1/2} = E_y^{k,n-1/2} + \frac{\Delta t}{\varepsilon_0 \Delta z} \left(H_x^{k+1/2,n} - H_x^{k-1/2,n}\right). \quad (22.65)$$

为了产生圆偏振行波，我们设置如下初始条件：

$$E_x = \cos\left(t - \frac{z}{c} + \phi_y\right), \quad H_y = \sqrt{\frac{\varepsilon_0}{\mu_0}} \cos\left(t - \frac{z}{c} + \phi_y\right), \quad (22.66)$$

$$E_y = \cos\left(t - \frac{z}{c} + \phi_x\right), \quad H_x = \sqrt{\frac{\varepsilon_0}{\mu_0}} \cos\left(t - \frac{z}{c} + \phi_x + \pi\right). \quad (22.67)$$

我们取相位 φ_x = π/2，φ_y = 0，因此它们的差 φ_x − φ_y = π/2，这导致圆偏振。我们用与高斯脉冲相同的方式加入初始条件，只不过现在使用这些余弦函数。

清单 22.3 给出了我们的实现 EMcirc.py，用于具有横向双分量 E 场和 H 场的波。图 22.10 展示了模拟的部分结果，其中你可以注意到 E 和 H 之间的相位差。

![](img/bccda43674e4a93dee81c749eba8d2f7_555_0.png)

图 22.10  自由空间中圆偏振波在 t = 100 时的 E 场和 H 场。

### 清单 22.3 CircPolarztn.py 通过 FDTD 时间步进求解自由空间中沿 z 方向传播的圆偏振波的麦克斯韦方程组。

```
# CircPolarztn.py: solves Maxwell eqs. using FDTD
from visual import *
scene = display(x=0, y=0, width=600, height=400,range=200,
    title="Circular polarization, E field in white, H field in yellow")
global phx, phy
max = 201
c = 0.01                         # Courant stable if c < 0.1
Ex = zeros((max+2,2),float)
Hy = zeros((max+2,2),float)
Ey = zeros((max+2,2),float)
Hx = zeros((max+2,2),float)
arrowcol= color.white
Earrows = []
Harrows = []
for i in range(0,max,10):
    Earrows.append(arrow(pos=(0,i-100,0), axis=(0,0,0), color=arrowcol))
    Harrows.append(arrow(pos=(0,i-100,0), axis=(0,0,0), color=color.yellow))
def plotfields(Ex,Ey,Hx,Hy):
    for n, arr in enumerate(Earrows):
        arr.axis = (35*Ey[10*n,1],0,35*Ex[10*n,1])
    for n, arr in enumerate(Harrows):
        arr.axis = (35*Hy[10*n,1],0,35*Hx[10*n,1])
def inifields():
    phx = 0.5*pi
    phy = 0.0
    k = arange(0,max)
```

