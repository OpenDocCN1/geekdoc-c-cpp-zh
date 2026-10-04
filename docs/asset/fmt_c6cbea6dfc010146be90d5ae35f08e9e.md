
- 27. Nilantan, R., Bauman, N., Dixon, J., and Venkatarajan, R., Topological torsion: A new molecular descriptor for SAR applications. Comparison with other descriptors. J. Chem. Inf. Model. 1987, 27, 82–85.
- 28. Kier, L., A shape index from molecular graphs. Quant. Str.–Act. Rel. Pharmacol., Chem. Biol. 1985, 4, 109–116.
- 29. Labute, P., A widely applicable set of descriptors, http://www.chemcomp.com/journal/vsadsec.htm, last accessed August 2008.
- 30. Williams, A., A perspective of publicly accessible/open-access chemistry databases. Discov. Today 2008, 13, 495–501.
- 31. Haider, N., “checkmol/match,http://www.pc.ac.at/~haider/cmf.html, last accessed August 2008.
- 32. Cormen, T., Leiserson, C., and Rivest, R., Introduction to Algorithms. MIT Press, 1998.
- 33. Ullmann, J., An algorithm for graph isomorphism. JACM 1976, 23.
- 34. Sayle, R., IMPROVED SMILES, http://www.daylights.com/emg00/structure., 2000.
- 35. Ballester, P. and Graham, W., Ultrafast shape recognition to search compound databases for similar molecules. J. Chem. Comput. 2007, 28, 1711–1723.
- 36. Good, A., Ewing, T., Gschewend, D., and Kuntz, I., A new molecular descriptor—applications in database search. J.-Comput-Aided Mol. Dev. 1995, 9, 1–12.
- 37. Guha, R., Dur, J., P., and Chen, R-NN: An intuitive approach to outlier detection using a distance based method. J. Chem. Inf. Model. 2006, 46, 1713–1722.
- 38. Xu, H. and Afrafiot, D., Nearest neighbor search in metric spaces using a data structure with a simple heuristic. J. Chem. Inf. Comput. Sci. 2003, 43, 1933–1941.
- 39. Bentley, J., Binary search trees used for associative searching. ACM 1975, 8, 509–517.
- 40. Gionis, A., Indyk, P., and Motwani, R., Similarity search in high dimensions via In: VLDB ’97: Proceedings of the 25th International Conference on Large Data Bases, Morgan Kaufmann Publishers, Inc.: San Francisco, CA, 1999.
- 41. Guttman, A., Bohm, C., Berthold, S., and Mein, D., Searching in high-dimensional spaces: Indexes for improving the performance of multimedia databases. ACM Comput. Surf. 2001, 33, 322–373.
- 42. Wang, W., Yang, J., and Muntz, R., Information organization and databases: Foundations of data organization. In: Kluwer Information in Engineering and Computer Science Series, Kluwer Academic Publishers: Norwalk, MA, 2000; Chapter PK-tree: A Spatial Index for High-Dimensional Point Data, pp. 281–293.
- 44. Ciaccia, P., Patella, M., and Zezula, M., An efficient access method for similarity search in metric spaces. In: VLDB ’97: Proceedings of the 23rd International Conference on Large Data Bases, Morgan Kaufmann Publishers, Inc.: San Francisco, CA, 1997.
- 45. Hellerstein, J., Naughton, J., and Pfeffer, A., Generalized search trees for database systems. In: VLDB '95: Proceedings of the 21st International Conference on Very Large Databases, Morgan Kaufmann Publishers Inc.: San Francisco, CA, 1995.
- 46. Schmid, E.-G., 个人通信, 2008.
- 47. Warr, W., Workflow and pipelining in chemoinformatics, http://www.qsarworld.com/qsar-workflow1.php, 最后访问于2008年7月.
- 48. Oinn, T., Addis, M., Ferris, J., Marvin, D., Senger, M., Greenwood, M., Carver, T., Glover, K., Pocock, M., Wipat, A., and Li, P., Taverna: A tool for the composition and enactment of bioinformatics workflows. Bioinformatics 2004, 20, 3045–3054.

## 13 序列对算法

在糖链、树及类树结构中的应用

Akutsu 龙

- 13.1 引言 ................................................................................................ 363
- 13.2 树编辑距离与树对齐 ............................................................ 364
- 13.3 糖链结构 ....................................................................................... 368
- 13.4 基础算法 ........................................................................................ 369
    - 13.4.1 MCST 算法 ...................................................................... 369
    - 13.4.2 全局与局部序列对齐 ................................................... 370
- 13.5 KaCM 算法 ....................................................................... 371
    - 13.5.1 全局糖链对齐 .......................................................... 371
    - 13.5.2 局部糖链对齐 ................................................................ 373
    - 13.5.3 精确匹配算法 ................................................................ 374
- 13.6 伪代码 ............................................................................ 374
    - 13.6.1 全局糖链对齐代码 ........................................................ 374
    - 13.6.2 局部糖链对齐的修改 ............................................... 376
- 13.7 示例说明 ................................................................................ 376
- 13.8 KaCM Web 服务器 ....................................................................... 379
- 13.9 结语 ................................................................................................. 379
- 参考文献 ....................................................................................................... 380

## 13.1 引言

糖链（Glycans），也称为碳水化合物，是重要的生物分子。特别是它们对于多细胞生物的发育和功能至关重要，并且通常位于细胞表面。某些糖链在细胞相互作用中起着重要作用。例如，肿瘤细胞产生一些异常糖链，这些糖链会被自然杀细胞上的受体识别。某些糖链在与伴侣蛋白协助蛋白质折叠中也起着重要作用。

尽管糖链如此重要，但直到21世纪初，很少有用于分析糖链的计算方法。自21世纪初以来，生物信息学领域已经了糖链的重要性并开展了各种研究。其中一项重要研究是构建糖链数据库。基于对 CarbBank 数据库的早期工作，构建了一个名为 KEGG Glycan 的新可用数据库 [1]。随着数据库的建立，人们发现没有用于糖链相似性搜索的工具。因此，开发了一种名为 KCaM（KEGG糖类匹配器）的搜索工具 [2]， 以及针对糖链的算法 [3]。在搜索工具开发之后，又开发了多种机器学习或计算方法，包括用于糖链对齐的评分矩阵 [4]、用于糖链分类的概率方法 [5]、基于新开发的树核的分类方法 [6,7]、利用基因表达数据 [8] 和串联质谱数据 [9] 对糖链进行阐明。

由于本节的目的不是给出一个全面的综述，而是对糖链对齐算法进行详细说明，因此我们侧重于糖链对齐。在本节中，我们首先回顾编辑距离和树对齐算法，因为糖链通常被表示为树，而树算法是基于这些概念的。接下来，我们将简要回顾糖链结构。在回顾了基础算法之后，我们将给出糖链对齐算法（KCaM算法）[3]的详细描述，并附带伪代码和示例。最后，我们将简要回顾 KCaM搜索工具 [2]，并讨论算法的局限性和未来可能的进展方向。

## 13.2 树编辑距离与树对齐

树是计算机科学中常用的数据结构，是图的特例。比较树的问题出现在生物信息学、化学信息学、结构化文本数据库（例如XML数据库）和图像分析等各个领域 [10]。特别是，许多基于树的研究对 RNA 二级结构进行了比较 [11]。虽然树被分类为根树和无根树，但本节重点关注根树，因为糖链通常像 RNA 二级结构一样被表示为根树。

树 `T` 由一组节点 `V(T)` 和一组有向边 `E(T)` 组成。节点分为内部节点和叶节点，其中存在一个称为根的特殊节点。在本节中，我们只考虑标记树，每个节点都分配来自有限集合 `Σ` 中的一个符号。

每个内部节点都有一个出边，而每个叶子节点没有出边。对于每条边 `(u, v)`，`u` 被称为 `v` 的父节点，`v` 是 `u` 的孩子。对于每个节点，`Chd(u)` 表示子节点集。因此，当且仅当 `u` 是叶节点时，`Chd(u) = {}`。那么我们可以看到边集的定义如下：

`E(T) = {(u, v) | v ∈ Chd(u), u ∈ V(T)}`

![](img/686d0e92a65d05409e4dcd6592863b77_377_0.png)

**图 13.1** 删除和插入操作。例如，`T_2` 是通过删除标记为‘D’的节点从 `T_1` 得到的。相反，`T_1` 是通过插入标记为‘D’的节点从 `T_2` 得到的。

根树有两种类型：有序树和无序树。如果兄弟节点之间给定了从左到右的顺序，则树被称为*有序树*。否则，它被称为*无序树*。在有序树中，这种从左到右的顺序在匹配节点之间必须保持。

虽然已经提出了多种方法来评估两棵树之间的相似性，但*树编辑距离*得到了广泛的研究和应用。有序树的树编辑距离定义如下（细节见 [10]），我们只考虑单位代价（即每次插入、删除或替换的代价为1）。令 `T` 为一棵根树。`label(v)` 表示节点 `v` 的标签。`|T|` 表示 `T` 的大小（节点数）。树的*编辑操作*是指删除、插入或替换（亦见图13.1）。

- *删除*：删除 `T` 中的一个非根节点 `u`，其父节点为 `v`，使得 `u` 的子节点按照子序列顺序插入到 `v` 的位置。
- *插入*：删除的相反。在 `T` 中作为 `u` 的孩子插入节点 `v`，使其成为 `u` 连续子序列的一部分。
- *替换*：更改 `T` 中节点 `v` 的标签。

`T_1` 和 `T_2` 之间的树编辑距离定义为将 `T_1` 转换为 `T_2` 的最小操作数。

编辑距离与有序编辑距离映射（或简称映射）之间存在紧密的联系 [10]。`A ⊆ V(T_1) × V(T_2)` 被称为映射，当对于任意对 `(u_1, v_1), (u_2, v_2) ∈ A` 满足以下条件时（见图13.2）：

- i. `u_1 = u_2` 当且仅当 `v_1 = v_2`
- ii. `u_1` 是 `u_2` 的祖先当且仅当 `v_1` 是 `v_2` 的祖先
- iii. `u_1` 在 `u_2` 的左侧，`v_1` 在 `v_2` 的左侧

令 `id(A)` 为具有相同标签的对的集合。最大化 `id(A)` 的映射定义了最大公共子树*，它是通过以下得到的树

# 366

# 化学信息学算法手册

![](img/686d0e92a65d05409e4dcd6592863b77_378_0.png)

**图 13.2** 有序编辑距离映射的示例。在这个示例中，`T_2` 是通过从 `T_1` 中删除标记为 'D' 的节点、插入标记为 'F' 的节点以及替换根节点的标签而得到的。因此，`T_1` 和 `T_2` 之间的距离为二。相应的有序编辑距离映射由虚线表示。

从 `T_1`（或 `T_2`）中删除未出现在 `id(A)` 中的节点。众所周知 [10]，树编辑距离等于：

`|T_1| + |T_2| - |A| - |id(A)|`

这意味着最大公共子树的计算等同于树编辑距离的计算。`A` 也可以被看作 `T_1` 和 `T_2` 之间的**对齐**（alignment）。

这里我们回顾一种用于计算树编辑距离的动态规划 [10]。对于森林 `F_1`，令 `T_1(u)` 和 `u` 分别表示 `F_1` 最右侧的树及其根节点，其中森林是**根树的集合**，我们假设 `F_1` 中的树是从左到右排序的。那么，`T_1(u)-u`、`F_1-u` 和 `F_1-T_1(u)` 分别表示通过从 `T_1(u)` 中删除 `u`、从 `F_1` 中删除 `u` 以及从 `F_1` 中删除 `T_1(u)` 得到的森林。对于森林 `F_2`，`T_2(v)`、`T_2(v)-v`、`F_2-v` 和 `F_2-T_2(v)` 以类似的方式定义。然后，树编辑距离通过以下动态规划**过程**计算（见图 13.3）：

```
D(ε, ε) = 0
D(F_1, ε) = D(F_1 - u) + 1
D(ε, F_2) = D(ε, F_2 - v) + 1
D(F_1, F_2) = min
```
