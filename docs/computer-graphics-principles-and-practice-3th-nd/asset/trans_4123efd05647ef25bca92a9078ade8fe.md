
必须考虑从所有其他光源到达 $P$ 的光，也就是说，来自某个点 $Q$ 的光在 $Q$ 处被反射而不是被发射，然后到达 $P$。这类光在 $P$ 处被反射，从而对从 $P$ 返回眼睛的出射辐射亮度作出贡献。我们再次用单样本估计这一入射间接辐射亮度。为此，我们递归地使用路径追踪代码。我们构造一条从 $P$（或非常接近 $P$）出发、沿某个随机方向 $\omega$ 射入场景的射线；用路径追踪器求出沿该射线返回的间接辐射亮度，并通过 BRDF 将其反射为从 $P$ 向眼睛传输的辐射亮度。当然，在这种情况下，我们不能在计算得到的辐射亮度中包含直接朝向 $P$ 发射的光——我们已经考虑过它了。因此，我们在第 24 行将 `includeEmissive` 设为 `false`。清单 32.7 展示了这一点。

### 清单 32.7：估计沿射线散射返回的间接光。

```cpp
Radiance3 App::estimateIndirectLight(
        const SurfaceElement& surfel, const Ray& ray, bool isEyeRay){
    Radiance3 L_o(0.0f);
    // Use recursion to estimate light running back along ray
    // from surfel, but ONLY light that arrives from
    // INDIRECT sources, by making a single-sample estimate
    // of the arriving light.

    Vector3 w_o = -ray.direction();
    Vector3 w_i;
    Color3 coeff;
    float eta_o(0.0f);
    Color3 extinction_o(0.0f);
    float ignore(0.0f);

    if (!isEyeRay || m_indirect) {
        if (surfel.scatter(w_i, w_o, coeff, eta_o, extinction_o, rnd, ignore)) {
            float eta_i = surfel.material.etaReflect;
            float refractiveScale = (eta_i / eta_o) * (eta_i / eta_o);

            L_o += refractiveScale * coeff *
                pathTrace(Ray(surfel.geometric.location, w_o).bumpedRay(0.0001f *
                    sign(surfel.geometric.normal.dot(w_o)),
                    surfel.geometric.normal), false);
        }
    }
    return L_o;
}
```

绝大部分工作都在 `surfel.scatter()` 中完成；它接收一条到达某点的射线 $r$，要么将其吸收，要么为其确定一个出射方向 $r'$，并返回一个系数；沿 $r'$ 到达的辐射亮度（即辐射亮度 $L(P, -r')$）应乘以该系数，以生成在 $P$ 点沿 $-r$ 方向散射的辐射亮度的单样本估计。

在检查 `scatter()` 代码之前，让我们更仔细地回顾一下上述描述。首先，`scatter()` 既可用于射线追踪/路径追踪，也可用于光子追踪。第二种用法也许更直观：有一点光能到达表面，它要么被吸收，要么沿一个或多个方向散射。`scatter()` 过程用于模拟这一过程。如果表面吸收率为 0.3，那么 `scatter()` 有 30% 的情况下会返回 `false`。其余 70% 的情况下，它会返回 `true` 并设置 $\omega_o$ 的值。给定指向光源的方向 $\omega_i$，为散射光选取特定方向 $\omega_o$（至少对于没有镜面项或透射项的表面）的概率大致与 $f(\omega_o, \omega_i)$ 成正比。在理想情况下，它会完全成正比。在我们的实现中，通常并非如此，但返回的系数包含一个 $f(\omega_o, \omega_i)/p(\omega_i)$ 因子，其中 $p(\omega_i)$ 是采样 $\omega_i$ 的概率，从而进行适当补偿。

如果存在镜面反射会怎样？假设 30% 的情况下入射光被吸收，50% 的情况下发生镜面反射，剩余 20% 的情况下按照朗伯散射模型散射。在这种情况下，`scatter()` 有 30% 的情况下会返回 `false`。50% 的情况下它会返回 `true`，并将 $\omega_o$ 设为镜面反射方向；剩余 20% 的情况下，$\omega_o$ 会按余弦加权分布分布在半球上（也就是说，沿法线方向出射的概率高，沿切线方向出射的概率低）。

让我们在实践中看看这一点，并查看清单 32.8 中 G3D 的 `scatter` 方法开头。

### 清单 32.8：scatter 方法的开头。

```cpp
1  bool SurfaceElement::scatter
2  (const Vector3& w_i,
3   Vector3&       w_o,
4   Color3&        weight_o, // coeff by which to multiply sample in path-tracing
5   float&         eta_o,
6   Color3&        extinction_o,
7   Random&        random,
8   float&         density) const {
9
10     const Vector3& n = shading.normal;
11
12     // Choose a random number on [0, 1], then reduce it by each kind of
13     // scattering's probability until it becomes negative (i.e., scatters).
14     float r = random.uniform();
15
16     if (material.lambertianReflect.nonZero()) {
17         float p_LambertianAvg = material.lambertianReflect.average();
18         r -= p_LambertianAvg;
19
20         if (r < 0.0f) {
21             // Lambertian scatter
22             weight_o = material.lambertianReflect / p_LambertianAvg;
23             w_o      = Vector3::cosHemiRandom(n, random);
24             density  = ...;
25             eta_o    = material.etaReflect;
26             extinction_o = material.extinctionReflect;
27             debugAssert(weight_o.r >= 0.0f);
28
29             return true;
30         }
31     }
32     ...
```

如你所见，材质有一个 `lambertianReflect` 成员，它表示三个颜色带中每个带的反射率；[^2] 这些值的平均值给出入射光发生朗伯散射的概率 $p$。如果随机值 $r$ 小于 $p$，我们就产生一条朗伯散射射线；否则，从 $r$ 中减去该概率，然后继续处理下一种散射。

> 内联练习 32.6：请说服自己，这种方法产生朗伯散射射线的概率为 $p$。

实际的散射过程相当直接：`cosineHemisphere` 方法生成一个向量，该向量在以 $\mathbf{n}$ 为极点的半球内服从余弦加权分布。该方法还返回交点 $n$ 侧材料的折射率（包括实部和虚部），以及一个系数（这里称为 `weight_o`），这个系数正是我们在对反射辐射亮度进行蒙特卡洛估计时需要使用到的数值。（返回的 `density` 值*不是*概率密度，而是为了其他算法而包含的一个相当不同的值，我们忽略它。）

散射代码的其余部分类似。回想一下，我们使用的反射模型是朗伯项、光泽项以及一个

### 清单 32.9：进一步的散射代码。

```cpp
Color3 F(0, 0, 0);
bool Finit = false;

if (material.glossyReflect.nonZero()) {

    // Cosine of the angle of incidence, for computing Fresnel term
    const float cos_i = max(0.001f, w_i.dot(n));
    F = computeF(material.glossyReflect, cos_i);
    Finit = true;

    const Color3 p_specular = F;
    const float p_specularAvg = p_specular.average();

    r -= p_specularAvg;
    if (r < 0.0f) { // Glossy (non-mirror) case
        if (material.glossyExponent != finf()) {
            float intensity = (glossyScatter(w_i, material.glossyExponent,
                                            random, w_o) / p_specularAvg);
            if (intensity <= 0.0f) {
                // Absorb
                return false;
            }
            weight_o = p_specular * intensity;
            density = ...;
        } else {
            // Mirror

            w_o = w_i.reflectAbout(n);
            weight_o = p_specular * (1.0f / p_specularAvg);
            density = ...;
        }

        eta_o = material.etaReflect;
        extinction_o = material.extinctionReflect;
        return true;
    }
}
```

[^2]: 按照惯例，我们会将这些称为“红”“绿”“蓝”，但在实现上没有重要变化，我们也可以记录 5、7 或 20 个光谱样本。
