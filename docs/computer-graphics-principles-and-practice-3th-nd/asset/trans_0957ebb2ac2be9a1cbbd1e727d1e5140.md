
为了数学上的便利，我们将考虑一个*有限*的场景，即它包含在以原点为中心、足够大的某个球体内；我们假设这个球体的内表面涂有非反射材料，因此所有照射到其上的光都会被吸收。在真实场景中，一旦光“离开”场景，我们便忽略它。但在本章中，有一个光线投射函数非常有用：它接收一个点 $P$ 和一个方向 $\mathbf{d}$，并返回从 $P$ 出发沿方向 $\mathbf{d}$ 的射线上第一个表面点 $Q$。如果场景没有被这个大球体包围，那么一条“射出场景”的射线不会击中任何东西，光线投射函数的值也就没有定义。因此，这个大黑球完全是为了数学上的便利，它对实际的光传输没有任何影响。

为了保持符号简洁，我们将进一步假设我们研究的是稳态情形，即不存在时间依赖：所有光源都已点亮足够长时间，使光在整个场景中散射并达到稳态。此外，我们将忽略波长依赖性，只研究辐射亮度，而不是*光谱*辐射亮度。

因此，我们的起点是一个曲面的集合，其并集是场景中所有表面点的集合 $\mathcal{M}$（包括大的包围黑球）。对于每个点 $P \in \mathcal{M}$，我们还知道 $f_r(P, \omega_i, \omega_o)$，即 $P$ 处的双向反射分布函数，它描述了以方向 $-\omega_i$ 到达 $P$ 的光中有多少变成以方向 $\omega_o$ 离开的光（正式定义见第26章）。在本节中，符号 $\omega_i$ 和 $\omega_o$ 将保留用于表示与 $P$ 处法向量 $\mathbf{n}_P$ 指向同一半平面的单位向量，即 $\omega_i \cdot \mathbf{n}_P \ge 0$ 且 $\omega_o \cdot \mathbf{n}_P \ge 0$。

除了场景几何和反射率之外，我们假设给定了场景中的**光照**，它由每个光源的每个点在每个方向上的发射辐射亮度来描述；换句话说，给定了一个函数

$$L^e : \mathcal{M} \times \mathbb{S}^2 \to \mathbb{R} : (P, \omega) \mapsto L^e(P, \omega), \qquad (29.1)$$

其中 $L^e(P, \omega)$ 表示从点 $P$ 沿方向 $\omega$ 离开的*发射辐射亮度*，即如果移除场景中所有其他光源和表面，使得完全没有光*到达*点 $P$、因而也没有光被反射时，你测量到的辐射亮度。

> 对于典型面光源的典型点 $P$，如果 $\omega \cdot \mathbf{n}_P < 0$，则 $L^e(P, \omega)$ 为零；换句话说，光只向光源的“外侧”辐射。对于像典型白色白炽灯泡这样的光源，所有这样的向外方向上的辐射亮度相同，即对于 $\omega \cdot \mathbf{n}_P > 0$，$L^e(P, \omega) = C$。由于这与朗伯表面反射的光类似，我们将这种光源称为**朗伯**光源。

如上所述，我们还假设有一个*光线投射函数*（见图29.1），

$$R : \mathcal{M} \times \mathbb{S}^2 \to \mathcal{M}, \qquad (29.2)$$

其中 $R(P, \omega)$ 是从 $P$ 出发沿方向 $\omega$ 的射线击中的第一个点。如果 $\omega \cdot \mathbf{n}_P \le 0$，则 $R(P, \omega) = P$，也就是说，一条*射入*形状内部的射线会立即击中该形状。如果 $\omega \cdot \mathbf{n}_P > 0$，则 $R(P, \omega)$ 是我们从 $P$ 沿方向 $\omega$ 看去所看到的点。更准确地说，$R(P, \omega)$ 是从 $P$ 沿方向 $\omega$ 的射线上最远的点 $Q$，且满足射线上严格位于 $P$ 和 $Q$ 之间的所有点都处于空白空间中。

![](img/f464cd0043eb5336aa0543fe20a0561b_835_0.png)

*图29.1：$R(P_1, \omega_1) = Q_1$，但 $R(P_2, \omega_2) = P_2$。*

光线投射函数及相关的**可见性函数**的算法表示——见练习29.1——是第36章和第37章的主题，但你在第15章已经见过基本示例。

在清楚地刻画了我们的假设之后，我们现在可以分析场景中的光传输。

### 29.2.1 渲染方程（第一版）

再次考虑反射率方程，即式26.80，将其改写为不依赖时间和波长的形式：

$$L^{\text{ref}}(P, \omega_o) = \int_{\omega_i \in \mathbb{S}^2(P)} L(P, -\omega_i) f_r(P, \omega_i, \omega_o) (\omega_i \cdot \mathbf{n}_P) \, d\omega_i, \tag{29.3}$$

它用从其他方向到达 $P$ 的光来表示在点 $P$ 沿*向外*方向 $\omega_o$ 反射的辐射亮度。

如果 $P$ 恰好是光源上的一个点，光也可能沿方向 $\omega_o$ 离开 $P$，因为光是在 $P$ 处*发射*的，而不是从那里反射的；也就是说，

$$L(P, \omega_o) = L^e(P, \omega_o) + L^{\text{ref}}(P, \omega_o) \tag{29.4}$$

$$= L^e(P, \omega_o) + \int_{\omega_i \in \mathbb{S}^2(P)} L(P, -\omega_i) f_r(P, \omega_i, \omega_o) (\omega_i \cdot \mathbf{n}_P) \, d\omega_i, \tag{29.5}$$

这是**渲染方程**的一个基本版本（例如，它只处理反射），它在给定函数 $L^e$ 和 $f_r$ 的情况下刻画函数 $L$。它最早由 Kajiya [Kaj86] 和 Immel 等人 [ICG86] 以略有不同的形式在计算机图形学中描述。它与辐射传输等学科中发展的类似方程完全类似。虽然我们将在后续章节中集中讨论 Kajiya 的描述和推导，但 Immel 等人给出的形式特别适合蒙特卡罗渲染所需的“采样”。

你会注意到，未知的辐射亮度函数 $L$ 出现在方程两边，其中一次在积分号下，就像未知函数 $h$ 出现在微分方程

$$h'(x) = 2h(x - 1), \tag{29.6}$$

两边，其中一次在导数内。式29.5称为**积分方程**，求解这样的方程通常比求解微分方程更困难。下一章将讨论寻找近似解的各种方法。

式29.4表达了辐射亮度函数 $L$，同时考虑*离开*点 $P$ 的辐射亮度和到达该点的辐射亮度。Arvo [Arv95] 将前者称为**表面辐射亮度**，将后者称为**场辐射亮度**。渲染方程告诉我们如何从场辐射亮度计算*表面*辐射亮度，因为它仅限于 $\omega_o \cdot \mathbf{n}_P > 0$ 的情形。但为了计算右端项，我们还必须知道如何计算*场*辐射亮度。

在这个方程中“闭合回路”的思想是：任何以方向 $-\omega_i$ 到达点 $P$ 的光，必定是从某个其他点 $Q \in \mathcal{M}$ 以方向 $-\omega_i$ *离开*的。点 $Q$ 必须是从 $P$ 沿方向 $\omega_i$ 可见的点。这些观察使我们能够写出**传输方程**：

$$L(P, -\omega_i) = L(R(P, \omega_i), -\omega_i), \tag{29.7}$$

对于任意满足 $\omega_i \cdot \mathbf{n}_P > 0$ 的 $\omega_i$。

在 $P$ 处；第三项是所有其他光。因此，渲染方程中的项 $L(P, -\omega_i)$ 已被拆分为三项之和。

这些项中的第一项（见代码清单29.2）是通过将关于所有可能入射方向的积分转换为对点光源的求和来计算的。积分中定义域的这种变化意味着我们也必须改变被积函数，使用第26.6.5节中的变量替换。

*代码清单29.2：点光源的反射光照。*

```cpp
Radiance3 App::estimateDirectLightFromPointLights(Surfel surfel, Ray ray){
    Radiance3 radiance(0.0f);
    for (int L = 0; L < m_world->lightArray.size(); ++L) {
        const GLight& light = m_world->lightArray[L];
        // Shadow rays
        bool visible = m_world->lineOfSight(surfel.geometric.location +
            surfel.geometric.normal * 0.0001f,
            light.position.xyz());
        if (visible) {
            Vector3 w_i = light.position.xyz() - surfel.shading.location;
            const float distance2 = w_i.squaredLength();
            w_i /= sqrt(distance2);
            // Attenuated radiance
            const Irradiance3& E_i = light.color / (4.0f * pif * distance2);
            radiance += (surfel.evaluateBRDF(w_i, -ray.direction()) *
                E_i * max(0.0f, w_i.dot(surfel.shading.normal)));
        }
    }
    return radiance;
}
```

如你所见，该过程循环遍历所有点光源，并且对于每个点光源，它检查该光源从 $P$ 是否*可见*，使用 `m_world->lineOfSight()`，即我们正在渲染的世界的可见性函数的实现。反射辐射亮度计算为 BRDF、点积 $\omega_i \cdot \mathbf{n}_r$ 和项 $E_i$ 的乘积，其中 $E_i$ 是经过上述变量替换因子调整后的入射辐射亮度。

第二项类似，涉及面光源如何被反射的估计。然而，第三项是最有趣的。在讨论它之前，我们还需要一点数学知识（我们将在第30章中详细展开）。

其思想是：任意函数 $h$ 在任意定义域 $D$ 上的积分，等于 $h$ 在该定义域上的平均值与定义域大小的乘积。当定义域是区间 $[a, b]$ 时，大小为 $b - a$；当定义域是单位半球时，大小为 $2\pi$，等等。“平均值”可以通过在定义域的 $n$ 个点上计算 $h$ 并取平均来估计。随着 $n$ 变大，估计会越来越好。但即使 $n = 1$ 也有效！也就是说，我们可以通过随机选择一个点 $x \in D$，计算 $h(x)$ 并乘以 $D$ 的大小来估计 $h$ 在定义域 $D$ 上的积分。这种估计通常不会很好，但如果我们多次重复估计过程，平均值将是一个相当好的估计。

我们将把它应用到这样的情况：$h$ 是反射率方程中的被积函数，$D$ 是上半球。让我们看看代码（见代码清单29.3）。
