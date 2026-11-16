

### 定理 2.1.0.6（第一个 MRRW 界）设 $0 < \delta < 1 - q^{-1}$。则

\(\alpha_q(\delta) \le H_q \left( \frac{1}{q}(q-1-(q-2)\delta - 2\sqrt{(q-1)\delta(1-\delta)}) \right).\)

特别地，如果 $q=2$，则当 $0 < \delta < 1/2$ 时，

\(\alpha_2(\delta) \le H_2 \left( \frac{1}{2} - \sqrt{\delta(1-\delta)} \right).\)

### 定理 2.1.0.7（第二个 MRRW 界）设 $0 < \delta < 1/2$。则

\(\alpha_2(\delta) \le \min_{0 \le u \le 1-2\delta} (1 + g(u^2) - g(u^2 + 2\delta u + 2\delta))\)

其中 \(g(x) = H_2((1 - \sqrt{1-x})/2)\)。

第二个 MRRW 界在 $q=2$ 且 $\delta < 0.272$ 时优于第一个 MRRW 界。令人惊讶的是，如果 $q=2$，则当 $0.273 \le \delta \le 0.5$ 时，两个界相等。练习 142 表明，当 $q=2$ 时，第二个 MRRW 界严格小于渐近 Elias 界。

### 练习 140 承接练习 139，为 $q=2, q=3$ 和 $q=4$ 绘制的图表添加来自第一个 MRRW 界的不等式图。（计算机绘图工具可能有帮助。）在每种情况下，对于 $\delta$ 的哪些值，第一个 MRRW 界比渐近 Singleton 界、渐近 Plotkin 界、渐近 Hamming 界和渐近 Elias 界更强？

### 练习 141 根据第二个 MRRW 界，\(\alpha_2(\delta) \le 1 + g((1-2\delta)^2) - g((1-2\delta)^2 + 2\delta(1-2\delta) + 2\delta)\)。验证当 $q=2$ 时，这是第一个 MRRW 界。

### 练习 142 本练习表明，当 $q=2$ 时，第二个 MRRW 界严格小于渐近 Elias 界。

- (a) 根据第二个 MRRW 界，\(\alpha_2(\delta) \le 1 + g(0) - g(2\delta)\)。验证当 $q=2$ 时，这是渐近 Elias 界。
- (b) 验证 $1 + g(u^2) - g(u^2 + 2\delta u + 2\delta)$ 的导数在 $u=0$ 处为负。
- (c) 部分 (a) 和 (b) 如何表明当 $q=2$ 时，第二个 MRRW 界严格小于渐近 Elias 界？

## 2.10.6 渐近 Gilbert-Varshamov 界

我们现在转向将要介绍的唯一渐近下界。这个界既是 Gilbert 界也是 Varshamov 界的渐近版本。我们将使用 Gilbert 界给出这个渐近界，并将验证渐近 Varshamov 界给出相同结果留作练习。

### 定理 2.1.0.8（渐近 Gilbert–Varshamov 界）如果 $0 < \delta \le 1 - q^{-1}$ 且 $q \ge 2$，则 \(\alpha_q(\delta) \ge 1 - H_q(\delta)\)。

证明：根据 Gilbert 界 \( A_q(n, \delta n) = A_q(n, \lceil \delta n \rceil) \ge q^n / V_q(n, \lceil \delta n \rceil - 1) \)。由于 \( \lceil \delta n \rceil - 1 \le \lfloor \delta n \rfloor \)，\( A_q(n, \delta n) \ge q^n / V_q(n, \lfloor \delta n \rfloor) \)。因此
\[ \alpha_q(\delta) = \limsup_{n \to \infty} n^{-1} \log_q A_q(n, \delta n) \]
\[ \ge \limsup_{n \to \infty} 1 - n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor - 1) = 1 - H_q(\delta) \]
根据引理 2.10.3。

### 练习 143 验证，对于 \( q \ge 2 \)，Varshamov 界的渐近版本在 \( 0 < \delta \le 1 - q^{-1} \) 时产生下界 \(\alpha_q(\delta) \ge 1 - H_q(\delta)\)。

渐近 Gilbert-Varshamov 界发现于 1952 年。这个界（理论上）保证存在一族码，其长度递增，相对距离趋近于 \(\delta\)，而码率趋近于 \(1 - H_q(\delta)\)。在下一节和第 13 章中，我们将构造具体的码族，即 lexicodes 和 Goppa 码，它们满足这个界。30 年来，没有人能构造出超过这个界的码族，许多人认为渐近 Gilbert-Varshamov 界实际上给出了 \(\alpha_q(\delta)\) 的真实值。然而，在 1982 年，Tsfasman, Vlăduţ 和 Zink [333] 展示了一族长度递增的码超过渐近 Gilbert-Varshamov 界。这族码来自一组称为代数几何码的码，在第 13 章中描述，它们推广了 Goppa 码。然而，这个构造适用的 \(\mathbb{F}_q\) 存在限制：\( q \) 必须是平方数且 \( q \ge 49 \)。特别是，目前尚无已知的二进制码族超过渐近 Gilbert-Varshamov 界。在图 2.2 中，我们给出了本节和第 1.12 节讨论的 \( q=2 \) 时 \(\alpha_q(\delta)\) 的五个上界和一个下界；参见练习 140。在此图中，虚线右侧 \(\alpha_q(\delta)\) 的实际值为 0。满足或超过渐近 Gilbert-Varshamov 界的二进制码族位于图中的点线区域。

### 练习 144 承接练习 140，为 \( q = 3 \) 和 \( q = 4 \) 绘制的图表添加来自渐近 Gilbert-Varshamov 界的不等式图，如图 2.2 中对 \( q = 2 \) 所做的那样。

## 2.11 Lexicodes

有趣的是，存在一类二进制线性码，其构造是第 2.8 节中描述的非线性码的贪心构造，只是向量选择的顺序是预先确定的。这些码称为 lexicodes [39, 57, 192]，我们将展示它们确实是线性的。构造表明 lexicodes 满足 Gilbert 界，这一事实留作练习。这意味着我们可以选择一族长度递增的 lexicodes，它们满足渐近 Gilbert-Varshamov 界。

构造长度 \( n \) 和最小距离 \( d \) 的 lexicodes 的算法如下。

![](img/0af7e79235839ec0eb8bcf8d229f37d4_114_0.png)

### 图 2.2 当 q = 2 时的渐近界。

### I. 将所有 n 元组按字典序排序：

- 0...000
- 0...001
- 0...010
- 0...011
- 0...100
- :

### II. 按如下方式构造长度 n 的向量类 L：

- (a) 将零向量 0 放入 L。
- (b) 在字典序中查找 L 中权重为 d 的第一个向量 x。将 x 放入 L。
- (c) 在字典序中查找下一个向量，其与 L 中每个向量的距离为 d 或更多，并将其加入 L。
- (d) 重复 (c)，直到字典列表中没有更多向量可查看为止。

集合 L 实际上是一个线性码，称为长度 n 和最小距离 d 的 lexicode。事实上，如果我们在恰当的位置提前停止该过程，我们就得到 L 的线性子码。为了证明这一点，我们需要一个由 Levenshtein [192] 提出的初步结果。如果 u 和 v 是长度 n 的二进制向量，我们说 u < v，前提是 u 在字典序中排在 v 之前。

### 引理 2.11.11 如果 u, v 和 w 是长度 n 的二进制向量，且 u < v + w 且 v < u + w，则 u + v < w。

证明：如果 u < v + w，则 u 和 v + w 具有相同的前导项，之后 u 有一个 0，而 v + w 有一个 1。我们可以这样表示：

```
u = a0 ...,
v = a1 ...
```

类似地，由于 v < u + w，我们有

```
v = b0 ...,
u + w = b1 ...
```

然而，我们不知道 a 的长度 i 和 b 的长度 j 是否相同。假设它们不同，且按对称性，i < j。那么我们有

```
v = b' x ...,
u + w = b' x ...
```

其中 b' 是 b 的前 i 个项。以两种方式计算 w，我们得到

```
w = u + (u + w) = (a + b')x ...,
w = v + (v + w) = (a + b')(1 + x) ...
```

这是一个矛盾。因此 a 和 b 具有相同的长度，给出

```
u + v = (a + b)0 ...,
w = (a + b)1 ...
```

表明 u < v + w。

### 定理 2.11.12 按生成顺序标记 lexicode 中的向量，使 c1 是零向量：

- (i) L 是一个线性码，向量 c2 是 L 的基。
- (ii) 在选择 c2 之后，接下来生成的 2^i - 1 个向量是 c1 + c2, c2 + c2, ..., c2^i-1 + c2。
- (iii) 设 Li = {c0, c1, ..., c2^i-1}。那么 Li 是一个 [n, i, d] 线性码。

证明：如果我们证明 (ii)，则得到 (i) 和 (iii)。(ii) 的证明关于 i 进行归纳。显然当 i = 1 时成立。假设前 2^i 个生成的向量如所声称。那么 Li 是线性的，基为 {c1, c2, ..., c2^i-1}。我们展示 Li+1 是线性的，接下来生成的 2^i 个向量在

