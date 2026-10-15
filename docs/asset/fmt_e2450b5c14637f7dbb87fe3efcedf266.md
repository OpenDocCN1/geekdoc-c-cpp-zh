
# 列表 8.11 旋转分子到主轴系（Python 编码）

```
#---------------------------------------- coords.py ----------------------------------------
# Contains routines for transforming the coordinates of systems of particles
# Author: Titus Beu, 2013
#--------------------------------------------------------------------------------------------
from eigsys import *

#============================================================================================
def MovetoCM(m, x, y, z, n):
#--------------------------------------------------------------------------------------------
# Moves a system of n particles to the CM system
#--------------------------------------------------------------------------------------------
mCM = 0e0; xCM = 0e0; yCM = 0e0; zCM = 0e0
for i in range(1,n+1):
    mCM += m[i]
xCM += m[i] * x[i]
yCM += m[i] * y[i]
zCM += m[i] * z[i]
xCM /= mCM; yCM /= mCM; zCM /= mCM

for i in range(1,n+1):
    x[i] -= xCM; y[i] -= yCM; z[i] -= zCM

#==============================================================================
def PrincipalAxes(m, x, y, z, n, isort):
#------------------------------------------------------------------------------
# Rotates a set of n particles to the system of principal axes
# isort = 1 - highest symmetry axis along x-axis
# isort = -1 - highest symmetry axis along z-axis
#------------------------------------------------------------------------------
Inert = [[0]*4 for i in range(4)]
Rot = [[0]*4 for i in range(4)]
MomInert = [0]*4

for i in range(1,4):
    for j in range(1,i+1): Inert[i][j] = 0e0

for i in range(1,n+1):
    mi = m[i]; xi = x[i]; yi = y[i]; zi = z[i]
    Inert[1][1] += mi * (yi*yi + zi*zi)                     # inertia tensor
    Inert[2][2] += mi * (zi*zi + xi*xi)
    Inert[3][3] += mi * (xi*xi + yi*yi)
    Inert[2][1] -= mi * xi*yi
    Inert[3][1] -= mi * zi*xi
    Inert[3][2] -= mi * yi*zi

Jacobi(Inert,Rot,MomInert,3)                               # diagonalize inertia tensor
EigSort(Rot,MomInert,3,isort)                              # sort eigenvalues and eigenvectors

for i in range(1,n+1):                                     # rotate system to principal axes
    xi = x[i]; yi = y[i]; zi = z[i]
    x[i] = Rot[1][1] * xi + Rot[2][1] * yi + Rot[3][1] * zi
    y[i] = Rot[1][2] * xi + Rot[2][2] * yi + Rot[3][2] * zi
    z[i] = Rot[1][3] * xi + Rot[2][3] * yi + Rot[3][3] * zi

return MomInert
```

```
# Rotation of a molecule to the system of principal axes
from math import *
from eigsys import *
from coords import *
from matutil import *
from graphlib import *

n = 5                                                       # number of particles
m = [0,12.000, 1.000, 1.000, 1.000, 1.000]                   # masses
x = [0, 0.000, 0.635,-0.635,-0.635, 0.635]                   # positions
y = [0, 0.000, 0.635,-0.635, 0.635,-0.635]                   # [0] not used
z = [0, 0.000, 0.635, 0.635,-0.635,-0.635]
r = [0, 0.300, 0.200, 0.200, 0.200, 0.200]                   # radii
col = ["", "red", "blue", "blue", "blue", "gray"]        # colors

dmax = 1.5e0                                      # cutoff distance for bonds

m[5] += 1e-10                                     # "mark" last particle to set principal symmetry axis

GraphInit(1200,600)

title = "Initial configuration"
PlotParticles(x,y,z,r,col,n,dmax,0e0,0e0,0,0e0,0e0,0,0.05,0.25,0.2,0.8,title)

MovetoCM(m,x,y,z,n)                               # move to CM system

MomInert = PrincipalAxes(m,x,y,z,n,1)             # align main symmetry axis to x
print("Structure aligned to x-axis:")
VecPrint(x,n); VecPrint(y,n); VecPrint(z,n)
print("Principal moments of inertia:")
VecPrint(MomInert,3)
title = "System of principal axes - main x"
PlotParticles(x,y,z,r,col,n,dmax,0e0,0e0,0,0e0,0e0,0,0.45,0.65,0.2,0.8,title)

MomInert = PrincipalAxes(m,x,y,z,n,-1)            # align main symmetry axis to z
print("\nStructure aligned to z-axis:")
VecPrint(x,n); VecPrint(y,n); VecPrint(z,n)
print("Principal moments of inertia:")
VecPrint(MomInert,3)
title = "System of principal axes - main z"
PlotParticles(x,y,z,r,col,n,dmax,0e0,0e0,0,0e0,0e0,0,0.75,0.95,0.2,0.8,title)

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_277_0.png)

图 8.2 甲烷分子在初始构型（左）、旋转到主轴系且主对称轴沿 `x`（中）、以及分别主对称轴沿 `z`（右）。

# 列表 8.12 旋转飞机（Python 编码）

```
# Rotation of an airplane
from math import *
from egsys import *
from coords import *
from matutil import *
from graphlib import *

n = 10                                          # number of corner points
m = [0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0]            # masses
x = [0,-2,-6, 2, 0, 2, 6, 1, 2,-2, 2]            # positions
y = [0,-2, 2,-6, 2, 0, 6, 2, 1,-2, 2]            # [0] not used
z = [0, 0, 0, 0, 0, 0, 0, 1, 1, 4, 1]

n3 = 9                                          # number of defining triangles
ind1 = [0, 1, 1, 1, 1, 1, 1, 1, 6, 1]            # indexes of triangle corners
ind2 = [0, 2, 3, 4, 5, 4, 5, 7, 7, 9]
ind3 = [0, 4, 5, 6, 6, 7, 8, 8, 8,10]

GraphInit(800,800)

title = "Initial configuration"
PlotStruct(x,y,z,n,ind1,ind2,ind3,n3,
           0e0,0e0,0,0e0,0e0,0,0.05,0.45,0.55,0.92,title)

MovetoCM(m,x,y,z,n)                             # move structure to CM

PrincipalAxes(m,x,y,z,n,1)                      # rotate airplane to principal axes
print("Airplane in system of principal axes:")
VecPrint(x,6); VecPrint(y,6); VecPrint(z,6)
title = "System of principal axes"
PlotStruct(x,y,z,n,ind1,ind2,ind3,n3,
           0e0,0e0,0,0e0,0e0,0,0.55,0.95,0.55,0.92,title)

f = pi/180e0
phi = 20                                        # yaw
cosp = cos(phi*f); sinp = sin(phi*f)
for i in range(1,n+1):                          # rotate airplane about z-axis
    xi = x[i]
    x[i] = cosp * xi - sinp * y[i]
    y[i] = sinp * xi + cosp * y[i]
print("\nRotated airplane yaw = {0:4.1f}".format(phi))
VecPrint(x,6); VecPrint(y,6); VecPrint(z,6)
title = "yaw = {0:4.1f}".format(phi)
PlotStruct(x,y,z,n,ind1,ind2,ind3,n3,
           0e0,0e0,0,0e0,0e0,0,0.05,0.45,0.05,0.42,title)

phi = -35                                       # roll
cosp = cos(phi*f); sinp = sin(phi*f)
for i in range(1,n+1):                          # rotate airplane about x-axis
    yi = y[i]
    y[i] = cosp * yi - sinp * z[i]
    z[i] = sinp * yi + cosp * z[i]
print("\nRotated airplane roll = {0:4.1f}".format(phi))
VecPrint(x,6); VecPrint(y,6); VecPrint(z,6)
title = "roll = {0:4.1f}".format(phi)
PlotStruct(x,y,z,n,ind1,ind2,ind3,n3,
           0e0,0e0,0,0e0,0e0,0,0.55,0.95,0.05,0.42,title)

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_280_0.png)

图 8.3 初始构型中的飞机（左上），绕 `x` 轴旋转至主轴系，主对称轴沿 `x`（右上），绕垂直 `z` 轴旋转（偏航）（左下），以及绕 `x` 轴旋转（滚转）（右下）。

## 问题 8.5

在 Hückel 理论框架下，通过求解标准特征值问题求出环状苯分子 `C₆H₆` 的本征能量和本征向量：

`H · C = C · E`.

哈密顿矩阵可以用库仑积分 `α = −6.9 eV` 和共振能 `β = −3.1 eV` 表示（Broglia and Heilbronner 1972）：

```
H = [ [α, β, 0, 0, 0, β], [β, α, β, 0, 0, 0], [0, β, α, β, 0, 0], [0, 0, β, α, β, 0], [0, 0, 0, β, α, β], [β, 0, 0, 0, β, α] ]
```

精确的本征值（`E` 的对角元素）和本征向量为

`E₁ = α + 2β`,    `E₂ = E₃ = α + β`,    `E₄ = E₅ = α − β`,    `E₆ = α − 2β`,

`C₁ = 1/√6 [1 1 1 1 1 1]ᵀ`, `C₂ = 1/2 [1 1 0 -1 -1 0]ᵀ`, `C₃ = 1/2 [1 0 -1 -1 0 1]ᵀ`,

`C₄ = 1/2 [1 -1 0 1 -1 0]ᵀ`, `C₅ = 1/2 [1 0 -1 1 0 -1]ᵀ`, `C₆ = 1/√6 [1 -1 1 -1 1 -1]ᵀ`.

利用例程 `EigSym`，证明非简并态 `E₁` 和 `E₆` 的精确本征值和本征向量被正确再现，并解释为什么简并态的本征向量与精确值不同，但仍是正确的。通过最大范数估计解的精度：

`‖H · C − C · E‖ = maxᵢⱼ |(H · C − C · E)ᵢⱼ|`,

其预期为零。

## 解

应注意，作为一般性质，对应于简并本征值的本征向量的任意线性组合仍是对应于相同本征值的本征向量。相应地，能级 `E₂ = E₃` 和 `E₄ = E₅` 为二重简并，可以通过任意线性组合 `γ₂C₂ + γ₃C₃` 以及分别 `γ₄C₄ + γ₅C₅` 正确描述。

Python 实现如清单 8.13 所示，C/C++ 版本作为补充材料提供（`P08-Hueckel.cpp`）。

### 清单 8.13 苯的 Hückel 方法（Python 编码）
