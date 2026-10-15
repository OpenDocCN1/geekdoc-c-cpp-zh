
现在我们介绍两个允许合并两个给定的 n-Gmap 以及将给定的 n-Gmap 限制为其 dart 子集的算法。与前面两个算法一样，这些操作作为结果构建一个新的 n-Gmap，在合并的情况下它是两个初始 n-Gmap 的副本，在限制的情况下它是初始 n-Gmap 的部分副本。因此，这两个算法再次使用关联数组来链接原始 dart 和副本。

算法 17 实现两个给定 n-Gmap 的合并操作。此操作总是可能的，因为在我们的数据结构中，两个不同的 n-Gmap 必然有两个不同的 dart 集合，而对于 n-Gmap 的另一种实现可能并非如此。

在新的 n-Gmap 中，我们认为一个标记是自由的，如果它在 n-Gmap `gm` 和 `gm′` 中都是自由的：这解释了第 2 行，它将 `gm″.FreeMarks` 初始化为两个自由标记集合的交集。在关联数组中，我们将每个原始 dart 与其对应的副本关联起来，既针对 `gm` 也针对 `gm′`。在创建所有 dart 之后，我们只需要使新 dart 之间具有与初始 n-Gmap 中原始链接相同的链接。这可以直接通过关联数组完成。

### 算法 17：`mergeNGMaps(gm, gm′)`：合并两个给定的 n-Gmap

```text
Input: gm, gm′: two n-Gmaps.
Output: The n-Gmap obtained by merging gm and gm′.

1  gm″ ← createNGMap(n);
2  gm″.FreeMarks ← gm.FreeMarks ∩ gm′.FreeMarks;
3  assoc ← an empty associative array between darts;
4  foreach dart d ∈ gm.Darts ∪ gm′.Darts do
5      assoc[d] ← createDartNGMap(gm″);
6  foreach dart d ∈ gm.Darts ∪ gm′.Darts do
7      d′ ← assoc[d];
8      for i ← 0 to n do
9          d′.Alphas[i] ← assoc[d.Alphas[i]];
10     for i ← 0 to NB_MARKS − 1 do
11         d′.Marks[i] ← d.Marks[i];
12 return gm″;
```

算法 18 实现将 n-Gmap 限制为给定 dart 子集的操作。如第 89 页定义 16 所见，此操作只有在 dart 子集对应于一组连通分量的情况下才可能。因此我们首先测试该属性是否满足，并在满足时才构建受限的 n-Gmap。注意，我们可以提出不同的变体，例如使用与不属于 D′ 的 dart 链接的所有非自由 dart，或不进行测试而假设用户始终给出连通分量集合的不安全版本……

合并操作的复杂度与两个给定 n-Gmap 的 dart 数（`#d₁` 和 `#d₂`）成线性关系，再乘以在关联数组中访问元素的复杂度，即 `O((#d₁ + #d₂) · log(#d₁ + #d₂))`。限制操作的复杂度与 `D′` 中的 dart 数成线性关系，乘以 `log |D′|`（这对应于复制的成本），加上初始测试的成本（检查 dart 子集是否对应于一组连通分量：第 1-3 行）。如果 `D′` 是一个搜索元素需要 log 时间的容器，则测试复杂度为 `O(|D′| · log |D′|)`。然而该测试可以通过首先标记 `D′` 中的所有 dart，然后遍历所有 dart 并仅验证每个 dart `d` 的 `αᵢ(d)` 是否被标记，从而在 `O(|D′|)` 中完成。因此算法 18 的整体复杂度为 `O(|D′| · log |D′|)`。

### 4.4.4 Sew/Unsew 操作

现在我们介绍 i-sew 操作及其逆操作 i-unsew。如第 4.2.2 节在介绍 sew 操作时所见，并非总是可以 i-sew 两个 dart：它们必须是 i-sewable。算法 19 允许测试两个给定 dart 是否为 i-sewable。该算法直接遵循第 90 页定义 18 给出的 i-sewable 定义。其主要原理是同时遍历两个轨道 `o_d` 和 `o_d′`，在测试其确实为同构的同时逐步构建同构。

首先在第 1 行，我们验证 `d ≠ d′` 且 `d` 和 `d′` 是 i-自由的。如果不是，则两个 dart 不是 i-sewable。其次我们创建两个通用迭代器，对应于两个轨道 `o_d = ⟨α₀, …, αᵢ₋₂, αᵢ₊₁, …, αₙ⟩(d)`

算法18：`restrictNGMap(gm, D')`：将n-Gmap限制到darts的一个子集

输入：`gm`：一个n-Gmap；

       `D' ⊆ gm.Darts`：darts的一个子集。

输出：将`gm`限制到`D'`后得到的n-Gmap。

1 foreach dart d ∈ D' do

2   for i ← 0 to n do

3     if d.Alphas[i] ∉ D' then error;

4 gm' ← createNGMap(n);

5 gm'.FreeMarks ← gm.FreeMarks;

6 assoc ← an empty associative array between darts;

7 foreach dart d ∈ D' do

8   assoc[d] ← createDartNGMap(gm');

9 foreach dart d ∈ D' do

10  d' ← assoc[d];

11  for i ← 0 to n do

12    d'.Alphas[i] ← assoc[d.Alphas[i]];

13  for i ← 0 to NB_MARKS − 1 do

14    d'.Marks[i] ← d.Marks[i];

15 return gm';

算法19：`sewableNGMap(gm,d,d′,i)`：测试两个darts对于n-Gmaps是否i-可缝合

输入：`gm`：一个n-Gmap；

        `d, d′ ∈ gm.Darts`：两个darts；

        `i ∈ {0,…,n}`。

输出：当且仅当`d`与`d′`是i-可缝合的，返回True。

1 if d = d′ or not isFreeNGMap(d,i) or not isFreeNGMap(d′,i) then

2   return false;

3 it ← generic iterator(gm,d,(0,…,i−2,i+2,…,n));

4 it′ ← generic iterator(gm,d′,(0,…,i−2,i+2,…,n));

5 f ← an empty associative array between darts;

6 while it is not to its end and it′ is not to its end do

7   f[it] ← it′;

8   foreach j ∈ {0,…,i−2,i+2,…,n} do

9     if it.Alphas[j] is defined in f and

10    f[it.Alphas[j]] ≠ it′.Alphas[j] then

11      return false;

12   advance it to its next position;

13   advance it′ to its next position;

14 if it is not to its end or it′ is not to its end then

15   return false;

16 return true;

且 `$o_{d'} = \langle \alpha_0,\ldots,\alpha_{i-2},\alpha_{i+2},\ldots,\alpha_n\rangle(d')$`。在主循环中，对于`it`和`it’`所指向的每一对darts，我们考虑`it`邻域中已经被考虑过的所有darts。确实，我们已经通过关联数组`f`在这些darts之间建立了同构，并且需要测试`i`-可缝合操作的局部性质是否满足（即 `f(α_j(it)) = α_j(it')`，其中 `f(it) = it'`）。如果不满足，我们直接返回`false`，因为知道两个darts `d`和`d'`不是`i`-可缝合的。否则我们继续主循环，直到至少一个迭代器结束。如果只有一个迭代器结束，则这两个darts不是`i`-可缝合的（两个轨道没有相同数量的darts）；否则，它们是`i`-可缝合的，我们返回`true`。

`i`-可缝合算法的复杂度为：`o_d`和`o_{d'}`两者中较小轨道中darts数量`#d`乘以`log #d`的线性时间。实际上，我们只要一个迭代器到达其结束位置就停止主循环，除了对关联数组中元素的访问是对数时间外，所有操作都是原子性的，而内层循环（第8行）以常数`n`为界。

`i`-缝合操作在算法20中给出，其中`i ∈ {0,…,n}`。该算法直接遵循`i`-缝合操作的定义（见第91页的定义19）。主循环遍历两个轨道 `o_d = ⟨α₀,…,αᵢ₋₂,αᵢ₊₂,…,αₙ⟩(d)` 和 `o_{d'} = ⟨α₀,…,αᵢ₋₂,αᵢ₊₂,…,αₙ⟩(d')`，并通过`α_i`将所有darts对关联起来。

**算法20：** `sewNGMap(gm,d,d’,i)`：为`n`-Gmaps执行两个darts的i-缝合

**输入：** `gm`：一个`n`-Gmap；

`d,d' ∈` `gm.Darts`：两个i-可缝合的darts；

`i ∈ {0,…,n}`。

**结果：** 缝合darts `d`和`d’`。

1  it ← generic iterator(gm,d,(0,...,i−2,i+2,...,n));

2  it’ ← generic iterator(gm,d’,(0,...,i−2,i+2,...,n));

3  while it is not to its end do

4      it.Alphas[i] ← it’;

5      it’.Alphas[i] ← it;

6      advance it to its next position;

7      advance it’ to its next position;

该算法的关键在于再次使用两个泛型迭代器 `(\mathrm{gm},d,(0,\ldots,i-2,i+2,\ldots,n))` 和 `(\mathrm{gm},d',(0,\ldots,i-2,i+2,\ldots,n))`，通过相同的`α`链接遍历两个轨道。由于我们知道`d`和`d'`是`i`-可缝合的，并且由于泛型迭代器按相同顺序使用序列中给定的索引，因此在`while`循环的每一步，两个迭代器都指向由定义19的同构`f`关联的两个darts。因此，我们只需将两个被指向的darts通过`α_i`关联起来，然后将两个迭代器移动到它们各自的下一个位置。注意，由于`α_i`是一个对合，这种关联是双向的。当两个迭代器到达其结束位置时，算法结束。

该算法的复杂度与轨道`⟨α₀, …, αᵢ₋₂, αᵢ₊₂, …, αₙ⟩(d)`中的darts数量成线性关系。

i-解缝操作在算法21中给出，其中`i ∈ {0, …, n}`。与i-缝合算法一样，它直接遵循i-解缝的定义（见第96页的定义20）。它遍历轨道`⟨α₀, …, αᵢ₋₂, αᵢ₊₂, …, αₙ⟩(d)`中的所有darts，并将dart `αᵢ(e)`与自身i-链接，将dart `e`与自身链接。

# 算法21：`unsewNGMap(gm,d,i)`：为n-Gmaps解缝两个darts

输入：`gm`：一个n-Gmap；

    `d ∈ gm.Darts`：一个非i-自由的dart；

    `i ∈ {0, …, n}`。

结果：解缝darts `d`和`αᵢ(d)`。

1 foreach dart e ∈ ⟨α₀, …, αᵢ₋₂, αᵢ₊₂, …, αₙ⟩(d) do

2   (e.Alphas[i]).Alphas[i] ← e.Alphas[i];

3   e.Alphas[i] ← e;

解缝算法的复杂度与所遍历轨道`⟨α₀, …, αᵢ₋₂, αᵢ₊₂, …, αₙ⟩(d)`中的darts数量成线性关系。

### 4.5 补充内容

本节提供一些补充定义：边界映射、对偶性、可定向性，最后给出2-Gmaps的分类，这与曲面的分类相对应。

注意，与这些新概念对应的算法没有给出，但推导出来并不复杂。对于边界映射和对偶映射，其原理与复制n-Gmap类似，只是根据定义修改α链接。

### 4.5.1 边界映射

在许多应用中，n-Gmaps的所有对合（除αₙ外）都没有不动点，即不存在dart `d`使得`αᵢ(d) = d`（其中`i < n`）。因此，每个n-cell的边界对应于一个无边界的(n − 1)-准流形，但对应于n-Gmap的n维准流形可以具有边界，这些边界对应于边界的(n − 1)-Gmap的连通分量。

考虑一个除维度n外没有边界的n-Gmap G。`G∂`是`G`的边界的(n − 1)-Gmap：因此它对应于一个无边界的(n − 1)-准流形。它通过保留`G`的所有n-自由darts以及所有`α_i`（∀`i ∈ {0, …, n−2}`）来定义。`α'_{n−1}`通过如下方式定义：对于每个n-自由dart，沿着darts路径`α_{n−1} ∘ (α_n ∘ α_{n−1})^k`跳过不属于边界的darts，直到获得一个n-自由dart。对于`n = 1`或`n = 2`，`G_∂`的任何分量都表示`G`的一个边界（参见图4.20中的2D示例）。对于`n ≥ 3`，`G_∂`的任何分量表示一个(n−1)-准流形，它覆盖`G`的一个边界。

边界概念在定义21中被推广，以便为任意n-Gmap定义i-边界映射。给定一个n-Gmap G，i-边界映射`G_{∂_i}`是一个覆盖`G`的不同i-边界的n-Gmap。更精确地说，`G`的不同i-边界与`G_{∂_i}`的连通分量之间存在一一对应。

# 定义21（i-边界映射） 设`G = (D, α_0, …, α_n)`是一个n-Gmap，且`i ∈ {0, …, n}`。i-边界映射`G_{∂_i} = (D', α'_0, …, α'_n)`是如下定义的n-Gmap：

+   1. `D' = {d ∈ D | d是i-自由的}`；

+   2. ∀`d' ∈ D'`：

+      • ∀`j ∈ {0, …, i−2, i+2, …, n}`，`α'_j(d') = α_j(d')`；

+      • `α'_{i+1}(d') = d'`；`α'_{i+1}(d') = d'`；

+      • `α'_{i−1}(d') = α_{i−1} ∘ (α_i ∘ α_{i−1})^k(d')`

+        `k`是使得`α_{i−1} ∘ (α_i ∘ α_{i−1})^k(d')`为i-自由的最小整数。

注意，`α'_{i−1}(d')`的定义有两种可能情况。第一种情况是，在沿着dart路径`α_{i−1}∘(α_i∘α_{i−1})^k(d')`前进时，到达一个i-自由dart `d'' ≠ d'`。在这种情况下，`α'_{i−1}(d') = d''`。第二种情况是，在沿着路径`α_{i−1}∘(α_i∘α_{i−1})^k(d')`前进时，到达一个(i−1)-自由dart。在这种情况下，路径继续前进，直到获得`d'`，它是路径中第一个i-自由dart，且`α'_{i−1}(d') = d'`。另外注意，根据定义，i-边界映射中的所有darts都是i-自由且(i+1)-自由的。

还要注意，广义的i-边界映射与初始n-Gmap具有相同的维度。对于`i < n`，这是必需的，以便在闭包操作（参见第185页第6.1节）期间将初始n-Gmap的darts与i-边界映射的darts正确关联。然而，对于`i = n`则不需要，因为没有高于i的维度。

当除`α_n`外的所有对合都没有不动点时，这个广义的i-边界映射定义可用于重新获得n-Gmap G的经典边界。首先计算`G_{∂_n}`，然后降低其维度（根据定义，`G_{∂_n}`中的每个dart `d`都满足`α_n(d) = d`），从而产生`G_∂`。

# 定义22（边界映射） 设`G`是一个除了可能在维度n处有边界外无其他边界的n-Gmap。边界的(n−1)-Gmap为`G_∂ = G^{−}_{∂_n}`。

![](img/6ba3cf72cbe3568e76a174448323bb33_147_0.png)

# FIGURE 4.20

(a) 2-Gmap G with 2-boundary.

(b) The corresponding 2-boundary map `G∂₂ = (D′, α₀′, α₁′, α₂′ = Id_D)`. 1-Gmap `G∂ = G∂₂̄ = (D′, α₀′, α₁′)` corresponds to a closed curve, i.e. to the boundary of the surface represented by G.

图 4.20 给出了一个具有 2-边界的 2-Gmap 及其对应的 2-边界映射的示例。图 4.21 中给出了第二个示例，展示了一个具有 3-边界的 3-Gmap 及其对应的 3-边界映射。注意在两种情况下，我们都通过降低其维度得到边界的 (n − 1)-Gmap。图 4.22 中给出的第三个示例展示了一种我们为定义 `α′_{i−1}(d′)` 而得到 `d′` 的情况（针对 darts 1、6、12 和 15）。

图 4.23 展示了图 4.22(a) 中给出的 2-Gmap 的 1-边界映射（该映射具有 1-边界和 2-边界），图 4.24 给出了 3-Gmap 的 1-边界映射的示例。

给定一个具有 i-边界的 n-Gmap G，则可以“填充”所有 i-边界，将 n-Gmap 与其 i-边界映射 `G∂ᵢ` 的一个拷贝链接起来。更精确地说，`G` 中属于边界的每个 dart 都通过 `αᵢ` 与 `G∂ᵢ` 拷贝中对应的 dart 链接：这产生了第 6.1 节中详细描述的 n-Gmap 的 i-闭包。

### 4.5.2 Duality
