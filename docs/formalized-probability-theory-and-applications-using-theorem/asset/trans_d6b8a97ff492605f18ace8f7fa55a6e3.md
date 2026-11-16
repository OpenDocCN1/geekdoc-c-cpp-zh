

### Definition 13.10

```
|- forall n k. binomial n k =
(binomial n 0 = (1:num)) /\
(binomial 0 (SUC k) = (0:num)) /\
(binomial (SUC n) (SUC k) = binomial n (SUC k) + binomial n k).
```

带有 n 个节点的整个 WSN 的覆盖强度已由函数 cvrge_intsty_network 正式指定，如定义 13.11 所示。后者以以下参数为输入：p：概率空间，X：返回扩展实数的随机变量，k：子网络数量，s：定义 13.8 中使用的求和集合，C：描述覆盖节点数量的随机变量，n：节点总数，q：每个传感器覆盖给定点的概率。

### Definition 13.11

```
|- forall p x k s c n q. cvrge_intsty_network p x k s c n q =
expectation p (x. cvrge_intsty p p x k s (num (C x))).
```

其中，上述定义中使用的函数 expectation 指定了返回扩展实数的随机变量的期望的高阶逻辑形式化，函数 num 使用实函数 floor 将扩展实数 (&m) 转换为其对应的自然值 m。

最终网络覆盖强度 cvrge_intsty_network 已得到正式验证：

### Theorem 13.4

```
|- forall p C q k s. (prob_space p) /\ (FINITE (p_space p)) /\
(0 < q < 1) /\ (events p = POW (p_space p)) /\ (1 <= n) /\ (1 < k)
/\ FINITE s /\ (CARD s = k) /\ (sn_covers p C p q n) /\
(expectation p # PosInf) /\ (expectation p # NegInf) /\
(forall i x. (i ∈ s) /\ (x ∈ p_space p) /\
sbst_non_empty rv (X i) p k (num(C x))))
==> cvrge_intsty_network p x k s c n q = Normal (1 - (1 - q/(s*k))^n)).
```

where

- 假设 (events p = POW (p_space p)) 表示事件集是样本空间的幂集。
- 假设 (1 <= n) 确保 WSN 包含至少一个节点，而 (0 < q < 1) 确保概率 q 位于 [0..1] 范围内。
- sn_covers p 是具有有限期望的二项式随机变量（定义 13.9），即 (expectation p C ≠ PosInf) ∧ (expectation p C ≠ NegInf)。
- 函数 (sbst_non_empty_rv (X i) p k (num(C x))) 与定义 13.7 中指定的相同，只是它将最后一个输入参数 (num(C x)) 作为随机变量 C 的输出值。

上述定理的证明主要基于勒贝格积分的一些运算以及期望的线性性质，后者进一步需要定理 13.5 来给出随机变量函数的期望。确实，如我们从定义 13.11 中所注意到的，网络覆盖强度 Cn 是随机变量 C 的函数的期望。此外，定理 13.5 的证明包括一些函数单射性的证明以及与随机变量函数相关的一些性质。最后，为了完成此证明，还需要大量与定理 13.6 相关的实分析内容，该定理形式化了实数的二项式定理，以及求和函数。

### Theorem 13.5

```
⊢ ∀ C p q n k. (prob_space p) ∧ (events p = POW (p_space p)) ∧ (FINITE (p_space p)) ∧ (1 < k) ∧ (0 < q < 1) ∧ (1 ≤ n) ∧ (sn_covers p C p q n)) ⇒ (expectation p (x. f_fct (num (C x)) k) = Normal (1 - q/(&k))^x
```

其中，函数 f_fct 定义如下

```
f_fct x k=Normal (1-1/k)^x (13.5)
```

### Theorem 13.6

```
⊢ ∀ (a:real) (b:real) n. (a + b) pow n = sum (0, SUC n) (i. &(binomial n i) * a pow i * b pow i)
```

在本节中，我们介绍了针对无线传感器网络的 k 集随机调度的新高阶逻辑形式化，使用了 HOL 定理证明器中可用的概率理论。这些形式化随后被用于正式推理覆盖性能属性。在下一节中，我们将展示开发的通用定理如何极大地促进现实世界 WSN 应用的正式分析。

## 13.3 森林火灾检测 WSN 的正式分析

无线传感器网络已被广泛用于森林火灾检测（Liu, Wu, Xiao, & Sun, 2011）。确实，森林火灾被认为是世界上最严重的自然灾害之一。它们威胁森林、动物和人类，并造成大量环境退化。确实，每年发生超过 100,000 起野火。例如，在突尼斯，仅在 2012 年 5 月 1 日至 7 月 25 日期间，就有 103 起火灾烧毁了 287 公顷森林。在这种情况下，传感器的主要工作是将温度、湿度和气压值感知并传输到基站。此外，感兴趣区域的恶劣性质使得通过空投传感器进行随机部署变得更加容易。在本节中，我们有兴趣正式分析部署用于森林火灾应用的无线传感器网络的覆盖性能。由于目标应用的安全关键特性，部署的 WSN 必须尽可能长时间保持存活，同时确保对任何火灾突破进行高效覆盖。然而，大多数现有的森林火灾检测 WSN 都面临寿命限制。为了延长整个网络寿命，针对使用无线传感器网络的给定森林火灾检测应用，提出了 k 集随机调度算法。在指定的应用中，节点的感知区域 r = 30，并部署在大小为 a = 100m x 100m 的森林区域内，而传感器覆盖某点的成功概率 q 为 q = r / a = 0.003。

基于前一节的理论工作，我们现在基于参数 n 和 k 对概率覆盖进行正式渐近分析（Elleuch, Hasan, Tahar & Abid, 2012）。为此，我们将先处理一般情况，然后将其实例化为给定的森林火灾应用。因此，我们简单地将 (cvrge_intsty_network p X k s C n q) 表示为 (Cn_wsn p X k s C n q)。在我们的应用背景下，我们可以通过特化定义 13.11 来正式指定给定的森林火灾检测应用，因为它描述了使用 k 集随机调度算法的 WSN 的通用覆盖强度。

### Definition 13.12

```
⊢ ∀ p X k s C n.
cn_wsn_first p X k s C n = cvrge_intsty_network p X k s C n
(0.003).
```

然后，我们在 HOL 中轻松检查 (cn_wsn_first p X k s C n) 等于

Normal (1 - (1 - (0.003/k)^n)) (13.6)

值得注意的是，由于空间限制，我们只提及与网络覆盖强度中使用的变量相关的主要数学假设。

部署的节点数 n 是一个常见的关键属性，对能量和覆盖都有显著影响。直觉上，部署太少的节点可能无法保证良好的覆盖，然而部署太多的节点可能导致能源浪费。在接下来的分析中，我们将通过验证为给定数量 k 的网络覆盖强度 Cn 至少为 t 所需的最小节点数 n_min 来正式确认这一直觉。这个下界可以基于定理 13.4 进行正式验证，该定理清晰地给出了网络覆盖强度 Cn_wsn、节点数 n 和不相交子网络数 k 之间的关系。

### Lemma 13.1

```
⊢ ∀ p X k s C n q t. (1 ≤ n) ∧ (1 < k) ∧ (0 < q < 1) ∧ (0 < t < 1) ∧ (Normal t ≤ Cn_wsn p X k s C n q) ⇒ ln(1-t) / (ln(1-q/k)) ≤ &n.
```

上述引理的证明基于超越函数的一些性质和算术推理。

接下来，我们在引理 13.2 中正式验证，网络覆盖强度 Cn_wsn 是 n 的增函数，即较大的 n 值会导致更好的覆盖强度。在这种情况下，监控区域任何点发生的事件预计会被更快地覆盖，因为周围区域可能部署了更多覆盖节点。

### Lemma 13.2

```
⊢ ∀ p X k s C q. (1 < k) ∧ (0 < q < 1) ⇒ (mono_incr (λn. real (Cn_wsn p X k s C (SUC n) q)))
```

其中，函数 real 用于将类型为扩展实数的网络覆盖强度转换为其对应的实数值，而 mono_incr 是 HOL 中递增序列的定义，我们定义如下：

### Definition 13.13

```
⊢ ∀ f. mono_incr f = ∀n, f n ≤ f (SUC n).
```

因此我们可以推断，在随机调度下，该调度将网络划分为给定数量 k 的子网络，任何网络覆盖强度 Cn_wsn 都可以通过增加部署的节点数 n 来实现。

此外，我们在引理 13.3 中正式验证，当 n 非常大时，Cn_wsn 趋近于其理想值 1。

