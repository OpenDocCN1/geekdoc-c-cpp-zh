
从物理上不可能显式构造 $S$ 的所有元素，因为它们的数量远多于宇宙中的粒子数（估计为 $10^{82}$）。

**备注：** 在 Python 中，使用 `len(S)` 询问 `S` 的基数是很自然的。但这是不可能的，因为 Python 要求 `len` 的结果是 `int` 类型的整数；这可能导致溢出，并且不允许对无限集返回 `Infinity`。

```sage
sage: len(S)
Traceback (most recent call last):
...
OverflowError: Python int too large to convert to C long
```

### 15.2.2 整数分拆

我们现在考虑另一个经典问题：给定正整数 $n$，它可以有多少种方式写成正整数之和 $n = i_1 + i_2 + \cdots + i_\ell$？需要区分两种情况：

- 和中元素的顺序不重要，此时我们称 $\{i_1,\ldots,i_\ell\}$ 为 $n$ 的一个*分拆*；
- 和中元素的顺序重要，此时我们称 $(i_1,\ldots,i_\ell)$ 为 $n$ 的一个*有序分拆*。

我们从 $n = 5$ 的分拆开始；和之前一样，首先构造这些分拆的集合：

```sage
sage: P5 = Partitions(5); P5
Partitions of the integer 5
```

然后询问它的基数：

```sage
sage: P5.cardinality()
7
```

我们看看这 7 个分拆；由于顺序无关紧要，按照惯例，各项按降序排列。

```sage
sage: P5.list()
[[5], [4, 1], [3, 2], [3, 1, 1], [2, 2, 1], [2, 1, 1, 1],
[1, 1, 1, 1, 1]]
```

分拆数的计算使用 Rademacher 公式（见 http://en.wikipedia.org/wiki/Partition_(number_theory)），该公式用 C 实现并经过高度优化，因此非常快：

```sage
sage: Partitions(100000).cardinality()
2749351056977569651267751632098635268817342931598005475820312598430214
73281149641370505074016607336215901587744774296248940493063070200461792
7644930355116010793424571901557189435097253124661084520063695589344642
4871628782839821623450092628538314045970213071306745106244192273123899
9702284408609370935531629697851569569892196108480158600569421098519
```

整数分拆是组合对象，天然配备许多运算。因此，它们作为比简单列表更丰富的对象返回。

```sage
sage: P7 = Partitions(7); p = P7.unrank(5); p
[4, 2, 1]
```

```sage
sage: type(p)
<class 'sage.combinat.partition.Partitions_n_with_category.element_class'>
```

例如，它们可以用 Ferrers 图图形化表示：

```sage
sage: print(p.ferrers_diagram())
****
**
*
```

我们让用户通过自省来探索可用的运算。注意，我们也可以直接通过以下方式构造一个分拆：

```sage
sage: Partition([4,2,1])
[4, 2, 1]
sage: P7([4,2,1])
[4, 2, 1]
```

如果希望限制分拆各部分 $i_1,\ldots,i_\ell$ 的可能取值，例如在找零时，可以使用 `WeightedIntegerVectors`。例如，以下计算：

```sage
sage: WeightedIntegerVectors(8, [2,3,5]).list()
[[0, 1, 1], [1, 2, 0], [4, 0, 0]]
```

表明使用 2 美元、3 美元和 5 美元钞票凑出 8 美元，可以使用一张 3 美元和一张 5 美元，或一张 2 美元和两张 3 美元，或四张 2 美元。

整数有序分拆以同样的方式操作：

```sage
sage: C5 = Compositions(5); C5
Compositions of 5
sage: C5.cardinality()
16
sage: C5.list()
[[1, 1, 1, 1, 1], [1, 1, 1, 2], [1, 1, 2, 1], [1, 1, 3],
 [1, 2, 1, 1], [1, 2, 2], [1, 3, 1], [1, 4], [2, 1, 1, 1],
 [2, 1, 2], [2, 2, 1], [2, 3], [3, 1, 1], [3, 2], [4, 1], [5]]
```

上面的数字 16 似乎很重要，暗示存在一个公式。我们看看 $n$ 从 0 到 9 的有序分拆数：

```sage
sage: [ Compositions(n).cardinality() for n in range(10) ]
[1, 1, 2, 4, 8, 16, 32, 64, 128, 256]
```

类似地，如果按长度考虑 5 的有序分拆数，我们会发现帕斯卡三角形的一行：

```sage
sage: x = var('x'); sum( x^len(c) for c in C5 )
x^5 + 4*x^4 + 6*x^3 + 4*x^2 + x
```

上面的例子使用了一个我们尚未见过的功能：C5 是可迭代的，因此可以像列表一样用于 for 循环或推导式（§15.2.4）。

**练习 54.** 证明上述例子所暗示的关于 $n$ 的有序分拆数以及长度为 $k$ 的 $n$ 的有序分拆数的公式；通过自省调查 Sage 是否使用这些公式计算基数。

### 15.2.3 其他一些有限枚举集

本质上，对于想在 Sage 中进行组合数学研究的所有有限集，原理都相同；首先构造一个为该集合建模的对象，然后按照统一接口¹提供适当的方法。现在我们再给出几个典型例子。

¹ 或者至少情况应当如此；仍有许多角落需要清理。

整数区间：

```sage
sage: C = IntegerRange(3, 21, 2); C
{3, 5, ..., 19}
sage: C.cardinality()
9
sage: C.list()
[3, 5, 7, 9, 11, 13, 15, 17, 19]
```

排列：

```sage
sage: C = Permutations(4); C
Standard permutations of 4
sage: C.cardinality()
24
sage: C.list()
[[1, 2, 3, 4], [1, 2, 4, 3], [1, 3, 2, 4], [1, 3, 4, 2],
 [1, 4, 2, 3], [1, 4, 3, 2], [2, 1, 3, 4], [2, 1, 4, 3],
 [2, 3, 1, 4], [2, 3, 4, 1], [2, 4, 1, 3], [2, 4, 3, 1],
 [3, 1, 2, 4], [3, 1, 4, 2], [3, 2, 1, 4], [3, 2, 4, 1],
 [3, 4, 1, 2], [3, 4, 2, 1], [4, 1, 2, 3], [4, 1, 3, 2],
 [4, 2, 1, 3], [4, 2, 3, 1], [4, 3, 1, 2], [4, 3, 2, 1]]
```

集合划分：

```sage
sage: C = SetPartitions([1,2,3]); C
Set partitions of {1, 2, 3}
sage: C.cardinality()
5
sage: C.list()
[[{1, 2, 3}], [{1}, {2, 3}], [{1, 3}, {2}], [{1, 2}, {3}], [{1}, {2}, {3}]]
```

8 个元素集合上的偏序（偏序集），在同构意义下：

```sage
sage: C = Posets(8); C
Posets containing 8 elements
sage: C.cardinality()
16999
```

让我们画出其中一个偏序集（见图 15.2）：

```sage
sage: show(C.unrank(20))
```

![](img/99840d73c45ee58b635c4eedc727fd9a_354_0.png)

图 15.2 一个 8 个顶点的偏序集。

可以遍历所有图（在同构意义下）。例如，有 34 个具有 5 个顶点的简单图（图 15.3）：

```sage
sage: len(list(graphs(5)))
34
```

以下是如何画出所有至多 4 条边的图（见图 15.3）：

```sage
sage: for g in graphs(5, lambda G: G.size() <= 4):
....:     show(g)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_355_0.png)

图 15.3 — 具有 5 个顶点且至多 4 条边的简单图。

然而，这些图的集合 *C* 在 Sage 中*尚不*可用；因此，以下命令尚未实现：

```sage
sage: C = Graphs(5); C.cardinality()
34
sage: Graphs(19).cardinality()
24637809253125004524383007491432768
sage: Graphs(19).random_element()
Graph on 19 vertices
```

到目前为止我们看到的内容原则上也适用于有限代数结构，例如二面体群：

```sage
sage: G = DihedralGroup(4); G
Dihedral group of order 8 as a permutation group
sage: G.cardinality()
8
sage: G.list()
[(), (1,4)(2,3), (1,2,3,4), (1,3)(2,4), (1,3), (2,4), (1,4,3,2), (1,2)(3,4)]
```

或有限域 ℤ/2ℤ 上的 2 × 2 矩阵代数：

```sage
sage: C = MatrixSpace(GF(2), 2); C.list()
[
[0 0]  [1 0]  [0 1]  [0 0]  [0 0]  [1 1]  [1 0]  [1 0]  [0 1]
[0 0], [0 0], [0 0], [1 0], [0 1], [0 0], [1 0], [0 1], [1 0],
[0 1]  [0 0]  [1 1]  [1 1]  [1 0]  [0 1]  [1 1]
[0 1], [1 1], [1 0], [0 1], [1 1], [1 1], [1 1]
]
```

```sage
sage: C.cardinality()
16
```

**练习 55.** 列出三个变量中所有次数为 5 的单项式（见 `IntegerVectors`）。操作有序集合划分 `OrderedSetPartitions` 和标准表（`StandardTableaux`）。

**练习 56.** 列出大小为 3、4 和 5 的交错符号矩阵，并尝试猜测其定义（见 `AlternatingSignMatrices`）。这些矩阵计数公式的发现和证明（见方法 cardinality）由物理学中的行列式计算所推动，是一段相当精彩的故事。特别是，Zeilberger 在 1992 年给出的第一个证明是由计算机程序自动产生的。它长达 84 页，需要近百人来验证 [Zei96]。

**练习 57.** 手工计算 $(\mathbb{Z}/2\mathbb{Z})^5$ 中向量的个数，以及 $\mathrm{GL}_3(\mathbb{Z}/2\mathbb{Z})$ 中矩阵的个数（也就是说，系数在 $\mathbb{Z}/2\mathbb{Z}$ 中的可逆 $3\times 3$ 矩阵的个数）。用 Sage 验证你的答案。推广到 $\mathrm{GL}_n(\mathbb{Z}/q\mathbb{Z})$。

### 15.2.4 集合推导式与迭代器

我们现在展示 Python 为构造（以及遍历）集合提供的一些可能性，其记法灵活且接近通常的数学用法，特别是它在组合数学中带来的好处。

我们首先构造有限集 $\{i^2 \mid i \in \{1,3,7\}\}$：

```sage
sage: [ i^2 for i in [1, 3, 7] ]
[1, 9, 49]
```

然后构造同一个集合，但让 $i$ 从 1 到 9：

```sage
sage: [ i^2 for i in range(1,10) ]
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

这种形式的 Python 构造称为*集合推导式*。可以添加一个子句，只保留那些 $i$ 为素数的元素：

```sage
sage: [ i^2 for i in range(1,10) if is_prime(i) ]
[4, 9, 25, 49]
```

组合多个集合推导式，可以构造集合 $\{(i,j)\mid 1\leq j<i<6\}$：

```sage
sage: [ (i,j) for i in range(1,6) for j in range(1,i) ]
[(2, 1), (3, 1), (3, 2), (4, 1), (4, 2), (4, 3),
 (5, 1), (5, 2), (5, 3), (5, 4)]
```

或生成帕斯卡三角形：

```sage
sage: [[binomial(n, i) for i in range(n+1)] for n in range(10)]
```
