
**算法 75：** 二维拓扑图的增量构建

**输入：** I：一个大小为 n₁ × n₂ 像素的二维标记图像。

**输出：** 与 I 对应的二维拓扑图。

```text
1  cm ← createNMap(2);
2  last ← Build the upper border of the image in the 2-map cm;
3  emb ← an interpixel matrix of size (n₁ + 1, n₂ + 1) initialized to false;
4  for j ← 0 to n₂ do
5      for i ← 0 to n₁ do
6          up ← computeUpFromLast(cm,last);
7          tmp ← createSquare(cm,last,up,(i,j),n₁);
8          V ← c₀(last);
9          if pixel(i − 1,j) belongs to the same region than pixel(i,j) then
10             V ← V \ c₁(last);
11             removeNMap(cm,last,1);
12         else switch on linel ((i,j),3) in emb;
13         if pixel(i,j − 1) belongs to the same region than pixel(i,j) then
14             V ← V \ c₁(up);
15             removeNMap(cm,up,1);
16         else switch on linel ((i,j),0) in emb;
17         if V = {v₀,…} ≠ ∅ then
18             if isRemovableNMap(cm,v₀,0) then
19                 if v₀.Betas[1] ≠ v₀ then removeNMap(cm,v₀,0);
20             else switch on pointel (i,j) in emb;
21         last ← tmp;
22  Remove all the darts connected with last;
23  tree ← Compute the enclosure tree of regions;
24  return (cm,emb,tree)
```

![](img/6ba3cf72cbe3568e76a174448323bb33_300_0.png)

**图 7.18**

(a) 折叠在圆柱体上的二维标记图像。

(b) 开始构建之前在 2-图中创建的初始边界。

为了考虑与无限区域的边界，图像四周各扩展一个像素，这些额外的像素属于无限区域。为了避免针对这些像素的特殊情况从而简化算法，每一行的最后一个像素与下一行的第一个像素视为同一像素（见图 7.18(a)）。这种等同处理等价于将图像折叠在圆柱体上，并使各行产生偏移，因此现在只需沿 x 方向推进当前像素即可遍历整个图像。

为了满足图像第一个像素（像素 (0, 0)）的不变量，首先在 2-图中构建一个上边界（参见图 7.18(b)）。该边界由第一个像素左侧的一个 dart 以及图像第一行像素上方的所有 dart 组成。该边界向图像右侧扩展一个像素以考虑无限区域。为了模拟圆柱体上的折叠，β₁ 将第一个像素左侧的 dart 与第一行最后一个像素上方的 dart 相连（在图中用虚线曲线表示）。只需在图像右侧的列中增加一个像素，因为由于圆柱体的作用，一行的最后一个像素也就是下一行的第一个像素。第一个像素左侧的 dart 就是第一个 last dart，准备与描述像素 (0, 0) 的方块进行 2-缝合。借助这个边界，图像的每个像素都可以被处理，而无需对第一列/最后一列和第一行/最后一行进行特殊处理。

在构建算法的主循环（第 4 行和第 5 行）中，我们处理像素 (i, j)。首先创建一个方块，并将其与 dart last 和 up 进行 2-缝合。这在算法 76 中完成，其中首先创建四个 dart，并通过 β₁ 连接（第 1 至 5 行）。然后，dart res[0] 与 dart last 进行 2-缝合，dart res[1] 与 dart up 进行 2-缝合（第 6 和 7 行）。最后，根据左上角点元的位置 (x, y) 初始化四个新 dart 的嵌入。考虑到图像在圆柱体上的弯曲，点元的位置按图像宽度加一取模计算。该函数返回 dart res[2]，它是新方块右侧的 dart，即处理图像下一个像素时的下一个 last。

注意，在构建算法的主循环中，只需保留 last dart，因为通过算法 77 可以从 last 计算出 up dart（算法 77 主要是绕包含 dart last 的顶点旋转，直到得到一个 2-自由 dart）。

在构建算法的下一步中，考虑包含 dart last 和 up 的两条边以及包含 dart last 的顶点，以测试它们是否应被移除或保留。如果像素 (i − 1, j) 与当前像素属于同一区域，则必须移除包含 last 的边。实际上，在这种情况下，这两个像素之间没有边界。注意，如果 i = 0，像素 (−1, j) 属于无限区域 R₀。因此，如果当前像素也属于无限区域（当 j = n₂ 时），则两个像素属于同一区域；否则，它们属于两个不同区域。如果 i = n₁，像素 (i, j) 属于无限区域，并且仅当像素 (i − 1, j) 也属于无限区域（当 j = n₂ 时）时，两个像素才属于同一区域。

**算法 76：** `createSquare(cm,last,up,(x,y),w)`：创建一个新的方块，并与 dart `last` 和 `up` 进行 2-缝合

**输入：** `cm`：一个二维拓扑图；

`last`：当前像素左侧的 dart；

`up`：当前像素上方的 dart；

`(x,y)`：方块左上角点元的坐标；

`w`：图像的宽度。

**结果：** 创建一个新的方块，并与 dart `last` 和 `up` 进行 2-缝合，其中 `(x,y)` 为方块左上角点元的坐标（在 `x` 轴上对 `w + 1` 取模）。

**输出：** 新方块右侧的 dart。

```text
1  for i ← 0 to 3 do
2      res[i] ← createDartNMap(cm);
3      if i > 0 then
4          res[i].Betas[0] ← res[i − 1]; res[i − 1].Betas[1] ← res[i];
5  res[0].Betas[0] ← res[3]; res[3].Betas[1] ← res[0];
6  res[0].Betas[2] ← last; last.Betas[2] ← res[0];
7  res[1].Betas[2] ← up; up.Betas[2] ← res[1];
8  x′ ← (x + 1) % (w + 1); y′ ← y + ((x + 1) / (w + 1));
9  res[0].Emb ← ((x,y + 1),1); res[1].Emb ← ((x,y),0);
10 res[2].Emb ← ((x′,y′),3); res[3].Emb ← ((x′,y′ + 1),2);
11 return res[2];
```

**算法 77：** `computeUpFromLast(cm,last)`：给定当前像素左侧的 dart，获取其上方（up）的 dart

**输入：** `cm`：一个二维拓扑图；

`last`：当前像素左侧的 dart。

**输出：** `up`：当前像素上方的 dart。

```text
1  up ← last.Betas[0];
2  while not isFreeNMap(cm,up,2) do
3      up ← up.Betas[2].Betas[0]
4  return up;
```

类似地，如果像素 $(i,j-1)$ 与当前像素属于同一区域，则必须移除包含 *up* 的边。如果 $j = 0$，像素 $(i,j-1)$ 属于无限区域，并且当像素 $(i,j)$ 也属于无限区域时，两个像素属于同一区域（$j = n_2$ 时同理）。通过应用第 205 页 6.2.2 节中给出的 1-移除操作来移除一条边。当一条边未被移除时（第 12 行和第 16 行），对应的线元会在像素间矩阵上被打开，因为该线元分隔了两个属于不同区域的像素。

最后，我们测试包含 dart *last* 的顶点是否需要被移除。为此，在处理边之前，将 $c_0(last)$ 中的 dart 集合存储在 $V$ 中（第 8 行）。当一条边被移除时，该边的 dart 也从 $V$ 中移除（第 10 行和第 14 行）。实际上，由于这些 dart 被移除，它们不再属于与 *last* 关联的顶点。处理完边之后，如果 $V$ 为空（第 17 行），则没有更多的顶点需要处理。否则，至少存在一个 dart $v_0 \in V$。如果 $c_0(v_0)$ 是可移除的，并且 dart $v_0$ 不是环，则必须移除该顶点。如果顶点可移除但边是环，则必须保留该顶点；否则，这将导致边也被移除，从而丢失一个边界。最后，如果顶点不可移除，则将点元 $(i,j)$（即对应于顶点 $c_0(v_0)$ 的点元）打开。实际上，在这种情况下，有不止两个线元与该点元关联。

像素 $(i,j)$ 的处理到此结束。*last* dart 被移动到最近创建的方块右侧的 dart 上，即像素 $(i+1,j)$ 的下一个 *last* dart。注意，由于圆柱体上的折叠，一行的最后一个像素无需特殊处理：一行的下一个 *last* 等于下一行的第一个 *last*。

在构建 2-图的过程中，可以计算与区域及不同单元相关的信息。例如，要计算每个区域的平均颜色，我们将添加到给定区域的每个像素的颜色累加，并递增其像素数量。在拓扑图构建完成后，通过将颜色总和除以像素数量即可直接计算出平均颜色。另一个例子是，要计算每条边的梯度，可以用被该边分隔的两个像素的颜色差的绝对值来初始化包含 dart *last* 的边的梯度（对包含 dart *up* 的边也类似），并将这两条边的长度初始化为 1。然后，当顶点被移除时，两条关联边的两个梯度（和两个长度）相加。在构建结束时，每条边与其所有线元的梯度总和及其长度相关联。借助这两个值，每条边的梯度可以直接计算出来。

图 7.19 展示了我们构建算法针对先前示例中使用的二维图像的前几个步骤。初始边界见图 7.18(b)。创建对应像素 $(0,0)$ 的方块之后的 2-图如图 7.19(a) 所示。该像素与像素 $(-1,0)$ 和像素 $(0,-1)$ 都不属于同一区域（后两者都属于 $R_0$），因此这两条边被移除。然后测试顶点 $c_0(last)$：由于它……
