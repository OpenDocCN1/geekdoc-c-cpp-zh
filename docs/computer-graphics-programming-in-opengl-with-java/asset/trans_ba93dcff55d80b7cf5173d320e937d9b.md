
## 参考文献

- **[BL78]** J. Blinn，“皱褶表面的模拟”，*Computer Graphics* 12，第 3 期（1978）：286–292。
- **[BN12]** E. Bruneton 和 F. Neyret，“面向高效准确表面着色的非线性预滤波方法综述”，*IEEE Transactions on Visualization and Computer Graphics* 18，第 2 期（2012），第 242–260 页。
- **[GI21]** GNU 图像处理程序，访问于 2021 年 3 月，http://www.gimp.org
- **[GN12]** GIMP *法线贴图插件*，访问于 2021 年 3 月，https://code.google.com/archive/p/gimp-normalmap/
- **[HT12]** J. Hastings-Trew，*JHT 的行星像素商店*，访问于 2021 年 3 月，http://planetpixelemporium.com/
- **[LU16]** F. Luna，*DirectX 12 3D 游戏编程入门*，第 2 版（Mercury Learning，2016）。
- **[ME11]** E. Meiri，*OGLdev 教程 26*，2011，访问于 2021 年 3 月，http://ogldev.atspace.co.uk/index.html
- **[PH21]** Adobe Photoshop，访问于 2021 年 3 月，http://www.photoshop.com
- **[SS15]** SSBump Generator，访问于 2021 年 3 月，https://sourceforge.net/projects/ssbumpgenerator/

## 参数化曲面

- 11.1 *二次贝塞尔曲线* ...... 261
- 11.2 *三次贝塞尔曲线* ...... 263
- 11.3 *二次贝塞尔曲面* ...... 266
- 11.4 *三次贝塞尔曲面* ...... 268
- *补充说明* ...... 270

20 世纪 50 年代和 60 年代，Pierre Bézier 在雷诺公司工作期间，开发了用于设计汽车车身的软件系统。他的程序利用了 Paul de Casteljau 早先开发的数学方程组，后者当时为竞争对手雪铁龙汽车制造商工作 [BE72, DC63]。de Casteljau 方程仅用少数标量参数来描述曲线，并配有一种巧妙的递归算法，称为“de Casteljau 算法”，用于以任意精度生成曲线。如今，这些方法被称为“贝塞尔曲线”和“贝塞尔曲面”，常用于高效建模多种曲面三维物体。

### 11.1 二次贝塞尔曲线

*二次贝塞尔曲线*由一组参数方程定义，这些方程使用三个*控制点*来指定特定的弯曲形状，每个控制点都是二维空间中的一个点。¹ 例如，考虑图 11.1 中所示的一组三个点 [p₀,p₁,p₂]。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_281_0.png)

¹ 当然，曲线可以存在于三维空间中。然而，二次曲线完全位于一个二维平面内。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_282_0.png)

**图 11.2** 参数位置 t = 0.75 处的点。

通过引入参数 t，我们可以建立一组定义曲线的参数方程。t 表示沿连接一个控制点到下一个控制点的线段距离的比例。对于线段上的点，t 的值在 [0,1] 范围内。图 11.2 展示了这样一个值 t = 0.75，分别应用于连接 p0-p1 和 p1-p2 的直线。这样做在两条原始直线上定义了两个新点 p01(t) 和 p12(t)。我们对连接两个新点 p01(t) 和 p12(t) 的线段重复此过程，沿直线 p01(t)-p12(t) 产生 t = 0.75 处的点 P(t)。P(t) 是所得曲线上的一个点，因此用大写 P 表示。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_282_1.png)

**图 11.3** 构建二次贝塞尔曲线。

对不同的 t 值收集许多点 P(t) 会生成一条曲线，如图 11.3 所示。采样的 t 参数值越多，生成的 P(t) 点就越多，所得曲线也越平滑。

现在可以推导二次贝塞尔曲线的解析定义。首先，我们注意到，连接两点 p_a 和 p_b 的线段 p_a p_b 上的任意点 p 可以用参数 t 表示如下：

$$p_{ab}(t) = t p_b + (1 - t) p_a$$

利用此式，我们求出点 p01 和 p12（分别是 p0-p1 和 p1-p2 上的点）如下：

$$p_{01}(t) = t p_1 + (1 - t) p_0$$
$$p_{12}(t) = t p_2 + (1 - t) p_1$$

类似地，连接这些点的线段上的一个点将是

$$P(t) = t p_{12}(t) + (1 - t) p_{01}(t)$$

代入 \(p_{12}\) 和 \(p_{01}\) 的定义可得

$$P(t)=t[t\mathbf{p}_2+(1-t)\mathbf{p}_1]+(1-t)[t\mathbf{p}_1+(1-t)\mathbf{p}_0]$$

因式分解并合并同类项可得

$$P(t)=(1-t)^2\mathbf{p}_0+(-2t^2+2t)\mathbf{p}_1+t^2\mathbf{p}_2$$

或

$$P(t)=\sum_{i=0}^{2}\mathbf{p}_i B_i(t)$$

其中

$$B_0(t)=(1-t)^2,\quad B_1(t)=-2t^2+2t,\quad B_2(t)=t^2$$

因此，我们通过控制点的加权和来求得曲线上的任意点。权重函数 *B* 通常称为“混合函数”（尽管名称 *B* 实际上源自 Sergei Bernstein [BE21]，他首次刻画了该多项式族）。注意，这些混合函数的形式都是二次的，这就是所得曲线被称为二次贝塞尔曲线的原因。

### 11.2 三次贝塞尔曲线

现在我们将模型扩展到*四个*控制点，从而得到如图 11.4 所示的*三次*贝塞尔曲线。三次贝塞尔曲线能够定义比二次曲线丰富得多的形状集合，而二次曲线仅限于凹形。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_283_0.png)

**图 11.4** 构建三次贝塞尔曲线。

与二次情况类似，我们可以推导三次贝塞尔曲线的解析定义：

$$\mathbf{p}_{01}(t)=t\mathbf{p}_1+(1-t)\mathbf{p}_0,\quad \mathbf{p}_{12}(t)=t\mathbf{p}_2+(1-t)\mathbf{p}_1$$

$$p_{23}(t) = t p_3 + (1 - t)p_2$$

$$p_{01-12}(t) = t p_{12}(t) + (1 - t)p_{01}(t)$$

$$p_{12-23}(t) = t p_{23}(t) + (1 - t)p_{12}(t)$$

曲线上的一个点则将是

$$P(t) = t p_{12-23}(t) + (1 - t)p_{01-12}(t)$$

代入 $p_{12-23}$ 和 $p_{01-12}$ 的定义并合并同类项可得

$$P(t) = \sum_{i=0}^{3} p_i B_i(t)$$

其中

$$B_0(t) = (1 - t)^3$$

$$B_1(t) = 3t^3 - 6t^2 + 3t$$

$$B_2(t) = -3t^3 + 3t^2$$

$$B_3(t) = t^3$$

渲染贝塞尔曲线有许多不同的技术。一种方法是使用固定增量，从 0.0 开始到 1.0 结束，迭代 t 的连续取值。例如，如果增量为 0.1，那么我们可以使用 t 值为 0.0、0.1、0.2、0.3 等的循环。对于每个 t 值，将计算贝塞尔曲线上对应的点，并绘制连接连续点的一系列线段，如图 11.5 中的算法所述。

```c
drawBezierCurve (controlPointVector C)
{   currentPoint = C[0];  // curve starts at first control point
    t = 0.0;
    while (t <= 1.0)
    {   // compute next point as the sum of the Control Points,
        // weighted by the blending function evaluated at 't'.
        nextPoint = (0,0);
        for (i=0; i<=3; i++)
            nextPoint = nextPoint + (blending(i,t) * C[i]);
        drawLine(currentPoint,nextPoint);
        currentPoint = nextPoint;
        t = t + increment;
    }
}

blending(i,t)
{   switch (i)
    {   case 0: return ((1-t)*(1-t)*(1-t));   // (1-t)^3
        case 1: return (3*t*(1-t)*(1-t));     // 3t(1-t)^2
        case 2: return (3*t*t*(1-t));         // 3t^2(1-t)
        case 3: return (t*t*t);               // t^3
    }
}
```

**图 11.5** 用于渲染贝塞尔曲线的迭代算法。

另一种方法是使用 de Casteljau 算法递归地将曲线对半细分，其中每个递归步骤中 t = 1/2。图 11.6 展示了左侧细分为新的三次控制点（$q_0, q_1, q_2, q_3$），以绿色显示，这是由 de Casteljau 推导得到的（完整推导见 [AS14]）。

该算法如图 11.7 所示。它反复将曲线段对半细分，直到每个曲线段足够直，进一步细分不会产生明显收益。在极限情况下（随着控制点生成得越来越接近），曲线段本身实际上等同于首末控制点（$q_0$ 和 $q_3$）之间的直线。因此，可以通过比较首控制点到末控制点的距离与连接四个控制点的三条线段长度之和，来判断一个曲线段是否“足够直”：

$$D_1 = |p_0-p_1| + |p_1-p_2| + |p_2-p_3|$$

$$D_2 = |p_0-p_3|$$

然后，如果 D1-D2 小于一个足够小的容差，则进一步细分没有意义。

de Casteljau 算法的一个有趣性质是，可以在实际不使用前述混合的情况下生成曲线上的所有点。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_285_0.png)

**图 11.6** 细分三次贝塞尔曲线。
