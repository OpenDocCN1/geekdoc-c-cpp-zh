

### 算法 60: `isInsertableNGMap(gm, c, i, assoc)`: 测试 i-单元是否可插入 n-Gmaps

**输入：** gm, c: 两个 *n*-Gmaps;

i ∈ {0, ..., n};

assoc: 一个从 c.Darts 到 gm.Darts 的映射。

**输出：** 当且仅当 c 可以根据 assoc 插入到 gm 中时为 True。

```text
1  if c contains more than one i-cell then return false;
2  if the i-cell in c is not removable then return false;
3  assoc⁻¹ ← an associative array between darts, inverse of assoc;
4  foreach dart d ∈ assoc do
5      if not isFreeNGMap(d, i) then return false;
6      d′ ← assoc[d];
7      foreach j ∈ {0, ..., i − 2, i + 2, ..., n} do
8          if d.Alphas[j] ∈ assoc and
              assoc[d.Alphas[j]] ≠ assoc[d].Alphas[j] then
9              return false;
10         if d′.Alphas[j] ∈ assoc⁻¹ and
                assoc⁻¹[d′.Alphas[j]] ≠ assoc⁻¹[d′].Alphas[j] then
11             return false;
12     d₂ ← d.Alphas[i + 1];
13     while d₂ ∉ assoc do
14         d₂ ← d₂.Alphas[i].Alphas[i + 1];
15     if assoc[d₂] ≠ d′.Alphas[i] then return false;
16 return true;
```

映射 assoc，对应于 Def. 68 中的 γ，以关联数组的形式实现（例如哈希表或二叉搜索树），从 c.Darts 到 gm.Darts。测试一个 dart d 是否属于 assoc 等价于在可插入性条件定义中测试 d 是否属于 BV′。assoc⁻¹ 由 assoc 计算得到（assoc⁻¹ 对应于 γ⁻¹），并存储在第二个关联数组中。它允许测试给定的 dart d 是否属于 BV。请注意，根据 assoc 和 assoc⁻¹ 的定义，遍历 assoc 的 darts（因此是 BV′）并考虑 d′ ← assoc[d] 等价于遍历 assoc⁻¹ 的 darts（因此是 BV）。

i-插入操作由算法 61 实现。不是构建新的 n-Gmap Gi(C, γ)，n-Gmap gm 被修改以获得与 Gi(C, γ) 同构的 n-Gmap。因此，只有 assoc 和 assoc⁻¹ 的 darts 的 Alphas[i] 链接需要被修改。

### 算法 61: `insertNGMap(gm, c, i, assoc)`: 在 n-Gmap 中插入一个 i-单元

输入：gm: 一个 n-Gmap;

c: 一个 n-Gmap，根据 assoc 是可插入的 i-单元;

i ∈ {0, …, n};

assoc: 一个从 c.Darts 到 gm.Darts 的映射。

结果：沿 assoc 将 i-单元 c 插入到 gm 中。

```text
1 foreach dart d′ ∈ c.Darts do
2   add d′ in gm.Darts;
3   remove d′ from c.Darts;
4   if d′ ∈ assoc then
5     d′.Alphas[i] ← assoc[d′];
6     assoc[d′].Alphas[i] ← d′;
```

算法 60 的复杂度为 n-Gmap c 的 darts 数 #d 与在关联数组中访问元素的复杂度 log #d 的线性乘积。事实上，可以在线性时间内遍历 i-单元 c，以测试 c 是否包含多于一个 i-单元。然后，可以再次在线性时间内测试该 i-单元是否可移除。assoc 中的元素数受限于 c 中的 darts 数，因此每次在 assoc 或 assoc⁻¹ 中的访问都在 log #d 内。最后，沿路径 (α′i+1 ◦ α′i) k ◦ α′i+1 ◦ γ⁻¹(d) 的循环的复杂度受限于 c 中的 darts 数，因为所考虑的路径是不相交的。这给出了算法的全局复杂度。

算法 61 的复杂度也在 n-Gmap c 的 darts 数 #d 与 log #d 的线性乘积中。这是显而易见的，因为 c 中的所有 darts 都被处理，使用由 assoc 描述的链接。

![](img/6ba3cf72cbe3568e76a174448323bb33_252_0.png)

**图 6.38**

四个操作之间的链接：移除、收缩、插入和扩展。

## 6.5 扩展

扩展操作是收缩操作的逆操作。它在现有的给定 (i − 1)-单元内部添加一个新的 i-单元，可能将该 (i − 1)-单元切分为两个。如前所述，扩展操作在这里仅针对 n-Gmaps 定义；对于 n-maps 的转换可以在没有特殊困难的情况下完成。

图 6.38 总结了四个操作之间的链接：移除、收缩、插入和扩展。

可扩展性条件和扩展操作，定义在 Defs. 70 和 71 中，直接由可插入性条件和插入操作通过对偶性推导得出（即 i + 1 被 i − 1 替换）。

### 定义 70（可扩展单元）

设 G = (D, α₀, …, αₙ) 和 C = (D′, α₀′, …, αₙ′) 为两个 n-Gmaps，i ∈ {0, …, n}，且 γ 是从 BV′ ⊆ D′ 到 BV ⊆ D 的双射。C 根据 γ 可 i-扩展到 G 当且仅当：

- C 恰好包含一个可收缩的 i-单元；
- ∀d′ ∈ BV′, d′ 是 i-自由的；
- ∀j ∈ {0, …, n} s.t. |i − j| ≥ 2:
  - ∀d ∈ BV s.t. αⱼ(d) ∈ BV, γ⁻¹ ∘ αⱼ(d) = αⱼ′ ∘ γ⁻¹(d);
  - ∀d′ ∈ BV′ s.t. αⱼ′(d′) ∈ BV′, γ ∘ αⱼ′(d′) = αⱼ ∘ γ(d′);
- ∀d ∈ BV, αᵢ(d) = γ ∘ (α′ᵢ₋₁ ∘ α′ᵢ)ᵏ ∘ α′ᵢ₋₁ ∘ γ⁻¹(d)，k 为使 (α′ᵢ₋₁ ∘ α′ᵢ)ᵏ ∘ α′ᵢ₋₁ ∘ γ⁻¹(d) ∈ BV′ 成立的最小正整数。

### 定义 71（扩展）

设 G = (D, α₀, …, αₙ) 和 C = (D′, α₀′, …, αₙ′) 为两个 n-Gmaps，BV ⊆ D，BV′ ⊆ D′，γ 是从 BV′ 到 BV 的双射，使得 C 根据 γ 是一个可扩展的 i-单元。C 在 G 中 i-扩展的结果 n-Gmap 为 G_Ei(C, γ) = (D″, α₀″, …, αₙ″)，定义为：

- D″ = D ∪ D′;
- ∀ j ∈ {0, …, n}, j ≠ i:
  - ∀ d ∈ D, α″_j(d) = α_j(d); ∀ d′ ∈ D′, α″_j(d′) = α′_j(d′);
- ∀ d ∈ D \ BV, α″_i(d) = α_i(d); ∀ d′ ∈ D′ \ BV′, α″_i(d′) = α′_i(d′);
- ∀ d ∈ BV, α″_i(d) = γ⁻¹(d); ∀ d′ ∈ BV′, α″_i(d′) = γ(d′).

请注意，i-扩展操作的定义与 i-插入操作的定义相同，唯一的区别在于考虑的是可扩展的 i-单元而不是可插入的 i-单元。

由于扩展操作是收缩操作的逆操作，第 6.3.1 节中介绍的示例也说明了扩展操作，但这里从结果开始。图 6.39 表示在 2-Gmap 中的 1-扩展。从图 6.39(a) 开始，2-Gmap C 描述的边被扩展到 2-Gmap G 中，根据 γ，产生图 6.39(b) 中表示的 G_{E_1}(C, γ)。

**图 6.39**

2-Gmap 的 1-扩展。

(a) 两个 2-Gmaps G 和 C，由双射 γ 链接。

(b) 2-Gmap G_{E_1}(C, γ)。

图 6.40 说明了在 2-Gmap 中的 2-扩展。从图 6.40(a) 开始，2-Gmap C 描述的面被扩展到 2-Gmap G 中，根据 γ。这产生了图 6.40(b) 中表示的 G_{E_2}(C, γ)。

由于扩展和插入非常相似，对应的算法也非常相似：参见算法 62 和 63。因此，这两个算法的复杂度也线性于 n-Gmap c 的 darts 数 #d 乘以 log #d。

![](img/6ba3cf72cbe3568e76a174448323bb33_254_0.png)

**图 6.40**

2-Gmap 的 2-扩展。

(a) 两个 2-Gmaps G 和 C，由双射 γ 链接。

(b) 2-Gmap G_{E_2}(C, γ)。

### 算法 62: `isExpansibleNGMap(gm,c,i,assoc)`: 测试 i-单元是否可扩展 n-Gmaps

**输入：** gm, c: 两个 n-Gmaps;

i ∈ {0, …, n};

assoc: 一个从 c.Darts 到 gm.Darts 的映射。

**输出：** 当且仅当 c 可以根据 assoc 在 gm 中扩展时为 True。

```text
1  if c contains more than one i-cell then return false;
2  if the i-cell in c is not contractible then return false;
3  assoc⁻¹ ← an associative array between darts, inverse of assoc;
4  foreach dart d ∈ assoc do
5      if not isFreeNGMap(d,i) then return false;
6      d′ ← assoc[d];
7      foreach j ∈ {0,…,i−2,i+2,…,n} do
8          if d.Alphas[j] ∈ assoc and
              assoc[d.Alphas[j]] ≠ assoc[d].Alphas[j] then
9              return false;
10         if d′.Alphas[j] ∈ assoc⁻¹ and
                assoc⁻¹[d′.Alphas[j]] ≠ assoc⁻¹[d′].Alphas[j] then
11             return false;
12     d₂ ← d.Alphas[i−1];
13     while d₂ ∉ assoc do
14         d₂ ← d₂.Alphas[i].Alphas[i−1];
15     if assoc[d₂] ≠ d′.Alphas[i] then return false;
16 return true;
```

### 算法 63: expandNGMap(gm, c, i, assoc): 在 n-Gmap 中扩展一个 i-单元

输入：gm: 一个 n-Gmap;

c: 根据 assoc 是一个可扩展的 i-单元;

i ∈ {0, …, n};

assoc: 一个从 c.Darts 到 gm.Darts 的映射。

结果：沿 assoc 将 i-单元 c 在 gm 中扩展。

```text
1 foreach dart d' ∈ c.Darts do
2   add d' in gm.Darts;
3   remove d' from c.Darts;
4   if d' ∈ assoc then
5     d'.Alphas[i] ← assoc[d'];
6     assoc[d'].Alphas[i] ← d';
```

## 6.6 倒角

倒角操作以 i-单元作为参数，并将其替换为 n-单元。它允许通过对其尖锐单元进行倒圆来平滑物体。在 2D 中，顶点或边可以被倒角（参见图 6.41 中的示例）。在两种情况下，当没有多重关联发生时，被倒角的单元被替换为一个新的面，该面的边界边数等于与被倒角单元关联的面数。例如在图 6.41 中：

- 当顶点被倒角时，新面与三条边关联；
- 当边被倒角时，新面与两条边关联。

请注意，只有给定的单元被倒角：例如，当倒角一条边时，其关联的顶点不会被倒角。

在 3D 中，顶点（参见图 6.42）、边（参见图 6.43）或面可以被倒角。当没有多重关联发生时，被倒角的单元被替换为一个体积，该体积的边界面数等于与被倒角单元关联的体积数。例如在图 6.42 中，新体积与八个面关联；在图 6.43 中，新体积与四个面关联。请再次注意，只有给定的单元被倒角，而不是其关联的单元。

这里介绍的倒角操作是一个基本操作。如图 6.44 所示，它是广义倒角操作的基础，后者包括多次应用基本倒角操作。在此示例中，从图 6.44(a) 表示的 3D 物体开始，先对边 e 进行倒角，然后对倒角边 e 之前与之关联的两个顶点进行倒角。这产生了图 6.44(b) 表示的物体，经过合并若干新单元的清理步骤之后。

