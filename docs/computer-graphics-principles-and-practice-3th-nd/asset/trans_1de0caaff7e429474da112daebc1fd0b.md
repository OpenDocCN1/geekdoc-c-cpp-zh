
## 清单 32.1：Blinn-Phong 反射率实现的一部分。

```cpp
Color3 SurfaceElement::evaluateBSDFfinite(w_i, w_o) {
    n = shading.normal;
    cos_i = abs(w_i.dot(n));

    Color3 S(Color3::zero());
    Color3 F(Color3::zero());
    if ((material.glossyExponent != 0) && (material.glossyReflect.nonZero())) {
        // Glossy

        // Half-vector
        const Vector3& w_h = (w_i + w_o).direction();
        const float cos_h = max(0.0f, w_h.dot(n));

        // Schlick Fresnel approximation:
        F = computeF(material.glossyReflect, cos_i);
        if (material.glossyExponent == inf()) {
            S = Color3::zero();
        } else {
            S = F * (powf(cos_h, material.glossyExponent) * ...
        }
    }
    ...
```

表面法线立即用于计算 cos θᵢ，这是用局部参考系表示两个输入向量之一的示例。半向量（`direction()`）返回一个由 ωᵢ 和 ωₒ 计算得到的单位向量，它们在代码中称为 w_i 和 w_o。计算 Fresnel 项的 Schlick 近似，并用它来确定光泽反射。省略代码的其余部分计算漫反射。这段代码缺少镜面反射项和基于斯涅尔定律的透射率的计算，它们各自对应于散射模型中的一个冲激。将这些冲激项分离出来，使得反射光的计算简单得多。回想一下，我们一直表示为积分的式子，即

$$\int_{\omega_i\in S^2_+(P)} L(P,-\omega_i) f_s(\omega_i,\omega_o)\,\omega_i\cdot n\,d\omega_i,$$ (32.3)

实际上是一个作用于 L 的线性算子的简写，该算子一部分由像上面这样的卷积积分定义，一部分由像镜面反射这样的冲激项定义；其中对于特定的 ωᵢ 值，被积函数仅对特定方向 ωₒ 非零；“积分”的值是某个常数（冲激系数）乘以 L(P, −ωᵢ)。

试图通过蒙特卡罗积分来近似镜面反射这样的项是徒劳的：我们永远不会随机选到理想的出射方向。幸运的是，这些项很容易直接计算，因此不需要近似。因此，`SurfaceElement` 类提供了一个方法（见清单 32.2），它返回计算反射辐射亮度所需的全部冲激（在这里是镜面反射冲激和透射冲激，不过如果我们在渲染双折射材料，就会有两个透射冲激，所以返回冲激数组是自然的）。

G3D 是围绕三角网格设计的。因此，`SurfaceElement` 类也包含一些与网格相关的项（见清单 32.3）。

## 清单 32.2：返回散射模型冲激部分的方法。

```cpp
void getBSDFImpulses (Vector3& w_i, Array<Impulse>& impulseArray) {
    const Vector3& n = shading.normal;

    Color3 F(0,0,0);

    if (material.glossyReflect.nonZero()) {
        // Cosine of the angle of incidence, for computing
        //Fresnel term
        const float cos_i = max(0.001f, w_i.dot(n));
        F = computeF(material.glossyReflect, cos_i);

        if (material.glossyExponent == inf()) {
            // Mirror
            Impulse& imp       = impulseArray.next();
            imp.w              = w_i.reflectAbout(n);
            imp.magnitude      = F;
            ...
```

## 清单 32.3：`SurfaceElement` 类的其他成员。

```cpp
class SurfaceElement {
public:
    ...
    struct Interpolated {
        /** The interpolated vertex normal. */
        Vector3 normal;
        Vector3 tangent;
        Vector3 tangent2;
        Point2 texCoord;
    } interpolated;

    /** Information about the true surface geometry. */
    struct Geometric {
        /** For a triangle, this is the face normal. This is useful
            for ray bumping */
        Vector3 normal;

        /** Actual location on the surface (it may be changed by
            displacement or bump mapping later). */
        Vector3 location;
    } geometric;
    ...
```

向量 `tangent` 和 `tangent2` 对应于上面的 **u** 和 **v**；对表面建模时，必须在每个顶点指定这些向量。使用纹理坐标的导数是一种生成它们的方法；如果我们在顶点 i 处有纹理坐标 (uᵢ, vᵢ)，就可以找到三角形内部 **u** 的线性近似，并由此确定 **u** 增长最快的方向 **u**。然后我们可以将 **v** 定义为 **n** × **u**，从而得到一个正交基。然而请注意，这是逐三角形的计算，并且 **u** 的计算不保证在三角形之间一致。实际上，由于制图者的困境（你无法将地球仪展平到一张纸上同时保持角度和距离），在整个曲面上一致地分配纹理坐标通常是不可行的。重要的是，任何各向异性 BRDF 只应在 **u** 和 **v** 定义一致的区域使用。

向量 `geometric.normal` 是三角面法线，而不是它所近似的表面法线。取决于表面最初是如何建模的，这些法线可能相同，或者表面法线可能是面法线的某种加权组合，或者可能完全由其他方法确定。三角面法线在光线追踪算法中很有用，因为如果 P 是一个本应位于三角形 T 上的点（见图 32.2），那么从 P 向场景中追踪的一条光线可能首先在 T 的某个点处与场景相交，这是因为舍入误差或表示误差将 P 稍微放在了 T 的一侧。通过沿 T 的法线轻微移动（**微移**）P，即用 P + εn 替换 P（其中 ε 很小），我们可以避免这种虚假相交。（也许“轻推”会是更好的术语，以避免与凹凸贴图的概念冲突，但 G3D 使用的术语是“微移”。）ε 应该多大？一个很好的经验法则是“不超过你期望在场景中看到的最小物体尺寸的 1%”。这隐含地为你的模型建立了一个条件：任何重要物体或特征都不应小于你将使用的浮点数中两个相邻数之间最大间隔的 100 倍。例如，如果你场景中的所有坐标都在 −100 到 100 之间，并且你使用 IEEE 32 位浮点数，那么由于接近 100 的两个浮点数之间的最大间隔约为 4 × 10^{-6}，你不应期望建模任何小于 4 × 10^{-4} 单位的特征。

![](img/f464cd0043eb5336aa0543fe20a0561b_936_0.png)

*图 32.2：将 P 微移到 P′ = P + εn 可防止从 P 出发的光线与 T 相交。*

**内联练习 32.4：** 如果我们正在追踪一条光线 P + td，我们可以沿光线“微移”P，也就是在方向 d 上轻微移动它。通过考虑几乎与表面相切的光线，论证这是一个坏主意。

光线微移是一种设计选择。它补偿了几何固定精度表示带来的某些问题。但作为一种设计选择，它也有重要的表示后果。例如，任何依赖于小于微移尺寸的特征的场景光照属性，都可能在我们的计算中被错误表示。这限制了我们计算模型能够以任何精度产生的内容。举例来说，想象透过两个几乎相切的光亮圆柱之间的间隙看太阳（见图 32.3）。一条典型太阳光线在圆柱之间穿过时会反弹多次。如果圆柱间距小于我们在路径追踪器中使用的微移尺寸，光很容易被吸收而不是反射。这是问题吗？如果微移尺寸相比光的波长很小，那就不是问题。为什么不是？因为对于那种尺度的间隙，衍射效应占主导，所以我们的光线光学模型本来就已经不准确了。这再次是“明智建模”原则的一个实例：当我们模拟某事物时，需要意识到我们的物理、数学和计算模型的局限性。

![](img/f464cd0043eb5336aa0543fe20a0561b_936_1.png)

*图 32.3：一条来自太阳的光线穿过两个几乎相切的光亮圆柱之间的间隙。*

### 32.3.1 镜子与点光源

如果我们在场景中允许点光源，那么当我们“从眼睛”追踪光线时，命中点光源的概率为零，因此在实践中几乎永远不会发生。类似地，如果我们允许完美镜子，我们无法写出散射
