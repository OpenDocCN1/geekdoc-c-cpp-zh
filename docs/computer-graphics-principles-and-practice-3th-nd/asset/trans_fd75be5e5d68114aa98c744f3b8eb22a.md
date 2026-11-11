
在本章中，我们选择表示表面的一个样本，而不是表示 BSDF。这意味着一个表面元素编码了一个位置、参考坐标系以及 BSDF 的任何空间变化参数，还包括 BSDF 本身。我们倾向于这种表示，因为它允许将渲染器的光线-表面采样部分与散射部分分离开来。这种分离在教学上有好处，因为它允许我们分别考虑渲染器的各个组成部分。它也有设计上的好处，因为这些组成部分变得模块化，我们可以混合不同的表面采样和散射采样方法。我们在此不考虑这一决策对效率的影响，但要注意，它被用于若干渲染库中，例如 PBRT（http://pbrt.org）和 The G3D Innovation Engine（http://g3d.sf.net）。

在实践中，f_s 必须支持两种不同的操作。第一种是直接求值：给定两个方向，我们希望计算该函数的值。这用于直接光照，此时我们已经选择了一条光传输路径，并希望知道沿该路径的传输量大小。第二种是采样。在这种情况下，我们给定入射光方向或出射光方向，并希望以与 f_s 成正比的概率密度选择另一个方向，可能还会按沿其中一个向量的投影面积进行加权。

对于直接求值和采样两者而言，像镜子或透镜那样不漫射光、而是反射或透射完美图像的散射，必须单独处理。函数 f_s 在对应于反射或透射的方向上取无穷大值，我们称之为**冲激**。因此，我们将大多数操作划分为分别处理有限部分和冲激部分的方法。

> ✓ **API 原则：** 从将使用 API 的程序员的视角来设计 API，而不是从实现 API 的程序员或在其推导中使用的数学记号的角度来设计。例如，将单个 BSDF f(ω_o, ω_i) 映射到函数 `API::Color3f f(Vector3 wi, Vector3 wo)` 很容易实现，但在真实渲染器中很难使用。

*Listing 14.6 给出了用于计算 f 的有限部分的接口。该方法抽象了像素着色器或光线追踪器中通常用于直接光照的算法。它实现起来相对直接。*

*Listing 14.6：散射函数直接求值的接口（类似于 G3D::Surfel）。*

```cpp
class BSDF {
protected:
    CFrame frame; // coordinate frame in which BSDF is expressed

    ...

public:

    class Impulse {
    public:
        Vector3 direction;
        Color3 magnitude;
    };

15  typedef std::vector<Impulse> ImpulseArray;
16
17  virtual ~BSDF() { }
18
19  /* Evaluates the finite portion of f(wi, wo) at a surface
20     whose normal is n. */
21  virtual Color3 evaluateFiniteScatteringDensity
22      (const Vector3&    wi,
23       const Vector3&    wo) const = 0;
24
25  ...
```

*Listing 14.7 给出了光子映射、递归（Whitted）光线追踪和路径追踪等算法所需的其余方法的接口。这些方法的实现和底层数学要稍微复杂一些。我们在此不再进一步讨论它们，只需指出：如果我们愿意使用相当低效的实现，那么给定有限散射密度和冲激后，这些散射方法仍然很容易实现。我们在这个接口中包含的特定方法并没有什么神圣不可更改之处。例如，在路径追踪的某些实现中，我们希望相对于与 BSDF 成正比的分布进行采样，而不带 ω_i · n 的额外加权因子，那么我们可能就会在接口中包含一个用于此目的的方法。*

*Listing 14.7：散射函数的散射方法和冲激方法接口。*

```cpp
1  class BSDF {
2
3  ...
4
5  /* Given wi, returns all wo directions that yield impulses in
6     f(wi, wo). Overwrites the ImpulseArray. */
7  virtual void getOutgoingImpulses
8      (const Vector3&    wi,
9       ImpulseArray&    impulseArray) const = 0;
10
11
12 /* Given wi, samples wo from the normalized PDF of
13    wo -> g(wi, wo) * |wi . n|,
14    where the shape of g is ideally close to that of f. */
15 virtual Vector3 scatterOut
16     (const Vector3&    wi,
17      Color3&          weight) const = 0;
18
19
20 /* Given wi, returns the probability of scattering
21    (vs. absorption). By default, this is computed by sampling
22    since analytic forms do not exist for many scattering models. */
23 virtual Color3 probabilityOfScattering(
24     const Vector3& wi) const;
25
26 /* Given wo, returns all impulses for wi. */
27 virtual void getIncomingImpulses
28     (const Vector3&    wo,
29      ImpulseArray&    impulseArray) const = 0;

/* Given wo, samples wi from the normalized PDF of wi -> g(wi, wo) * |wi . n|. */
virtual Vector3f scatterIn(
    const Vector3f wo,
    Color3f& weight) const = 0;


/* Given wo, returns the a priori probability of scattering (vs. absorption). */
virtual Color3f probabilityOfScattering(const Vector3f& wo) const = 0;

};
```

BSDF 实现有两个来源。**测量型 BSDF** 由对真实表面进行的数千或数百万次受控测量构建而成。测量成本高昂（或者自己执行起来很棘手），但它能提供极高的物理真实感。描述 BSDF 的数据通常很大，但一般较为平滑，因此适合压缩。

**解析型 BSDF** 用具有物理意义或美学意义的参数来描述表面外观。它们通常表示为简单函数的和与积，这些函数对大多数参数取值为零，并在参数空间的一个狭窄区域上平滑地上升为一个瓣。那些对底层物理进行建模的解析型 BSDF 可用于预测。我们现在描述一些简单但流行的解析型 BSDF。

### 14.9.2 朗伯

朗伯观察到，大多数平坦的粗糙表面反射的光能与表面法线和入射光方向之间夹角的余弦成正比。这被称为**朗伯定律**。对于具有恒定 BSDF 的表面，这可由几何关系推出，因为表面的投影面积与入射光角度的余弦成正比。恒定 BSDF 之所以被称为朗伯型，是因为它遵循这一定律。

尽管很少有表面表现出真正的朗伯反射，但大多数绝缘体都可以用朗伯型 BSDF 进行可辨识的近似。随后可通过添加其他项来处理残余误差，如下一小节所述。

近似朗伯表面的例子包括用平光（即哑光）涂料粉刷的墙、干燥的泥土，以及从数米外观察的皮肤和布料。将它们近似为朗伯表面的主要误差在于，当以掠射角观察时，它们往往看起来比恒定 BSDF 所预测的更光亮。

在实践中，近似朗伯的外观通常是因为表面对光在非常浅的层面上有一定渗透性，并且到光出射时所有方向性都已丢失。光泽高光是由光优先在接近镜面反射方向附近反射造成的。当这种情况没有发生时，表面看起来就是哑光的。

Listing 14.8 实现了朗伯型 BSDF 的求值方法。我们为每个频带指定一个“朗伯常数”k_l，也就是一种*颜色*。k_l 的各分量必须分别位于 [0, 1] 范围内。它们表示表面对每种“颜色”光的反射率。较大的值更亮，因此 (1, 0, 0) 看起来是亮红色，而 (0.2, 0.4, 0.0) 是深棕色。当然，很少有真实表面在任何颜色通道上真正具有完美吸收或完美反射率。许多基于物理的渲染系统还倾向于在任一颜色通道处于任一极限时冒除以零的风险，因此实践中最好在开区间 (0, 1) 上选择常数。

