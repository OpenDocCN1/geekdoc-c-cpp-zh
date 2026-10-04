
# 第 18 页

## 定理 6 (YZ 分解)

每一个酉矩阵 `U` 可以写为乘积

```
U = e^{i\beta}R_z(2\delta)R_y(2\alpha)R_z(2\gamma) (18)
```

其中 `\alpha, \beta, \gamma, \delta` 是实数。换句话说，`U` 是相位移动、绕 `Z` 轴两次旋转以及绕 `Y` 轴旋转的复合（按适当顺序）。

**证明。** 通过使用 (17) 中的 `R_y(\theta)` 和 `R_z(\theta)` 以及定理 5 的分解 `U = ABC`，我们看到 `A = R_z(2\delta)` 且 `B = R_y(2\alpha)`。`C` 呢？首先选择 `\beta := \frac{\theta+\gamma}{2}` 和 `\gamma := \frac{\theta-\gamma}{2}`。由于 `\beta + \gamma = \theta`，我们可以重写 `C` 为：

```
C = \begin{bmatrix} i & 0 \\ 0 & i \end{bmatrix} = e^{i\beta}\begin{bmatrix} e^{-i\gamma} & 0 \\ 0 & e^{i\gamma} \end{bmatrix} = e^{i\beta}R_z(2\gamma).
```

**证毕。** 备注：乘以 `e^{i\beta}` 称为 `\beta` 的相位移动。

## 30. 量子 Toffoli 门

令 `U` 为任意酉矩阵。按照 [1]，对于任意 `n \ge 1`，定义一个显然是酉的 `2^n \times 2^n` 矩阵。这推广了上述的 Toffoli 门 `T_n = T_n(x_1, \dots, x_{n-1})`。事实上，`T_n` 只是 `T_{n-1}(X)`，其中 `X = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}` 是泡利矩阵。我们可以类似的描述 `T_{n-1}(U)` 对特征态 `|x_1 \dots x_{n-1}\rangle` 的作用如下：`T_{n-1}(U)|x_1 \dots x_{n-1}\rangle` 如下

```
\begin{cases} |x_1 \dots x_{n-1}\rangle & \text{for } i = 0 \\ |x_1 \dots y_{n-1}\rangle & \text{if } i = 1 \end{cases}
```

最后一个比特被 `U` 变换。控制图见 6(a)。

## 31. 控制-门的实现

给定一个酉矩阵 `U`，我们如何实现控制-U 门？使用 `A, B, C` 和某些控制-NOT 门来实现 `T_n(U)` 是不易的。

# 2 × 2 酉矩阵的结构

# 第 22 次讲座

# 第 19 页

## 定理 7

如果 `U \in C^{2\times2}` 是酉的，则存在酉矩阵 `A, B, C` 和 `\beta > 0` 使得 `ABC = I` 且

```
U = e^{i\beta}
```

**证明。** 利用定理 6 的分解 (18)。令 `\alpha, \beta, \gamma, \delta` 为选定的实数。很容易检查 `ABC = I`。剩余的是证明 `U = e^{i\beta}`。

同样，`XYX = -Y`。注意 `XZ = -Z`。

```
YXZ = -X
```

从这些基本性质，我们可以得出 `XBX = -Y`。

```
ZXZ = -Y
```

同样，`ZYZ = -X`。

```
ZYZ = -X
```

同样，`XYX = -Z`。

# 练习题

**8.1：** 给出 Hadamard 矩阵 `H` 和泡利矩阵 `\sigma_x, \sigma_y, \sigma_z` 的分解（利用定理 5）。

**8.2：** 验证 `R_j(\theta)(j = x, y, z)` 对应于绕 `j` 轴旋转角度 `\theta`。

**8.3：** 考虑泡利矩阵 `\sigma_i` (`i = x, y, z` 或 `i = 1, 2, 3`)。证明：

- (i) `\sigma_i` 的特征值为 `\pm1`。
- (ii) `\sigma_{i-1}\sigma_i = i\sigma_{i+1}`，其中下标加法模 3。

**8.4：** 给出定理 5 的后续变体，其中 `U` 被写为 `R_x` 和 `R_y` 矩阵的乘积。

**8.5：** (i) 布洛赫球上的哪些点对应于以下状态：

```
|+rangle = H(0) = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)
|-rangle = H(1) = \frac{1}{\sqrt{2}}(|0\rangle-|1\rangle)
|\alpha\rangle = \frac{1}{\sqrt{3}}(|0\rangle+\sqrt{4}|1\rangle)
|b\rangle = \frac{1}{\sqrt{4}}(|0\rangle)
```

# §10. 超密编码与量子隐形态

(ii) 证明哈达玛门（Hadamard gate）在布洛赫球上的作用可以用文中描述的（旋转后的反射）来描述。

(iii) 同样，描述迪拉克矩阵 `\sigma_x, \sigma_y, \sigma_z` 在布洛赫球上的作用。

**练习 8.6：** 证明 `T_2(U)` 对于“大多数” `2 \times 2` 的 `U` 都是通用的。

# §9. 不克隆定理

在讨论量子电路这一主题之前，我们先证明来自 Wootters 和 Zurek (1982) 的一个关于酉变换的基本性结果。该结果表明，我们无法完美地复制一个未知态。首先，回想复制异或门 `T_2(x, y)`。我们有

```
T_2(x,0) = (x, x).
```

因此，比特 `x` 已经被复制或克隆了。下一个结果显示，通过量子门来实现这一点是不可能的。

**定理 8** *设 `S = S_1 \otimes S_2` 为希尔伯特空间，其中 `S_1` 的维至少为 2。不存在酉变换 `U`，使得对于所有的 `x \in S_1`，*

```
U(|x,0)) = |x,x).
```

**证明。** 通过反证法，假设 `U` 存在。设 `[x], [y]` 为 `S_1` 中的线性无关向量。那么 `U(|x,0)) = |x,x|` 且 `U(|y,0)) = |y,y|`，根据 `U` 的线性性质，

```
U(|z,0)) = \frac{1}{\sqrt{2}}|x,x| + |y,y
```

然而，我们注意到

```
|z,z\rangle = [z] \otimes [z] = \frac{1}{2}(|x\rangle + |y\rangle) \otimes (|x\rangle + |y\rangle) = \frac{1}{2}(|x,x| + |y,y|).
```

但向量 `[x], [y]` 在 `S` 中线性无关意味着，这些向量的任何线性组合相等当且仅当它们的系数相同时。`U(|z,0)) \neq |z,z\rangle`。

**证毕。**

这与我们之前的结论一致，即分离门可以被看作量子门。我们说 `T_2` 可以复制第一个比特。这个悖论的解决是语言上的：当被视为经典门 `T_2` 时，它可以复制第一个比特。当 `T_2` 被看作量子门且 `x` 是叠加态时，`T_2(|x,0)) \neq |x,x|`。

该定理的一个结果是量子密码学：它意味着安全的量子密钥生成是可能的。然而，不克隆定理并没有提到不完美复制的可能性。事实上，已经提出了“弱复制”技术。

**练习 9.1：** 补充一个细节以证明如果 `|x|, |y|` 在 `S` 中线性无关，那么 `|xx\rangle, |xy\rangle, |yx\rangle` 在 `S` 中线性无关。

# §10. 超密编码与量子隐形态

我们给出了贝尔态或 EPR 熵对两个惊讶的应用。`^{11}` 这些应用是互为的，因此将它们放在一起看很有趣。在这里我们区分了两种传输信息的信道：如果它传输经典比特，则它是**经典**的；如果它传输量子态，则它是**量子**的。我们有很多经典信道的例子，从无线电到电话。量子信道已经在实验设置中得到证明。

`^{11}` 以 John S. Bell (1964) 以及 A. Einstein, N. Rosen 和 Podolsky (1935) 的名字命名。

这两个应用涉及这个问题：如果我们有一种某种类型的信道，我们如何利用它来有效地传输另一种类型的数据？

在两个应用中，都有一个预备设置。有一个处于贝尔态的 2 量子比特：

```
|\beta_{00}\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)
```

Alice 持有第一个量子比特（命名为 `a`），Bob 持第二个量子比特（命名为 `b`）。Alice 和 Bob 如何获得这两个比特并不重要。也许他们见面是为了让各自的比特以这种方式纠缠。或者，我们想象由第三方准备这一对，并将其发送给 Alice 和 Bob。

产生这种贝尔态的一种方法是从处于状态 `|00\rangle` 的 `ab` 对开始，对 `a` 施加 `H` 门，对 `b` 施加控非门（即 `T_2` 门）（使用 `a` 作为控制）。见图 7 (a)。

图 7：(a) 产生贝尔态，(b) 隐形态 `|x\rangle`。需要记住的是，只要两个量子比特与外界保持隔离，无论距离多远，它们都保持“纠缠”状态。例如，如果 Bob 测量他的 `b` 量子比特并看到 0，那么 Alice 的 `a` 量子比特将瞬间变为 0。在某种意义上，这种信息的传输比光速还快，这在现实生活中似乎没有任何用处。

## §2. 传输一个比特

让我们从简单的问题开始：假设 Alice 和 Bob 共享一个量子信道，Alice 想要传输一个量子比特。该方案来自 Bennett 和 Wiesner (1992)，被称为超密编码。Mattle, Jozurter 和 Zeilinger (1996) 的实验验证了这种形式。假设 Alice 想要传输两个经典比特 `x, y \in \{0,1\}`。如果 `x=1`，则翻转比特。如果 `y=1`，则取反相位。

| x | y | Alice 的操作 |
|---|---|---|
| 0 | 0 | `|00\rangle + |11\rangle` |
| 0 | 1 | `|01\rangle + |10\rangle` |
| 1 | 0 | `|00\rangle - |11\rangle` |
| 1 | 1 | `|01\rangle - |10\rangle` |

Alice 将她的 `a` 发送给 Bob。接收到 `a` 后，Bob 对 `ab` 实施如下变换：

```
B = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{pmatrix}
```

检查 `B` 是酉变换，Bob 的 word 最终处于 `|xy\rangle` 状态。他现在可以恢复 `x` 和 `y`。

# §11. 量子算法

## 3. 传输两个经典比特

反之，假设 Alice 和 Bob 有一个经典信道，Bob 想要向 Alice 传输一个量子比特。这种应用被称为隐形态，来自 Bennett, Brassard, Peres 和 Wootters (1993)，各种实验已经验证了这一点。

像之前一样 Alice 和 Bob 持贝尔态 `|\beta_+\rangle = (|00\rangle + |11\rangle)/\sqrt{2}`。Bob 想要通过经典信道向 Alice 发送这种状态，Bob 有任何方法吗？

这里是协议的概要。首先，Bob 将 `b` 和 `c` 纠缠，然后对 `b` 和 `c` 进行测量，并将测量结果发送给 Alice。根据这些信息，Alice 对她的 `a` 量子比特执行一个适当的变换。

这里是详细细节。请参考图 7(b)。设 `|x\rangle = \alpha|0\rangle + \beta|1\rangle`，`\alpha, \beta \in \mathbb{C}`。

```
ab 量子比特初始状态为
|x_0\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) \otimes (\alpha|0\rangle + \beta|1\rangle)
= \frac{1}{\sqrt{2}}(\alpha|00\rangle + |10\rangle + \beta|01\rangle + \beta|11\rangle).
```

- Bob 使用 `c` 量比特作为控制对 `b` 量子比特执行控非门。这产生了状态：

```
|x_1\rangle = \frac{1}{\sqrt{2}}(\alpha|000\rangle + |110\rangle) + \beta(|011\rangle + |101\rangle).
```

- 然后 Bob 对 `c` 量比特应用 `H` 门，产生状态：

```
|x_2\rangle = (\alpha|00\rangle + |11\rangle) \otimes (|0\rangle + |1\rangle) + \beta(|01\rangle + |10\rangle) \otimes (|0\rangle - |1\rangle)
```

其中我们有 `a` 态（在图 7(b) 中），这由表计指示。这产生了比特 `b_1c_1 \in \{00, 01, 11\}`，每个的概率为 1/4。

- Bob 使用无线波发送经典比特 `b_1c_1` 给 Alice。

- 根据收到的比特 `b_1c_1`，Alice 可以对她的 `a` 量子比特应用一个简单的酉变换 `X = X_{b1c1}` 来恢复状态 `|x\rangle`。

# §11. 量子算法 第 22 课 第 23 页

**34.** 存在一种偏差，认为“量子计算机本质上比经典计算机更强大”。这可以形式化为关于复杂度类之间包含关系的问题。遗憾的是，我们无法直接解决这些问题，因为这将意味着经典复杂度理论中某些深层假设的解决。我们的首要目标是证明某些特定问题可以使用量子计算机比经典计算机更高效地解决。在这里，大多数结果都是带有条件的，即量子计算机比任何已知的经典算法更高效地解决问题。我们还应该记住，量子算法本质上是概率性的，因此我们只将其与经典随机算法进行比较。

但什么样的量子可以利用量子计算机的特殊能力呢？是否存在明显的任务使得量子计算机做得比经典计算机更高效：量子系统模拟？这难道费曼提出的吗？让我们注意，量子计算机的优势在于能够同时演化多个状态。另一方面，如果我们测量量子态，只能得到一个结果（概率较小）。因此，为了计算，我们需要以某种控制的方式管理这些状态，使概率向目标状态倾斜。量子计算的一种观点（见 Cleve 等人 [14]）基本上是多体系统干涉测量的应用。这与经典计算机不同，在利用其力量之前，必须开发全新的计算技术。

**35. 德多特问题（Deutsch's Problem）。** Deutsch [15] 对量子计算机优于经典计算机的优势给简单的演示。假设我们有一个量子盒 `B`，它包含 2 比特变换

```
B(x)
```

对于某个未知函数 `f: \mathbb{B} \rightarrow \mathbb{B}`。`f` 的所有可能性包括：常数 `0` (`f(0)=f(1)=0`)、常数 `1` (`f(0)=f(1)=1`)、恒等变换 (`f(x)=x`) 或取反 (`f(x)=1-x`)。德多特问题是确定 `f(0)=f(1)` 是否为常数，或 `f(0)\neq f(1)`（平衡）。如果这是一个经典变换，我们需要访问两次黑盒，分别 `x=0` 和 `x=1`。但由于是量子性的，我们可以展示一次访问的解决方案。

考虑 (12) 中的哈达玛矩阵 `H`。如果我们准备输入为 `|0\rangle \otimes |0\rangle`，然后对其施变换 `H_2 = H \otimes H`（见 ...）

```
|x\rangle \otimes |y\rangle = \frac{1}{\sqrt{2}}(|0\rangle \otimes |0\rangle) - \frac{1}{\sqrt{2}}(|0\rangle \otimes |1\rangle)。
```

如果我们通过黑盒，状态变为：

```
B(|x\rangle \otimes |y\rangle) = |x\rangle \otimes |y\oplus f(x)\rangle
= |x\rangle \otimes \frac{1}{\sqrt{2}}(|0\oplus f(x)\rangle - |1\oplus f(x)\rangle)
= |x\rangle \otimes \frac{(-1)^{f(x)}}{\sqrt{2}}(|0\rangle - |1\rangle)
= (-1)^{f(x)}|x\rangle \otimes \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)
= (-1)^{f(x)}|x\rangle \otimes |y\rangle
```

第一个比特非常有趣：

```
(-1)^{f(x)}|x\rangle =
\begin{aligned}
&= \frac{(-1)^{f(x)}}{\sqrt{2}}(|0\rangle + |1\rangle)\\
&= \frac{(-1)^{f(0)}}{\sqrt{2}}(|0\rangle + (-1)^{f(1)}|1\rangle)\\
&= \frac{(-1)^{f(0)}}{\sqrt{2}}(|0\rangle + |1\rangle)|\text{如果 } f \text{ 是常数}\\
&= \frac{(-1)^{f(0)}}{\sqrt{2}}(|0\rangle - |1\rangle)|\text{如果 } f \text{ 是平衡}
\end{aligned}
```
