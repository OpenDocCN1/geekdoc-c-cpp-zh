
## 36.5 视锥剔除与裁剪

假设在光栅化下，我们依赖某种精确方法来获得正确的可见性，例如深度缓冲或 Newell 等人的深度排序算法。为避免写入非法或不正确的内存地址，假设我们对视口执行二维**剪刀裁剪**。这只是说，光栅化器可能生成视口外的 (x, y) 位置，但我们只允许它写入视口内位置的内存。我们也可以在深度方向进行剪刀裁剪：不得写入任何深度表明其位于相机后方或远平面之后的样本。

回顾第 13 章，一个矩形视口与平行于图像平面的近平面和远平面定义了一个称为视锥体的三维空间体积。这是一个底面为矩形、顶部被截去的棱锥。在三维中裁剪到视锥体的侧面，对应于将图元的投影裁剪到视口，并且与仅在二维中进行剪刀裁剪产生等效结果。

仅靠剪刀裁剪可以确保正确性，但可能导致效率低下。例如，大多数被光栅化的图元可能无法通过剪刀测试。在这种情况下，有三种与视锥体相关的常见方法可以提高效率。

- **视锥剔除：** 为提高效率，消除完全位于视锥体外的多边形。
- **近平面裁剪：** 针对近平面裁剪多边形，以启用更简单的光栅化算法，并避免在未通过深度剪刀测试的样本上浪费计算。
- **整个视锥体裁剪：** 为提高效率，将多边形裁剪到侧面和远平面。

一般来说，让剪刀裁剪和裁剪相互补充是一种好策略。只在各自具有高效率且实现复杂度低的情况下使用它们。例如，先基于视锥体进行粗剔除，然后裁剪到近平面，并在二维中进行剪刀裁剪。对于投影相对于视口较小的图元，这会使剪刀测试通常通过，这意味着大多数执行了大量计算的光栅化图元的大部分通常位于屏幕上。

### 36.5.1 视锥剔除

消除视锥体外的多边形很简单。一种三维算法针对包围视锥体的每个平面测试多边形的每个顶点。假设这些平面的朝向使得视锥体是六个正半空间的交集。如果存在某个平面，使得多边形的所有顶点都位于负半空间，那么该多边形必定完全位于视锥体外，可以被剔除。对于小多边形，对每个多边形执行此测试可能并不高效。例如，如果一个多边形至多影响一个样本，那么对单个点进行三维包围盒测试会产生相同结果。因此，视锥剔除可以在包围盒层次结构上执行。

刚才描述的三维视锥剔除算法的一个缺点是它可能过于保守。位于视锥体外但靠近角或边的多边形可能与多个平面相交。

### 36.5.2 裁剪

### 36.5.2.1 Sutherland-Hodgman 二维裁剪

有许多裁剪算法。也许最简单的是 Sutherland 和 Hodgman [SH74] 算法的二维变体。它用一个（任意）源多边形针对第二个凸边界多边形进行裁剪（见图 36.16）。该算法通过让源多边形依次针对穿过边界多边形每条边的直线进行增量裁剪来推进，如代码清单 36.3 所示。

> **内联练习 36.5：** 构造一个示例输入多边形，当用 Sutherland-Hodgman 算法针对单位正方形裁剪时，会产生带有退化边的多边形（即这些边在顶点 *v* 处以 180° 的外角相接）。

![](img/f464cd0043eb5336aa0543fe20a0561b_1095_0.png)

*图 36.16：红色输入多边形被裁剪到凸的蓝色边界多边形上；结果是黄色阴影区域的边界。*

对于视口裁剪，Sutherland-Hodgman 算法应用于投影后的多边形和视口矩形。对于在视口外有显著面积的投影多边形，裁剪到视口是比逐采样点进行剪刀测试更高效的替代方案。该算法作为通用几何操作在许多场景中也很有用，包括最初对形状进行建模。

*代码清单 36.3：二维 Sutherland-Hodgman 裁剪的伪代码。*

```text
// the arrays are the vertices of the polygons.
// boundaryPoly must be convex.
function polyClip(Point sourcePoly[], Point boundaryPoly[]) :
    for each edge (A, B) in boundaryPoly:
        sourcePoly = clip(sourcePoly, A, Vector(A.y-B.y, B.x-A.x))
    return sourcePoly

// True if vertex V is on the "inside" of the line through P
// with normal n. The definition of inside depends on the
// direction of the y-axes and whether the winding rule is
// clockwise or counter-clockwise.
function inside(Point V, Point P, Vector n):
    return (V - P).dot(n) > 0

// Intersection of edge CD with the line through P with normal n
function intersection(Point C, Point D, Point P, Vector n):
    distance = (C - P).dot(n) / n.length()
    t = (D - C).length()
    return D * t + C * (1 - t)

// Clip polygon sourcePoly against the line through P with normal n
function clip(Point sourcePoly[], Point P, Vector n):
    Point result[];

    // Add the last point, if it is inside
    D = sourcePoly[sourcePoly.length - 1]
    Din = inside(D, P, n)
    if (Din): result.append(D)

    for (i = 0; i < sourcePoly.length; ++i) :
        C = D, Cin = Din

        D = sourcePoly[i]
        Din = inside(D, P, n)

        if (Din != Cin):  // crossed the line
            result.append(intersection(C, D, P, n))

        if (Din): result.append(D)

    return result
```

该算法会产生一些退化边，这些边对多边形光栅化没有影响，但当我们在其他场景中应用相同思路时可能引发问题。

### 36.5.2.2 近平面裁剪

二维 Sutherland-Hodgman 算法可以推广到更高维度。要将多边形裁剪到平面，我们遍历各条边，寻找与平面的交点。我们可以对整个视锥体这样做，每次处理一个平面。不过，现在只考虑裁剪到近平面这一步。

在相机空间中，多边形边与近平面的交点很容易找到，因为近平面有一个简单的方程：z = −zn。事实上，这与用直线裁剪多边形是完全相同的问题，因为我们可以将问题正交投影到 xz 平面或 yz 平面。我们将多边形上线性变化的顶点属性线性插值到裁剪引入的新顶点，就好像它们是额外的空间维度一样。代码清单 36.4 以伪代码给出了细节，用于将由顶点列表指定的多边形裁剪到平面 z = −zn，其中 zn < 0。

*代码清单 36.4：将由 `vertex` 数组表示的多边形裁剪到近平面 z = −zn。*

```python
function clipPolygon(inputVertices, zn):
    outVertices = []
    Let start = inputVertices.last()
    for end in inputVertices:
        if end.z <= zn:
            if start.z > zn:
                // We crossed into the frustum
                outVertices.append(clipLine(start, end, zn))

            // the endpoint of this edge is in the frustum
            outVertices.append(end)

        elif start.z <= zn:
            // We crossed out of the frustum
            outVertices.append(clipLine(start, end, zn))

        start = end

    return outVertices

function clipLine(start, end, zn):
    a = (zn - start.z) / (end.z - start.z)
    // This holds for any vertex properties that we
    // wish to linearly interpolate, not just position
    return start * a + end * (1 - a)
```

### 36.5.3 裁剪到整个视锥体

针对近平面裁剪之后，我们可以保证多边形中的每个顶点都有 z < 0。这意味着我们可以将多边形投影到**齐次裁剪空间**，如第 13 章所述，通过透视投影将视锥体映射到一个立方体。

我们可以在投影之前继续用 Sutherland-Hodgman 裁剪处理三维中的其他视锥体平面。然而，侧面平面不像近平面那样与某个轴正交，因此裁剪到这些平面时每个顶点需要更多操作。相比之下，在透视投影*之后*，每个视锥体平面都与某个轴正交，所以对侧面平面的裁剪和对近平面的裁剪同样高效。也就是说，裁剪再次成为二维操作。裁剪到远平面既可以在投影之前进行，也可以在投影之后进行。

在笛卡尔三维空间中针对近平面进行裁剪时，我们能够线性插值诸如纹理坐标之类的逐顶点属性。在齐次裁剪空间中，这些属性沿边不再线性变化，因此我们不能直接进行线性插值。不过，这种关系几乎同样简单。

在实践中，我们不需要为每次边裁剪操作执行所有这些运算。相反，在投影位置时，我们可以通过 u′ = −u/z 投影每个属性。然后，我们可以像属性是线性且所有操作都是二维的那样，对所有裁剪都在 u′ 属性上执行。回顾一下，光栅化需要以透视正确的方式插值属性，因此它本来就会沿扫描线对 u′ 属性进行操作（参见 *深度缓冲*）。只有在逐样本“着色”步骤中，我们才通过使用双曲插值后的 z 值计算 u = −u′/z，返回到原始属性空间。因此，在实践中，三维属性的裁剪（和光栅化）成本与二维属性相同，并且所有二维优化技术（如有限差分）都可以应用于 u′ 值。

### 36.6 背面剔除

不透明实体对象的背面必然从观察者的直接视线中隐藏。对象本身会遮挡观察射线。因此，剔除位于对象背面的图元可以保守地消除大约一半的场景几何体。如前所述，背面剔除在计算可见性函数时是一种很好的优化，但不适用于整个渲染管线。当我们考虑整个渲染管线时，图像可能受到相机不能直接看到的点的影响，例如通过镜中反射看到的物体，以及由视场外物体投射的阴影。因此，虽然背面剔除是优化可见性时最先想到的工具之一，但重要的是要在正确的阶段应用它。人们偶尔会看到程序在错误阶段进行剔除所导致的错误，例如当阴影投射者不在视野内时阴影消失。

尽管背面剔除可以应用于参数曲面，但通常在多边形上执行。这是因为在多边形上的单个点进行测试就能表明整个多边形位于对象正面还是背面，所以测试多边形非常高效。曲线可能需要在多个点进行测试，或对整个表面进行解析测试，才能作出相同判断。

我们凭直觉就能识别物体的背面——也就是我们看不到的那一面！——但如何在几何上区分它呢？考虑一个没有自相交的封闭多边形网格，以及位于多面体外部的点 Q 处的观察者。
