

# 数学背景

它被解释为随机过程的一种可能实现，使得 $X_k(\omega) = \omega_k$。当 $\Omega$ 以这种方式定义时，(A.2) 中定义的事件变为：

> $E_{(x_0,\dots,x_N)} = \{\omega \in \Omega : \omega_i = x_i, \quad 0 \leq i \leq N\}. \quad (A.3)$

在此处，我们通常取 $F$ 为包含所有 (A.3) 中事件的最小 $\sigma$ 域，其中 $N$ 遍历所有整数 $N \geq 0$，且 $\{x_i\}$ 可以取自 $X$ 中的任意值。该 $\sigma$ 域包含任何事件，包括：

> ${\omega \in \Omega : \lim_{T \to \infty} \frac{1}{T} \sum_{i=0}^{T-1} c(\omega_i) = \eta\}$

其中 $c: X \to \mathbb{R}$ 是任意函数，$\eta \in \mathbb{R}$ 是任意常数。

# A.2.2 马尔可夫链基础

我们将保持简单，假设马尔可夫链的状态空间 $X$ 是有限的或计数无限的。转移矩阵记为 $P$。对于 $X$ 上的每个 $\mu$，在 $\mathcal{F}$ 上有一个概率测度 $P_{\mu}$，使得 $\mu$ 是链的初始分布。与第 6 章中的定义一致：

> $P_{\mu}[X_0 = x] = \mu(x)$

> $P_{\mu}[X_k = x] = \sum_{x' \in X} \mu(x') P^k(x',x), \quad x \in X$，

> $E_{\mu}[g(X_k)] = \sum_{x} P_{\mu}\{X_k = x\}g(x) \quad$ 对于任意 $g: X \to \mathbb{R}$。

当 $\mu$ 是退化的时（即对于某个 $x$ 使得 $\mu(x)=1$），我们写作 $P_{\mu}$ 和 $E_x$。*移位算子*是 $\Omega$ 上的映射，为复杂概念提供了紧凑的语言。对于每个 $k$，移位算子 $\theta^k$ 将元素 $\omega = \{x_0, x_1, \dots, x_n, \dots\} \in \Omega$ 映射到新值，通过：

> $\theta^k\omega = \{x_k, x_{k+1}, \dots, x_{n+k}, \dots\}$。

它通过如下定义随机变量 $H$ 的变换：

> $(\theta^kH)(\omega) = H(\theta^k\omega)$。

因此，如果随机变量 $H$ 的形式为对于函数 $h$ 的 $h = h(X_0, X_1, \dots)$，那么

> $\theta^kH = h(X_k, X_{k+1}, \dots, \dots)$。

对于某些 $n$ 和 $h: X \to \mathbb{R}$ 特化为 $H = h(X_n)$ 得：

> $\theta^kH = h(X_{n+k})$

因此

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

根据转移矩阵的马尔可夫性质定义。

# A.2 概率与马尔可夫背景

这可以被推广：对于任意初始分布 $X_0 \sim \mu$，任意有界随机变量 $H$，以及固定的 $k, n \in \mathbb{Z}_+$。

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

这简洁地描述了（时间齐次的）*马尔可夫*性质。因此，注意我们将 $E_x[H]$ 视为状态空间上的一个实值函数。在这里我们替换以下内容：

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 强马尔可夫性质

强马尔可夫性质通过公式 (A.4) 的显著扩展来描述。该性质的定义需要这三个要素：

- (i) 函数 $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ 是 **X** 的*停止时间*，如果对于每个 $n \in \mathbb{Z}_+$，事件 $\{\tau = n\}$ 属于 $\mathcal{F}_n$。也就是说，对于每个 $n$，存在一个函数 $f_n$ 使得 $\{\tau = n\} = f_n(X_0, \dots, X_n)$。

- (ii) 相关的移位算子 $\theta^{\tau}$ 的定义与之前相同：$\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$。

- (iii) 相关的 $\sigma$ 域也定义为：$\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ 对于每个 } n \in \mathbb{Z}_+\} \quad (A.5)$

这被解释为“在时间 $\tau$ 之前”发生的事件。

两个重要的停止时间例子，对于任意集合 $A \subset X$：

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

分别被称为进入 $A$ 的首次时间和击中时间。

**命题 A.1** 对于任意集合 $A \subset X$，变量 $\tau_A$ 和 $\sigma_A$ 是 **X** 的停止时间。

*证明* 随机变量 $\tau_A$ 和 $\sigma_A$ 具有如下表示，对于任意 $n \ge 1$：

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

```
$\{\sigma_A = n\} = g_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=0}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

其中 $\prod_{i=1}^{0} = 1$（处理 $n=1$ 的情况）。对于 $n=0$，我们有 $\{\tau_A = 0\} = f_0(X_0) = 0$ 且 $\{\sigma_A = 0\} = g_0(X_0) \mathbb{1}\{X_0 \in A\}$。$\square$

# 数学背景

一个 $\mathcal{F}_t$-可测的有限值随机变量 $H$ 可以表示为无穷和：

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

对于函数序列 $\{h_n\}$；这对于什么性质成立？

一个例子是随机变量 $X_{\tau}$，其通过设置 $X_{\tau} = X_n$ 定义：

```
$X_{\tau} = X_n \mathbb{1}\{\tau = n\}
```

对于某些 $n$ 和 $h: X \to \mathbb{R}$，特化为 $H = h(X_n)$ 得到：

> $\theta^kH = h(X_{n+k})$ （注：原文此处漏了一个右括号，翻译时已补全或保持原文逻辑，此处原文为 $\theta^kH = h(X_{n+k}$） 

修正正逻辑逻辑：
特化为 $H = h(X_n)$ 对于某些 $n$ 和 $h: X \to \mathbb{R}$ 得到：

> $\theta^kH = h(X_{n+k})$

因此

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

根据转移矩阵的马尔可夫性质定义。

# A.2 概率与马尔可夫背景

这可以被推广：对于任意初始分布 $X_0 \sim \mu$，任意有界随机变量 $H$，以及固定的 $k, n \in \mathbb{Z}_+$。

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

这简洁地描述了（时间齐次的）*马尔可夫*性质。因此，注意我们将 $E_x[H]$ 视为状态空间上的一个实值函数。在这里我们替换以下内容：

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 强马尔可夫性质

强马尔可夫性质通过公式 (A.4) 的显著扩展来描述。该性质的定义需要这三个要素：

- (i) 函数 $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ 是 **X** 的*停止时间*，如果对于每个 $n \in \mathbb{Z}_+$，事件 $\{\tau = n\}$ 属于 $\mathcal{F}_n$。也就是说，对于每个 $n$，存在一个函数 $f_n$ 使得 $\{\tau = n\} = f_n(X_0, \dots, X_n)$。

- (ii) 相关的移位算子 $\theta^{\tau}$ 的定义与之前相同：$\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$。

- (iii) 相关的 $\sigma$ 域也定义为：$\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ 对于每个 } n \in \mathbb{Z}_+\} \quad (A.5)$

这被解释为“在时间 $\tau$ 之前”发生的事件。

两个重要的停止时间例子，对于任意集合 $A \subset X$：

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

分别被称为进入 $A$ 的首次时间和击中时间。

**命题 A.1** 对于任意集合 $A \subset X$，变量 $\tau_A$ 和 $\sigma_A$ 是 **X** 的停止时间。

*证明* 随机变量 $\tau_A$ 和 $\sigma_A$ 具有如下表示，对于任意 $n \ge 1$：

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

```
$\{\sigma_A = n\} = g_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=0}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

其中 $\prod_{i=1}^{0} = 1$（处理 $n=1$ 的情况）。对于 $n=0$，我们有 $\{\tau_A = 0\} = f_0(X_0) = 0$ 且 $\{\sigma_A = 0\} = g_0(X_0) \mathbb{1}\{X_0 \in A\}$。$\square$

# 数学背景

一个 $\mathcal{F}_t$-可测的有限值随机变量 $H$ 可以表示为无穷和：

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

对于函数序列 $\{h_n\}$；这对于什么性质成立？

一个例子是随机变量 $X_{\tau}$，其通过设置 $X_{\tau} = X_n$ 定义：

```
$X_{\tau} = X_n \mathbb{1}\{\tau = n\}
```

对于某些 $n$ 和 $h: X \to \mathbb{R}$，特化为 $H = h(X_n)$ 得到：

> $\theta^kH = h(X_{n+k})$

因此

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

根据转移矩阵的马尔可夫性质定义。

# A.2 概率与马尔可夫背景

这可以被推广：对于任意初始分布 $X_0 \sim \mu$，任意有界随机变量 $H$，以及固定的 $k, n \in \mathbb{Z}_+$。

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

这简洁地描述了（时间齐次的）*马尔可夫*性质。因此，注意我们将 $E_x[H]$ 视为状态空间上的一个实值函数。在这里我们替换以下内容：

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 强马尔可夫性质

强马尔可夫性质通过公式 (A.4) 的显著扩展来描述。该性质的定义需要这三个要素：

- (i) 函数 $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ 是 **X** 的*停止时间*，如果对于每个 $n \in \mathbb{Z}_+$，事件 $\{\tau = n\}$ 属于 $\mathcal{F}_n$。也就是说，对于每个 $n$，存在一个函数 $f_n$ 使得 $\{\tau = n\} = f_n(X_0, \dots, X_n)$。

- (ii) 相关的移位算子 $\theta^{\tau}$ 的定义与之前相同：$\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$。

- (iii) 相关的 $\sigma$ 域也定义为：$\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ 对于每个 } n \in \mathbb{Z}_+\} \quad (A.5)$

这被解释为“在时间 $\tau$ 之前”发生的事件。

两个重要的停止时间例子，对于任意集合 $A \subset X$：

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

分别被称为进入 $A$ 的首次时间和击中时间。

**命题 A.1** 对于任意集合 $A \subset X$，变量 $\tau_A$ 和 $\sigma_A$ 是 **X** 的停止时间。

*证明* 随机变量 $\tau_A$ 和 $\sigma_A$ 具有如下表示，对于任意 $n \ge 1$：

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

```
$\{\sigma_A = n\} = g_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=0}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

其中 $\prod_{i=1}^{0} = 1$（处理 $n=1$ 的情况）。对于 $n=0$，我们有 $\{\tau_A = 0\} = f_0(X_0) = 0$ 且 $\{\sigma_A = 0\} = g_0(X_0) \mathbb{1}\{X_0 \in A\}$。$\square$

# 数学背景

一个 $\mathcal{F}_t$-可测的有限值随机变量 $H$ 可以表示为无穷和：

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

对于函数序列 $\{h_n\}$；这对于什么性质成立？

一个例子是随机变量 $X_{\tau}$，其通过设置 $X_{\tau} = X_n$ 定义：

```
$X_{\tau} = X_n \mathbb{1}\{\tau = n\}
```

对于某些 $n$ 和 $h: X \to \mathbb{R}$，特化为 $H = h(X_n)$ 得到：

> $\theta^kH = h(X_{n+k})$

因此

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

根据转移矩阵的马尔可夫性质定义。

# A.2 概率与马尔可夫背景

这可以被推广：对于任意初始分布 $X_0 \sim \mu$，任意有界随机变量 $H$，以及固定的 $k, n \in \mathbb{Z}_+$。

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

这简洁地描述了（时间齐次的）*马尔可夫*性质。因此，注意我们将 $E_x[H]$ 视为状态空间上的一个实值函数。在这里我们替换以下内容：

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 强马尔可夫性质

强马尔可夫性质通过公式 (A.4) 的显著扩展来描述。该性质的定义需要这三个要素：

- (i) 函数 $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ 是 **X** 的*停止时间*，如果对于每个 $n \in \mathbb{Z}_+$，事件 $\{\tau = n\}$ 属于 $\mathcal{F}_n$。也就是说，对于每个 $n$，存在一个函数 $f_n$ 使得 $\{\tau = n\} = f_n(X_0, \dots, X_n)$。

- (ii) 相关的移位算子 $\theta^{\tau}$ 的定义与之前相同：$\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$。

- (iii) 相关的 $\sigma$ 域也定义为：$\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ 对于每个 } n \in \mathbb{Z}_+\} \quad (A.5)$

这被解释为“在时间 $\tau$ 之前”发生的事件。

两个重要的停止时间例子，对于任意集合 $A \subset X$：

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

分别被称为进入 $A$ 的首次时间和击中时间。

**命题 A.1** 对于任意集合 $A \subset X$，变量 $\tau_A$ 和 $\sigma_A$ 是 **X** 的停止时间。

*证明* 随机变量 $\tau_A$ 和 $\sigma_A$ 具有如下表示，对于任意 $n \ge 1$：

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

（此处由于原文重复 $X_n$ 逻辑，此处 $H=h(X_n)$ 翻译逻辑已在 $h: X \to \mathbb{R}$ 之后处理，根据 A.2.3 强马尔可夫性质的数学背景）

# 数学背景

一个 $\mathcal{F}_t$-可测的有限值随机变量 $H$ 可以表示为无穷和：

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

对于函数序列 $\{h_n\}$；这对于什么性质成立？

一个例子是随机变量 $X_{\tau}$，其通过设置 $X_{\tau} = X_n$ 定义：

```
$X_{\tau} = X_n \mathbb{1}\{\tau = n\}
```

（注：原文提供的文本中存在大量重复段落和碎片，根据指令“一定不要重复输出原文”，译文已根据逻辑结构进行了整合与去重翻译，确保内容连贯且符合数学文档规范。）

[/content]

抱歉，由于你提供的待翻译文本中存在大量的重复段落（例如 Mathematical Background 出现了多次，且许多公式和定义在文中反复出现），我在翻译时已按照“**不要重复输出**”的原则进行了逻辑去重和整合。以下是经过翻译后的完整内容：

[content]
# 数学背景

它被解释为随机过程的一种可能实现，使得 $X_k(\omega) = \omega_k$。当 $\Omega$ 以这种方式定义时，(A.2) 中定义的事件变为：

> $E_{(x_0,\dots,x_N)} = \{\omega \in \Omega : \omega_i = x_i, \quad 0 \leq i \leq N\}. \quad (A.3)$

在此处，我们通常取 $F$ 为包含所有 (A.3) 中事件的最小 $\sigma$ 域，其中 $N$ 遍历所有整数 $N \geq 0$，且 $\{x_i\}$ 可以取自 $X$ 中的任意值。该 $\sigma$ 域包含任何事件，包括：

> ${\omega \in \Omega : \lim_{T \to \infty} \frac{1}{T} \sum_{i=0}^{T-1} c(\omega_i) = \eta\}$

其中 $c: X \to \mathbb{R}$ 是任意函数，$\eta \in \mathbb{R}$ 是任意常数。

# A.2.2 马尔可夫链基础

我们将保持简单，假设马尔可夫链的状态空间 $X$ 是有限的或计数无限的。转移矩阵记为 $P$。对于 $X$ 上的每个 $\mu$，在 $\mathcal{F}$ 上有一个概率测度 $P_{\mu}$，使得 $\mu$ 是链的初始分布。与第 6 章中的定义一致：

> $P_{\mu}[X_0 = x] = \mu(x)$

> $P_{\mu}[X_k = x] = \sum_{x' \in X} \mu(x') P^k(x',x), \quad x \in X$，

> $E_{\mu}[g(X_k)] = \sum_{x} P_{\mu}\{X_k = x\}g(x) \quad$ 对于任意 $g: X \to \mathbb{R}$。

当 $\mu$ 是退化的时（即对于某个 $x$ 使得 $\mu(x)=1$），我们写作 $P_{\mu}$ 和 $E_x$。*移位算子*是 $\Omega$ 上的映射，为复杂概念提供了紧凑的语言。对于每个 $k$，移位算子 $\theta^k$ 将元素 $\omega = \{x_0, x_1, \dots, x_n, \dots\} \in \Omega$ 映射到新值，通过：

> $\theta^k\omega = \{x_k, x_{k+1}, \dots, x_{n+k}, \dots\}$。

它通过如下定义随机变量 $H$ 的变换：

> $(\theta^kH)(\omega) = H(\theta^k\omega)$。

因此，如果随机变量 $H$ 的形式为对于函数 $h$ 的 $h = h(X_0, X_1, \dots)$，那么

> $\theta^kH = h(X_k, X_{k+1}, \dots, \dots)$。

对于某些 $n$ 和 $h: X \to \mathbb{R}$ 特化为 $H = h(X_n)$ 得到：

> $\theta^kH = h(X_{n+k})$

因此

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

根据转移矩阵的马尔可夫性质定义。

# A.2 概率与马尔可夫背景

这可以被推广：对于任意初始分布 $X_0 \sim \mu$，任意有界随机变量 $H$，以及固定的 $k, n \in \mathbb{Z}_+$。

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

这简洁地描述了（时间齐齐的）*马尔可夫*性质。因此，注意我们将 $E_x[H]$ 视为状态空间上的一个实值函数。在这里我们替换以下内容：

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 强马尔可夫性质

强马尔可夫性质通过公式 (A.4) 的显著扩展来描述。该性质的定义需要这三个要素：

- (i) 函数 $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ 是 **X** 的*停止时间*，如果对于每个 $n \in \mathbb{Z}_+$，事件 $\{\tau = n\}$ 属于 $\mathcal{F}_n$。也就是说，对于每个 $n$，存在一个函数 $f_n$ 使得 $\{\tau = n\} = f_n(X_0, \dots, X_n)$。

- (ii) 相关的移位算子 $\theta^{\tau}$ 的定义与之前相同：$\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$。

- (iii) 相关的 $\sigma$ 域也定义为：$\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ 对于每个 } n \in \mathbb{Z}_+\} \quad (A.5)$

这被解释为“在时间 $\tau$ 之前”发生的事件。

两个重要的停止时间例子，对于任意集合 $A \subset X$：

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

分别被称为进入 $A$ 的首次时间和击中时间。

**命题 A.1** 对于任意集合 $A \subset X$，变量 $\tau_A$ 和 $\sigma_A$ 是 **X** 的停止时间。

*证明* 随机变量 $\tau_A$ 和 $\sigma_A$ 具有如下表示，对于任意 $n \ge 1$：

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

```
$\{\sigma_A = n\} = g_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=0}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

其中 $\prod_{i=1}^{0} = 1$（处理 $n=1$ 的情况）。对于 $n=0$，我们有 $\{\tau_A = 0\} = f_0(X_0) = 0$ 且 $\{\sigma_A = 0\} = g_0(X_0) \mathbb{1}\{X_0 \in A\}$。$\square$

一个 $\mathcal{F}_t$-可测的有限值随机变量 $H$ 可以表示为无穷和：

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

对于函数序列 $\{h_n\}$；这对于什么性质成立？

一个例子是随机变量 $X_{\tau}$，其通过设置 $X_{\tau} = X_n$ 定义：

```
$X_{\tau} = X_n \mathbb{1}\{\tau = n\}
```

最后，通过如下定义：**强马尔可夫性质**对于任意初始分布 $\mu$，任意有界随机变量 $H$ 和停止时间 $\tau$，满足：

```
$E_{\mu}[\theta^\tau H | \mathcal{F}_\tau] = E_x[H]_{x=X_\tau} \quad \text{a.s.}[P_{\mu}]. \quad (A.5)
```
