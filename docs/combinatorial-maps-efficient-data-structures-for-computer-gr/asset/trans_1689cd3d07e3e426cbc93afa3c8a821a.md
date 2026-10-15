

**Algorithm 66:** `triangulationNGMap(gm,d,i)`: triangulation of an *i*-cell for *n*-Gmaps

**Input:** `gm`: an *n*-Gmap;  
`d ∈ gm.Darts`: a dart;  
`i ∈ {1, ..., n}`.

**Result:** Make a triangulation of the *i*-cell `cᵢ(d)`.

**Output:** A dart of the new vertex.

```text
1  phi ← an array of i + 1 empty associative arrays between darts;
2  foreach dart d′ ∈ cᵢ(d) do
3      for j ← 0 to i − 1 do
4          phi[j][d′] ← createDartNGMap(gm);
5      phi[i][d′] ← d′;
6  foreach dart d′ ∈ cᵢ(d) do
7      phi[0][d′].Alphas[0] ← phi[1][d′];
8      for j ← 1 to i do
9          phi[0][d′].Alphas[j] ← phi[0][d′.Alphas[j − 1]];
10     for j ← i + 1 to n do
11         phi[0][d′].Alphas[j] ← phi[0][d′.Alphas[j]];
12     for k ← 1 to i − 1 do
13         for j ← 0 to k − 2 do
14             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j]];
15         phi[k][d′].Alphas[k − 1] ← phi[k − 1][d′];
16         phi[k][d′].Alphas[k] ← phi[k + 1][d′];
17         for j ← k + 1 to i do
18             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j − 1]];
19         for j ← i + 1 to n do
20             phi[k][d′].Alphas[j] ← phi[k][d′.Alphas[j]];
21 foreach dart d′ ∈ cᵢ(d) do
22     d′.Alphas[i − 1] ← phi[i − 1][d′];
23 return phi[0][d];
```

![](img/6ba3cf72cbe3568e76a174448323bb33_271_0.png)

**FIGURE 6.53**  
(a) A 2D object.  
(b) The result of the 1-triangulation operation applied to the edges of (a).  
(c) The result of the 2-triangulation operation applied to the faces of (b). This is the barycentric triangulation of the initial object.

与倒角操作类似，cᵢ(d) 中的 darts 的 αᵢ₋₁ 链接被修改（第 22 行）。为避免副作用，此修改在第二个循环中进行，在为新 darts 定义 α 链接之后。此外，cᵢ(d) 的 darts 在第一个循环中被存储在数据结构中（第 2 行）；第二个循环的迭代是通过数据结构进行的，而不是通过单元迭代器（第 21 行）。最后，算法返回属于新顶点的其中一个 dart，因为它可以在其他算法中使用（如我们在第 265 页算法 74 中将会看到）。

算法 66 的复杂度与给定 i-单元的 darts 数目 #d 乘以 log #d 成线性关系。

给定 n-Gmap 的 *barycentric triangulation* 可以通过对 n-Gmap 的 i-单元从 i = 1 到 i = n 应用 i-三角剖分操作来定义。例如，参见图 6.53(a) 中表示的 2D 对象。它包含 12 个顶点、17 条边和 6 个面。1-三角剖分操作应用于其所有边，产生图 6.53(b) 中表示的 2D 对象。该对象包含 29 个顶点、34 条边和 6 个面。然后，2-三角剖分操作应用于其所有面，产生图 6.53(c) 中表示的 2D 对象。该对象包含 35 个顶点、84 条边和 50 个面。这就是初始对象的重心三角剖分：一个顶点对应于初始对象的每个单元。

![](img/6ba3cf72cbe3568e76a174448323bb33_274_0.png)

# **FIGURE 7.1**

Example of embedding of a 2-map in \(\mathbb{R}^2\). Embedding of vertices is represented by dashed lines, embedding of edges is represented by lines and embedding of faces is not represented.

\(M\) 的 embedding 与 \(M\) 具有相同的结构。注意，这里解释的机制对 \(n\)-maps 和 \(n\)-Gmaps 都有效。一种经典的方法是将 \(n\)-map 嵌入到欧几里得空间 \(\mathbb{R}^d\) 中。注意，\(n\)-map 的维数 \(n\) 不一定等于欧几里得空间的维数 \(d\)。\(n\) 将被称为 *组合维数*，而 \(d\) 将被称为 *环境维数*。

2-map 嵌入到 \(\mathbb{R}^2\) 中的表示见图 7.1。2-map 的每个顶点都与 \(\mathbb{R}^2\) 中的一个点相关联（例如顶点 \(\{1,6\}\) 与点 \((0,2)\) 相关联，顶点 \(\{7\}\) 与点 \((1,3)\) 相关联）；每条边都与一个开线段相关联（例如边 \(\{6\}\) 与线段 \(](0,2),(1,3)[\) 相关联，边 \(\{1,5\}\) 与线段 \(](0,2),(2,2)[\) 相关联）；每个面都与一个开平面区域相关联（面 \(\{5,6,7\}\) 与由 \(\{(x,y) \in \mathbb{R}^2|y > 2 \text{ and } y < x-2 \text{ and } y < -x+4\}\) 定义的平面区域相关联，面 \(\{1,2,3,4\}\) 与由 \(\{(x,y) \in \mathbb{R}^2|x > 0 \text{ and } x < 2 \text{ and } y > 0 \text{ and } y < 2\}\) 定义的平面区域相关联）。

我们可以通过检查 2-map 中两个相邻单元是否与平面中的两个相邻元素相关联且反之亦然来验证此示例是一个正确的嵌入。例如，与点 \((0,2)\) 相关联的顶点 \(\{1,6\}\) 与与线段 \(](0,2),(2,2)[\) 相关联的边 \(\{1,5\}\) 相邻，且点 \((0,2)\) 属于该线段的边界。

该 2-map 被“线性嵌入”到 \(\mathbb{R}^2\) 中：顶点与点相关联，边与线段相关联，面与多边形相关联。

![](img/6ba3cf72cbe3568e76a174448323bb33_275_0.png)

# FIGURE 7.2

Embedding a 2-map in ℝ²: edges and faces are implicitely embedded.

更一般地，线性嵌入是将 iD 超平面的一部分与每个 i-单元相关联。这种类型的嵌入经常被使用，因为它易于处理。然而还存在许多其他类型的嵌入。例如，可以使用样条曲线嵌入边或使用 NURBS 曲面嵌入面。然而即使在这些情况下，嵌入仍然是将 iD 几何元素与 i-单元相关联，并且与单元之间的关联相关的约束仍必须得到满足。给定嵌入的选择将取决于应用的具体需求。

注意，可以避免显式描述所有几何对象，当其中一些对象可以通过其他单元的嵌入和 n-map 中的关联关系计算出来时。例如，上面介绍的线性嵌入，这里为简化起见以 n = 2 解释。在这种情况下，任何边的嵌入都是其两个端点所关联的两个点为端点的开线段。因此，不必显式地将开线段与边相关联，因为它们可以从 0-嵌入中获取。类似地，任何面的嵌入都是一个平面的一部分，其边界包含与相邻边相关联的所有线段。因此，也不需要显式描述此 2-嵌入，因为它可以通过 1-嵌入获取。因此，只需将点与顶点相关联即可线性嵌入 2-map（参见图 7.2）。这通常是定义线性嵌入的方式，对任意 n 而言。注意，一致性约束仍必须得到满足：例如，与同一条边相邻的两个顶点所关联的点必须定义一条线段，即它们必须不同；与一个面相邻的顶点的点必须共面，否则面的形状未定义；等等。

相反，可以采用对偶方法，这里为简化起见以线性嵌入和 n = 2 解释；但实际上，它通常应用于非线性嵌入（例如修剪曲面：参见 [2]）。将 \(\mathbb{R}^3\) 的一个平面与任何面相关联。该平面是面的支撑空间。与共享一条边的两个相邻面相关联的曲面沿一条线相交：该线是公共边的支撑空间。与共享一个顶点的所有边相关联的所有线在一点相交，该点是顶点的嵌入。与一条边相关联的线段由其支撑线定义，由其相邻顶点的点所限制。类似地，与一个面相关联的平面部分可以从其支撑平面和与相邻边相关联的线获取。事实上，所有嵌入信息都可以从与面相关联的支撑空间获取，因为其他单元的嵌入可以推导出来。这里也必须满足一致性约束：例如，与一条边共享的两个边的平面必须不同。该方法可以推广到更高维，也可用于非线性嵌入。例如，与面相关联的支撑空间通常是自由曲面（例如 NURBS）。

隐式嵌入的主要优点是：

+   1. 减小内存占用：需要存储的几何元素更少，需要描述的链接更少；
+   2. 简化操作：只需处理一种类型的嵌入；
+   3. 提高有效性保证：某些单元嵌入的有效性约束可能因使用相邻单元的嵌入而得到保证。

主要缺点是存在额外成本，因为可能需要显式计算（关于）不同的隐式嵌入；但通常这种成本很小。

将嵌入与 i-单元相关联有多种可能性。然而由于单元是 darts 的集合，这种关联始终是通过 darts 完成的。例如，可以向每个 dart 添加一个指针，该指针指向包含该 dart 的 i-单元的嵌入。此解决方案允许直接访问所有嵌入。然而它需要更新 i-单元的所有 darts 的指针以初始化其嵌入。此外，每个 dart 和每个具有嵌入的维数 i 都有一个指针。也可以创建一个关联数组，将 i-单元的每个 dart 与其对应的嵌入关联起来。这允许在不修改 dart 数据结构的情况下添加或删除特定嵌入。此外，如果使用哈希表，则可以平均在常数时间内访问 dart 的嵌入。作为最后一个例子，可以只将每个 i-单元的一个 dart 与对应的 i-嵌入关联起来。节省内存空间，因为描述的关系更少；此外，这可以加快修改 darts 与嵌入之间链接的一些操作，因为只有一个 dart 需要修改。然而，

