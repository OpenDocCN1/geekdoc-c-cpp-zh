
这里我们在某些地方使用 \(P - Q\) 而不是 \(Q - P\)，以避免多余的负号或绝对值。

估计*任意*函数 \(g\) 在*任意*区域上的积分的一种方法是：在该区域中随机选取一点 \(X\)，计算 \(g(X)\)，再乘以该区域的面积。（我们将在第30章更详细地讨论这一点。）如果重复这一过程，那么每个单独的估计值可能不会很好，但随着我们选取的（独立）点越来越多，它们的平均值会越来越好。将其应用到上面的积分中，如果我们在光源上选取 \(N\) 个点 \(Q_j \in R\)，则可以将反射光估计为

$$\begin{aligned}
L(P,\omega_o) &= \int_{Q\in R} L(P,S(P-Q)) f_p(S(Q-P),\omega_o)\,\mathbf{n}\cdot S(Q-P)\cdot \frac{\mathbf{m}\cdot S(P-Q)}{\|Q-P\|^2}\,dQ \tag{14.28}\\
&\approx \sum_{j=1}^{N} L(P,S(P-Q_j)) f_p(S(Q_j-P),\omega_o)\,\mathbf{n}\cdot S(Q_j-P)\cdot \frac{\mathbf{m}\cdot S(P-Q_j)}{\|Q_j-P\|^2}\frac{A}{N}. \tag{14.29}
\end{aligned}$$

因子 \(A/N\) 的另一种解释是，每个样本 \(Q_j\) 代表光源面积的 \(1/N\)。

通过令 \(\omega_{i,j}\) 为从 \(P\) 指向光源上第 \(j\) 个样本点 \(Q_j\) 的单位向量 \(S(Q_j-P)\)，我们可以在一定程度上简化该表达式中的记号。于是有

$$L(P,\omega_o) \approx \sum_{j=1}^{N} L(P,\omega_{i,j}) f_p(\omega_{i,j},\omega_o)\,\mathbf{n}\cdot\omega_{i,j}\frac{-\mathbf{m}\cdot\omega_{i,j}}{\|Q_j-P\|^2}\frac{A}{N}. \tag{14.30}$$

若用 \(M(P,Q,\mathbf{m})\) 表示值

$$M(P,Q,\mathbf{m}) = A L(P,\omega_{i,j}) \frac{-\mathbf{m}\cdot\omega_{i,j}}{\|Q_j-P\|^2}, \tag{14.31}$$

则反射辐射亮度变为

$$\begin{aligned}
L(P,\omega_o) &\approx \frac{1}{N}\sum_{j=1}^{N} M(P,Q_j) f_p(\omega_{i,j},\omega_o)\,\mathbf{n}\cdot\omega_{i,j} \tag{14.32}\\
&= \frac{1}{N}\sum_{j=1}^{N} M(P,Q_j,\mathbf{m}) f_p(S(Q_j-P),\omega_o)\,\mathbf{n}\cdot S(Q_j-P). \tag{14.33}
\end{aligned}$$

\(M\) 的单位是 \(\mathrm{m}^2\) 乘以辐射亮度单位再乘以 \(d\omega/dA\) 的单位，即每平方米球面度；净单位是 \(\mathrm{W/m^2}\)。我们将 \(M\) 称为**双距离**（bidistance），以表明它依赖于*两个*点：一个在光源上，一个在接收表面上。我们提醒，这并不是一个标准的辐射度量学术语。

我们稍后会回到 \(M\) 的解释，但这个方程的结构引导我们得到遵循代码清单14.11结构的伪代码：

```text
repeat N times:
  // Computed by the emitter
  L_i = ...
  M_i = L_i + max(-m.dot(w_i), 0.0f) * A / |L_p - Q|^2

  // Computed by the integrator (i.e., renderer)
  if there is an occluder on the line from P to Q then M_i = 0
  L_o += M_i * bsdf.evaluate(...) * n.dot(w_i) / N
```

因此，对已弃用的固定功能 OpenGL Phong 着色以及（在某种程度上）WPF 中的着色的一种解释是，光的“强度”对应于函数 \(M\)，其单位是瓦特每平方米。然而，这个特定量在辐射度量学中并没有标准名称，我们不会再提及它。还值得注意的是，在使用经典模型的大多数简单渲染中，\(1/r^2\) 衰减实际上并未建模，因此把 \(M\) 中使用的量当作强度这一说法有些可疑。事实是，如果你希望用经典模型近似物理现实，那么你*应该*使用 \(1/r^2\) 衰减，并且应该为光源赋予根据 \(M\) 的公式计算出的“强度”值。

### 14.11.3.4 将接口应用于光子发射

双向光线追踪和光子映射等算法会从光源出发，将虚拟光子的路径向前追踪到场景中。这些虚拟光子与其所模拟的真实光子在两个方面有所不同。第一个区别是，它们的状态包括位置、传播方向以及光子的*功率*。真实光子传输*能量*，但渲染考虑的是稳态光传输，因此它追踪的是能量传递速率。更准确地说，每个虚拟光子模拟的是一束光子流，或者说模拟的是一段光传输路径。与真实光子的第二个区别是，数以万亿计的真实光子才构成一幅真实图像，而渲染器通常只采样几百万个虚拟光子（尽管每个虚拟光子代表一束光子流，因此实际上隐含地模拟了多得多的真实光子）。

光子追踪的第一步是从场景中的光源发射光子。代码清单14.12展示了如何使用我们的光源接口，以与每个光源功率成正比的概率密度函数采样 `numPhotons` 个发射的虚拟光子。

*代码清单14.12：从一组光源生成 `numPhotons` 个光子；例如，用于光子映射。*

```cpp
void emitPhotons
(const int                  numPhotons,
 const Array<Light*>&       lightArray,
 Array<Photon>&             photonArray) {

  Power totalPower;
  for (int i = 0; i < lightArray.size(); ++i)
    totalPower += lightArray[i]->power();

  for (int p = 0; p < numPhotons; ++p) {
    // Select light with probability L.power.sum()/totalPower.sum()
    const Light* light = chooseLight(lightArray, totalPower);

    Point3        Q;
    Vector3       w_o;

    const Color3& c = light->emitPhoton(Q, w_o);
    photonArray.append(Photon(c*totalPower/numPhotons, Q, w_o));
  }
}
```

## 14.11.4 矩形面光源

现在，我们建模一个从单侧发光的平面矩形面片，如图14.30所示。这将是一个所谓的“朗伯发射体”，这意味着，如果我们限制视野使该发射体完全充满视野，那么无论其方向或距离如何，我们感知到的发射体亮度都相同。我们用一个标准正交参考系描述光源的方向，其中 m 是发射光子一侧的单位法线，u 和 v 是沿边缘的轴。边缘长度由 extent 给出，光源以点 C 为中心。

![](img/f464cd0043eb5336aa0543fe20a0561b_427_0.png)

光源发射的总功率为 Φ。这意味着，如果我们增大 extent，场景中的照明水平看起来会保持不变，但发射体表面看起来会变暗，因为同样的功率被分布在更大的面积上。

朗伯发射体上一点 Q 在任意方向 ω 上发射的辐射亮度（W/(m² sr)）等于总发射功率（W）除以发射体面积（m²）与所谓的“投影立体角”（sr）之积

$$L(Q,\omega)=\frac{\Phi}{A\int_{\Omega_+}[-\gamma\cdot m]\,d\gamma}=\frac{\Phi}{A\,\pi\,\mathrm{sr}}$$ (14.34–14.35)

关于此术语及其他辐射度量学术语的讨论，见第26.7.1节。

我们现在可以计算由 Q 引起的 P 处辐射亮度。令 ωᵢ = S(Q − P)。从 Q 沿方向 −ωᵢ 离开的光以方向 −ωᵢ 到达 P。根据式14.35，离开光的辐射亮度为 Φ/(A π sr)。因此

$$M_i(Q,P)=L(P,-\omega_i)\frac{A}{\|Q-P\|^2}(-m\cdot\omega_i)\,\mathrm{sr}$$
$$=\frac{\Phi}{A\,\pi\,\mathrm{sr}}\frac{A}{\|Q-P\|^2}(-m\cdot\omega_i)\,\mathrm{sr}$$
$$=\frac{(-m\cdot\omega_i)\Phi}{\|Q-P\|^2\pi}$$ (14.36–14.38)

假设 P 位于光源的发光侧，并且到 Q 的视线未被遮挡。代码清单14.13给出了基于该推导的此类光源关键 Light 方法的实现。

代码清单14.13：单侧矩形朗伯发射体的模型。

```cpp
class RectangularAreaLight : public Light {
private:
    // Orthonormal reference frame of the light
    Vector3 u, v, m;
    Vector2 extent;

    // Center of the source
    Point3 C;

    Power3 Phi;

public:

    ...

    Vector4 randomPoint() const {
        return Vector4(C +
            u * (random(-0.5f, 0.5f) * extent.x) +
            v * (random(-0.5f, 0.5f) * extent.y), 1.0f);
    }

    float area() const {
        return extent.x * extent.y;
    }

    Power3 power() const {
        return Phi;
    }

    Power3 biradiance(Vector4 Q, Vector3 P) const {
        assert(Q.w == 1);
        const Vector3& w_i = (Q.xyz() - P).direction();

        return Phi * max(-m.dot(w_i), 0.0f) /
            (PI * (P - Q.xyz()).squaredLength());
    }
};
```

## 14.11.5 半球面光源

一个向内发射的大半球形光源是天空或环境中其他远处部分的常见模型。代码清单14.14将矩形面光源的概念适配到这样的穹顶。该模型有两个自然的扩展：引入一个坐标系，使半球可以任意居中并定向；以及用图像调制穹顶上的功率，以更好地模拟复杂环境和具有高度变化性的天空。

代码清单14.14：一个朝向内部的半球形光穹模型，以原点为中心，并关于 y 轴具有旋转对称性。

```cpp
class HemisphereAreaLight : public Light {
private:
    // Radius
    float r;
    Power3 Phi;

public:

    ...

    Vector4 randomPoint() const {
        return Vector4(hemiRandom(Vector3(0.0f, 1.0f, 0.0f)) * r, 1.0f);
    }
}
```
