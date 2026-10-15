

这会减慢对给定 dart 的嵌入的访问速度，因为有必要遍历其 *i*-cell 的所有 darts 才能找到与嵌入链接的 dart。

## 7.2 几何建模

*n*-Gmaps 和 *n*-maps 已用于几何建模以构造和修改几何对象。本节重点介绍 Moka [211] 的构想，这是一款基于 3-Gmaps 的 3D 几何建模器。选择 3-Gmaps 是为了简化数据结构和操作的实现，归功于其同质性。许多实现选择与维度无关。首先，我们在第 7.2.1 节中解释 *n*-Gmaps 在 ℝᵈ 中的线性嵌入。然后在第 7.2.2 节中描述几何操作。最后，在第 7.2.3 节中提供了一个对象构造的示例。

### 7.2.1 *n*-Gmaps 在 ℝᵈ 中的嵌入

如上所述，*n*-Gmap 通过为 *n*-Gmap 的每个顶点关联 ℝᵈ 中的一个点而线性嵌入到 ℝᵈ 中。其他单元被隐式嵌入。为了表示顶点与点之间的这种关联，我们选择将每个顶点的 *一个* dart 与其对应的点链接起来。这一选择是为了有利于修改操作，因为只需修改一个 dart 与其嵌入之间的关联即可修改嵌入。这种解决方案是以访问嵌入操作为代价的，因为必须遍历属于该顶点的所有 darts 才能找到具有链接的那个。需要注意的是，与点链接的 dart 的选择无关紧要：可以从同一顶点的任何 dart 中选择。

对于描述与金字塔相邻的立方体的 3-Gmap 的这种嵌入在图 7.3(a) 中进行了说明。九个点与 3-Gmap 的九个顶点相关联，并且每个顶点的一个 dart 与其关联的点链接。图 7.3(b) 显示了 MOKA 中表示该对象的快照。

为了表示这种嵌入，Dart 数据结构（在第 4.4 节第 108 页引入）通过添加一个指针（称为 Point）进行修改，该指针指向描述关联点的结构。点由 *d double* 的数组表示，对应于坐标（参见结构 GeometricalPoint）。对于未与点链接的 darts，Point 指针设为 NULL（一些高级编程技术使得可以通过使用两类不同的 darts 来避免为未链接点的 darts 表示此指针）。

# Listing 7.1

# FIGURE 7.3

(a) 3-Gmap 在 ℝ³ 中的嵌入。

(b) 在 Moka 中描述的该对象的快照。

# dD point data structure

```
structure GeometricalPoint
{ double coord[d] ; };
```

基本方法允许管理与 n-Gmaps 关联的几何点。检索与给定顶点关联的点在算法 67 中描述。检查顶点的 darts：如果当前 dart 的 Point 指针非 NULL，则返回关联的点。如果所有 darts 都链接到 NULL，则该顶点没有关联的点。当 n-Gmap 正确嵌入时，这种情况不应该发生，但在构造新对象期间可能会发生。

算法 67 的复杂度与 c₀(d) 中的 darts 数量成线性关系。需要注意的是，平均情况下会检查一半的 darts，因为一旦找到与 Point 关联的 dart，循环就会结束。

算法 68 实现了将给定顶点关联的点设置为给定值 p 的方法。首先检查是否已将点与顶点关联（第 1 行）。当不是这种情况时，创建一个新点并将其与 dart d 关联（第 3 行和第 4 行）。最后将点的数值设置为 p（第 5 行）。

算法 68 的复杂度也与 c₀(d) 中的 darts 数量成线性关系，这是由于对现有点的第一次搜索。

算法 69 描述了删除与给定顶点关联的点的方法。该算法的复杂度也与 c₀(d) 中的 darts 数量成线性关系。

```
**Algorithm 67:** getPoint(d): get the geometrical point associated with a vertex

**Input:** gm: an embedded *n*-GMap;

&emsp;&emsp;&emsp;&emsp;&emsp;d ∈ gm.Darts: a dart.

**Output:** The geometrical point associated with c₀(d).

1. **foreach** dart e ∈ c₀(d) **do**
2. &emsp;**if** e.Point ≠ NULL **then**
3. &emsp;&emsp;**return** e.Point;
4. **return** NULL;
```

```
**Algorithm 68:** setPoint(d,p): set the geometrical point associated with a vertex

**Input:** gm: an embedded *n*-GMap;

&emsp;&emsp;&emsp;&emsp;&emsp;d ∈ gm.Darts: a dart;

&emsp;&emsp;&emsp;&emsp;&emsp;p: a geometrical point.

**Result:** Set the geometrical point associated with c₀(d) to p.

1. p′ ← getPoint(d);
2. **if** p′ = NULL **then**
3. &emsp;p′ ← create new GeometricalPoint;
4. &emsp;d.Point ← p′;
5. set the point in p′ to p;
```

```
**Algorithm 69:** `deletePoint(d)`: delete the geometrical point associated with a vertex

**Input:** gm: an embedded *n*-Gmap;

             d ∈ gm.Darts: a dart.

**Result:** Delete the geometrical point associated with c₀(d).

1. `foreach dart e ∈ c₀(d) do`
2.   `if e.Point ≠ NULL then`
3.      `delete e′.Point;`
4.      `e′.Point ← NULL;`
5.      `return;`
```

### 7.2.2 几何操作

第 4.4 节和第 6 章（第 108 页和第 185 页）中已介绍了一些用于处理 *n*-Gmaps 的组合操作。这些操作必须修改以处理嵌入的 *n*-Gmaps，以便相应地更新嵌入。幸运的是，这可以很容易地完成，这是由于对象拓扑与其嵌入之间的区别。确实，darts 和 α 链接对应于对象的拓扑，而几何点集合对应于嵌入。如以下所示，操作可以仅处理拓扑，仅处理嵌入，或同时处理两者。

通常当顶点被修改时，关联的几何点也必须被修改。修改 *n*-Gmap 中顶点的操作是：创建新顶点；销毁现有顶点；合并多个顶点；分割一个顶点。相应的嵌入操作是：创建新的几何点；删除关联的几何点；移除除一个之外的所有几何点；复制几何点。需要注意的是，一些组合操作不涉及嵌入修改。例如，*i*-close 操作对于 *i* > 0 时就是这种情况（参见第 6.1 节第 185 页）。确实，此操作不会创建新的 darts，也不会合并或分割现有顶点。操作创建的新 darts 与现有 darts 链接，因此它们将属于现有顶点。所有结果顶点都对应于初始顶点，其嵌入不会被修改。

#### 7.2.2.1 立方体创建

算法 70 描述了在 *n*-Gmap 中拓扑创建立方体（*n* ≥ 2）。创建六个正方形面，并进行 2-sewn（参见图 7.4(a)）。创建正方形面很简单：它包括创建八个 darts，两两通过 α₀ 和 α₁ 缝合（此处未给出算法）。由于此操作纯粹是组合的，所有 darts 都起相同的作用。

```
**Algorithm 70:** `createTopoCube(gm)`: create a topological cube in an *n*-Gmap

**Input:** `gm`: an *n*-Gmap, *n* ≥ 2.

**Output:** A dart of the new topological cube created in `gm`.

```text
1  for i ← 0 to 5 do
2      d[i] ← one dart of a new square face created in gm;
3  sewNGMap(gm,d[0],d[4].Alpha₀.Alpha₁.Alpha₀.Alpha₁,2);
4  sewNGMap(gm,d[0].Alpha₀.Alpha₀.Alpha₁,d[3].Alpha₀.Alpha₁.Alpha₁,2);
5  sewNGMap(gm,d[0].Alpha₀.Alpha₁.Alpha₀.Alpha₁,
           d[2].Alpha₀.Alpha₁.Alpha₁,2);
6  sewNGMap(gm,d[0].Alpha₁,d[1].Alpha₀.Alpha₁.Alpha₁,2);
7  sewNGMap(gm,d[5],d[2].Alpha₁,2);
8  sewNGMap(gm,d[5].Alpha₀.Alpha₁,d[1].Alpha₁.Alpha₀,2);
9  sewNGMap(gm,d[5].Alpha₁.Alpha₀.Alpha₁,d[4].Alpha₁,2);
10 sewNGMap(gm,d[5].Alpha₁,d[3].Alpha₁.Alpha₀,2);
11 sewNGMap(gm,d[1].Alpha₁.Alpha₀.Alpha₁,
           d[2].Alpha₁.Alpha₀.Alpha₁,2);
12 sewNGMap(gm,d[1],d[4].Alpha₁.Alpha₀.Alpha₁,2);
13 sewNGMap(gm,d[2],d[3].Alpha₁.Alpha₀.Alpha₁,2);
14 sewNGMap(gm,d[3],d[4],2);
15 return d[0];
```
```

可以很容易地添加几何层以便在 ℝᵈ 中创建嵌入的立方体。由于组合操作创建了新的顶点，几何层包括创建新的 *d*D 点。拓扑立方体创建后，*d*D 点与相应的 darts 关联。算法 71 描述了在 ℝ³ 中几何创建立方体（参见图 7.4(b)）。

需要注意的是，该算法可以改进，因为在拓扑立方体创建时没有任何点与任何 dart 关联。因此，可以避免在 `setPoint` 函数中进行的测试，以搜索已与几何点关联的顶点中的 dart。

#### 7.2.2.2 几何缝合

几何操作的第二个示例在算法 72 中描述：几何 *i*-sew 操作。应用组合操作时可能会合并多个顶点；因此，额外的几何层包括删除与这些合并顶点关联的几何点。这种删除是作为预备步骤添加到第 122 页算法 20 中，该算法实现了组合 *i*-sew 操作。需要注意的是没有顶点被识别

