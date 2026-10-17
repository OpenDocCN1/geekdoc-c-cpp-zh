
我们使用符号 $\mathbf{v}_1 \wedge \mathbf{v}_2$ 来表示 $\mathbf{v}_1 \wedge \mathbf{v}_2$。因此，如果 $\mathbf{q}_1$ 和 $\mathbf{q}_2$ 是纯四元数，即 $a_1 = a_2 = 0$，那么

```
$$\mathbf{q}_1 \mathbf{q}_2 = -\langle\mathbf{v}_1, \mathbf{v}_2\rangle + \mathbf{v}_1 \wedge \mathbf{v}_2$$
```

因此，四元数乘法综合了 $\mathbb{R}^3$ 中的两种向量乘积：标量积和叉积（在某种意义上，这让我们看到了这种操作的巨大潜力）。注意 $\mathbf{v}$ 是纯四元数，在前面的方程中取 $\mathbf{q}_1 = \mathbf{q}_2 = \mathbf{v}$，我们得到

```
$$\mathbf{v}^2 = -\langle\mathbf{v}, \mathbf{v}\rangle = -|\mathbf{v}|^2$$
```

特别，如果 $\mathbf{v}$ 是单位纯四元数，则 $\mathbf{v}^2 = -1$。

## 4. 旋转空间

每个四元数 $q = a + \mathbf{v}$ 都可以写成形式 $a + b\mathbf{u}$，其中 $|\mathbf{u}| = 1$ 是单位四元数。事实上，我们只能取

```
$$\mathbf{u} = \frac{\mathbf{v}}{|\mathbf{v}|}, \quad \text{and} \quad b = |\mathbf{v}|.$$
```

观察四元数在形式 $q = a + b\mathbf{u}$ 中的表示，由于 $|\mathbf{u}| = 1$，$\mathbf{u}$ 是纯单位四元数，我们有 $u^2 = -1$。然而在这种表示中，如果 $q$ 是单位的，我们有

```
$1 = |q|^2 = a^2 + b^2|\mathbf{u}|^2 = a^2 + b^2.$
```

因此，存在 $\theta \in \mathbb{R}$使得 $a = \cos \theta$ 且 $b = \sin \theta$，我们可以写为 $\mathbf{q} = \cos \theta + \sin \theta \mathbf{u}$。

注意我们得到的与复数的相似性。复数的形式为 $x + iy$，其中 $i^2 = -1$；此外，每个模为 1 的单位数 $i$ 都可以写成 $\cos \theta + i\sin \theta$。区别在于，与复数 $i$ 不同，表示 $p = a + b\mathbf{u}$ 中的单位四元数 $\mathbf{\hat{u}}$ 取决于 $p$。

结果显示四元数具有与复数类似的代数性质，交换律除外。我们最后的测试是将复数的结果扩展到四元数。这是下一节的主题。

### 4.7. 四元数表示旋转

给定一个单位四元数 $\mathbf{q}$，我们通过 $R_q(\mathbf{p}) = \mathbf{q}\mathbf{pq}^*$ 定义变换 $R_q: \mathbb{R}^4 \to \mathbb{R}^4$。我们有 $|R_q(\mathbf{p})| = |\mathbf{p}|$，因此变换 $R_q$ 是正交的。自然的问题：如何通过四元数得到 $SO(3)$ 中的旋转？

一个想法是将每个 $q \in \mathbb{R}^3$ 关联变换 $R_q$。不幸的是，$R_q \notin SO(3)$，纯四元数空间 $\mathbb{R}^3$ 不被 $R_q$ 保持。用四元数表示 $SO(3)$ 更好。

观察单位四元数 $\mathbf{q}$ 在形式 $q = \cos \theta + \sin \theta \mathbf{u}$ 中的表示，其中 $|\hat{u}| = 1$；这显示该四元数定义了一个角度和轴 $\mathbf{u}$。自然期望这个四元数表示绕 $u$ 轴的旋转。我们将证明旋转角度为 $2\theta$。

给定单位四元数 $\mathbf{q}$，我们定义变换 $\varphi_q: \mathbb{R}^3 \to \mathbb{R}^3$，并很快将上述变换的性质。

#### 4.7. 四元数

变换 $\varphi_q$ 是良定义的。这意味着 $\varphi_q(\mathbf{v}) \in \mathbb{R}^3$。事实上，只需证明 $\text{Re}(\varphi_q(\mathbf{v})) = 0$ 即可：

```
\text{Re}(\mathbf{q}\mathbf{vq}^*) = \text{Re}(\mathbf{q}^*\mathbf{v}) = 0.
```

变换 $\varphi_q$ 是线性的。事实上，

```
\varphi_q(\mathbf{u} + \mathbf{v}) = q(\mathbf{u} + \mathbf{v})q^* = q\mathbf{uq}^* + q\mathbf{v}q^* = a(q\mathbf{u}^*) + (q\mathbf{v})^* = a\varphi_q(\mathbf{u}) + \varphi_q(\mathbf{v}).
```

变换 $\varphi_q$ 是正交的。事实上，

```
$|\varphi_q(\mathbf{v})| = |q\mathbf{v}q^*| = |q||\mathbf{v}||q^*| = |\mathbf{v}|.$
```

变换 $\varphi_q$ 是 $\mathbb{R}^3$ 的旋转。事实上，正如我们看到的，只需证明 $\varphi_q$ 是正的。在这种情况下，注意当 $\mathbf{q} = I$ 时，$I: \mathbb{R}^3 \to \mathbb{R}^3$ 是恒等变换。由于单位四元数空间是连通的（因为它是 $\mathbb{R}^4$ 中的球面），我们通过连续性证明，对于每个四元数 $\mathbf{q}$ $\varphi_q$ 都是正的。

$\varphi_q$ 的旋转轴是四元数 $\mathbf{u}$。只需证明 $\varphi_q(\mathbf{u}) = \mathbf{u}$ 即可：

```
\varphi_q(\mathbf{u}) = q\mathbf{uq}^* = (\cos \theta + \sin \theta\mathbf{u})(\cos \theta - \sin \theta\mathbf{u}) = (\cos \theta)^2\mathbf{u} - (\sin \theta)^2\mathbf{u}^3 = (\cos \theta)^2\mathbf{u} - (\sin \theta)^2(-\mathbf{u}) = \mathbf{u}.
```

$\varphi_q$ 的旋转角度是 $2\theta$。我们通过解决问题提供这一事实的几何证明：给定绕轴 $r$ 旋转角度 $\theta$ 的 $R$，我们如何得到表示 $\varphi_q$ 的四元数 $\mathbf{q}$？为了回答这个问题，考虑图 4.6，它显示了点 $P$ 绕 $OH$ 轴旋转角度 $\beta$ 的 $R$。点 $P$ 的像是 $P'=R(P)$。

**图 4.6.** 绕轴旋转角度 $\beta$。

让我们取正交系 $\{\mathbf{u}, \mathbf{v}, \mathbf{n}\}$，其中 $\mathbf{u} = \vec{OH}$，$\mathbf{v} = \vec{OV}$，$\mathbf{n}$ 是旋转方向。我们还定义向量

```
\mathbf{h} = \vec{OH}, \quad \mathbf{p} = \vec{OP}, \quad \mathbf{u}' = \vec{HP'}
```

其中 $\mathbf{u} \perp \mathbf{v}, \mathbf{u} \perp \mathbf{n}$ 且 $|\mathbf{u}| = 1$。由于 $\mathbf{h}$ 是 $\mathbf{p}$ 在 $\mathbf{n}$ 方向上的正交投影，我们有 $\mathbf{h} = \langle\mathbf{p}, \mathbf{n}\rangle\mathbf{n}$。很容易验证

```
\mathbf{p}' = \mathbf{h} + \mathbf{u}' = \langle\mathbf{p}, \mathbf{n}\rangle\mathbf{n} + \cos\beta\mathbf{u} + \sin\beta\mathbf{v}
```

我们有：

$$R(P) = \varphi_{\mathbf{q}}(\mathbf{p}) = \mathbf{q}\mathbf{p}\mathbf{q}^*$$

$$= (\mathbf{c} + \mathbf{t})(\hat{\mathbf{p}})(\mathbf{c} - \hat{\mathbf{t}})$$

$$= (\mathbf{c} + \mathbf{t})((\hat{\mathbf{p}}, \hat{\mathbf{t}}) - \hat{\mathbf{p}} \wedge \hat{\mathbf{t}} + c\mathbf{p}))$$ 

$$= \mathbf{c}\hat{\mathbf{p}} - (\mathbf{t}, -\hat{\mathbf{p}} \wedge \mathbf{t}) - c(\mathbf{t}, \hat{\mathbf{t}})$$

$$= \hat{\mathbf{t}} \wedge (-\hat{\mathbf{p}} \wedge \mathbf{t}) + c(-\hat{\mathbf{t}} \wedge \hat{\mathbf{t}} + c\mathbf{p}) + \langle\hat{\mathbf{t}}, \hat{\mathbf{t}}\rangle$$

$$= \langle\hat{\mathbf{t}}, \hat{\mathbf{p}}\rangle - (\mathbf{t}, \hat{\mathbf{t}}) + 2(c\mathbf{t}(\hat{\mathbf{p}}) + c^2\langle{\mathbf{t}, \hat{\mathbf{t}}\rangle)$$

$$= (c^2 - (\mathbf{t}, \hat{\mathbf{t}})^2 + 2(\mathbf{t}, \hat{\mathbf{p}}) + 2c(\langle{\mathbf{t}, \hat{\mathbf{p}}\rangle))$$

在方程 (4.10) 得到的 $\varphi_{\mathbf{q}}$ 表达式中代入 $c = \cos\theta$ 和 $\mathbf{t} = \hat{\mathbf{n}}\sin\theta$，得到：

$$R(P) = (\cos^2\theta - \sin^2\theta)\hat{\mathbf{p}} + 2\sin\theta\cos\theta(\hat{\mathbf{p}} \wedge \hat{\mathbf{n}})\hat{\mathbf{n}} + 2\sin\theta\cos\theta(\hat{\mathbf{n}} \wedge \mathbf{p})$$

$$= \cos(2\theta)\hat{\mathbf{p}} + (1-\cos(2\theta))\mathbf{n}\wedge\mathbf{p}$$

将此方程与方程 (4.9) 比较，我们可以看到 $\varphi_{\mathbf{q}}$ 是绕由单位向量 $\mathbf{n}$ 定义的轴旋转角度 $2\theta$ 的旋转。

上述结果可以总结为：

**定理 4.3 (四元数表示旋转)。** *绕由单位向量 $\mathbf{n}$ 定义的轴旋转角度 $2\theta$ 的旋转由 $\varphi_{\mathbf{q}}(\mathbf{v}) = \mathbf{q}\mathbf{v}\mathbf{q}^{-1}$ 表示。*

因此，我们得到了一个变换：$S^3 \rightarrow SO(3)$，$\varphi(\mathbf{q}) = \varphi_{\mathbf{q}}$，它用 $\mathbb{R}^4$ 中单位球面 $S^3$ 点表示空间中的旋转。接着，根据 $\varphi_{\mathbf{q}}$ 的定义，我们有 $\varphi_{\mathbf{q}} = \varphi_{-\mathbf{q}}$。从几何上看，这一事实是显而易见的，因为绕 $n$ 轴旋转角度 $\theta$ 等于绕 $-n$ 轴旋转角度 $2\pi - \theta$。因此，变换 $\varphi_{\mathbf{q}}$ 不是单射。然而，毫不费力看出：

$$\varphi_{\mathbf{q}} = \varphi_{-\mathbf{q}} \Leftrightarrow \pm\mathbf{q}.$$

我们将这一证明留给本章末尾的练习题。

上述结果显示球面的对点定义了相同的旋转。因此，空间 $SO(3)$ 自然地等同于 $\mathbb{R}^4$ 中的单位球面 $S^3$，且对点被等同。我们知道这是 3 维实射空间 $RP^3$。然而，我们不会使用这种 $SO(3)$ 与 $RP^3$ 之间的关联。上述结果的重要方面是旋转空间 $SO(3)$ 可以由四元数表示。只需注意球面的对点表示相同的旋转。

关于用四元数表示 $SO(3)$ 中的旋转的一个重要事实是乘法运算是被保持的，即：

$$\varphi_{\mathbf{u}_1\mathbf{u}_2} = \varphi_{\mathbf{u}_1}\varphi_{\mathbf{u}_2}.$$

验证这一点是显而易见的：对于每个 $\mathbf{v} \in \mathbb{R}^3$，有：

$$\varphi_{\mathbf{u}_1\mathbf{u}_2}(\mathbf{v}) = \varphi_{\mathbf{u}_1}\varphi_{\mathbf{u}_2}(\mathbf{v})$$

这一事实表明我们可以通过四元数的积来替换两次旋转。特别地，注意这一结果回答了我们在开头的问题：如果旋转 $R_1$ 和 $R_2$ 由单位向量 $\mathbf{u}_1$ 和 $\mathbf{u}_2$ 定义轴，那么旋转 $R_1R_2$ 的轴是四元数 $\mathbf{u}_1, \mathbf{u}_2$ 的积。

### 4.7 指数与对数

考虑向量 $\mathbf{v} \in \mathbb{R}^3, \mathbf{v} \neq 0$；令 $\hat{\mathbf{v}} = \mathbf{v}/|\mathbf{v}|$ 为从 $\mathbf{v}$ 通过归一化得到的单位四元数。使用符号 $\theta = |\mathbf{v}|$，有 $\mathbf{v} = \theta\hat{\mathbf{v}}$。在指数函数的泰勒级数中代入 $e^{\theta\hat{\mathbf{v}}}$：

$$e^{\theta\hat{\mathbf{v}}} = \sum_{n=0}^{\infty} \frac{(\theta\hat{\mathbf{v}})^n}{n!}$$

考虑到 $\hat{\mathbf{v}}^2 = -1$，直接计算得出：

$$e^{\theta\hat{\mathbf{v}}} = \cos\theta + \sin\theta\hat{\mathbf{v}}.$$

我们可以定义指数 $\exp: \mathbb{R}^3 \to S^3$ 为：

$$\exp(\mathbf{v}) = \begin{cases} \cos\theta + \sin\theta\hat{\mathbf{v}} & \text{if } \mathbf{v} \neq 0 \\ (1, 0, 0) & \text{if } \mathbf{v} = 0 \end{cases}$$

其中 $\hat{\mathbf{v}} = \mathbf{v}/|\mathbf{v}|$。我们也会使用符号 $\exp(\mathbf{v}) = e^{\mathbf{v}}$。注意如果 $\mathbf{v}$ 是单位四元数，则 $\mathbf{v} = \cos\theta + \sin\theta\hat{\mathbf{v}}$，且 $|\mathbf{v}| = 1$。对于复数，由于 $|\mathbf{v}| = \theta$，有 $e^{\theta\hat{\mathbf{v}}} = \cos\theta + \sin\theta\hat{\mathbf{v}}$，这是对数函数 $\log: \mathbb{R}^3 \to S^3$ 的相似表达式，它是指数函数的逆函数。对于 $\mathbf{q} \in S^3, \mathbf{q} = \cos\theta + \sin\theta\hat{\mathbf{u}}, |\mathbf{u}| = 1$，有：

$$\log(\mathbf{q}) = \theta\mathbf{u} \in \mathbb{R}^3.$$

验证 $e^{\log(\mathbf{q})} = \mathbf{q}$ 是显而易见的。有时坐标是有用的：在指数和对数的显式定义中，如果 $\mathbf{u} = w + x\mathbf{i} + y\mathbf{j} + zk \in S^3$，我们可以写：

$$\log(w, x, y, z) = \arccos(w) \frac{(x, y, z)}{\sqrt{x^2 + y^2 + z^2}}.$$

相似地，如果 $\mathbf{v} = (x, y, z) \in \mathbb{R}^3$，有：
