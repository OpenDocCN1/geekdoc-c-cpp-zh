
```
Algorithm 4.4 OnlineKmeans(DataStream, K, λ)
1: 𝒢 ← KEmptyLists()
2: M ← ArbCenters(Data, K) //Find K arbitrary centers
3: repeat
4:   j ← FindNN(DataStream_i, M) //Find NN in M of newest data item
5:   M ← UpdateCenter(M_j, DataStream_i, λ) //Update M_j with Equation 4.1 and store in M
6:   𝒢 ← UpdateGroup(j, DataStream_i) //Update 𝒢 with corresponding new data item
7: until DataStream == ∅
8: Output: 𝒢, M
```

## 4.2 Jarvis-Patrick

Jarvis-Patrick算法有两种基本形式，它们基于对生成最近邻表以形成划分时所施加的约束。最基本的约束是要考虑的最近邻表的总体长度K。也就是说，在聚类组装过程中，只考虑最多K个最近邻。下一个约束是K_min，其中K_min ≤ K，且K_min ≥ 1。任意两个各自的K长度近邻列表之间，至少要有K_min个近邻匹配，才能属于同一个簇。这两个约束都会带来邻近性平局的问题，导致聚类模糊性，这将在第9章中讨论。

下面的算法4.4概述了简单的Jarvis-Patrick(K, K_min)版本。必须在FindNN(Data, K)中找到所有行的K个近邻，这需要对每一行进行排序，整体复杂度为O(N^2 log N)——或者调用K次min()。当然，如果K > log N，这也没有帮助。在最坏情况下，朴素算法必须额外搜索O(KN^2)对。在实践中，K_min和K_max与数据的相互作用使得最坏情况不太可能发生。创建和排序近邻列表占了执行时间的大部分。该算法具有一种类似于最小生成树的近邻链式形式。因此，一方面，该算法不受某些算法产生的超球形（排斥区域算法）或超矩形（递归划分区域）区域的限制，但由于链式过程在一定程度上是局部化的，它通常会产生许多单点簇。该算法在化学信息学中常被用于相当大规模的聚类[120]。FindNN(Data,K)是高度并行的，但Jarvis-Patrick的核心部分不是。因此，通过并行化来扩展算法以适应非常大的数据集的努力是有限的。然而，数万级别的中等规模近邻表用Jarvis-Patrick处理是相当可行的。因此，对于这种规模的数据集，它是一个方便的工具箱算法，即使仅仅是为了与其他算法结果进行比较。

为了了解该算法如何处理非常小的真实数据样本，将一组苯二氮卓类化合物中12种化合物的SMILES字符串转换为每个768位的基于键的指纹，然后用Tanimoto相似性度量进行比较。相似性度量值见表4.1。第一列到第十二列的每一行都可以看作是一个未排序的近邻表。近邻列表行中的粗体单元格表示K=5的最近邻；具有相同相似性得分的单元格是位于K=5约束处的平局；带下划线的单元格编号是位于K=5约束内的邻近性平局。比较值的精度被截断以方便地放入表中，但这些邻近值实际上是精确的有理数，粗体和带下划线的值确实是邻近性平局。

表中的最后一列包含K=5的最近邻索引列表。Jarvis–Patrick在K=5和K_min=3时生成的聚类为(1, 10, 11)、(2, 3, 4, 5, 6, 7, 8, 9)和单点簇(12)。读者可以检查表的最后一列，并识别产生这三个簇的K_min=3约束。注意，索引12不在任何K=5列表中。将K_min改为K_min=2会产生以下聚类：(1, 3, 4, 5, 10, 11)、(2, 6, 7, 8, 9)和单点簇(12)。这一变化将数据元素3、4和5移入第一个簇。约束被放宽了，因为现在只需两个近邻匹配即可认为两行在同一簇中。同样，通过检查K=5列表，读者也可以自己组装出这些簇。

### 算法 4.4 Jarvis–Patrick(Data, K, K_min)

```
1: NNK ← FindNN(Data, K) //Create nearest neighbor table with K-length constraint
2: p ← 1
3: repeat
4:   i ← 1
5:   j ← i + 1
6:   C_p ← i //Add i to cluster C_p
7:   repeat
8:     if K_min criterion is met between (i,j) rows for all j in NNK then
9:       C_p ← j //Add j to cluster C_p
10:      RemoveRow(NNK, j) //Remove the jth row from NNK
11:    else
12:      j ← j + 1
13:    end if
14:  until j > RowLength(NNK)
15:  RemoveRow(NNK, i) //Remove the ith (first) row from NNK
16:  p ← p + 1
17: until NNK = NULL
18: Output: C //Return set of clusters C
```

第二种常见的Jarvis-Patrick变体去掉了最近邻列表的长度K，并用百分比P_min取代K_min约束，P_min是两个最近邻之间需要匹配的最少最近邻百分比，才能被认为属于同一个簇。

### 算法 4.5 Jarvis–Patrick(Data, P_min, Threshold)

```
1: NNK ← FindNN(Data, Threshold) //Create nearest neighbor table at a (dis)similarity threshold
2: p ← 1
3: repeat
4: i ← 1
5: j ← i + 1
6: C_p ← i //Add i to cluster C_p
7: K_min ← min(length(NNK(i)), length(NNK(j))) //K_min constraint min of row lengths of i and j
8: repeat
9:   if P_min criterion is met between (i,j) rows for all j in NNK then
10:     C_p ← j //Add j to cluster C_p
11:     RemoveRow(NNK, j) //Remove the jth row from NNK
12:   else
13:     j ← j + 1
14:   end if
15: until j > RowLength(NNK)
16: RemoveRow(NNK, i) //Remove the ith (first) row from NNK
17: p ← p + 1
18: until NNK = NULL
19: Output: C //Return set of clusters C
```

## 4.3 谱聚类

谱聚类于1990年代末伴随图像处理被引入。例如，像素聚类是图像分割的重要部分，其中像素可以是RGB颜色向量，或卫星图像中常见的七个光谱带。这类问题可能相对较大，尽管维度通常很小，像素数量可达数十万或数百万，因此谱聚类通常用于小图像或较大图像的子集。幸运的是，计算相当大矩阵的特征值和特征向量是可能的，这使得谱聚类能够处理数千个数据项、维度较高的中等规模数据集，变得更加合理。因此，谱聚类已开始在化学信息学应用中使用，一些小组正在探索其在早期药物发现过程中对各种数据类型的有效性[18, 58]。

通常有两种方法，一种[103]与PCA或MDS非常相似，通过从相似度矩阵$A$计算拉普拉斯矩阵的k个特征向量来降低数据维度：

$$L = I - D^{-\frac{1}{2}} A D^{-\frac{1}{2}}, \tag{4.2}$$

其中对角矩阵$D$的第$i$个条目为$\sum_{j=1}^{N} A_{ij}$。维度的选择只需某个$k \in \mathbb{N}$，其中$k$个特征向量作为数据特征的列。这些非常类似于载荷或线性因子。变换后的数据再由任何聚类算法进行聚类，但最常用的是$K$-means。

另一种更有趣的方法[122]同样计算拉普拉斯矩阵，但基于第一和第二特征值递归划分数据，自下而上构建层次结构。

## 4.4 自组织映射

自组织映射是一种将$N$维空间非线性投影到特殊形式的二维表面的方法。该算法可以被看作是$K$-means与二维弹性或力导向MDS方法的结合。然而，该表面有一个特殊性质：它是一个环面——构成SOM的网格的边缘是环绕的。因此，沿边缘形成的簇与对侧边缘的簇密切相关。SOM有时被称为*拓扑有序映射*，因为它们试图将问题原始空间中的邻近关系保留到更简单的空间或拓扑中，而不一定是因为结果呈现为诸如环面之类的奇特拓扑对象。数据在环面投影上的网格中心被拉伸（符合弹性与拓扑隐喻）朝向单个数据点，但与$K$-means类似，只是靠近该点的网格中心。这个过程是迭代进行的，所有点都经过这个过程，直到达到指定迭代次数。因此，该算法的参数包括：每个点移动网格中心的程度；邻域大小定义接近程度；迭代次数。这里的“网格”是广义的，指简单的均匀平铺。例如，网格不必是正方形的，也可以是六边形的。SOM也像$K$-means一样对原始空间采样，并且擅长创建密集簇并将它们适当地放置在网格区域中。

SOM对输入参数特别敏感，在某些条件下可能在地图中产生不理想的扭结，此时学习是局部化的。此外，SOM对输入顺序敏感——输入顺序的改变可能导致累积的学习变化，从而导致不同的，
