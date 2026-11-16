

![](img/672fe9a2d008ba627b1991e15d70f43e_257_0.png)

```
$(e_1 \wedge e_3) \cap (e_2 \wedge e_3) = (e_1 \wedge e_3) \lrcorner (e_2 \wedge e_3)$
$= ((e_1 \wedge e_3) \lrcorner I) \lrcorner (e_2 \wedge e_3)$
$= \langle e_1 e_3 e_1 e_2 e_3 \rangle_{3-2} \lrcorner (e_2 \wedge e_3)$
$= \langle -e_2 e_3 e_1 \rangle_{3-2}$
$= -e_3$
(2.1.17)
```

- 4. 我们证明欧拉定理，即两个旋转的乘积是另一个旋转，通过得到结果旋转的具体公式。我们以通常的方式将四元数视为标量 \(\beta_0\) 加上旋转轴 \(\mathbf{q} = \beta e_i + \beta e_j + \beta e_k\)，写作 \(\beta_0 + \mathbf{q}\)。假设任何单一旋转都可以表示为四元数。回顾伪标量 \(\mathbf{I} = e_1 \wedge e_2 \wedge e_3\) 并使用之前的定义，我们用变换 \(\beta_0 + \mathbf{q} \rightarrow \beta_0 - \mathbf{Iq}\) 将此四元数表示重写为 GA 版本。现在相乘两个四元数，可以很容易地从方程 2.1.18 中读出定义结果四元数的标量和向量。这证明了欧拉定理，并为结果标量和向量得出了具体答案。使用通常的四元数计算此关系既混乱又临时，但使用几何代数则很简单。

*我们假设任何旋转都可以由四元数表示。我有一个证明，但它写不下在这个页边空白里。*

```
$(p_0 + \mathbf{p})(q_0 + \mathbf{q}) \to (p_0 - \mathbf{I}\mathbf{p})(q_0 - \mathbf{I}\mathbf{q})$
$= p_0 q_0 - p_0 \mathbf{I}\mathbf{q} - q_0 \mathbf{I}\mathbf{p} + \mathbf{I}\mathbf{p} \mathbf{I}\mathbf{q}$
$= p_0 q_0 - \mathbf{p}\mathbf{q} - \mathbf{I}\mathbf{q} \cdot q_0 - \mathbf{I}\mathbf{p} \cdot \mathbf{p}$
$= p_0 q_0 - \mathbf{p} \cdot \mathbf{q} - \mathbf{p} \wedge \mathbf{q} - p_0 \mathbf{I}\mathbf{q} - q_0 \mathbf{I}\mathbf{p}$
$= p_0 q_0 - \mathbf{p} \cdot \mathbf{q} - \mathbf{I} (p_0 \mathbf{q} + q_0 \mathbf{p} + \mathbf{q} \times \mathbf{p})$
$\to (p_0 q_0 - \mathbf{p} \cdot \mathbf{q}) + (p_0 \mathbf{q} + q_0 \mathbf{p} + \mathbf{q} \times \mathbf{p})$ (2.1.18)
```

- 5. 需要一个具体的旋转示例：绕 \(\mathbf{e}_1\) 旋转 \(\pi/2\) 之后再绕 \(\mathbf{e}_2\) 旋转 \(\pi/2\) 的复合，结果是绕向量 \((\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)/\sqrt{3}\) 旋转 \(2\pi/3\)。该计算使用前一个示例中的四元数表示。回顾我们将角度除以 2。证明见方程 2.1.19。

  \(\left( \cos \frac{\pi}{4} + \mathbf{e}_1 \sin \frac{\pi}{4} \right) \left( \cos \frac{\pi}{4} + \mathbf{e}_2 \sin \frac{\pi}{4} \right) \to \frac{1}{\sqrt{2}}(1+\mathbf{e}_{32}) \frac{1}{\sqrt{2}}(1+\mathbf{e}_{13})\)
  \(= \frac{1}{2}(1+\mathbf{e}_{13}+\mathbf{e}_{32}+\mathbf{e}_{21})\)
  \(= \frac{1}{2} - \frac{\sqrt{3}}{2} \mathbf{I} \frac{(\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)}{\sqrt{3}}\)
  \(\to \cos \frac{\pi}{3} + \frac{(\mathbf{e}_1 + \mathbf{e}_2 + \mathbf{e}_3)}{\sqrt{3}} \sin \frac{\pi}{3}\) (2.1.19)

- 6. 一次旋转整个多重向量的示例是将由双向量 \(\mathbf{B} = \mathbf{e}_1 \wedge \mathbf{e}_2\) 定义的平面绕向量 \(\mathbf{a} = \mathbf{e}_1 + \mathbf{e}_3\) 旋转 60 度。无需首先将平面分解为分量向量。我们从归一化转子 \(\mathbf{R} = \cos(\pi/6) - \mathbf{I}\mathbf{a}/(\sqrt{2}) \sin(\pi/6)\) 开始。然后旋转后的平面如方程 2.1.20 所示。

  \(\mathbf{R}\mathbf{B}\mathbf{R}^{-1} = \left( \cos \frac{\pi}{6} - \frac{\mathbf{e}_{23} - \mathbf{e}_{13}}{\sqrt{2}} \sin \frac{\pi}{6} \right) (\mathbf{e}_1 \wedge \mathbf{e}_2) \left( \cos \frac{\pi}{6} + \frac{\mathbf{e}_{23} - \mathbf{e}_{13}}{\sqrt{2}} \sin \frac{\pi}{6} \right)\)
  \(= \frac{1}{2} \mathbf{e}_{12} + \frac{\sqrt{6}}{4} (\mathbf{e}_{13} + \mathbf{e}_{23}).\) (2.1.20)

*这样做避免了对平面应用旋转并不得不重新计算法线的问题。回顾，旋转平面的法线不是平面的旋转法线！通常平面由一个点和法线定义，旋转平面需要得到两个与法线正交的线性无关向量，旋转这两个向量，计算新法线，并得到新点。*

- 7. 给定平面中的向量 a、b 和 c，我们可以找到向量 x，使得“a 与 b 之比等于 c 与 x 之比”，如图 2.1.10 所示。如果我们是实数，我们会解 x · c = b : a。GA 的表现也相同，因为我们现在可以通过将比率乘以 c 来除以向量，从而得到答案 x = ba⁻¹c。

![](img/672fe9a2d008ba627b1991e15d70f43e_259_0.png)

- 8. 同样在平面中，我们找到直线 (x − a) ∧ u = 0 到原点的距离，如图 2.1.11 所示。我们找到垂直于直线并经过原点的向量 d，其长度即为距离。使用示例 2.1.1 中的法线条件和面积条件的相同推理，得到 d = (a ∧ u)u⁻¹，从而得到距离 |d|。这对从平面到原点的距离是否也适用？

- 9. 为了展示投影公式的示例，我们将向量 a = α₁e₁ + α₂e₂ + α₃e₃ 投影到平面 B = e₁ ∧ e₂ 上，我们选择该平面以便轻松验证答案。由于平面方向良好，我们知道答案应该是 α₁e₁ + α₂e₂。计算验证了这一点，如方程 2.1.21 所示。

```
P_B(a) = (a · B)B⁻¹
= ⟨(α₁e₁ + α₂e₂ + α₃e₃)(e₁₂)⟩₂(e₂₁)
= (α₁e₂ − α₂e₁)(e₂₁)
= α₁e₁ + α₂e₂
(2.1.21)
```

- 10. 我们找到平面中两条直线交点的通用公式（这只是克莱姆法则，但我们完全直观和几何地推导了它）。参见图 2.1.12；第一次看时这很难看出来。

### FIGURE 2.1.11 从点到直线的距离计算很简单。

我们可以将两条给定的直线 \((\mathbf{x}-\mathbf{a})\wedge\mathbf{u}=0\) 和 \((\mathbf{x}-\mathbf{b})\wedge\mathbf{v}=0\) 写成展开形式 \(\mathbf{x}\wedge\mathbf{u}=\mathbf{a}\wedge\mathbf{u}\) 和 \(\mathbf{x}\wedge\mathbf{v}=\mathbf{b}\wedge\mathbf{v}\)。设 \(\mathbf{U}=\mathbf{a}\wedge\mathbf{u}\) 和 \(\mathbf{V}=\mathbf{b}\wedge\mathbf{v}\)。很明显，交点是 \(\mathbf{u}\) 和 \(\mathbf{v}\) 的线性组合。为了找到系数，我们看图。对应于 \(\mathbf{V}\) 的面积除以对应于 \(\mathbf{u}\wedge\mathbf{v}\) 的面积，给出所需的 \(\mathbf{u}\) 的倍数，而将 \(\mathbf{U}\) 除以 \(\mathbf{u}\wedge\mathbf{v}\) 给出 \(\mathbf{v}\) 的倍数。但是，由于必须考虑双向量的方向，我们需要在 \(\mathbf{v}\) 方向上反转 \(\mathbf{u}\wedge\mathbf{v}\)。因此最终答案必须是

```
\(\mathbf{x}=\frac{\mathbf{V}}{\mathbf{u}\wedge\mathbf{v}}+\frac{\mathbf{U}}{\mathbf{v}\wedge\mathbf{u}}\cdot\mathbf{v}.\)
```

精通几何代数的人会画出图并能立即写出这个方程。有了 GA 引擎，就不需要复杂的直线交点例程——只需要几何积！

![](img/672fe9a2d008ba627b1991e15d70f43e_260_1.png)

### FIGURE 2.1.12 可视化克莱姆法则的图形方法。

- 11. 一道课后练习；给定平面三角形，顶点为 $(x_i, y_i)$，$i=1,2,3$，证明面积是方程 2.1.22 中行列式的绝对值。仅使用解析几何，这个证明需要大量工作，但使用 GA 非常简短（大约半页）。提示：使用外积很容易。推广到更高维度：

```
\(Area = \frac{1}{2} \begin{vmatrix} x_1 & y_1 & 1 \\ x_2 & y_2 & 1 \\ x_3 & y_3 & 1 \end{vmatrix}.\) (2.1.22)
```

- 12. 作为最后一个示例，考虑寻找将一个方向移动到另一个方向的旋转问题，如图 2.1.13 所示。

![](img/672fe9a2d008ba627b1991e15d70f43e_261_0.png)

例如，我们可能希望将 AI 控制的飞船与玩家控制的飞船对齐。如果我们将方向存储为四元数，那么这只是求逆并相乘，但如果我们只有定义每个方向的三个线性无关向量，那么找到这个旋转需要大量工作。我们不要求向量正交，只要求线性无关。假设存在一个旋转（转子）\(\mathbf{R}\)，使得 \(\mathbf{b}_i = \mathbf{R}\mathbf{a}_i\mathbf{R}^{-1}\) 对 \(i=1,2,3\) 成立。我们想求解这三个方程以求 \(\mathbf{R}\)。令 \(\mathbf{R} = \alpha - \mathbf{B}\)，其中 \(\mathbf{B}\) 为某个双向量（因此 \(\mathbf{R}^{-1} = \alpha + \mathbf{B}\)）。大胆的读者应在继续之前尝试使用线性代数求解此问题。我们定义一个互易框架（其作用有点像正交标准框架），用上标表示：设

