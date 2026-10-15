


**算法 1：createNGMap(n)**：创建新的 n-GMap

**输入：** n：n-GMap 的维度。

**输出：** 一个空的新 n-GMap。

```text
1  gm ← a new nGMap;
2  gm.Darts ← ∅;
3  gm.FreeMarks ← ∅;
4  for i ← 0 to NB_MARKS − 1 do
5      add i in gm.FreeMarks;
6  return gm;
```

**算法 2：reserveMarkNGMap(gm)**：为 n-Gmaps 预留新标记

**输入：** gm：一个 n-GMap。

**输出：** 新预留标记的索引；如果没有更多可用标记则为 −1。

```text
1  if gm.FreeMarks is empty then return −1;
2  i ← an element of gm.FreeMarks;
3  remove i from gm.FreeMarks;
4  return i;
```

**算法 3：freeMarkNGMap(gm, i)**：为 n-Gmaps 释放预留标记

**输入：** gm：其所有 darts 对标记 i 均未标记的 n-GMap；i：预留标记的索引。

**结果：** 释放预留标记 i。

```text
1  add i into gm.FreeMarks;
```

不是通过直接查看 d.Marks[i]（见算法 4），并且我们可以通过将 d.Marks[i] 设置为 true/false 来标记/取消标记该 dart（见算法 5 和 6）。

**算法 4：isMarkedNGMap(d, i)**：测试 dart 是否为 n-Gmaps 标记

**输入：** d：一个 dart；i：预留标记的索引。

**输出：** 当且仅当 d 对标记 i 被标记时为 True。

```text
1  return d.Marks[i];
```

**算法 5：markNGMap(d, i)**：为 n-Gmaps 标记一个 dart

**输入：** d：一个 dart；i：预留标记的索引。

**结果：** 将 dart d 标记为标记 i。

```text
1  d.Marks[i] ← true;
```

**算法 6：unmarkNGMap(d, i)**：为 n-Gmaps 取消标记一个 dart

**输入：** d：一个 dart；i：预留标记的索引。

**结果：** 取消 dart d 对标记 i 的标记。

```text
1  d.Marks[i] ← false;
```

所有这些算法的复杂度均为常数时间，因为我们仅使用原子操作且没有循环，除算法 1 外，但在这种情况下 NB_MARKS 是一个常数值。我们使用栈来存储空闲标记的集合，从而可以以常数时间访问新的空闲标记，并以常数时间插入和删除元素。

请注意，可以在 nGMap 数据结构中添加一组布尔掩码，该掩码为每个标记定义了对应于已标记/未标记的值。借助这些掩码，我们能够以常数时间反转 n-Gmap 所有 darts 的标记值。这对于在我们知道它们全部被标记时取消 n-Gmap 所有 darts 的标记非常高效。

### 4.4.2 迭代器

正如我们之前所见，cell 是通过轨道概念定义的。因此，能够遍历给定 n-Gmap 的给定轨道所属的 darts 非常重要。幸运的是，这可以通过算法 7 轻松实现。该算法是通用的，因为它允许遍历任意轨道 ⟨αᵢ₁, …, αᵢₖ⟩(d)

在主循环期间第二次在取消标记步骤期间），并且所有操作都是原子操作。

算法 7 例如可以用序列 (0, ..., i − 1, i + 1, ..., n) 来使用，以便遍历包含给定 dart 的 i-cell c_i(d) 的所有 darts，对于任意 i ∈ {0, ..., n}。例如，我们可以使用序列 (0, 1, 2) 来遍历包含给定 dart 的 3-Gmap 中的体积的所有 darts。

请注意，该通用算法可以在若干特定情况下通过使用 n-Gmaps 的属性进行优化。例如，我们可以避免使用栈 P 来遍历 3-Gmap 中面的 darts，因为存在允许遍历这些 darts 的线性顺序：例如，给定 dart d，我们依次应用 α0 和 α1 以遍历轨道 ⟨α0, α1⟩(d)，然后对 d 应用 α3，并再次依次应用 α0 和 α1。这项优化基于 α0 ∘ α3 和 α1 ∘ α3 都是对合的事实。其他轨道的遍历也可以出于类似原因以这种方式进行优化。

该算法是若干其他算法的基础，这些算法允许根据关联和邻接关系遍历某些特定 cell。我们通过展示三个有用的示例来说明这一点。在第一个示例中，详细说明在算法 8 中，我们遍历 n-Gmap 的每个 i-cell 的一个 dart。该算法允许我们恰好处理每个 i-cell 一次。

**算法 8：n-Gmaps 的每个 i-cell 的一个 dart 的迭代器**

**输入：** gm：一个 n-Gmap；i ∈ {0, ..., n}。

**结果：** 遍历 gm 的每个 i-cell 的一个 dart。

```text
1  ma ← reserveMarkNGMap(gm);
2  foreach dart d ∈ gm.Darts do
3      if not isMarkedNGMap(d,ma) then
4          // process dart d
5          mark all the darts in c_i(d) for ma;
6  unmark all darts for ma;
7  freeMarkNGMap(gm,ma);
```

算法 8 遍历 n-Gmap 的所有 darts，并且对于每个未标记的 dart d，它会为 ma 标记包含 d 的 i-cell c_i(d) 的 darts。请注意，这些 darts 是通过使用序列 (0, ..., i − 1, i + 1, ..., n) 的算法 7 进行标记的。为了优化算法，我们在算法 7 中使用算法 8 中预留的相同标记 ma（事实上，由于第 5 行的目标是标记 c_i(d) 中的所有 darts，因此在迭代器中为这些 darts 使用局部标记并在迭代器结束时取消标记这些 darts 是无用且低效的）。在算法 8 结束时，我们需要取消标记所有已标记的 darts。这里我们处于 n-Gmap 的所有 darts 均被标记的情况，因此我们可以简单地否定标记 ma 的掩码。

算法 8 的复杂度与 n-Gmap 的 dart 数量成线性关系，因为每个 dart 都在第一个循环（算法第 2 行）中被考虑，因此每个 dart 在第 5 行中恰好被标记一次。

第二个示例给出的算法 9 是在给定两个维度 i 和 j 且 i ≠ j 的情况下，遍历与给定 j-cell 关联的每个 i-cell 的一个 dart。

**算法 9：n-Gmaps 的与 j-cell 关联的每个 i-cell 的一个 dart 的迭代器**

**输入：** gm：一个 n-Gmap；d ∈ gm.Darts：一个 dart；i ∈ {0, …, n}；j ∈ {0, …, n}；且 i ≠ j。

**结果：** 遍历与 c_j(d) 关联的每个 i-cell 的一个 dart。

```text
1  ma ← reserveMarkNGMap(gm);
2  foreach dart e ∈ c_j(d) do
3      if not isMarkedNGMap(e,ma) then
4          // process dart e
5          mark all the darts in c_i(e) for ma;
6  unmark all marked darts for ma;
7  freeMarkNGMap(gm,ma);
```

该算法与前一个算法类似，只是将对 n-Gmap 所有 darts 的循环替换为对 c_j(d) 所有 darts 的循环（通过使用算法 7 实现）。根据 n-Gmaps 中关联的定义，我们可以确定在此循环期间我们至少会发现每个关联 i-cell 的一个 dart，并且通过使用标记，我们确保每个 i-cell 只被处理一次。为了取消标记所有已标记的 darts，我们通过反转已标记和未标记 darts 的角色来重用相同的算法。

该算法的复杂度与遍历期间发现的 dart 数量成线性关系，即与 c_j(d) 的 dart 数量加上关联 cell 的 dart 数量成线性关系。

最后一个示例给出的算法 10 允许遍历与给定 i-cell 相邻的每个 i-cell 的一个 dart。

再次我们使用与前两个示例相同的原理，但在这里，我们必须为每个 e ∈ c_i(d) 测试 dart α_i(e)。事实上，由于 n-Gmaps 中邻接关系的定义，我们知道 c_i(d) 的所有相邻 i-cell 都可以通过此类 dart 到达。

**算法 10：n-Gmaps 的与 i-cell 相邻的每个 i-cell 的一个 dart 的迭代器**

**输入：** gm：一个 n-GMap；d ∈ gm.Darts：一个 dart；i ∈ {0, ..., n}。

**结果：** 遍历与 c_i(d) 相邻的每个 i-cell 的一个 dart。

```text
1  ma ← reserveMarkNGMap(gm);
2  foreach dart e ∈ c_i(d) do
3      if not isMarkedNGMap(e.Alphas[i], ma) then
4          // process dart e.Alphas[i]
5          mark all the darts in c_i(e.Alphas[i]) for ma;
6  unmark all marked darts for ma;
7  freeMarkNGMap(gm,ma);
```

到达其结束位置（即遍历结束）。下一节中给出的一些算法使用这种类型的实现（例如第 121 页的算法 19 和 20）。

### 4.4.3 基础工具

我们现在提出实现第 4.2 节中定义的基础工具的算法。

**算法 11：isFreeNGMap(d,i)：测试 dart 对 n-Gmaps 是否为 i-自由**

**输入：** d：一个 dart；i ∈ {0, ..., n}。

**输出：** 当且仅当 d 为 i-自由时为 True。

```text
1  return d.Alphas[i] = d;
```

添加孤立 darts 和删除孤立 darts 的算法是直接的，因为它们只是在 darts 集合中添加或删除元素。在算法 12 中，当我们创建一个 dart 时，我们将所有 α 链接初始化为新 dart 本身，以便它在所有维度上都是 i-自由的。此外，我们将其所有标记初始化为 false，以便它对所有可能的标记都是未标记的。

请记住，删除 dart 操作只能应用于孤立 darts。因此算法 13 以孤立 dart 作为输入并将其从 darts 集合中删除。测试 d 是否孤立很容易：我们测试 d 是否对所有 i ∈ {0,...,n} 都是 i-自由的。

这三个算法的复杂度为常数时间，因为 n 和

