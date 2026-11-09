
## 3.4 采样

超大数据集会给计算资源带来沉重负担。因此，人们开发了一些方法：这些方法并不必检查所有数据的成对关系，而是对成对关系进行采样，并基于采样结果形成整个数据集的划分。这种聚类形式类似于蒙特卡洛积分，其中会涉及伪随机采样和准随机采样的概念。它还基于一个简单事实：如果数据项 A 与数据项 B 非常不相似，而数据项 C 与数据项 B 非常接近，那么可以推断数据项 A 与数据项 C 也非常不相似。如果已经计算了 A 与 B、B 与 C 之间的不相似性关系，那么可能无需计算 A 与 C 之间的不相似性。随机选择一个数据项，确定其余所有数据项相对于它的不相似度值。将处于某个近邻阈值以内的那些项纳入，令其成为一个簇，然后将它们从后续考虑中排除。对剩余数据项重复此过程，以类似方式形成所有后续簇。由于我们排除了第一个簇中的项，而没有确定它们与任何其他项的不相似性，但只对随机选中的那一项进行了确定，因此有 $k \times (N - k - 1)$ 个不相似度无需计算，其中 $k$ 是排除区域中的项数减去随机选中的那一项。在每次迭代中，簇成员的数量很可能会变化，但原则上计算的不相似度数量仅为 $O(G \times N)$，其中 $G$ 是簇的数量，而不是生成所有成对不相似度所需的 $O(N^2)$ 计算。

```text
Algorithm 3.4 SimpleLeader(Data, Threshold)
1: DataElement ← SampleRandom(Data) //Arbitrarily choose a data element from the data
2: Data ← Data \ DataElement //Remove DataElement from Data
3: Append(DataElement, C) //Append the DataElement to first cluster, C
4: repeat
5:    C ← Append(FindNN(Data, Threshold, DataElement), C) //Append NNs to cluster, C
6:    Append(C, G) //Append cluster C to set of clusters G
7:    Data ← Data \ C //Remove cluster elements from data
8:    DataElement ← SampleRandom(Data) //Arbitrarily choose a data element from the data
9: until |Data| == 0
10: Output : G
```

在另一种簇采样形式中，会计算所有成对不相似度，但只存储其中一小部分值，并由另一种聚类采样算法对这些值进行操作。也就是说，如果存在一个不相似度阈值，并且我们知道不关心该不相似度阈值之外的分组，那么我们可以选择不存储这些值，也不在聚类过程中对它们进行操作。尽管所有成对不相似度都已计算，但由于需要处理的不相似度值集合小得多，聚类采样算法很可能会快得多。排除区域算法的一个特点是，它们往往会产生大量单例（即每个簇只有一个成员的簇）。在该算法下，单例分为两类：一类是在给定阈值下不靠近任何其他数据元素的单例；另一类是处于某个或多个邻居的阈值之内，却被排除在任何排除区域之外的单例。这些*伪单例*可以被收集起来，并分配到某个排除区域簇中，只要它们在该簇的阈值内存在最近邻。

```text
Algorithm 3.5 ExclusionRegion(SparseMatrix)
1: repeat
2:   C ← FindLargestSetNN(SparseMatrix) // Assign largest row in matrix to cluster, C
3:   SparseMatrix ← SparseMatrix \ C // Remove row and its elements from the matrix
4:   Append(C, G) // Append cluster C to set of clusters G
5: until SparseMatrix == NULL
6: Output : G
```

## 3.5 重叠

在许多情况下，由于数据所表示的度量或空间，组或类会相互混杂并发生重叠。考虑图 3.9。假设该散点图中的数据表示按点标记显示的四个真实类别。这些类别发生重叠，边界用围绕每个类别的凸包表示，然而我们的互斥算法会将其划分为四个组，忽略类别的重叠。如果允许在一定程度上放松互斥约束，我们或许能够得到重叠簇，从而依据以这种重叠方式描述数据的数据特征和度量，更好地定义这些类别。

在某些情况下，相关领域的专家可能更偏好重叠簇而不是互斥簇，因为某些数据项的归属存在歧义，或者某些数据项可能很容易具有多个类别归属。例如，考虑在分类学中有时无法确定一个生物体属于哪个类群。与其强行作出类别判定，不如表示该生物体属于多个类群的不确定性，这可能更有用。有些聚类算法返回的结果正是如此。在许多情况下，返回互斥簇的算法可以被修改为返回重叠簇。

在假设伪单例可能在多个排除区域中都有最近邻的前提下，可以将通用的排除区域算法 3.5 修改为产生重叠簇。有人可能会认为，最好将伪单例分配到其最近邻所在的排除区域。这样确实会产生互斥区域。然而，对于离散度量，最近邻值可能存在并列。这种歧义可用于产生重叠簇。图 3.10 显示了参与重叠的数据集比例与所应用 Tanimoto 阈值的关系。对三种不同的指纹进行了比较，其中最短的基于键的指纹显示，数据集中参与重叠组的比例最大。

```text
Algorithm 3.6 ExclusionRegionOverlapping(SparseMatrix)
1: repeat
2:     TiedRows ← FindLargestSetsNN(SparseMatrix) //Find largest row(s)
3:     i = 1
4:     repeat
5:         C ← AssignClusters(TiedRows[i]) //Assign rows to cluster non-disjoint clusters
6:         Append(C, G) //Append cluster C to set of clusters G
7:         i = i + 1
8:     until i == |TiedRows| //Repeat until largest tied rows processed
9:     SparseMatrix ← SparseMatrix \ TiedRows //Remove row and its elements from the matrix
10: until SparseMatrix == NULL
11: F ← FindFalseSingletons(SingletonClusters(G))
12: G' ← DistributeFalseSingletons(F, G) //Distribute false singletons to any cluster with a NN
13: Output : G'
```

由于重叠簇是一种覆盖而不是划分，任何显著重叠都可能在组合上呈爆炸式增长。如果各组在阈值尺度上分离良好，那么歧义会非常小；在实践中，这种情况下大多数重叠只涉及少量伪单例，或许还涉及少量大小相同的重叠组。

## 3.6 模糊

模糊聚类与重叠簇原理相关，但与上一节所述的简单重叠聚类不同，数据元素在其可能所属的那些簇中具有隶属度。有时将隶属度视为概率是有用的，但并不一定需要按这种意义来考虑。模糊聚类有点类似于 K-means，它尝试在某些准则下，迭代地细化对那些最相似组的隶属度或隶属概率。因此，例如在迭代次数结束时，许多数据元素对大多数簇的隶属度非常小或为零，只有少数几个簇的各自隶属度显著，甚至仅对单个簇具有排他性。可以根据数据项各自最高的最终隶属系数将其分配到互斥簇，也可以利用这些系数将其归属于多个簇，从而形成覆盖而不是划分。

```text
Algorithm 3.7 Fuzzy(Data,K,Threshold)
1: U ← FEmptyLists(K)
2: M' ← AssignMembership(Data,K) //Assign memberships
3: repeat
4:   M ← M'
5:   U ← FindCenters(Data,M,K) //Find the cluster centroids
6:   M' ← ComputeMembership(Data,U) //Compute memberships to current cluster
7: until MembershipDifference(M,M') < Threshold
8: G ← AssignGroups(M) //From final membership, M, assign groups to G
9: Output: G, M
```

模糊聚类通常有一个学习参数，该参数在一定范围内多少有些任意，甚至可以在迭代过程中更新和改变。这类调优参数也出现在下一节关于自组织聚类方法的内容中。它们给这些方法带来一种近乎难以名状、颇具艺术感的感觉，因为需要确定输入哪些初始值和后续值才能得到有用的聚类结果。这些方法可以相当快速地收敛，并高效地得到合理的解，但它们通常不够快，无法用于非常大规模的聚类。

## 3.7 自组织

自组织聚类算法要么使用预设数量的簇或节点，要么生成簇（不一定是预定义的），其中簇由数据自适应得到。自组织（SO）算法的主要区别在于：它们针对各个数据项调整许多（可能是全部）簇节点或它们的邻域，而不是像 K-means [158] 那样仅仅根据近邻计算质心作为响应。

在生物信息学中大量使用、并在一定程度上也用于药物设计的最流行的自组织算法是 SOM（自组织映射）。

