

## 46 计算的极限

在本书中，我们始终假设 $f$ 和 $g$ 是定义在正整数上的正值非递减函数。

## 定义 3.5 重述

对于定义在正整数上的正值函数 $f$ 和 $g$，如果存在一个正整数 $C$，使得对于所有正整数 $n$，都有 $f(n) \le C g(n)$，则 $f$ 是 $O(g)$。

有时将 $O(g)$ 视为一个集合非常方便，我们可以说 $f \in O(g)$ 而不是 $f$ 是 $O(g)$。有些作者会说 $O(f) = g$，但最好避免这种写法。$f \in O(g)$ 与 $f$ 是 $O(g)$ 之间的区别很少引起问题。

## 3.9 有用的定理

以下两个定理对于证明一个函数是另一个函数的 $O$ 很有用。直接极限通常没用，因为任何描述算法阶数的函数都是递增的、正的且趋于无穷大的。

这是一个应用洛必达法则（l'Hospital's rule）的标准案例。

### 定理 3.6

如果 $f$ 和 $g$ 是正函数，

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = C$$

对于某个正数 $C$，则 $f$ 是 $O(g)$。

### 证明

这是对极限定义的简单应用。如果

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = C$$

那么存在一个 $N$，使得：

$$n \ge N, \frac{f(n)}{g(n)} \le C+1$$

### 定理 3.7 (洛必达法则)

如果

$$\lim_{x\to\infty} \frac{f(x)}{g(x)}$$

是一个如下形式的未极限：

$$\begin{pmatrix} \infty \\ \infty \end{pmatrix} (\text{或 } \begin{pmatrix} 0 \\ 0 \end{pmatrix})$$

则

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = \lim_{x\to\infty} \frac{f'(x)}{g'(x)}$$

其中 $f'$ 是 $f$ 对 $x$ 的导数。

### 证明

参考任何标准微积分教材。l'Hospital 这个名字也写成 Lospital 或 L'Hôpital。在任何情况下，$s$ 都不发音。

简单应用：$n \ln n$ 是 $O(n^2)$。当 $n$ 很大时，$(n \ln n)$ 和 $n^2$ 都会变得非常大（趋于无穷）——算法中计算步骤的所有函数也是。通过使用洛必达法则，我们得到：

$$\lim_{x\to\infty} \frac{n\ln n}{n^2} = \lim_{x\to\infty} \frac{\ln n}{n} = \lim_{x\to\infty} \frac{1/n}{1} = \lim_{x\to\infty} \frac{1}{n} = 0$$

## 48 计算的极限

## 3.10 O 表示法的性质

以下性质很有用；且都易于证明。

- 对于所有 $f$，$f$ 是 $O(f)$。
- $f$ 是 $O(1)$ 当且仅当它是一个有界函数。
- 在任何 $O$ 计算中都可以忽略常数因子；即对于任何正常数 $K$Kf(n)$ 是 $O(f(n))$。
- 对于任何基数 $a$ 和 $b (b > 1)$，$\log_a$ 是 $O(\log_b n)$。
- 对于任何基数 $b (b > 1)$，log_b n$ 是 $O(n)$。
- 对于所有 $b > 1, k \ge 0$n^k$ 是 $O(b^n)$。因此 $n^5$ 和 $n^{51}$ 都是 $O(2^n)$。
- 如果 $r \le s$，则 $n'$ 是 $O(s')$。
- 任何多项式 $p(n)$ 都是 $O(p \text{ 中的最高阶项})$。（因此 $7n^5 + 11n^2 + 5n + 1111$ 是 $O(n^5)$）。

- 对于所有 $k > 0, k$ 是 $O(f)$。
- 当且仅当 $f$ 是 $O(g)$ 且 $h$ 是 $O(g)$ 时，$f + h$ 是 $O(g)$。
- 如果 $f$ 是 $O(h)$ 且 $g$ 是 $O(h)$，则 $f + g$ 是 $O(h)$。
- 如果 $f$ 是 $O(h_1)$ 且 $g$ 是 $O(h_2)$，则 $f + g$ 是 $O(\max(h_1, h_2))$。
- 如果 $f$ 是 $O(h_1)$ 且 $g$ 是 $O(h_2)$，以此此类推。

## 3.11 寻找 O：分析算法

分析算法涉及假设。两点说明：(1) 通常一样，我们不关心最好情况，且 (2) 如果算法是一个搜索决策问题。

### 示例：列表是否包含某个特定元素？

```
Algorithm: (1) element = false
(2) for each element in list
(3) if element == key
    element = true
(4) return element
```

### 示例：最大公约数 (GCD)

```
Algorithm: (1) while m != 0
  (2) r = n mod m
  (3) n = m
  (4) m = r
(5) return n
```

