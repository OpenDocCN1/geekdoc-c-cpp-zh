
在 3D 中原理类似。例如，考虑图 6.5(a) 中给出的 3-Gmap，并应用 3-闭包操作。如果首先处理 dart `d = 32`，则创建一个新的 dart `d' = 32'`，并且 darts `32` 和 `32'` 被 3-缝合。第一个循环（第 4 行）考虑 `j ∈ {0,1}`，但在两种情况下，`α_j(32)` 都是 3-自由的。第二个循环（第 11 行）允许定义 `α_2`。从 `d'' = α_2(32)` 开始，经过一次迭代得到 `d'' = 19`；它是 3-自由的，因此 `α_2` 未为 dart `32'` 定义。现在考虑 `d = 31`；创建一个新的 dart `d' = 31'`，并且 darts `31` 和 `31'` 被 3-缝合。在第一个循环期间，darts `31'` 和 `32'` 被 0-缝合。现在考虑 `d = 20`；创建一个新的 dart `d' = 20'`，并且 darts `20` 和 `20'` 被 3-缝合。第一个循环期间没有进行缝合；darts `20'` 和 `31'` 被 2-缝合，因为得到 dart `d'' = 31`，其满足 `α_3(31)` 是 2-自由的，并且它不是 3-自由的。

# 6.1.2 对于 n-图

对于 `i ≥ 2` 的 i-闭包操作，对于 n-图 `M` 在定义 56 中定义。与 n-Gmaps 一样，会为 `M` 中每个 i-自由 dart 创建新的 darts；这些 darts 通过 `β_j`，`∀j ∈ {1,…,n}`，`j ≠ i`，根据 i-边界映射 `M_{\partial_i}` 的逆中的相应链接进行相互链接（参见定义 49 第 175 页）；每个新 dart 通过 `β_i` 与其在 `M` 中的对应 dart 链接。

**定义 56 (i-闭包)** 设 `M = (D, β_1, …, β_n)` 是一个 n-图，`i ∈ {2,…,n}`，且 `M_{\partial_i}^{-1} = (D', β_1', …, β_n')` 是 `M` 的 i-边界映射的逆。`M` 的 i-闭包是 n-图 `M_i-close = (D'', β_1'', …, β_n'')` 定义为：

1. `D'' = D ∪ {d''_1, …, d''_{|D'|}}`，其中 `{d''_1, …, d''_{|D'|}}` 是一组新 darts，使得双射 `f` 将 `D'` 映射到 `{d''_1, …, d''_{|D'|}}`；
2. `∀j ∈ {1,…,n}` 使得 `j ≠ i`：
   - `∀d ∈ D`，`β_j''(d) = β_j(d)`；
   - `∀d' ∈ D'`，`β_j''(f(d')) = f(β_j'(d'))`；
3. `∀d ∈ D \ D'`，`β_i''(d) = β_i(d)`；
4. `∀d ∈ D'`，`β_i''(d) = f(d)`，`β_i''(f(d)) = d`。

2-闭包操作在图 6.6 中进行了说明。从 (a) 中具有边界的 2-图开始，通过应用 2-闭包操作得到的图 (b) 中的 2-图没有 2-边界。在初始 2-图中有六个 2-自由 darts，因此创建了六个新的 darts，编号为 13 到 18。这些新 darts 通过 `β_2''` 与其对应的 darts 链接。此外，这些新 darts 通过 `β_1''` 相互链接，根据 2-边界映射 `M_{\partial_2}^{-1}` 的逆中的相应链接。

图 6.7 中描绘的 2-图具有 1-边界和 2-边界。在这种情况下，2-闭包操作产生一个没有 2-边界的 2-图，但它仍然具有 1-边界。

![Figure 6.6](img/6ba3cf72cbe3568e76a174448323bb33_215_0.png)

**FIGURE 6.6**  

2-图 的 2-闭包。  

(a) 一个具有 2-边界的 2-图 `M`。Darts `2, 3, 7, 10, 11, 12` 是 2-自由的。  

(b) 2-图 `M_2-close`。新 darts 编号为 13 到 18。

![Figure 6.7](img/6ba3cf72cbe3568e76a174448323bb33_215_1.png)

**FIGURE 6.7**  

2-图 的 2-闭包。  

(a) 一个具有 1-边界和 2-边界的 2-图 `M`。  

(b) 2-图 `M_2-close`。新 darts 编号为 12 到 15。该 2-图没有 2-边界，而仍然具有 1-边界。

1-闭包操作在定义 57 中定义。

**定义 57 (1-闭包)** 设 `M = (D, β_1, …, β_n)` 是一个 n-图，`n > 0`，且 `M_{\partial_1} = (D', β_1', …, β_n')` 是相应的 1-边界映射。`M` 的 1-闭包是 n-图 `M_1-close = (D'', β_1'', …, β_n'')` 定义为：

1. `D'' = D ∪ {d''_1, …, d''_{|D'|}}`，其中 `{d''_1, …, d''_{|D'|}}` 是一组新 darts，使得双射 `f` 将 `D'` 映射到 `{d''_1, …, d''_{|D'|}}`；
2. `∀j ∈ {2,…,n}`：
   - `∀d ∈ D`，`β_j''(d) = β_j(d)`；
   - `∀d' ∈ D'`，`β_j''(f(d')) = f(β_j'(d'))`；
3. `∀d ∈ D \ D'`，`β_1''(d) = β_1(d)`；
4. `∀d ∈ D'`，`β_1''(d) = f(d)`，`β_1''(f(d)) = β_0^k(d)`，其中 `k` 是使得 `β_0^k(d)` 是 0-自由的最小正整数。

与 `i ≥ 2` 的 i-闭包定义相比有两个区别。首先，考虑 1-边界映射 `M_{\partial_1}` 而不是其逆。事实上，`D'` 中的所有 darts 都是 1-自由的，因此 `M_{\partial_1} = M_{\partial_1}^{-1}`。其次，`β_1''(f(d))` 不等于 `d`，因为 `β_1` 不是对合。它等于 `β_0^k(d)`，`k` 为使得 `β_0^k(d)` 是 0-自由的最小正整数。直观上，`β_1` 定义了多边形线，而 `β_0` 是 incident 于 `d` 的开放多边形线的第二个端点。

1-闭包操作在图 6.8 中进行了说明。

![Figure 6.8](img/6ba3cf72cbe3568e76a174448323bb33_216_0.png)

**FIGURE 6.8**  

1-图 的 1-闭包。  

(a) 一个具有 1-边界的 1-图 `M`。  

(b) 1-图 `M_1-close`。Dart `4` 是新的。

从 (a) 中描绘的具有边界的 1-图开始，通过应用 1-闭包操作得到图 (b) 中没有边界的 1-图。在初始 1-图中，有一个 1-自由 dart（编号为 3），因此创建了一个 dart（编号为 4）。`β_1''(3) = f(3) = 4`，因为 dart `4` 是对应于 dart `3` 的新 dart。然而，定义 `β_1''(4)` 更复杂，因为需要检索属于同一多边形线的 0-自由 dart。因此必须计算 `β_0^k(3)`，其中 `k` 是使得 `β_0^k(3)` 是 0-自由的最小正整数。因此 `β_1''(4) = β_0^2(3) = 1`。

1-闭包操作的另一个例子在图 6.9 中给出，但这里是对于 3-图。有两个 1-自由 darts 编号为 3 和 4，因此创建了两个新的 darts（编号为 7 和 8）。由于 darts 3 和 4 在 1-边界映射 `M_{\partial_1}` 中是 3-缝合的，对应的 darts 7 和 8 在 `M_1-close` 中也同样地是 3-缝合的：`β_1''(3) = f(3) = 7`，因为 dart `7` 对应于 1-自由 dart `3`（类似地，`β_1''(4) = 8`），并且 `β_1''(7) = β_0^3(3) = 1`（类似地，`β_1''(8) = β_0^2(4) = 2`）。

![](img/6ba3cf72cbe3568e76a174448323bb33_217_0.png)

## FIGURE 6.9

1-closure for 3-map.

(a) A 3-map `M` with 1-boundary, 2-boundary and 3-boundary. Darts `3` and `4` are 1-free.

(b) The 3-map `M_{1-close}`. Dart `7` and `8` are new darts associated with darts `3` and `4`.

As for `n`-GMaps, a *closure operation* can be defined for removing all boundaries for all dimensions. For that, all the possible `i`-closure operations are applied, from `i = 1` to `i = n`. For example, starting from the 3-map given in Fig. 6.9(a), the 1-closure operation produces the 3-map shown in Fig. 6.9(b), which has no 1-boundary. Then, the 2-closure operation produces the 3-map given in Fig. 6.10(a), which has no 2-boundary. Finally, the 3-closure operation produces the 3-map given in Fig. 6.10(b), which has no 3-boundary, and thus no boundary at all.

Algorithm 48 implements the `i`-closure operation for `n`-maps and for `i ∈ {2, …, n}`. This algorithm follows directly the `i`-closure definition (see Def. 56). As for Algorithm 47, the `i`-boundary map is not explicitly computed.

In this algorithm, the new darts are created and linked by `β_i` with the corresponding `i`-free darts (cf. item 4 of the `i`-closure definition). Then, the other `β` links are defined, according to the definition of the boundary map. `β_{i+1}` is initialized to `∅` for all the new darts (second item of the `i`-boundary map definition), by definition of the `createDartNMap` function.

All `j`, such that `|i-j| ≥ 2`, have to be considered, thus two cases occur: if `i = 2`, this is the set `{4, …, n}`; otherwise, this is the set `{0, 1, …, i-2, i+2, …, n}`. For all `j` in this set, `β_j` is deduced from the definition of `β_i` for the `i`-free dart `d`. Indeed, `β_i ∘ β_j` is a partial involution. As `β_i(d) = d'` and `β_j(d) = d''`, it is necessary to have `β_j(d') = β_i(d'')`. Since `d' = f(d)`, defining `β_j^{-1}(d') = β_i(d'')` is equivalent to define `β_j''^{-1}(f(d)) = f(β_j'(d))`: this corresponds to item 2 of the `i`-closure definition (remember that in the algorithm, `β_i` denotes also `β_i'` and `β_i''`).

![](img/6ba3cf72cbe3568e76a174448323bb33_218_0.png)

## FIGURE 6.10

Closure for 3-map.

(a) The 3-map `M'` obtained from Fig. 6.9(b) by applying the 2-closure operation. Darts `9` to `16` are new darts.

(b) The 3-map `M'_{3-close}`. The forty black darts are new darts, describing the external volume enclosing the two initial cubes.

```
Algorithm 48: closeNMap(cm,i): i-close an n-map

Input: cm: an n-map;
       i ∈ {2, …, n}.
Result: cm is i-closed.

1  if i = 2 then S ← {4, …, n};
2  else S ← {0, 1, …, i − 2, i + 2, …, n};
3  foreach i-free dart d ∈ cm.Darts do
4      d′ ← createDartNMap(cm);
5      d.Betas[i] ← d′; d′.Betas[i] ← d;
6      foreach j ∈ S do
7          d″ ← d.Betas[j];
8          if not isFreeNMap(cm,d,j) and not isFreeNMap(cm,d″,i)
9          then
10             d′.Betas[inv(j)] ← d″.Betas[i];
11             d″.Betas[i].Betas[j] ← d′;
12         d″ ← d.Betas[inv(i − 1)];
13         while not isFreeNMap(cm,d″,i) and not isFreeNMap(cm,d″.Betas[i],inv(i − 1)) do
14             d″ ← d″.Betas[i].Betas[inv(i − 1)];
15         if not isFreeNMap(cm,d″,i) then
16             d′.Betas[i − 1] ← d″.Betas[i];
17             d″.Betas[i].Betas[inv(i − 1)] ← d′;
```

Note that `β_j` is defined for `d` only if `d` is not `j`-free and `d''` is not `i`-free. Indeed, if `d` is `j`-free, then `d'` must be also `j`-free, and thus there is nothing to do as darts are created free in all dimensions. If `d''` is `i`-free, it is not possible yet to define the `β_j` links between `d'` and `β_i(d'')`, as the new dart associated with `β_j(d)` is not yet created. This will be done in a future step of the algorithm, when dart `β_j(d)` will be processed. This is why this definition is done in both directions.
