
### 14.10.4 自发光

通常希望渲染出看起来发光、但实际上并不照亮其他表面的物体。例如，汽车尾灯和计算机设备上的 LED 对场景其余部分的光照贡献可能微乎其微，但它们自身在图像中需要显得明亮。这些效果可以通过正常渲染场景，然后以加法混合方式混合自发光分量来模拟，就好像它是使用 `BlendFunc(ONE, ONE)` 渲染的一个新表面。

一些特别吸引人的效果源于本身看似透明的介质所产生的这种自发光。例子包括霓虹灯发出的光、闪电、科幻作品中的“力场”以及奇幻魔法效果。在这些情况下，底层表面是否可见并不重要——自发光分量的加法混合方式保持不变。

### 14.10.5 泛光与镜头光晕

镜头光晕和泛光是在真实相机的光路内产生的效果。可以对真实光路进行建模，但仅仅为了实现这些现象，更有效的方法是在渲染帧之上使用 `BlendFunc(ONE, ONE)`，以加法混合方式叠加由额外几何体产生的贡献。泛光模拟入射光在镜头内的扩散以及传感器的饱和。它通常通过仅模糊屏幕上最亮的区域，并将其贡献加回帧中来模拟。镜头光晕源于物镜内镜头之间的多次反射。它通常通过沿屏幕上穿过明亮位置（例如太阳）的二维直线渲染一系列虹膜形状（例如六边形或圆盘形）多边形来模拟。

## 14.11 光源模型

计算机图形学中的**光源**是一种光的来源。我们在日常生活中遇到的光源在发射光谱、表面积和强度方面差异极大。例如，太阳巨大而遥远，聚光灯明亮而小巧，交通信号灯相对昏暗且带有颜色。我们在虚拟世界中可能遇到的光源进一步扩展了这种差异；例如，发光的真菌洞穴、魔法独角兽的光环，或星际飞船上的导航灯。

在介绍光源模型之前，我们必须先讨论光。你知道光是能量（以光子形式），沿射线在空间中传播，并在表面发生散射。计算机图形学中有许多光的模型，但它们都从表示能量通过空间中某一点的速率开始。我们在此给出简要概述，并将详细内容推迟到第26章。即使不理解光传输背后的动机和物理原理，也可以使用本章的模型渲染图像。不过，我们建议你在渲染出第一批图像后阅读第26章，以建立更深入的理解。

### 14.11.1 辐射亮度函数

考虑空间中我们想要了解其光照的某一点 X。这个点经常位于场景中的某个表面上，但并非必须如此。从方向 ω 入射到 X 的光量记为 L(X, ω)。这隐含地定义了关于两个变量 X 和 ω 的函数 L，称为**辐射亮度函数**，也称为**全光函数**。需要明确的是，参数 ω 表示传播方向。如果有光子经过点 P 并沿方向 ω 传播，那么 L(P, ω) ≠ 0，而 L(P, −ω) = 0 也完全可能。按照惯例，我们将限制 ω 为单位向量的情况。L 的单位是瓦特每平方米-球面度，即 W · m⁻² · sr⁻¹。表面积以平方米为单位测量，球面度是角度度量的球面类似物，称为**立体角**。角度可以度量平面中二维单位圆上的一维区域，你可以用“每弧度”来表示某量通过该一维区域的速率。我们用“每球面度”来度量通过三维空间中单位球面上的二维区域（立体角）的能量。

知道辐射亮度沿穿过空无一物的空间的射线守恒是很有用的。因此，如果我们已知 L(X, ω)，那么只要沿该射线距 X 为 t 的范围内没有遮挡物体，我们也就知道 t > 0 时的 L(X + tω, ω)。

### 14.11.2 直接光与间接光

我们将直接从光源到达某点的光，与从场景中某个表面反射后间接到达该点的光区分开来。例如，在户外游泳池附近，阳光直接照射到你的头顶，但它也会从水面反射，间接照到你的下巴底部。如果没有间接光，那么你的下巴底部将看起来完全没有被照亮。间接光源于光源与场景之间的相互作用，因此我们将其视为光传输模型的一部分，而不是光源模型的一部分。

### 14.11.3 实用与艺术考量

代码清单 14.10 给出了一组光源类实现的典型基类。其方法支持将光源集成到渲染器中的实用方面，而不是光发射的物理方面。

代码清单 14.10：所有光源的基类，省略了简单的实现细节。

```cpp
/** Base class for light sources */
class Light {
public:
    const std::string name() const;

    virtual CoordinateFrame cframe() const;

    /* for turning lights on and off */
    virtual bool enabled() const;

    /* true for physically-correct lights */
    virtual bool createsLambertianReflection() const;

    /* true for physically-correct lights */
    virtual bool createsGlossyReflection() const;

    /* true for physically-correct lights */
    virtual bool createsGlobalIllumination() const;

    /* true for physically-correct lights */
    virtual bool castsShadows() const;

    ////////////////////////////////////////
    // Direct illumination support

    /* Effective area of this emitter. May be finite,
       zero, or infinite. */
    virtual float surfaceArea() = 0;

    /* Select a point uniformly at random on the surface
       of the emitter in homogeneous coordinates. */
    virtual Vector4f randomPoint() const = 0;

    /* Biradiance (solid-angle-weighted radiance) at P due
       to point Q on this light, in W / m^2. Q must be a value
       previously returned by randomPoint(). */
    virtual Biradiance4 biradiance
        (const Vector4f Q, const Point3& P) const = 0;

    ////////////////////////////////////////
    // Photon emission support

    /* Total power; may be infinite */
    virtual Power3 totalPower() const = 0;

    /* Returns the position Q, direction of propagation w_o, and
       normalized spectrum of an emitted photon chosen with
       probability density proportional to the photon emission density
       function for this light. */
    virtual Color3 photon(Point3& Q, Vector3& w_o) const = 0;
};
```

我们为每个光源分配一个参考坐标系（`cframe`）。对于位于有限位置的光源，这是发光体的质心和参考朝向。对于无限远的光源（即方向光源），这是场景中的一个参考坐标系和便于显示 GUI 操作控件以操纵该光源的位置。

### 14.11.3.1 非物理工具

以非物理方式操纵光与场景的交互通常很有用。这些做法可能出于艺术意图而偏离物理规律，但也可能用于补偿渲染模型本身的缺陷。也就是说，正确的模型配上错误的数据（或反之）无法产生正确的图像，因此有时我们必须通过有意违反物理规律来补偿已知的局限和近似，以使最终结果看起来更真实。图 14.10 所示的类包含若干此类工具，例如以不投射阴影或不参与朗伯反射计算的光源形式存在。当然，使用该类的渲染器必须遵循这些设置，它们才能生效。
