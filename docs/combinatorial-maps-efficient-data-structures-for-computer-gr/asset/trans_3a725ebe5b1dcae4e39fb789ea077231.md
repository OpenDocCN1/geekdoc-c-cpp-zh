

$i$-边界映射的允许关闭一个边界，通过将其 darts 与 $n$-Gmap 或 $n$-map 的对应 $i$-自由 darts 识别。

## 6.1.1 对于 $n$-Gmaps

$i$-闭合操作对于 $n$-Gmap $G$ 在 Def. 55 中定义。它包括为 $G$ 中的每个 $i$-自由 dart 创建新的 darts。然后，新 darts 通过 $\alpha_j$，$\forall j \in \{0, \ldots, n\}$，$j \ne i$ 相互链接，使用 $i$-边界映射 $G_{\partial i}$ 中的对应链接（参见 Def. 21 后 124）；每个新 dart 通过 $\alpha_i$ 与其对应的 dart 在 $G$ 中链接。

> **Definition 55** *(i-closure)*  设 $G = (D, \alpha_0, \ldots, \alpha_n)$ 为 $n$-Gmap，$i \in \{0, \ldots, n\}$，且 $G_{\partial i} = (D', \alpha'_0, \ldots, \alpha'_n)$ 为对应的 $i$-边界映射。$G$ 的 $i$-闭合是 $n$-Gmap $G_{i\text{-close}} = (D'', \alpha''_0, \ldots, \alpha''_n)$ 定义为：

- 1. $D'' = D \cup \{d''_1, \ldots, d''_{|D'|}\}$，其中 $\{d''_1, \ldots, d''_{|D'|}\}$ 是一组新的 darts，使得双射 $f$ 将 $D'$ 映射到 $\{d''_1, \ldots, d''_{|D'|}\}$。
- 2. $\forall j \in \{0, \ldots, n\}$ s.t. $j \ne i$:
  - $\forall d \in D$, $\alpha''_j(d) = \alpha_j(d)$;
  - $\forall d' \in D'$, $\alpha''_j(f(d')) = f(\alpha'_j(d'))$.
- 3. $\forall d \in D \setminus D'$, $\alpha''_i(d) = \alpha_i(d)$;
- 4. $\forall d' \in D'$, $\alpha''_i(d') = f(d)$, $\alpha''_i(f(d)) = d$.

$D'' \setminus D$（即新的 darts）与 $D'$（即 $G$ 的 $i$-边界的 darts）之间的链接是通过双射 $f$ 定义的。注意，两个 darts 集合之间可以考虑任意双射，因为新 darts 的顺序无关紧要。还要注意 $D' \subseteq D$，根据边界映射的定义：这解释了为什么新 darts 被添加到 $D$ 并与 $D'$ 链接。

1-闭合操作在图 6.1 中说明。从 (a) 中所示的具有边界的 1-Gmap 开始，通过应用 1-闭合操作得到 (b) 中所示的 1-Gmap；注意该 1-Gmap 没有边界。在初始 1-Gmap 中，有两个 1-自由 darts（编号为 1 和 6）；因此创建了两个新的 darts（编号为 7 和 8）；此外，$f(6)$（分别 $f(1)$）任意设为 7（分别 8）。由于 darts 1 和 6 在 1-边界映射 $G_{\partial 1}$ 中是 0-缝合的，对应的 darts 7 和 8 在 $G_{1\text{-close}}$ 中也是 0-缝合的：$\alpha''_1(1)=8$（分别 $\alpha''_1(6)=7$），因为 $f(1)=8$（分别 $f(6)=7$）。

1-闭合操作的另一个例子在图 6.2 中给出；它在此应用于 3-Gmap。在此示例中，四个 darts，即 1、6、7 和 12，是 1-自由 darts；因此创建了四个新的 darts，编号为 13、14、15 和 16，并分别通过双射 $f$ 与 1、6、7 和 12 关联。由于 darts 1 和 6 在 1-边界映射 $G_{\partial 1}$ 中是 0-缝合的，对应的 darts 13 和 14 在 $G_{1\text{-close}}$ 中也是 0-缝合的（darts 7 和 12 及其对应的 darts 15 和 16 也是如此）。此外，由于 6 和 12 在

## FIGURE 6.1

1-closure for 1-Gmap.
(a) A 1-Gmap G with 1-boundary.
(b) The 1-Gmap G₁-close. 7 and 8 are new darts, such that f(6) = 7 and f(1) = 8.

## FIGURE 6.2

1-closure for 3-Gmap.
(a) A 3-Gmap G with 1-boundary, 2-boundary and 3-boundary. The four darts 1, 6, 7 and 12 are 1-free.
(b) The 3-Gmap G₁-close. Dart 13, 14, 15 and 16 are new darts, respectively associated with darts 1, 6, 7 and 12.

![](img/6ba3cf72cbe3568e76a174448323bb33_210_0.png)

## FIGURE 6.3

2-closure for 2-Gmap.

(a) A 2-Gmap $G$ with 2-boundary. Darts 5, 6, 7, 8, 13, 14, 15, 16, 17, 18, 23, 24 are 2-free.

(b) The 2-Gmap $G_{2\text{-close}}$. New darts are numbered from 25 to 36.

1-边界映射 $G_{\partial_1}$ 中是 3-缝合的，14 和 16 在 $G_1$-close 中也是 3-缝合的（1 和 7 及其对应的 darts 13 和 15 也是如此）。$\alpha''_1(1)=f(1)=13$（分别 $\alpha''_1(6)=14$，$\alpha''_1(7)=15$ 和 $\alpha''_1(12)=16$）。

图 6.3 中给出了 2-Gmap 中 2-闭合操作的示例。从 (a) 中描绘的具有 2-边界的 2-Gmap 开始，通过应用 2-闭合操作得到的 (b) 中所示的 2-Gmap 不再有 2-边界。在此示例中，有十二个 2-自由 darts，因此创建了十二个编号从 25 到 36 的新 darts。这些新 darts 通过 $\alpha''_2$ 与其对应的 darts 链接。此外，这些新 darts 通过对合 $\alpha''_0$ 和 $\alpha''_1$ 链接，根据 2-边界映射 $G_{\partial_2}$ 的对应对合。

我们可以在图 6.4 中看到一个具有 1-边界和 2-边界的 2-Gmap。在这种情况下，2-闭合操作产生一个没有 2-边界的 2-Gmap，但它仍然具有 1-边界。

得益于 $i$-闭合定义，很容易定义一个 *闭合操作* 来消除所有维度中的所有边界。为此，依次应用所有可能的 $i$-闭合操作，从 $i=0$ 到 $i=n$。例如，从图 6.2(a) 中给出的 3-Gmap 开始（它没有 0-边界），并应用 1-闭合操作，得到图 6.2(b) 中所示的 3-Gmap：该 3-Gmap 没有 1-边界。然后应用 2-闭合操作，产生图 6.5(a) 中给出的 3-Gmap，它没有 2-边界。最后，应用 3-闭合操作，产生图 6.5(b) 中的 3-Gmap，它没有 3-边界，因此完全没有边界。

算法 47 实现了 $n$-Gmaps 的 $i$-闭合操作。该算法直接遵循 $i$-闭合定义（参见 Def. 55）。注意

## FIGURE 6.4

2-closure for 2-Gmap.

(a) A 2-Gmap G with 1-boundaries and 2-boundaries.

(b) The 2-Gmap G₂-close. New darts are numbered from 25 to 32. This 2-Gmap has no 2-boundary, but it still has 1-boundaries.

![](img/6ba3cf72cbe3568e76a174448323bb33_211_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_211_1.png)

## FIGURE 6.5

Closure for 3-Gmap.

(a) The 3-Gmap G' obtained from Fig. 6.2(b) by applying the 2-closure operation. Darts 17 to 32 are new darts.

(b) The 3-Gmap G'₃-close. The eighty black darts are new darts, describing the external volume enclosing the two initial cubes.

![](img/6ba3cf72cbe3568e76a174448323bb33_211_2.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_211_3.png)

$i$-边界映射并未显式计算；尽管如此，新 darts 是根据其定义链接的。

```
**Algorithm 47:** `closeNGMap(gm,i)`: i-close an $n$-Gmap

**Input:** `gm`: an $n$-Gmap;  
$i \in \{0,\ldots,n\}$.

**Result:** `gm` is i-closed.

```text
1  foreach i-free dart d ∈ gm.Darts do
2      d′ ← createDartNGMap(gm);
3      d′.Alphas[i] ← d; d.Alphas[i] ← d′;
4      foreach j ∈ {0, …, i − 2, i + 2, …, n} do
5          d″ ← d.Alphas[j];
6          if not isFreeNGMap(d,j) and not isFreeNGMap(d″,i) then
7              d′.Alphas[j] ← d″.Alphas[i];
8              d″.Alphas[i].Alphas[j] ← d′;
9      if i > 0 then
10         d″ ← d.Alphas[i − 1];
11         while not isFreeNGMap(d″,i) and not
           isFreeNGMap(d″.Alphas[i],i − 1) do
12             d″ ← d″.Alphas[i].Alphas[i − 1];
13         if not isFreeNGMap(d″,i) then
14             d′.Alphas[i − 1] ← d″.Alphas[i];
15             d″.Alphas[i].Alphas[i − 1] ← d′;
```
```

在此算法中，新 darts 被创建并通过 $\alpha_i$ 与对应的 $i$-自由 darts 链接。这对应于 $i$-闭合定义的第 4 项。然后，其他 $\alpha$ 链接根据边界映射的定义确定。$\alpha_{i+1}$ 对于所有新 darts 初始化为恒等式（$i$-边界映射定义的第二项）：这是 `createDartNGMap` 函数的结果。

对于所有 $j \in \{0,\ldots,i-2,i+2,\ldots,n\}$，$\alpha_j$ 是从 $i$-自由 dart $d$ 上的 $\alpha_j$ 定义推导出来的。确实，$\alpha_i \circ \alpha_j$ 是一个对合。由于 $\alpha_i(d)=d'$ 且 $\alpha_i(d)=d''$，必须有 $\alpha_i(d')=\alpha_j(d'')$；因为 $d'=f(d)$ 且 $\alpha_i(d'')$ 等价于 $\alpha_j''(f(d))=f(\alpha_j'(d))$：这对应于 $i$-闭合定义的第 2 项（记住，在此算法中，$\alpha_i$ 也代表 $\alpha_i'$ 和 $\alpha_i''$）。

注意 $\alpha_j$ 只能在 $d$ 不是 $j$-自由且 $d''$ 不是 $j$-自由时定义。确实，如果 $d$ 是 $j$-自由，则 $d'$ 也必须是 $j$-自由；因此，无需操作，因为 darts 在所有维度中创建时都是自由的。如果 $d''$ 是 $i$-自由，则 $d'$ 与 $\alpha_i(d'')$ 之间的 $\alpha_j$ 链接尚无法定义：与 $\alpha_j(d)$ 关联的新 dart 尚未创建。此定义将在算法的未来步骤中完成，当处理 dart $\alpha_j(d)$ 时。确实，将有可能定义

