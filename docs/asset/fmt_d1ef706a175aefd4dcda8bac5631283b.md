
这种预处理特性被描述为适用于广泛的数据分布。直观地说，($L_p$) 距离的相对对比度随着维度的增加而减小。这种距离度量的集中效应降低了该度量在分类方面的效用。

## 距离集中与聚类

距离集中效应意味着，如果远邻和近邻属于同一个分布（且对分布的性质满足某些微弱条件），那么它们的距离是相似的。由于聚类涉及来自不同分布的数据，关键问题在于这些分布是否足够分离。在这种情况下，距离集中对于聚类的分离并不是一个问题。

Hinneburg 等人 [76] 研究了 $L_p$ 范数（即 $p \in \mathbb{N}$）在高维空间中的行为。作者们通过分析论证表明，$L_1$ 和 $L_2$ 是高维空间中唯一有用的范数。此外，他们还研究了利用投影进行区分的方法，其有效性取决于不满足距离度量三角形不等式的局部不相似性度量。Aggarwal 等人 [11] 在类似的背景下研究了分数的 $L_p$ 距离度量（$0 < p < 1$）。作者观察到，在高维设置下，$p$ 的较小值能提供更好的结果。

这些研究经常被用作高维数据专门方法的动机。然而，所有这些研究通常假设数据遵循单一分布。在这种情况下，距离集中对于聚类的分离并不是一个问题。

## 9.2.2 后果

维数诅咒的这第三、第四方面实际上是开发高维数据子空间聚类专门方法的主要动力，尽管这一点并不总是被认可。文献中经常对第二个方面的浅层提述偏离了要点。但尽管如此，所提出的方法（在某种程度上可能是无意中）实际上解决了第3和第4个方面的问题。

几十年来，研究一直关注无关（噪声）属性（有时称为掩盖变量 [53]）对聚类算法性能的影响 [100, 52, 59, 127]。它们讨论了如何识别哪些属性对聚类结构完全没有贡献。那么聚类任务应该集中在剩余的属性上。在某些情况下，属性的贡献可以是加权的，而不是离散的决策（贡献或掩盖）。这种问题的观点显然与降维 [66, 132] 有关。

我们在这里勾勒的子空间聚类领域是一个更复杂的视角。原因是降维作为聚类之前的第一步并不总能解决问题，因为属性的选择或属性之间的相关性通常是簇的特征，而不是完整数据的特征。换句话说，掩盖变量可能会掩盖某些簇，但可能有助于发现其他簇。

不同特征或特征的不同相关性在单个聚类解决方案中可能与不同的簇相关的现象，被称为“特征相关性”或“局部特征相关性”，其全局意义在于：它们仅为原始数据生成一个子空间，然后在该空间中进行聚类。局部特征相关性或特征相关性问题描述了这样观察：需要多个子空间，因为每个簇可能存在于不同的子空间。因此，聚类算法设计的关键要求是推导出某数据子集的特征，与在该空间内表现出显著相似性的数据集的某些启发式方法之间的交互——显然，两个任务（子空间确定 vs. 簇分配）之间的循环依赖，这在最基础的问题描述中已经存在了。

当比较不同维度的 $\epsilon$ 范围查询时，第5个方面就是一个问题，这在许多可用算法中都是这样做的。

## 9.3 高维数据子空间中的聚类任务

对于适用于高维数据的特定聚类算法的设计，上述勾勒的维数诅咒的所有方面都是相关的。然而，驱动子空间聚类的动力方法主要是无关属性（第3方面）和相关属性（第4方面）。这两种现象导致了不同类型的子空间，对具体算法提出了不同的挑战。

### 9.3.1 子空间的分类

#### 9.3.1.1 轴平行子空间

相关属性与无关属性的区分通常假设：相关属性在对应簇上出现值的方差与属性值的总范围相比很小，而无关属性在给定簇内的方差则很高（或与其他簇的相同属性值或背景噪声值无法区分）。例如，可以假设给定簇的相关属性服从标准差较小的正态分布，而无关属性在完整数据上呈均匀分布。这些假设的几何直觉涉及到：簇的点在无关轴的方向上是散乱的，而在相关属性上是紧密聚集的。当仅选择相关属性时（通过投影到子空间，即由这些属性跨越的子空间）时，该簇在子空间中将看起来像是一个全维簇。在全维空间（包括无关属性）中，簇点形成一个平行于无关轴的超平面。由于这种几何方法，这种类型的簇被称为轴平行子空间簇。

### 9.3.2 任意方向子空间

如果两个属性 $a_i$ 和 $a_j$ 对于一组点是线性相关的，那么这些点将沿着由这两个属性之间对应相关性的线性依赖定义的超平面分散。与该超平面正交的子空间是一个子空间，点在该$a_i$ 和 $a_j$ 组合值的方差上紧密聚集。该子空间是任意方向的，因此与轴平行子空间相比是更一般的情况。

### 9.3.3 特殊情况

上述子空间类型与上述讨论的维数诅咒有直接关系。需要注意的是，从现有算法的角度来看，存在特殊类型的子空间。事实上，有一大类算法被称为“双聚类”（bi-clustering）、“协同聚类”（co-clustering）、“双模聚类”（two-mode clustering）或“基于模式的聚类”（pattern-based clustering）[9]。

## 高维数据聚类

适当的子空间启发式方法。从开性的轴平行子空间聚类方法开始，研究了两种搜索子空间的相反基本技术，即自顶向下搜索 [12] 和自下向上搜索 [14]。

**自顶向下的子空间搜索。** 自顶向下方法的原理是从全维空间确定簇的子空间。这通常通过为一组点（簇成员）确定一个属性子来实现，使得这些点在投影到该子空间时满足聚类标准。显然，困境在于，为了确定一个簇，至少必须识别出[某些]簇成员。另一方面，为了确定聚类成员关系，必须知道每个簇的子空间。为了避免这种聚类依赖，自顶向下的方法依赖于一个相当严格的假设，这被称为*局部性假设* [90]。该假设认为簇可以从（临时）簇中心或（临时）簇成员在全维数据空间中的局部邻域推导出。换句话之，假设在全维空间中，每个簇的子空间可以从簇代表或簇成员的局部邻域中学习——如果子空间的维度并不小于数据的维度，这个假设可能是合理的。

其他不依赖局部性的自顶向下方法使用随机采样或启发式方法来生成潜在簇成员集。

**自下向上的子空间搜索。** 数据空间中所有可能的子空间的指数级搜索空间，等同于事务数据库领域市场篮子分析中频繁项集的搜索空间。例如，一个项集可能包含项目 *A, B, C* 等。`APRIORI` 算法 [15] 的核心思想是从大小为 1 的项集（“事务”）开始（包含某个项目，而不忽略事务中也包含的其他项目），并根据较小项集是频繁的知识，从搜索中排除那些不再频繁较大的项集。例如，如果一个 1-项集 *A* 不是频繁的（即我们对该项集的计数少于最小支持阈值），那么包含 *A* 的所有 2-项集、3-项集等（例如 **{A, B}*, **{A, C}*）都不可能是频繁的（因为项集 *A* 本身未满足最小支持阈值）。从理论上说，搜索空间仍然是指数，但在实践中搜索被大幅加速。

将项集问题转移到子空间聚类，每个属性代表一个项目，每个簇代表一个事务。频繁属性跨越相应的子空间。寻找属性等于找到所有包含至少一个簇的子空间的属性组合。这一观察是许多自下向上子空间聚类方法的原理。包含簇的子空间是通过采用类似于频繁项集挖掘算法的搜索策略，搜索所有包含至少一个簇的 1 维子空间来确定的。要应用任何频繁项集挖掘，聚类算法必须实现向下封闭属性（也称为单调性属性）：

如果子空间 S 包含一个簇，则任何子空间 T *⊆* S 也必须包含一个簇。

为了进行剪枝（即从考虑中排除特定的子空间），可以使用反单调逆推律。

- 如果子空间 T 不包含簇，则任何超集 S ⊇ T 都不可能包含簇。

请注意，存在不使用类似 `APRIORI` 搜索，而是使用其他启发式搜索的自下向上算法。

# 数据聚类：算法与应用

应用高效的子空间搜索策略解决了维度灾咒的第 1 个方面。选择相关的属性子集对应于维度灾咒的第 3 个方面。在将相似性度量适应局部邻域时，需要考虑第 2 个方面，且子空间在不同方法是不同的。第 5 个方面通常是这类方法的主要问题，因为单调性会在不同维度的子空间产生相同的距离阈值。

### 9.4.1 聚类算法

两种基本技术最初产生了两种“子空间”范式，被该领域的先驱命名为“子空间聚类” [14] 和“投影聚类” [12]。对于后者，出现了一种名为“软聚类” [82] 的变体。许多算法并没有明确属于这些类别之一。我们将一些示例列为“混合方法”。

**投影聚类。** 投影聚类的目标是找到元组 $(O_i, D_i)$，$O_i$ 是属于簇 $i$ 的对象集合，$D_i$ 是根据给定标准与 $O_i$ “相似”的属性子集。引入投影聚类任务的是 `PROCLUS`，一种质心算法。首先确定潜在簇集 $M$。在迭代细化过程中，对于每个质心，通过最小化每个维度上点的标准差来确定子空间。分配给最近质心的点通过替换为新质心进行细化。算法输出数据划分为簇（由质心表示）和（可能为空）噪声点。`PROCLUS` 的质心模型倾向于在其相应子空间产生球形簇。此外，由于可能的质心集 $M$ 是在随机过程中确定的，具有相同参数化的运行会导致不同的簇。`PROCLUS` 的变体例如 `BIT` [130] 和 `SSPC` [134]。`BIT` 使用启发式方法增强效率和聚类精度。`SSPC` 提供使用领域知识进一步增强的能力。`PreCon` 应用了基于密度的（全维）聚类算法 `DBSCAN` [46]，使用捕捉每个簇子空间的特殊度量。这种特殊距离的定义基于分配给点的子空间偏好：如果邻域内点的差小于用户定义的阈值 $\delta$，点之间的特殊距离为加权距离，其中子空间偏好的维度通过常数 $\kappa$ 加权，算法自动确定簇的数量并处理噪声。然而，`PreCon` 要求用户指定难以猜测的输入参数。特别是半径 $\epsilon$，在不同维度具有不同的含义（参见维度灾咒的第 5 个方面），但既用于全维空间中的局部邻域（局部性假设），也用于低维空间中的适应邻域。

## 高维数据聚类

`Tree` [96] 是一种展示该主题有趣变体的方法。其基本思想是为所有现有点以及在数据空间均匀分布的点分配一个类别标签，对其进行聚类。然后训练决策树来分离这两个类。结果是，属性独立、自适应且以灵活顺序进行划分。然而，选择划分基于信息增益评估，成本较高。此外，叠加数据的密度可能会严重影响结果。现有簇的分布是未知的，寻找合适的参数化似乎相当困难。另一个问题是相邻区域的合并。如果边界彼此不“接触”，簇就可以被分离。

**软聚类。** 有大量关于软聚类的文献 [43, 55, 79, 28, 42, 98]。这些是源自 k-means 聚类的有用优化方法，使用某些权重向量对属性进行加权。其中，在距离量上引入了 $i=1,\dots d$ 的权重 $w_i$：

$$\|x-y\|_p^p = \sum_{i=1}^{d} w_i |x_i - y_i|^p$$

通常，在这些方法中，权重至少满足条件

$$0 < w_i \leq 1,$$

即为了确保优化技术的适用性，没有任何属性被真正遗漏，因此结果聚类位于全维的尽管是倾斜的数据空间。聚类并非真实在投影空间中搜索（即没有为特定簇分配子空间）这一事实由“软”一词指示。然而，这些方法通常被命名为“子聚类”，这反映了这里讨论的差异。本质上，所有这些方法都可以看作 EM 聚类的变体 [40]。

从几何角度上看，这些方法的影响仅仅允许簇的形状变为轴平行椭圆。这并不一定考虑到不同属性的相关性或无关性。它更多地涉及到每个簇属性的某种归一化。

这些方法的示例是 `LAC`（局部适应聚类）[43]，它从 $k$ 个质心和 $k$ 组 $d$ 个权重（对应 $d$ 个属性）开始。算法通过调整权重来近似 $k$ 个高斯分布。

`COSA` [55] 是另一个显著示例，它并不定义聚类，而仅仅是一个可以被任意聚类算法使用的相似性矩阵。矩阵包含每个点的子空间偏好权重。`PreCon` 点 $p$ 的权重通过从 $p$ 的欧几里得 $k$ 近邻开始，并计算每个维度上的平均距离分布来确定。粗来说，给定属性的权重是点 $p$ 到其所有属性下的所有 $k$ 近邻距离之比。沿某个属性的 $k$ 近邻方差越大，分配给该属性的权重越高。然而，权重不能变为 0。只要向量权重发生变化，就会使用当前权重重新确定 $k$ 近邻，且邻居的数量是一个输入参数。与 `PreCon` 非常不同，权重可以取任意值，而不是两个固定值。此外，权重矩阵使用几种全维聚类算法进行测试，而不是集成到某个特定的算法中。注意，权重向量的影响在像 `PreCon` 这种预先未定义簇形状的密度方法中非常不同。

# 数据聚类：算法与应用

正如我们所见，这些方法忽略了高维数据中不同问题之间复杂的相互关系。因此，为了进一步参考，读者可以参考该方向的一些近期示例。尽管它们与我们在此概述的算法之间的联系和区别并不明确，但关于相关工作的详细章节非常适合作为该方向某些专门研究中提供的“软性”投影聚类方法历史的介绍 [79, 29, 82]。

**子空间聚类（Subspace Clustering）。** 从狭义上说，子空间聚类的目标是寻找特征空间中所有子空间中的所有聚类。这一目标显然被神化为这些方法所使用的自下而上的技术，该技术基于聚类的某些单调属性，允许应用 `APRIORI` 搜索。然而，子空间聚类的定义（在所有子空间中寻找所有聚类）与子空间搜索（自下而上，应用 `APRIORI` 搜索）之间的关系是历史性的，而非本质性的。无论采用什么方法，我们认为该问题视为一个引导类别。尽管如此，大多数方法都是对 `APRIORI` 搜索方法的某种改进。

在这一特定任务中，寻找所有子空间中所有聚类的先驱方法是 `CLIQUE` [14]，它使用基于网格的聚类方法。数据通过轴对齐网格被划分为宽度为 $\delta$ 的等大小单元。只有包含至少 $\tau$ 个点的单元被认为是稠密的。聚类被定义为稠密单元的最大集合。由于稠密单元满足向下封闭属性，因此可以以自下而上的方式高效地探索子空间聚类。对于所有的 1 维单元，通过类似于 `APRIORI` 的过程从 k 维单元计算出 (k+1) 维稠密单元。如果一个 (k+1) 维单元到某个 k 维单元的投影不是稠密的，那么该 (k+1) 维单元就不可能是稠密的。此外，引入了一种基于最小描述长度原理的启发式方法，以丢弃不感兴趣的子空间内的单元（即仅包含少量稠密单元的子空间）。通过这种方式，算法的效率提高了，但是以结果不完整为代价（即可能丢失某些真实的聚类）。

`CLIQUE` 有一些变体；让我们考虑三个著名的例子。`ENCLUS` [34] 方法也依赖于固定网格，用于可能包含一个或多个密度稠密单元的子空间。引入了三个子空间的质量标准，其中一个取代了向下封闭属性。子空间聚类的生成与 `CLIQUE` 类似。另一种名为 `MAFIA` [111] 的 `CLIQUE` 变体使用宽度为 $\delta$ 的重叠窗口的自适应网格作为网格的 1 维单元。

总结，所有基于网格的方法都使用了一种简单但相当高效的聚类模型。每个结果聚类的形状对应于相应子空间中具有轴对齐的多边形。显然，`CLIQUE` 及其变体的准确性和效率主要取决于网格的粒度和位置定位。更高的网格粒度会导致更高的运行时间需求，但可能会产生更准确的结果。

## 投影聚类 vs 子空间聚类

“投影聚类（projected clustering）”和“子空间聚类（subspace clustering）”术语在文献中的定义并不统一，但传统上，追溯到先驱方法 `CLIQUE` 和 `PROCLUS`，任务被区分如下：

投影聚类旨在对集合进行划分，其中每个数据点恰好属于一个聚类，且每个聚类被分配特定的属性子集。在这些属性上投影后，聚类遵循所应用算法定义的聚类标准。

## 高维数据聚类

子空间聚类旨在寻找所有子空间中的所有聚类。结果是，每个数据点可以同时属于许多聚类（即聚类在不同的子空间中可以发生大幅重叠）。这种方法在检索聚类时通常会导致冗余的聚类。

文献中的许多方法并没有明确地属于这些传统类别之一，研究中的观点倾向于认为更合适的问题描述应该位于这些原型类别之间的某个地方，允许聚类重叠，但限制聚类的冗余。最终，一个合适的聚类不应由算法定义，而应由领域特定的需求定义。

注意，这些类别与（或在早期方法中偶然）子空间研究的类别（自上而下 vs 自下而上）无关。

`SUBCLU` [84] 使用密度连接集的 `DBSCAN` 聚类模型 [46]。证明密度连接集使得 `DBSCAN` 能够以类似于 `APRIORI` 的样式在子空间中搜索基于密度的聚类。生成的聚类在相应的子空间可以是任意形状和大小。事实上，对于每个子空间，`SUBCLU` 放置了通过应用于该子空间的 `DBSCAN` 发现的聚类。与基于网格的方法相比，`SUBCLU` 实现了更好的聚类质量，但运行时间更高。

观察到，对某些密度阈值的偏向（如 `SUBCLU` 和基于网格的方法所使用的）会导致某种相似性（回顾维度的方面 5）。一方面，需要更严格的阈值来将低维子空间中的聚类从噪声区分开，并会在高维子空间中丢失聚类。另一方面，检测高维聚类的更宽松的阈值将产生过量的低维聚类。受此启发，问题的不确定性通过名为 `DISC` [18]（以及 Sim 等人 [19, 70, 100]）的聚类模型得到了解决。`DISC` 基于自适应维度的密度量。这种方法的一个主要缺点是缺乏反单调属性，因此无法进行搜索。因此定义了“弱密度”作为一种补救措施，提供了反单调属性。然而，这种补救再次引入了全局密度阈值，使得动机问题的预期解决方案失效。正如这个示例所示，维度诅咒始终困扰着搜索者。

聚类的初始公式——在所有子空间中寻找所有聚类 [14]——在许多论文后被采用是值得疑的，因为获取的大量聚类信息是没有用的。聚类的描述是基于项集的概念 [129]。什么构成良好的聚类在这里与算法的设计密切相关，即根据预期结果定义（与这有意义的相反）。

因此，随后的方法通常集中于通过减少聚类的冗余来限制结果聚类，以保持最高维度。相关方法旨在报告具有代表性的子空间聚类 [19]。Sim 对这些问题给出了更广泛的概述

让我们知道这些

**混合方法（Hybrid Approaches）。** 大多数方法不使用划分，而是追求某些 [117, 136]。通过这种方式，可以发现子空间聚类的层次（即低维聚类的信息是由高维聚类的属性子集组成的）。点与聚类之间的距离反映了由相应的聚类定义的维度。在 `COH` 中，权重是每个对象学习的，而不是整个聚类。然而，权重的学习基于单个属性，而不是整个特征空间。`DISH` 使用了一种受密度聚类算法 `OPTICS` 启发的算法。然而，`DISH` 扩展了 `OPTICS` 的聚类排序，以便发现子空间聚类的层次（一个低维子空间可能嵌入到多个高维聚类中）。

`HARP` [133] 是一种类似于单链聚类 [126, 121] 的层次聚类算法，但不产生子空间聚类的层次。从单元聚类开始，只要结果聚类具有最小数量的相关属性，`HARP` 就会迭代合并聚类。根据阈值引入了属性的相关性评分，该阈值具有严格的值并随着聚类的增大而逐渐降低。由于设计，`HARP` 在寻找低维聚类方面有问题。树图可以在任何层次切割。

`SCHISM` [120] 挖掘子聚类而不是聚类；因此它不是真正的子空间聚类算法，但解决了一个相关问题：寻找。它对数据库进行类似于网格的离散化，并应用带回溯的深度搜索来寻找有趣的子空间。

`FIRES` [87] 在第一步使用用户熟悉的任何聚类技术计算 1 维聚类。然后通过应用某种合并这些 1 维聚类。

# 聚类高维数据

簇的聚类（Clustering of clusters）由交点的数量定义。生成的簇代表了真实子空间簇的超矩形近似。作为一个可选的后期处理，这些近似可以通过任何聚类算法精炼为包含投影到相应子空间中的点。尽管 `FIRES` 使用了从自底向上的搜索策略，但它非常高效，因为它没有采用随数据空间维度呈多项式比例增长的最坏情况穷举搜索启发式方法。然而，用户可能需要牺牲聚类准确性来换取这种性能提升。目前无法指定 `FIRES` 产生的簇是否可能重叠，这在一定取决于框架中间步骤使用的聚类算法。通常情况下，簇可能会重叠，通常 `FIRES` 不会产生所有子空间中的所有簇。

`P3C` [102, 103] 从 1 维簇开始，这些簇可能近似于维数子空间簇。这些簇通过类似于 `APRIORI` 的自底向上搜索策略进行合并。由这种合并过程产生的最大维簇近似被称为簇核心（cluster cores）。在精炼步骤中，使用类似于 EM 的聚类过程对簇进行精炼。每个簇被视为 EM 算法的初始簇。使用马哈拉比距离将点分配给簇核心。`P3C` 的最终输出是一个矩阵，它记录了每个数据点属于每个投影簇的概率。从该矩阵中，可以通过将每个点分配给概率最高的簇，获得数据点到簇的不交划分。如果允许簇重叠，则每个点可以被分配给概率大于 $1/k$ 的簇。`P3C` 不像 `APRIORI` 风格的算法那样产生子空间中的所有簇，但报告了使用 EM 进行的最终聚类计算结果。

Moiser 和 Sander [101] 首次尝试将恢复显著子空间簇转化为一个优化问题。此外，作者还提出了一种迭代算法 `STATPC`，用于为该优化问题搜索局部优化解。

最近一些有趣的进展将集成聚类（ensemble clustering）[58] 的技术与子空间聚类的思想相结合，产生了“子空间聚类集成”（subspace clustering ensembles）41]或“投影聚类集成”64, 63, 62]。

## 9.4.2 任意方向子空间中的聚类

### 9.4.2.1 簇模型

相关性簇模型（即位于任意方向子空间中的簇）可以基于线性方程组，该组描述了包含相关性簇 $C \in \mathbb{R}^d$ 中点的 $\lambda$ 维超平面。该方程组由 $d-\lambda$ 个关于点和亲性的方程组成，每个方程由所有簇成员的平均点 $x_c = (x_i \cdot x_c)$给出：

$$v_{1(\lambda+1)} \cdot (x_1 - x_c) + v_2 \cdot (x_2 - x_c) + \dots + v_{\lambda+1} \cdot (x_{\lambda+1} - x_c) = 0$$
$$v_1 \cdot (x_1 - x_c) + v_2 \cdot (x_2 - x_c) + \dots + v_d \cdot (x_d - x_c) = 0 \ (9.5)$$

其中 $v_{ij}$ 是从 $C$ 的协方差矩阵推导出（例如通过主成分分析 (PCA) [83]）的特征向量矩阵 $V_C$ 中第 $i$ 行第 $j$ 列的值。前 $\lambda$ 个特征向量（也称为强特征向量）提供了高方差的方向并跨跨包含 C 的超平面。剩余的 $d-\lambda$ 个弱特征向量代表垂直子空间。相应的线性方程组也可以给出：

$$\hat{V}_C^c \cdot x = \hat{V}_C^c \cdot x_c \ (9.6)$$

$V_C^T$ 的亏亏（defect）给出了自由属性的数量，剩余的可能涉及线性相关。根据构造，该方程组对于所有点 $x \in C$ 至少是满秩的，因此为簇提供了定量模型 [5]。簇偏离平面的允许偏差程度以及评估方法随方法而异。因此，在任意聚类的领域，未来的研究也应该考虑更精细、更复杂的模型。

## 9.4.2.2 基础技术与示例算法

寻找包含簇的定向子空间的基础技术是主成分分析 (PCA) 和霍夫变换（Hough-transform）。这种通用聚类算法的第一种方法是 `ORCLUS` [13]，它使用了类似于轴对齐方法 `PROCLUS` [12] 的思想。`ORCLUS` 是一种类似于 k-means 的方法，在开始时选取 $k_c > k$ 作为种子，根据基于相应簇子空间特征系统的距离函数将数据对象分配到这些种子（即簇对象表现出高密度的投影子空间中的距离）。特征系统迭代地自适应更新后簇的当前状态。通过合并成对来迭代地减少簇的数量 $k_c$，直到达到用户指定的 $k$。最近的簇对是合并后的簇在投影空间（由弱特征向量跨越）中平均距离最近的对。从较大的参数 $k_c$ 值开始 $k_c$ 可以增加有效性，但也会增加运行时间。

与 `ORCLUS` 相反，算法 [32] 基于基于密度的聚类范式 [48]。因此，在簇从种子生长并满足密度标准之前，簇的数量是不预先决定的。否则，选择另一个种子开始一个新簇。密度标准是点邻域内必须满足的最少点数。`P3C` 不像 `APRIORI` 风格算法那样产生子空间中的所有簇，但报告了使用 EM 进行的最终聚类计算结果。

如前所述，任意方向子空间的聚类方法也被称为“相关性聚类”（correlation clustering）[32, 141]。但需要注意的是，该术语在机器学习中指的是一个完全不同的问题，在该问题中，数据的划分尽可能与从过去数据中学习的成对相似性函数 $f$ 保持[22]。

## 9.5 开放问题与当前研究方向

一些有趣的研究方向在 KDD 2010 [50] 的“发现、总结和使用多聚类”（MultiClust）工作会系列、ECML/PKDD 2011 [109] 以及 SDM 2012 [1110] 上引起了关注。有趣的是，子空间聚类问题与其它领域（如集成聚类、替代聚类或多重聚类）的问题相似[93]。这些领域共同存在的问题包括：(i) 如何处理聚类方案的多样性（多样化的聚类方案应该被统一还是分别展示？），(ii) 如何向聚类算法用户有效地总结和展示密度，(iii) 如何处理簇的冗余性，以及如何评估多个聚类方案之间的相似性。与子空间聚类起源的祖父频繁模式匹配的关系，已从这些领域研究的较新视角进行了讨论[94]。

正如我们所指出的，子空间聚类结果的冗余性继承自最早方法的自下而上策略，该策略来源于频繁模式匹配。对于当前的子空间聚类研究，消除过多的冗余是一个主要课题[70, 105]。多重聚类[28, 36, 80, 72] 的研究似乎从相反的方向处理这一问题，但关注的是相同的问题，即允许某些冗余，以排除可能有趣的概念，尽管它们可能与其他簇有部分重叠。相关的思路包括通过直接评估不同划分之间的某种距离概念来解决不同簇的判别性问题（即所谓的替代聚类方法）[60, 61, 21, 38, 19, 37, 116]。

一个与冗余问题的问题涉及适当的密度水平。这也是基于密度的聚类中的一个通用问题[81]，但对于子空间聚类，这个问题变得更加严重。对于 APRI 风格的空间搜索，固定密度阈值并不适用于所有可能的子空间。例如，考虑 `CLIQUE` 风格的网格方法：超立方体的体积随维度的增加呈指数增长；密度降低。因此，任何选择的阈值都需要识别（最多）特定维度的簇。这促成了对自适应密度阈值的研究[18, 106]。在使用欧几得距离（$L_2$）时，e 范围的适当选择也变得极具挑战性，不仅对于子空间，对于任意方向聚类也是如此，因为超球体积随维度增加而呈现出的反直觉行为。以对象数量或半径 $k$ 个最近邻作为 e 范围查询的邻域大小被提倡为解决这一问题的方法[7]，以至少解决某些方面，例如为密度估计定义良好的（非空）对象集，或估计邻域的空间特征。

任意方向聚类中一个相当的问题是任意方向簇的显著性。（如上所述，对于轴对齐子空间聚类，至少已经采取了一些步骤[101]）。此外，对于重叠簇（子空间聚类中的常见问题，但在其他领域也是如此），目前尚无适当的评估方法。不同的评估方法各不相同，且都忽略了某些要求。这个问题由 Färber 等人[49] 进行了概述并进行了更详细的讨论。文献中仅能找到改进评估方法论的一些初步步骤[115, 92, 66, 9]。

因此，文献中仍然缺乏一项对比广泛选择的算法优点的全面研究。目前只有两种对比特定精选的子空间聚类算法的初步尝试[104, 108]，其中所采用的评估程序并不完全令人信。本章讨论的某些算法可以在 ELKI 框架的统一实现可用。

尽管实值特征向量的基本技术仍存在未解决的问题，但已经尝试将子空间聚类推广到更复杂的数据。所谓的 3D 数据为对象和属性添加了第三分量（例如时间）。这意味着不再需要矩阵，而是需要一个三阶张量[140, 123, 83, 81]。虽然 3D 应用可以完全访问第三分量（作为不同的时间点），但动态或流数据中的应用通常不能。何时使用聚类算法来掌握子空间聚类结构（以及可能对结构进行某些后处理）。还存在尝试处理动态或流数据中的子空间聚类[10, 138, 66, 112]。其他挑战包括数据质量不高或存在不确定性[71]。当某些对象被标记时，最近某些子空间聚类方法可以用于半监督子空间聚类[134, 131, 56]。某些方法在聚类过程中同时使用额外的图信息[68, 67]。最近的一项调查将此类问题和方法称为“增强子空间聚类”[122]。

## 9.6 结论

数据挖掘及相关学科（如统计、模式识别、机器学习以及应用科学，如生物信息学）的研究产生了聚类技术，并解决了高维数据聚类这一专门问题。每年都有许多会议和期刊对该问题提出新方法。然而，许多研究人员认为，不存在适用于所有问题且通用适用于任意数据的通用聚类技术。具体的数据集会影响算法的选择，这对于聚类也是如此，即使当某些任务涉及高维数据时也是。

在本章中，我们引导读者找到最适合他们所面临任务的文献，区分了不同的问题设置：轴对齐子空间聚类与“子空间聚类”族（狭义意义上）、“（软性）投影聚类”以及日益增“混合”方法；以及任意方向子空间中的聚类（也称为“相关性聚类”）。在这些领域中，可以找到受“维度灾咒”影响的不同问题设置。维度灾咒不是我们能够解决的。这种“灾咒”有不同的方面，如果某种方法考虑了其中一个方面，其他方面将继续困扰研究者。

不同的方法带有不同的偏。。领域专家应该决定在给定应用中哪种偏差（如果有的话）最有意义。例如，在给定应用中专门搜索轴对齐子空间簇可能是有意义的。

## 高维数据聚类

任意方向聚类中一个相当的问题是任意方向簇的显著性。（如上所述，对于轴对齐子空间聚类，至少已经采取了一些步骤[101]）。此外，对于重叠簇（子空间聚类中的常见问题，但在其他领域也是如此），目前尚无适当的评估方法。不同的评估方法各不相同，且都忽略了某些要求。这个问题由 Färber 等人[49] 进行了概述并进行了更详细的讨论。文献中仅能找到改进评估方法论的一些初步步骤[115, 92, 66, 9]。

因此，文献中仍然缺乏对比广泛选择的算法优点的全面研究。目前只有两种对比特定精选的子空间聚类算法的初步尝试[104, 108]，其中所采用的评估程序并不完全令人信服。本章讨论的某些算法可以在 ELKI 框架的统一实现可用。

# 数据聚类：算法与应用

任意方向聚类中一个相当的问题是任意方向簇的显著性。（如上所述，对于轴对齐子空间聚类，至少已经采取了一些步骤[101]）。此外，对于重叠簇（子空间聚类中的常见问题，但在其他领域也是如此），目前尚无适当的评估方法。不同的评估方法各不相同，且都忽略了某些要求。这个问题由 Färber 等人[49] 进行了概述并进行了更详细的讨论。文献中仅能找到改进评估方法论的一些初步步骤[115, 92, 66, 9]。

# 高维数据聚类

- [7] E. Achtert, C. Böhm, H.-P. Kriegel, P. Kröger, and A. Zimek. 鲁棒、完整且高效的相关性聚类。Proceedings of the 7th SIAM International Conference on Data Mining (SDM), Minneapolis, 2007.
- [8] E. Achtert, C. Böhm, P. Kröger, and A. Zimek. 相关性聚类层次体系的挖掘。Proceedings of the 18th International Conference on Scientific and Statistical Database Management (SSDBM), Vienna, Austria, pages 119–128, 2006.
- [9] E. Achtert, S. Goldhofer, H.-P. Kriegel, E. Schubert, and A. Zimek. 聚类评估——指标与视觉支持。Proceedings of the 28th International Conference on Data Mining (ICDE), Washington, DC, pages 1285–1288, 2012.
- [10] C. Aggarwal, J. H. Wang, and P. S. Yu. 高维流投影聚类的一个框架。Proceedings of the 30th International Conference on Very Large Data Bases (VLDB), Toronto, Canada, pages 852–863, 2004.
- [11] C. Aggarwal, A. Hinneburg, and D. Keim. 高维空间中距离指标的意外行为。Proceedings of the 8th International Conference on Data Mining Theory (ICDT), London, UK, pages 420–434, 2001.
- [12] C. Aggarwal, C. M. Protopcioulos, J. L. Wolf, P. S. Yu, and J. S. Park. 投影聚类的快速算法。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Philadelphia, PA, pages 61–72, 1999.
- [13] C. Aggarwal and P. S. Yu. 高维空间中广义聚类的发现。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Dallas, TX, pages 70–81, 2000.
- [14] R. Agrawal, J. Gehrke, D. Dunopoulos, and P. Raghavan. 数据挖掘应用的高维数据自动子空间聚类。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Seattle, WA, pages 94–105, 1998.
- [15] R. Agrawal and R. Srikant. 规则挖掘的快速算法。Proceedings of the 20th International Conference on Very Large Data Bases (VLDB), Santiago of Chile, pages 487–499, 1994.
- [16] M. Ankers, M. B. Beunig, H.-P. Kriegel, and J. Sander. OPTICS：通过排序点以识别聚类结构。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Philadelphia, PA, pages 49–60, 1999.
- [17] I. Assent. 高维数据聚类。Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery, 2(4):340–350, 2012.
- [18] I. Assent, R. Krieger, E. Müller, and T. Seidl. DUSC：维度无偏聚类。Proceedings of the 7th IEEE International Conference on Data Mining (ICDM), Omaha, NE, pages 409–414, 2003.
- [19] I. Assent, M. S. Gülnemann, R. Krieger, and T. Seidl. 少即是多：非冗余子空间聚类。MultiClust: 17th International Workshop on Discovering, Summarizing and Using Multiple Clusters Held in Junction with KDD 2010, Washington, DC, 2010.
- [20] M. S. Aziz and C. K. Reddy. 一种鲁棒无缝聚类算法。Proceedings of the 14th Pacific-Asia Conference on Knowledge Discovery and Data Mining (PAKDD), Hyderabad, India, pages 28–37, 2010.

# 数据聚类：算法与应用

- [21] E. Bae and J. Bailey. COALA：一种提取高质量、高相似性替代聚类的新方法。Proceedings of the 6th IEEE International Conference on Data Mining (ICDM), Hong Kong, China, pages 53–62, 2006.
- [22] N. Bansal, A. Blum, and S. Chawla. 相关性聚类。Machine Learning, 56:89–113, 2004.
- [23] R. Bellman. 自适应控制过程：引导之旅。Princeton University Press, 1961.
- [24] A. Belussi and C. Faloutsos. 使用“相关性”分形维度估计空间查询的选择性率。Proceedings of the 21st International Conference on Very Large Data Bases (VLDB), Zurich, Switzerland, pages 299–310, 1995.
- [25] K. P. Bennett, U. Fayyad, and D. Geiger. 用于近似邻查询的基于密度的索引。Proceedings of the 5th ACM International Conference on Knowledge Discovery and Data Mining (KDD), San Diego, CA, pages 223–249, 1999.
- [26] T. Bernecker, M. E. Houle, H.-P. Kriegel, P. Kröger, M. Lenz, and E. Schubert. 相似性排名随时间的质量。Proceedings of the 12th International Symposium on Spatial and Temporal Databases (SSTD), Minneapolis, MN, pages 422–440, 2011.
- [27] K. Beyer, J. Goldstein, R. Krishna, and U. U. 什么是“最近邻”？Proceedings of the 7th International Conference on Database Theory (ICDT), Jerusalem, Israel, pages 217–235, 1999.
- [28] S. Bickel and T. Scheffer. 多视图聚类。Proceedings of the 4th IEEE International Conference on Data Mining (ICDM), Brighton, UK, 19–26.
- [29] C. Bouveyn, S. Girard, and C. Schmid. 高维聚类。Computational Statistics and Data Analysis, 52:502–519, 2007.
- [30] C. Böhm, S. Bertchold, and D. Keim. 用于改进数据库性能的高维空间搜索。ACM Surveys, 33(3):322–373, 2001.
- [31] C. Böhm, K. Kaiser, H.-P. Kriegel, and P. Kröger. 局部偏好的密度聚类。Proceedings of the 4th IEEE International Conference on Data Mining (ICDM), Brighton, UK, 27–34.
- [32] C. Böhm, K. Kaiser, P. Kröger, and A. Zimek. 对象的聚类。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Paris, France, pages 455–466, 1999.
- [33] K. Chakrabrabarti and S. Mehra. 大规模空间中的发现。Proceedings of the 26th International Conference on Very Large Data Bases (VLDB), Cairo, Egypt, pages 89–100, 2000.
- [34] C. H. Cheng, A. Fu, and Y. Zhang. 用于数值数据的子空间聚类。Proceedings of the 2nd ACM International Conference on Knowledge Discovery and Data Mining (KDD), San Diego, CA, pages 84–93, 1996.
- [35] R. Agrawal, J. Gehrke, D. Dunopoulos, and P. Raghavan. 数据挖掘应用中的高维数据自动子空间聚类。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Seattle, WA, pages 94–105, 1998.
- [36] Y. Cui, S. Fern, and J. Bailey. 多视图聚类发现。Proceedings of the 4th SIAM International Conference on Data Mining (SDM), Lake Buena Vista, FL, pages 517–522, 2004.
- [37] I. Dang and R. Ravi. 替代聚类的生成。Proceedings of the 10th SIAM International Conference on Data Mining (SDM), Omaha, NE, pages 133–142, 2010.
- [38] I. Davidson and Z. Qi. 基于约束的聚类。Proceedings of the 8th IEEE International Conference on Data Mining (ICDM), Pisa, Italy, pages 773–778, 2008.
- [39] I. Davidson, S. Sha, and L. Shamis. 基于 SAT 的聚类框架。Proceedings of the 10th SIAM International Conference on Data Mining (SDM), Columbus, OH, pages 94–105, 2010.
- [40] A. P. Dempster, N. Laird, and D. Rubin. 来自不完整数据的最大似然法。Journal of the Royal Society: Series B, 39(1):1–31, 1977.
- [41] C. Domeniconi. 子空间聚类集成（邀请演讲）。3rd MultiClust Workshop, SIAM Data 2012, Anaheim, CA, 2012.
- [42] C. Domeniconi, D. Gunopoulos, S. Ma, B. Yan, M. Al-Razgan, and D. Papadopoulos. 用于高维数据的局部自适应指标。Data Mining and Discovery, 14(1):63–97, 2002.
- [43] C. Domeniconi, D. Papadopoulos, D. Gunupolos, and S. Ma. 高维数据的子空间聚类。Proceedings of the 4th SIAM International Conference on Data Mining (SDM), Lake Buena Vista, FL, pages 517–522, 2004.
- [44] R. O. Duuda and P. Hart. 使用 变换检测图像中的线和曲线。Communications of the ACM, 15(1):11–15, 1972.
- [45] R. J. Durant and A. Kabhan. “最近邻”是否有意义：逆定理及其启示。Journal of Complexity, 25(4):385–397, 2003.
- [46] M. Ester, H.-P. Kriegel, J. Sander, and X. Xu. 一种在大型空间数据库中发现聚类的基于密度的算法。Proceedings of the 2nd ACM International Conference on Knowledge Discovery and Data Mining (KDD), Portland, OR, pages 226–231, 1996.
- [47] E. Evistill-Castro. 为什么有这么多聚类算法——个人观点。ACM SIGKDD Explorations, 4(1):65–75, 2002.
- [48] C. Faloutsos and I. Kamel. 超越均匀性和独立性：使用分形数据概念分析 R树。Proceedings of the ACM International Conference on Management of Data (SIGMOD), Minneapolis, MN, pages 4–13, 1994.
- [49] I. Fäber, S. Gummemann, H.-P. Kriegel, P. Kröger, E. Müller, S. Schubert, T. Seidl, and A. Zimek. 在聚类评估中使用类别标签的方法。MultiClust: 1st International Workshop on Discovering, Summarizing and Using Multiple Clusters Held in Junction with KDD 2010, Washington, DC, 2010.

# 数据聚类：算法与应用

- [50] X. Z. Fern, I. Davidson, and J. G. Dy. MultiClust 2010: 发现、总结和使用多个聚类。ACM SIGKDD 12(2):47–49, 2010.

- [51] M. A. Fischer and R. C. Bolles. 随机样本一致：一种模型拟合范式，应用于图像分析和自动制图。Communications of the ACM, 24(6):381–395, 1981.

- [52] E. B. Folkes, R. Gananadesikan, and J. R. Kettenring. 聚类中的变量选择。Journal of Classification, 5:205–228, 1998.

- [53] E. B. Folkes and K. C. Mallows. 比较两种层次聚类的方法。Journal of the American Statistical Association, 78(33):553–569, 1983.

- [54] D. François, V. Wertz, and M. Verleysen. 分数型属性的连接。IEEE Transactions on Knowledge and Data Engineering, 19(7):873–886, 2007.

- [55] J. H. Friedman and J. J. Meulman. 基于属性子集的对象聚类。Journal of the Royal Statistical Society: Series B (Statistical Methodology), 66(4):825–849, 2004.

- [56] É. Fromont, A. Prado, and C. Robertant. 基于约束的子空间聚类。Proceedings of the 9th SIAM International Conference on Data Mining (SDM), Sparks, NV, 26–37, 2009.

- [57] G. Gan, C. Ma, and J. Wu. 数据聚类：理论、算法与应用。Philadelphia, PA: Society for Industrial and Applied Mathematics (SIAM), 2007.

- [58] G. Ghosh and A. Acharya. 聚类集成。Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery, 1(4):305–315, 2011.

- [59] R. Gananadesikan, J. R. Kettenring, and S. L. Tao. 聚类分析中的变量权重与选择。Journal of Classification, 12(1):113–136, 1995.

- [60] G. Dondek and T. Hofmann. 基于条件集的非冗余聚类。Proceedings of the 11th ACM International Conference on Knowledge Discovery and Data Mining (SIGKDD), Chicago, IL, pages 70–77, 2005.

- [61] G. Dondek and T. Hofmann. 非冗余数据聚类。Proceedings of the 4th IEEE International Conference on Data Mining (ICDM), Brighton, UK, pages 75–82, 2004.

- [62] F. Gullo, C. Domeniconi, and A. Tagarelli. 通过投影集成推进聚类。Proceedings of the 17th ACM International Conference on Knowledge Discovery and Data Mining (SIGKDD), San Diego, CA, pages 733–744, 2011.

- [63] F. Gullo, C. Domeniconi, and A. Tagarelli. 实现单目标投影集成。Proceedings of the 10th IEEE International Conference on Data Mining (ICDM), Sydney, Australia, pages 833–838, 2010.

- [64] F. Gullo, C. Domeniconi, and A. Tagarelli. 投影集成。Proceedings of the 9th IEEE International Conference on Data Mining (ICDM), Miami, FL, pages 794–799, 2009.

- [65] A. Gupta, R. Krauthgart, and J. R. Lee. 有边界嵌入、分形与低失真嵌入。Proceedings of the 44th Annual IEEE Symposium on Computer Science (FOCS), Cambridge, MA, pages 534–543, 2003.

- [66] I. Guyon and A. Elisseeff. 变量选择导论。Journal of Machine Learning, 3:17–182, 2002.

## 高维数据聚类

- [67] S. Ginnemann, B. Boden, and T. Seidl. 在特征向量组中寻找基于密度的聚类。Data Mining and Knowledge Discovery, 25(2):243–269, 2012.

- [68] S. Ginnemann, I. Färber, B. Boden, and T. Seidl. 子空间聚类遭遇密集挖掘：范式综合。Proceedings of the 22nd International Conference on Scientific and Statistical Database Management (SSDBM), Heidelberg, Germany, pages 482–500, 2010.

- [69] S. Ginnemann, I. Färber, E. Müller, I. Assent, and T. Seidl. 子空间聚类的外部度量。Proceedings of the 20th ACM Conference on Information and Knowledge Management (CIKM), Glasgow, UK, pages 1363–1372, 2011.

- [70] S. Ginnemann, I. Färber, E. Müller, and T. Seidl. ASCL：替代子空间聚类。MultiClust: 第一届 International Workshop on Discovering, Summarizing and Using Multiple Clusters in Conjunction with KDD 2010, Washington, DC, 2010.

- [71] S. Ginnemann, H. Kremer, and T. Seidl. 不确定数据的子空间聚类。Proceedings of the 10th SIAM International Conference on Data Mining (SDM), Columbus, OH, pages 385–396, 2010.

- [72] S. Ginnemann, E. Müller, J. Harpar, and T. Seidl. 高维数据空间中的正交概念检测。Proceedings of the 18th ACM Conference on Information and Knowledge Management (CIKM), Hong Kong, China, pages 1317–1326, 2009.

- [73] J. Han, M. Kamer, and J. Pei. 数据挖掘：概念与技术，第3版。Morgan Kaufmann, 2011.

- [74] R. Haralick and R. Harpaz. 线性流形聚类。Proceedings of the 4th International Conference on Machine Learning and Data Mining in Pattern Recognition (MLDM), Leipzig, Germany, pages 132–141, 2005.

- [75] R. Harpaz and R. Haralick. 子空间相关性挖掘。Proceedings of the IEEE Symposium on Computational Intelligence and Data Mining (CIDM), Honolulu, HI, pages 335–342, 2007.

- [76] A. Hinneburg, C. C. Aggrawal, and D. A. Keim. 高维空间中的最近邻是什么？Proceedings of the 26th International Conference on Very Large Data Bases (VLDB), Cairo, Egypt, pages 506–515, 2000.

- [77] P. V. C. Hough. 识别复杂模式的方法与手段。美国专利3066654, 1962年12月18日.

- [78] M. E. Houle, H.-P. Kriegel, P. Kröger, E. Schubert, and A. Zimek. 共享邻域数据库击胜维度灾难？Proceedings of the 22nd International Conference on Scientific and Statistical Database Management (SSDBM), Heidelberg, Germany, pages 482–500, 2010.

- [79] J. Z. Huang, M. K. Ng, H. Rong, and Z. Li. k-means型聚类中的自动变量权重。IEEE Transactions on Pattern Analysis and Machine Intelligence, 27(5):657–668, 2005.

- [80] P. Jain, R. Meka, and I. S. Dhillon. 不同聚类的同步无监督学习。Statistical Analysis and Data Mining, 1(3):195–210, 2008.

- [81] L. Ji, K.-L. Tan, and A. K. Hung. 3D数据集中的频繁闭聚类挖掘。Proceedings of the 32nd International Conference on Very Large Data Bases (VLDB), Seoul, Korea, pages 811–822, 2006.

- [82] L. Jing, M. K. Ng, and J. Zhuang. 用于高维稀疏数据子空间聚类的熵权重k-means算法。IEEE Transactions on Knowledge and Data Engineering, 19(8):1026–1041, 2007.

- [83] I. T. Jolliffe. 主成分分析。

- [84] K. Kailing, H.-P. Kriegel, and J. Seidl. 多维数据的子空间聚类。Proceedings of the 5th IEEE International Conference on Data Mining, Lake Vista, FL, pages 246–257, 2004.

- [85] E. Korn, B. Pagel, and C. Falouts. 关于“维度灾难”。IEEE Transactions on Knowledge and Data Engineering, 3:96–111, 2001.

- [86] H.-P. Kriegel, P. Kröger, and J. Sander. 基于密度的聚类通用框架。Proceedings of the 23rd International Conference on Scientific and Statistical Database Management (SSDBM), Portland, OR, pages 387–404, 2011.

- [87] H.-P. Kriegel, P. Kröger, and J. Sander. 高效聚类。Proceedings of the 5th IEEE International Conference on Data Mining (ICDM), Houston, TX, pages 250–257, 2005.

- [88] H.-P. Kriegel, P. Kröger, and J. Sander. 基于密度的聚类。Wiley Interdisciplinary Reviews: Data Mining, 1(3):231–240, 2011.

- [89] H.-P. Kriegel, E. Schubert, and Zimek. 增强PCA相关算法鲁棒性的通用框架。Proceedings of the 20th International Conference on Scientific and Statistical Database Management (SSDBM), Hong Kong, China, pages 418–435, 2008.

- [90] H.-P. Kriegel, P. Kröger, and A. Zimek. 高维数据聚类：子空间聚类、模式和相关性聚类的综述。ACM Transactions on Knowledge Discovery from Data (TKDD), 3(1):1–58, 2009.

- [91] H.-P. Kriegel, P. Kröger, and A. Zimek. 子空间聚类。Wiley Interdisciplinary Reviews: Data Mining, 2(4):351–364, 2012.

- [92] H.-P. Kriegel, E. Schubert, and A. Zimek. 多聚类方案评估。2nd MultiClust Workshop: Summarizing and Using Multiple Clusters in Conjunction with PKDD 2011, Athens, Greece, pages 55–66, 2011.

- [93] H.-P. Kriegel and A. Zimek. 子空间聚类、集成聚类、替代聚类、多视图聚类：我们能从中学习到什么？MultiClust: 第一st International Workshop on Discovering, Summarizing and Using Multiple Clusters in Conjunction with KDD 2010, Washington, DC, 2010.

- [94] P. Kröger and A. Zimek. 子空间聚类技术。In L. Liu and M. T. Özsü, Encyclopedia of Database Systems, pages 2873–2875, 2009.

- [95] J. Li, X. Huang, C. Selke, and J. Yong. 在噪声中寻找相关性聚类的快速算法。Proceedings of the 11th Pacific-Asia Conference on Knowledge Discovery and Data Mining (PAKDD), Nanjing, China, pages 639–647, 2007.

- [96] B. Liu, Y. Xia, and P. S. Su. 通过决策树构建进行聚类。Proceedings of the 9th ACM Conference on Information and Knowledge Management (CIKM), Washington, DC, pages 20–29, 2000.

# 高维数据聚类

[97] G. Liu, J. Li, K. Sim, and L. Wong. 灵活维度划分的子空间聚类. In Proceedings of the 23rd International Conference on Data Engineering (ICDE), Istanbul, Turkey, pages 1250–1254, 2007.

[98] Y. Lu, S. Wang, S. Li, and C. Zhou. 用于高维数据变量权重的粒子群优化. Machine Learning, 82(1):43–70, 2010.

[99] S. C. Madeira and A. L. Oliveira. 生物数据分析的双层聚类算法：综述. IEEE/ACM Transactions on Computational Biology and Bioinformatics, 1(1):24–45, 2004.

[100] G. W. Millikan. 六种误差扰动对十五种聚类算法的影响。 Psychometrika, 45(3):325–342, 1980.

[101] G. Moise and J. Sander. 在高维数据中寻找非冗余的具有统计显著性的区域：子空间聚类的新方法. In Proceedings of the 14th ACM Conference on Knowledge Discovery and Data Mining (SIGKDD), Las Vegas, NV, pages 533–541, 2008.

[102] G. Moise, J. Sander, and M. Ester. P3C: 一种鲁棒的投影聚类算法. In Proceedings of the 6th IEEE Conference on Data Mining (ICDM), Hong Kong, China, pages 414–425, 2006.

[103] G. Moise, J. Sander, and M. Ester. 鲁棒投影聚类. Knowledge and Information Systems (KAIS), 14(3):273–298, 2008.

[104] G. Moise, A. Zemek, H.-P. Kriegel, and J. Sander. 子空间与投影聚类：实验评估与分析. Knowledge and Information Systems (KAIS), 21(3):299–326, 2009.

[105] E. Müller, I. Assent, S. Gümann, R. Krieger, and T. Seidl. 相关性子空间聚类：在高维数据中挖掘最非冗余的聚类. In Proceedings of the 9th International Conference on Data Mining (ICDM), Miami, FL, pages 377–386, 2009.

[106] E. Müller, I. Assent, R. Gümann, and T. Seidl. DenSest: 高维数据数据挖掘的密度估计. In Proceedings of the 9th SIAM International Conference on Data Mining (SDM), Sparks, NY, pages 173–184, 2009.

[107] E. Müller, I. Assent, and T. Seidl. HSM: 高维数据中的异构子空间聚类. In Proceedings of the 21st International Conference on Scientific and Statistical Database Management (SSDBM), New Orleans, LA, pages 497–516, 2009.

[108] E. Müller, S. Gümann, I. Assent, and T. Seidl. 高维数据子空间投影中的聚类效果评估. In Proceedings of the 35th International Conference on Very Large Data Bases (VLDB), Lyon, France, pages 1270–1281, 2009.

[109] E. Müller, S. Gümann, I. Assent, and T. Seidl, 编辑. MultiClust研讨会：发现、总结和使用多个聚类，与 ECMLDD2011 联合举行，Athens, Greece, 2011.

[110] E. Müller, T. Seidl, S. Venkatubanian, and A. Zimek, 编辑. MultiClust研讨会：发现、总结和使用多个聚类，与 SIAM Data Mining 2012 联合举行，Anaheim, CA, 2012.

# 数据聚类：算法与应用

[111] H. S. Nages, S. Go, and A. Choudhary. 海量数据聚类的自适应网格. In Proceedings of the 1st SIAM International Conference on Data Mining (SDM), New York, NY., pages 1–17, 2001.

[112] I. Ntoutsi, A. Zimek, T. Palpan, and H.-P. Kriegel. 高维数据的基于密度聚类. In Proceedings of the 12th SIAM International Conference on Data Mining (SDM), Anaheim, CA, 2012.

[113] B.-U. Pagel, F. Korn, and A. Faltouts. 使用多个维度的维度诅咒. In Proceedings of the 16th International Conference on Data Engineering (ICDE), San Diego, CA, pages 589–598, 2000.

[114] L. Parsons, E. Haque, and H. Liu. 高维数据的子空间聚类：综述. ACM SIGKDD Explorations, 6(1):90–105, 2004.

[115] A. Patrikainen and M. Meila. 包含性子空间聚类. IEEE Transactions on Knowledge and Data Engineering, 18(7):902–916, 2006.

[116] J. M. Phillips, P. Raman, and S. Venkatubanian. 生成多样化的高质量聚类。与 ECMLDD2011 联合举行，Athens, Greece, pages 80–91, 2011.

[117] C. M. Coproc, M. Jones, P. K. Agarwal, and T. M. Murali. 用于快速聚类的蒙特卡洛算法. In Proceedings of the ACM International Conference on Management of Data (SIGMOD), Madison, WI, pages 418–427, 2002.

[118] Z. J. Qi and I. Davidson. 聚类的原则性框架. In Proceedings of the 15th ACM Conference on Knowledge Discovery and Data Mining (SIGKDD), Paris, France, pages 717–726, 2009.

[119] M. Radan, A. Nanopoulos, and M. Ivanović. 向量模型中的失效结果. In Proceedings of the 33rd International Conference on Research and Development in Information Retrieval (SIGIR), Geneva, Switzerland, pages 186–193, 2010.

[120] K. Sequeira and M. J. Zaki. SCHISM: 一种新的子空间挖掘方法. International Journal of Business Intelligence and Data Mining, 1(2):137–160, 2005.

[121] R. Lisbon. SLINK: 单链聚类的高效算法. The Computer Journal, 16(1):30–34, 1973.

[122] K. Sim, V. Gopakrishnan, A. Zimek, and G. Cong. 增强聚类的综述. Mining and Knowledge Discovery, 26(2):332–397, 2013.

[123] K. Sim, J. Li, V. Gopakrishnan, and G. Liu. 用于价值投资的股票和财务比率最大二图挖掘. In Proceedings of the 6th IEEE International Conference on Data Mining (ICDM), Hong Kong, China, pages 1059–1066, 2006.

[124] K. Sim, A. K. Poern, and V. Gopakrishnan. 序列数据中的可操作子空间挖掘. In Proceedings of the 10th SIAM International Conference on Data Mining (SDM), Columbus, OH, pages 442–453, 2010.

[125] J. L. Sagle, C. L. Chang, and S. L. Heller. 数据聚类与重组算法. IEEE Transactions on Systems, Man, and Cybernetics, 5(1):121–128, 1975.

[126] P. H. A. Sneath. 计算机在分类学中的应用. Journal of General Microbiology, 17(2):201–222, 1957.

[127] D. Steinley and M. J. Brusco. 聚类分析中的变量选择：八种经验比较. Psychometrika, 73(1):125–144, 2009.

[128] R. Vidal. 基于密度的聚类. Signal Processing, 28(1):1–10, 2009.

[129] J. V and A. Zimek. MultiClust研讨会：发现、总结和使用多个聚类，与 ECMLDD2011 联合举行，Athens, Greece, pages 11–18, 2011.

[130] H. Go, J. Lee, and M. Kim. FINDIT: 一种快速且智能的聚类. Information and Software Technology, 46(4):255–271, 2004.

[131] B. Yan and C. Domen. 高维数据的度集成. In Proceedings of the 17th European Conference on Machine Learning (ECML), Berlin, Germany, pages 509–520, 2006.

[132] L. Yang. 距离保持. Interdisciplinary Reviews, 1(5):369–380, 2011.

[133] K. Y. Yip, D. W. Cheung, and M. K. Ng. 一种实用的投影聚类算法. IEEE Transactions on Knowledge and Data Engineering, 16(11):1387–1397, 2004.

[134] K. Y. Yip, D. W. Cheung, and M. K. Ng. 关于极低维的发现. In Proceedings of the 21st International Conference on Data Engineering (ICDE), Tokyo, Japan, pages 329–350, 2004.

[135] M. L. Yiu and N. Mam. 基于频繁模式的迭代投影聚类. In Proceedings of the 3rd IEEE International Conference on Data Mining (ICDM), Melbourne, FL, pages 689–692, 2003.

[136] M. L. Yiu and N. Mam. 通过子空间挖掘迭代投影聚类. IEEE Transactions on Data Engineering, 17(2):176–189, 2005.

[137] M. J. Zaki, M. Peters, I. Assent, and T. Seidl. CLICKS：分类数据集中挖掘子空间聚类的有效算法. Data & Knowledge Engineering, 60(1):51–70, 2007.

[138] Q. Zhang, J. Liu, and W. Wang. 多数据流增量式子空间聚类. In Proceedings of the 7th IEEE International Conference on Data Mining (ICDM), Omaha, NE, pages 727–732, 2003.

[139] X. Zhang, F. Pan, and W. Wang. CARE: 高维数据中寻找局部线性相关性. In Proceedings of the 24th International Conference on Data Engineering (ICDE), Cancun, Mexico, pages 130–139, 2008.

[140] L. Zhao and M. J. Zaki. TRICLUSTER：在3D微阵列数据中挖掘协同聚类的有效算法. In Proceedings of the ACM International Conference on Management of Data (SIGMOD), Baltimore, MD, pages 694–705, 2005.

[141] A. Zimek. 相关性聚类. ACM SIGKDD Explorations, 11(1):53–54, 2009.

[142] A. Zimek, E. Schubert, and H-P. Kriegel. 高维数值数据无监督异常值检测综述. Statistical Analysis and Data Mining, 5(5):363–387, 2012.

## 第10章
## 流数据聚类算法综

Charu C. Aggrawal
IBM T. J. Watson Research Center
Yorktown Heights, NY
charu@us.ibm.com

- 10.1 引言 231
- 10.2 基于划分代表元的方法 233
- 10.2.1 STREAM 算法 233
- 10.2.2 ClStream: 微聚类框架 235
- 10.2.2.1 微聚类定义 235
- 10.2.2.2 金字塔型时间帧 236
- 10.2.2.3 基于 ClStream 的在线聚类 237
- 10.3 基于密度的流聚类 239
- 10.3.1 DenStream: 基于密度的微聚类 240
- 10.3.2 基于网格的流算法 241
- 10.3.2.1 D-Stream 算法 241
- 10.3.2.2 其他基于网格的算法 242
- 10.4 概率流算法 243
- 10.5 高维流的聚类 243
- 10.5.1 HPSTREAM 方法 244
- 10.5.2 其他高维流算法 244
- 10.6 离散和类别流的聚类 245
- 10.6.1 使用 k-Means 对二值数据流聚类 245
- 10.6.2 StreamCluD 算法 245
- 10.6.3 大规模域聚类 246
- 10.7 文本聚类 249
- 10.8 流聚类的其他场景 252
- 10.8.1 不确定性数据流的聚类 253
- 10.8.2 图形流的聚类 253
- 10.8.3 数据流的分布式聚类 254
- 10.9 讨论与结论 254
- 参考文献 255

## 10.1 引言

近年来，硬件的进步使我们能够以快速的速度自动重建日常生活中的交易和其他信息。这些过程产生了海量的在线数据，并以无限制的速度增长。这类在线数据被称为数据聚类：算法与应用。由于数据流具有突发性、紧迫性和广泛的应用，关于数据流管理和分析的问题在近年来得到了广泛研究 [1]。

聚类和分类等许多重要问题在数据社区已得到广泛研究。该问题已经在多种方法的背景下得到了调查，例如 k-means、k-medians、基于密度的方法和概率聚类方法。关于聚类方法的详细讨论可以参见 [42, 44]。文献中的大多数经典方法并不一定是针对大数据集和数据流背景设计的。流场景的出现带来了一系列独特的挑战，这些挑战是 [42, 44] 中提出的大多数经典方法无法解决的。

流场景背景下的特定挑战如下：

- 流具有海量数据，无法在磁盘上显式存储数据。因此，数据需要在单次通过（single pass）中进行处理，其中聚类过程所需的所有信息都需要存储和维护。处理每个记录的时间必须很小且恒定。否则，模型构建过程将永远跟不上数据流。
- 数据流中的模式可能会随时间不断演变 [3]。从流挖掘的角度来看，这意味着底层聚类模型需要不断更新。一个实用的模型必须在任何时候可用，因为流的结束可能永远不会到来，而且分析可能在任何时间点都需要结果。
- 不同领域的数据可能对数据聚类带来不同的挑战。例如，在具有多种属性的大规模域中，在不显著增加问题计算复杂性的情况下，可能无法存储许多类的类的表示。因此，需要为大规模域的数据流聚类设计空间高效的方法。

显然，从流处理的角度来看，扩展性问题是一个首要问题，但绝不是唯一的问题。在流处理的背景下，时间局部性也非常重要，因为数据中的底层模式可能会演变，过去历史中的聚类可能对未来不再具有相关性。扩展性问题在极大型数据集的数据聚类背景下也存在 [31, 37, 51, 63]。在这种情况下，主要限制是算法对数据的扫描次数不能超过一次（或至少是少数）。由于在数据库中 I/O 操作传统上比内存操作昂贵得多，当底层算法被设计为最小化数据扫描次数而不是最小化 CPU 操作次数时，通常会获得最佳性能。在数据流背景下，时间局部性问题也非常重要，在聚类过程中不应被忽略。因此，各种流聚类算法尝试通过基于快照的方法、基于衰减的技术、窗口化等来考虑此类流。我们将尽可能指出这些方法的使用点。

本章的结构如下：在下一节中，我们将学习基于 k-means 或 k-medians 方法的聚类方法。在第 10.3 节中，我们将研究用于流聚类的基于密度的方法。第 10.4 节讨论了用于数据流聚类的概率算法。第 10.5 节介绍了高维流算法。第 10.6 节介绍了离散和类别流聚类的方法。第 10.7 节讨论了文本流聚类的方法。第 10.8 节讨论了数据流聚类的其他场景。第 10.9 节给出了结论和总结。

## 流聚类算法综
## 10.2 基于划分代表元的方法

许多聚类方法基于划分代表元。这些包括 k-means 和 k-medians 等方法。在经典文献中，这些方法需要对数据进行多次扫描。然而，在流场景下，不需要多次扫描，因为有足够的数据。代表元集的定义使得每个点都分配给其最近的代表元。在本节中，我们将首先讨论 k-means 变体。

### 10.2.1 STREAM 算法

`STREAM` 方法 [36, 53] 基于微聚类。其核心思想是将流分成若干块（chunks），每个块都能装入主内存。对于原始的 $\mathcal{D}$，我们将其划分为 $\mathcal{D}_1, \dots, \mathcal{D}_n$，每个块最多包含 $m$ 个数据点。$m$ 的值由内存预算定义。目标是选取代表元以使数据点的平方误差和（SSE）最小化。对于集合 $S$ 中的数据点集 $X_1, \dots, X_m$ 和包含 $k$ 个代表元的集合 $Y = Y_1, \dots, Y_k$，目标函数定义为：

$$Objective(S, Y) = \sum_{X_i \in S, Y_j \in Y} dist(X_i, Y_j) \quad (10.1)$$

分配用 $\in$ 表示。点与记录之间的距离平方和由 $dist(\cdot)$ 定义。在处理完第一个块后，我们得到了一组 $k$ 个中位数，并将其存储。分配给每个代表元的点数被存储为 1 级代表元。独立地处理下一个块以找到其最优中位数代表元。在第二个块结束时，我们将拥有 $2-k$ 个代表元。存储代表元的内存需求也随时间增加，在处理块后，当代表元数量超过 $m$ 时，会对这组 $r-k$ 个点应用第二次聚类，以便将存储在代表元上的点用于聚类过程中。产生的代表元被存储为 2 级代表元。通常，当第 $p$ 级代表元的数量达到 $m$ 时，它们被转换为 $k$ 个第 $p+1$ 级代表元。然后，该过程将导致所有级别的代表元数量增加，尽管高级代表元的数量增长速度远慢于低级。在处理完整个流之后（或当特定需要聚类结果时），所有不同级别的剩余代表元将汇在一起，通过最后一次调用 $k$-medians 子程序进行聚类。

显然，特定算法的选择对于 k-medians 的质量至关重要。影响最终输出质量的唯一因素是

# 数据聚类：算法与应用

将问题分解为若干块并进行分层聚类的效果。这种分解如何影响输出的最终质量？[53] 已经表明，除非在中间阶段用于 k-medians 聚类的特定子程序，否则输出的最终质量是不可能是任意的。

引理 10.2.1。`STREAM` 算法中 k-medians 聚类的子程序具有近似因子 $c$。那么，`STREAM` 算法的近似因子不优于 $5 \cdot c$。

[53] 中的工作通过为 k-medians 问题设计更有效的子程序，扩展了 [36] 中的原始工作。该解决方案基于选址问题（facility location problem）。请注意，聚类问题的拉格朗日松弛可以建模为选址问题，其中我们放宽了代表点数量的限制，并使用拉格朗日乘子将其纳入目标函数中。这些代表点类似于选址问题中的设施，与代表点相关的成本在物理上可以被可视化为为了服务其客户（数据点）而“建立”设施的成本。因此，我们为每个包含的设施添加了 $\lambda$（拉格朗日参数）。分配的成本与之前相同。因此，在设施集 $Y'$ 中的新目标函数表达式如下：

$$\text{Objective}(S, Y') = \sum_{X_i \in S, Y_j \in Y'} \text{dist}(X_i, Y_j) + \lambda \cdot |Y'| \quad (10.2)$$

与之前的情况不同，$Y'$ 的基数在目标函数层面可能不是最优的，除非适当选择了拉格朗日参数（或设施成本）$\lambda$。为了使用这种方法解决 k-medians 子程序，需要两个步骤 [53]：

- 给定特定的 $\lambda$ 值，我们如何确定最优目标函数值？
- 如何确定 $\lambda$ 的值，使得最优解中的设施数量为 $k$？

解决方案的最后很容易。只要最优设施数量随 $\lambda$ 单调地变化，就可以对 $\lambda$ 采用二分搜索来确定合适的值。[53] 表明，最优设施数量随 $k$ 单调地变化。

为了解决问题的第一部分，提出了一种名为 `LSEARCH` 的局部搜索算法。在该算法中，我们从一组设施 $O$ 和对这些设施的数据点的分配 $x$ 开始。然后，我们反复检查随机选择的当前不在 $O$ 中的设施 $x$，通过将 $x$ 添加到 $O$ 以及其他设施来计算目标函数的改进。这种目标函数的改进被称为 $gain(x)$。为此使用了如所述的某些数据点重新分配到设施以及关闭设施的规则。

具体而言，当 $x$ 添加到 $O$ 时（如果有改进），允许任何数据点被重新分配到 $x$，并且允许关闭一个设施 $y$ 并将其所有点分配给 $x$。只要开启 $x$ 的成本不超过从 $y$ 节省的成本，后一种情况就会产生。因此，$gain(x)$ 的值可能为正。只有当 $gain(x) > 0$ 时，设施 $x$ 才被加入 $O$。按随机顺序对所有设施重复，最终的设施集和重新分配重复 $\Omega(\log m)$ 次，以对底层质量提供保证。

`STREAM` 算法的一个主要局限是它对底层数据流并不特别敏感。在许多情况下，底层流中的模式可能会演变并发生显著变化。因此，聚类过程能够适应变化并提供不同时间跨度的洞察是至关重要的。从这个意义上说，`ClStream` 算法能够在不同的时间粒度上提供显著更好的洞察。

# 10.2.2 ClStream：微聚类框架

由于数据自然地对算法设计施加了单通过（one-pass）限制，使用传统算法在不同时间跨度的聚类中提供这种灵活性变得更加困难。例如，在这种情况下，对 [53] 中基于流的 k-means 算法直接扩展需要同时维护所有可能时间跨度的聚类中间结果。这种计算负担随着数据进展而增加，可能会迅速成为实现的瓶颈。此外，在许多情况下，分析师可能希望确定之前时刻的聚类，并将其与当前聚类进行比较。这需要更大的灵活性，对于快速数据流来说可能很快变得不明智。

因此，流聚类的自然设计是将过程分为在线微聚类组件和离线微聚类组件。在线微聚类组件需要快速数据流中非常高效的聚合统计传递。离线组件使用这些汇总统计与其他输入相结合，以便在需要时为用户提供对聚类的快速理解。

假设数据由一组多维记录 $X_1, \dots X_k$ 组成，到达时间戳 $T_1, \dots T_k$。每个 $X_i$ 都是包含 $d$ 维的多维记录，记为 $X_i = (x_i^j)$。

微聚类框架的设计旨在捕捉数据流的汇总信息，以便于跨时间跨度的聚类和分析。这种汇总信息由以下结构定义：

- **微聚类（Microclusters）：** 我们捕捉有关数据流的汇总信息，以便于跨时间跨度的聚类和分析。这种汇总信息由以下结构定义：（注：原文此处重复）
- **金字塔时间框架（Pyramidal Time Frame）：** 离线组件使用这些汇总统计与其他输入相结合，以便在需要时为用户提供对聚类的快速理解。

# 流数据聚类算法综

| 快照顺序 | 时钟时间（最后5个快照） |
|---|--|
| 0 | 55 54 53 52 51 |
| 1 | 54 52 50 48 46 |
| 2 | 52 48 44 40 36 |
| 3 | 48 40 32 24 16 |
| 4 | 48 32 16 |
| 5 | 32 |

表 10.1: $\alpha = 2$ 且 $l = 2$ 时存储快照示例

**证明：** [5]。
对于较大的 $l$ 值，时间跨度可以尽可能地接近到所需的精度。例如，通过选择 $l=10$，可以将任何时间跨度的误差控制在 $0.2\%$ 以内，而100年共需要 $(2^{10}+1)\cdot\log_2(100\cdot365\cdot24\cdot60) \approx 32343$ 个快照。由于历史快照可以存储在磁盘上，主内存只需维护当前快照，从实际角度来看，这一要求是可行的。还可以根据用户对存储快照特定时刻的偏好指定金字塔时间窗口，让我们考虑流在时钟为1的情况下运行，$\alpha=2$ 且 $l=2$ 的情况。每个级别存储 $2^2+1=5$ 个快照。那么，在时钟为55时，存储了表10.1所示所示时刻的快照。
我们注意到，不同顺序之间存在大量的快照。从实现的角度来看，存储了时间为16, 24, 32, 36, 40, 44, 48, 50, 51, 52, 53, 54 和 55 的微聚类状态。显易看出，时钟时间越多，连续快照之间的距离越小（粒度越好）。我们还注意到本节估计的存储需求没有考虑这种冗余。因此，到目前为止提出的需求实际上是最坏情况需求。

## 10.2.2.3 基于 ClStream 的在线聚类

微聚类阶段是算法的在线数据收集部分。其目标是在足够高水平的（时间和空间）粒度上维持统计数据，以便离线组件（如周期性聚类或算法分析）有效使用。该算法以迭代方式工作，始终维护一组微聚类。假设算法在任何时刻都存储总共 $q$ 个微聚类。我们将这些微聚类标记为 $\mathcal{M}_1...\mathcal{M}_q$。对于每个微聚类 $i$，在首次创建时，我们创建一个唯一的 $id$。如果两个微聚类合并为一个，则会创建一个 $ids$ 列表以识别由其组成的微聚类。$q$ 的值取决于存储微聚类所需的可用内存大小。因此，$q$ 的典型值远大于数据中自然簇的数量，但远小于在大规模数据流中长时间内到达的数据点数量。这些微聚类代表簇的当前快照，随着新数据点的到达，它们在流的过程中发生变化。每当时钟被任何整数 $i$ 的 $\alpha^i$ 整除时，其状态就会存储在磁盘上。在 $\alpha^r$ 单位时刻，算法将删除在过去时刻存储的任何 $r$ 阶微聚类。

# 238 数据聚类：算法与应用

每当新数据点 $X_i$ 到达时，微聚类都会更新以反映变化。每个数据点都需要被吸收到一个微聚类中，或者形成自己的簇。首选方案是将数据点吸收到现有的微聚类中。确定每个点到微聚类中心 $M_1...M_k$ 的距离。数据点 $X_i$ 到微聚类中心 $M_j$ 的距离值记为 $dist(M_j, X_i)$。由于微聚类的中心位于簇特征向量中，该值可以很容易地计算。此距离用于比较簇 $M_p$ 与数据点 $X_i$ 的距离。在许多情况下，数据点 $X_i$ 自然属于簇 $M_p$。情况如下：

- 数据点 $X_i$ 对应离群值。
- 由于数据流的演变，数据点 $X_i$ 对应新簇的开始。

在有更多数据点到达之前无法区分这两种情况，数据点 $X_i$ 需要被分配到具有唯一 id 的自己的簇中。为了做出此决定，使用 $M_p$ 的簇特征向量来判断数据点是否落在微聚类 $M_p$ 的边界内。如果是，则使用CF属性将数据点 $X_i$ 添加到微聚类 $M_p$。这被定义为 $M_p$ 中数据点到中心均方根偏差的 $1/m$。我们将其定义为边界。对于具有多个之前点的簇，最大边界是一个启发值。具体而言，它被选择为最近簇的3倍。

如果数据点不在最近微聚类的边界内，将创建一个微聚类并分配一个新的 $id$，以便在数据流的任何阶段识别它。然而，为了创建此微聚类，必须减少其他簇的数量，以删除或合并旧簇。我们的管理算法首先确定删除离群值是否安全。如果不是，任何微聚类都可能是可以删除的离群值。虽然可以简单地选择点最少的微聚类进行删除，但这通常会导致误导性结果。

在某些情况下，给定的微聚类可能对应流历史中的过去点，但在当前视图中不再是活动簇。理想目标是估计每个簇中 $m$ 个列表的平均时间戳，并删除最旧的时间戳。虽然这是可能的，但维护每个微聚类时间戳的开销可能是巨大的。相反，可以使用最后添加到微聚类的时间戳作为其年龄的代理。

## 10.3 基于密度的聚类

基于密度的方法 [18, 30] 为聚类目的构建数据的密度分布。通常使用核密度估计方法 [58] 来构建底层数据的平滑密度。随后，将数据分离为密度连接区域。这些密度连接区域可能有不同的形状和大小。基于密度的算法的优势之一是不假设簇的隐含形状。例如，当使用欧式距离函数时，总是假设簇是球形的。基于密度的聚类的另一个方面是在于限制簇的数量，而是使用密度阈值来确定连接区域。当然，这改变了呈现给算法的参数性质（密度阈值而非簇的数量），但它并不意味着该方法是无参数的。流场景下的主要挑战是构建可以在数据单次扫描中高效执行的基于密度的算法，因为密度估计过程可能是计算密集型的。有两类技术：

## 流数据聚类综

每当新数据点 $X_i$ 到达时，微聚类都会更新以反映变化。每个数据点都需要被吸收到一个微聚类中，或者形成自己的簇。首选方案是将数据点吸收到现有的微聚类中。确定每个点到微聚类中心 $M_1...M_k$ 的距离。数据点 $X_i$ 到微聚类中心 $M_j$ 的距离值记为 $dist(M_j, X_i)$。由于微聚类的中心位于簇特征向量中，该值可以很容易地计算。此距离用于比较簇 $M_p$ 与数据点 $X_i$ 的距离。在许多情况下，数据点 $X_i$ 自然属于簇 $M_p$。情况如下：

- 数据点 $X_i$ 对应离群值。
- 由于数据流的演变，数据点 $X_i$ 对应新簇的开始。

在有更多数据点到达之前无法区分这两种情况，数据点 $X_i$ 需要被分配到具有唯一 id 的自己的簇中。为了做出此决定，使用 $M_p$ 的簇特征向量来判断数据点是否落在微聚类 $M_p$ 的边界内。如果是，则使用CF属性将数据点 $X_i$ 添加到微聚类 $M_p$。这被定义为 $M_p$ 中数据点到中心均方根偏差的 $1/m$。我们将其定义为边界。对于具有多个之前点的簇，最大边界是一个启发值。具体而言，它被选择为最近簇的3倍。

如果数据点不在最近微聚类的边界内，将创建一个微聚类并分配一个新的 $id$，以便在数据流的任何阶段识别它。然而，为了创建此微聚类，必须减少其他簇的数量，以删除或合并旧簇。我们的管理算法首先确定删除离群值是否安全。如果不是，任何微聚类都可能是可以删除的离群值。虽然可以简单地选择点最少的微聚类进行删除，但这通常会导致误导性结果。

在某些情况下，给定的微聚类可能对应流历史中的过去点，但在当前视图中不再是活动簇。理想目标是估计每个簇中 $m$ 个列表的平均时间戳，并删除最旧的时间戳。虽然这是可能的，但维护每个微聚类时间戳的开销可能是巨大的。相反，可以使用最后添加到微聚类的时间戳作为其年龄的代理。

# 数据聚类：算法与应用

- 第一类技术将微聚类技术扩展到此类情况，放宽对微簇数量的限制，并对每个微簇的半径和“权重”施加限制。密集区域通过连接满足类似于 [30] 中连通性条件的密集微簇生成。
- 第二类技术将数据空间划分为网格，然后确定密集网格。数据中的区域通过拼接连接的密集网格来重构。

我们将在本节中讨论这两类技术。

### 10.3.1 DenStream：基于密度的微聚类

`DenStream` 算法 [24] 将微聚类与密度估计方法相结合以实现有效的聚类。第一步是定义核心对象，其定义为在 $\varepsilon$-邻域内数据点权重至少为 $\mu$ 的对象。密度区域定义为核心对象 $\varepsilon$ 邻域的并集。

在密集数据流的背景下，很难自然地定义这些密集区域。因此，以微簇的形式定义较小粒度的密集区域。微簇被定义为一组权重至少为 $\mu$ 的数据点，且其关于中心的半径小于 $\varepsilon$。我们注意到数据点的权重是基于其持续时间的衰减加权函数。因此，如果 $f(\delta t)$ 是自数据点到达以来的时间，其权重由：

$$f(\delta t) = 2^{-\delta t}$$

由于微簇的半径被限制小于 $\varepsilon$，这意味着当 $\varepsilon$ 值较小时，微簇的数量远大于数据中自然簇的数量。同时，核心簇的数量权重至少包含 $\mu$。我们注意到与标准微聚类定义的关键区别在于，微簇的数量不受限制，尽管每个微簇的半径受到了限制。因此，这种方法对底层应用使用了不同的参数。微簇也被称为 c-microcluster。

一个直接观察是，当任何算法首次形成微簇时，很难量化定义为微簇所需的数据点权重。因此，在 [24] 中定义了潜在核心微簇和离群微簇的概念。在前一种情况下，微簇包含至少 $\beta-\mu$ 的权重（对于某些 $\beta \in (0,1)$），在后一种情况下，它包含小于 $\beta-\mu$ 的权重。此外，如果没有足够的数据点来补偿衰减，随着时间的推移，衰减点的权重也会从 $p$-microcluster 变为 $o$-microcluster。因此，在其生命周期内，一个微簇可能会从离群微簇变为潜在核心微簇，最终变为核心微簇状态。这两类微簇分别被称为 $p$-microclusters 和 $o$-microclusters。

当新数据点到达时，对其进行处理的操作可能有以下几种可能性：

- 如果第一步是将其插入 $p$-microcluster 中，只要在不违反半径限制的情况下即可。
- 如果第一步不可行，下一步是将其插入 $o$-microcluster 中，只要在不违反半径限制的情况下即可。
- 如果第一步和第二步都不可行，则创建一个包含该数据点的新 $o$-microcluster。

这种方法的一个挑战是，$o$-microclusters 的数量随着时间的推移而增加，因为会创建新的 $o$-microclusters，并且某些 $p$-microclusters 会衰减回 $o$-microclusters。从那时起，我们修剪一些 $o$-microclusters，这将使其成为 $p$-microclusters 的潜力。自创建 $o$ 微簇以来经过的 $\delta t$ 越大，其预期权重越大。因此，每隔 $T_p$ 次，我们修剪所有权重小于阈值 $\psi(\delta t)$ 的微簇，其中：

$$\psi(\delta t) = \frac{2-\lambda\cdot(\delta t+T_p)}{2-\lambda\cdot(T_p)-1} \quad (10.4)$$

该过程持续进行以动态维护微簇。我们注意到，单个微簇可以重构为密度连通区域，以便通过创建最终的簇集。创建任意形状簇的整体方法在 [24] 中进行了讨论。

### 10.32 基于网格的流算法

### 10.32.1 D-Stream 算法

[25] 提出了一种用于数据实时密度聚类的名为 `D-Stream` 的方法。在尝试定义细粒度高密度区域方面它与 [30] 有许多相似之处。概念层面的主要区别是这是使用网格而不是微簇完成的。在前一种情况下，使用衰减函数 $f(\delta t)$ 表示点 $X$ 从其到达到当前时间 $t_i$ 的权重：

$$f(\delta t(\mathbf{X},t_i)) = \mu^{-\delta t(\mathbf{X},t_i)} \quad (10.5)$$

在这里，我们假设 $\mu > 1$，这与 [25] 中的符号不同。我们注意到，该衰减函数与 [6, 30] 中提出的相同，通过相对于参数 $\lambda$ 定义关系并假设 $\mu = 2^{-\lambda}$。根据 [25] 每个时间戳恰好到达一条记录的假设，可以证明所有数据点的权重和不超过 $\mu /(\mu-1)$。

网格通过对每个维度进行离散化形成。对于第 $i$ 个维度，分为 $p_i$ 个区间。这种离散化自然地定义了 $\eta = \Pi p_i$ 个单元。对于每个单元 $S$，其权重 $W(S,t_i)$ 定义为当前时间 $t_i$，如下：

$$W(S,t_i) = \sum_{\mathbf{X}\in S} f(\delta t(\mathbf{X},t_i)) \quad (10.6)$$

我们注意到，这在本质上类似于密度连通区域，以便创建最终的簇集。创建任意形状簇的整体方法在 [24] 中进行了讨论。

过程持续进行以动态维护微簇。我们注意到，单个微簇可以重构为密度连通区域，以便创建最终的簇集。创建任意形状簇的整体方法在 [24] 中进行了讨论。

这种方法的一个挑战是，$o$-microclusters 的数量随着时间的推移而增加，因为会创建新的 $o$-microclusters，并且某些 $p$-microclusters 会衰减回 $o$-microclusters。从那时起，我们修剪一些 $o$-microclusters，这将使其成为 $p$-microclusters 的潜力。自创建 $o$ 微簇以来经过的 $\delta t$ 越大，其预期权重越大。因此，每隔 $T_p$ 次，我们修剪所有权重小于阈值 $\psi(\delta t)$ 的微簇，其中：

$$\psi(\delta t) = \frac{2-\lambda\cdot(\delta t+T_p)}{2-\lambda\cdot(T_p)-1} \quad (10.4)$$

该过程持续进行以动态维护微簇。我们注意到，单个微簇可以重构为密度连通区域，以便创建最终的簇集。创建任意形状簇的整体方法在 [24] 中进行了讨论。

一个直接观察是，当任何算法首次形成微簇时，很难量化定义为微簇所需的数据点权重。因此，在 [24] 中定义了潜在核心微簇和离群微簇的概念。在前一种情况下，微簇包含至少 $\beta-\mu$ 的权重（对于某些 $\beta \in (0,1)$），在后一种情况下，它包含小于 $\beta-\mu$ 的权重。此外，如果没有足够的数据点来补偿衰减，随着时间的推移，衰减点的权重也会从 $p$-microcluster 变为 $o$-microcluster。因此，在其生命周期内，一个微簇可能会从离群微簇变为潜在核心微簇，最终变为核心微簇状态。这两类微簇分别被称为 $p$-microclusters 和 $o$-microclusters。

当新数据点到达时，对其进行处理的操作可能有以下几种可能性：

- 如果第一步是将其插入 $p$-microcluster 中，只要在不违反半径限制的情况下即可。
- 如果第一步不可行，下一步是将其插入 $o$-microcluster 中，只要在不违反半径限制的情况下即可。
- 如果第一步和第二步都不可行，则创建一个包含该数据点的新 $o$-microcluster。

网格通过对每个维度进行离散化形成。对于第 $i$ 个维度，分为 $p_i$ 个区间。这种离散化自然地定义了 $\eta = \Pi p_i$ 个单元。对于每个单元 $S$，其权重 $W(S,t_i)$ 定义为当前时间 $t_i$，如下：

$$W(S,t_i) = \sum_{\mathbf{X}\in S} f(\delta t(\mathbf{X},t_i)) \quad (10.6)$$

# 流聚类算法综述

为了合并相邻单元格。因此，[55]中的方法提供了更大的灵活性，正如在原始算法中讨论的那样。

## 10.4 概率流式算法

概率聚类的一种常用方法是混合模型建模（mixture modeling），其中数据被假设为由已知分布（如高斯分布）的混合体生成的。通常，该分布的参数会通过 EM 算法从实际数据记录中进行学习 [59]。[59] 中的主要论点是，基于概率密度的聚类算法比在整个数据集上应用 EM 算法要高效得多。另一方面，已经证明可以使用 EM 算法来为新到达的数据提供一个更新过程。尽管如此，由于 EM 算法要求人们学习学习大量的参数，当数据演变非常快时，这种方法可能不会有效。

概率模型常用于聚类的另一个领域是主题建模（topic modeling）[41]的情况。在这种技术中，使用软聚类（soft clusters）来对数据进行软聚类，其中词汇和文档以概率的方式分配到不同的划分中。由于主题建模方法使用了 EM 算法，它在实践中可能运行很慢。因此，[20] 提出了一种用于文本主题建模的方法。[20] 中的工作提出了三种常用批处理算法的在线变体：隐狄利克特分布 (LDA) [22]、狄利克特多项分布 (DCM) 混合 [29] 和 von-Mises Fisher (vMF) 混合模型 [21]。[20] 显示，这种 vMF 方法的主题变体提供了最好的结果。对这些主题建模算法的详细研究超出了本综述的范围。感兴趣的读者请参考 [20]。

## 10.5 聚类高维数据流

在许多情况下，数据流是非常高维的，因为对于挖掘过程可以使用大量的特征。高维情况对传统静态数据案例领域的聚类算法构成了特殊的挑战。这是由于高维空间中数据的稀稀疏性（sparsity）导致的。在高维空间中，所有点对都倾向于彼此几乎等距。因此，以有意义的方式定义基于距离的聚类通常是不现实的。最近有一些关于投影聚类（projected clustering）的高维基于距离的数据技术工作。在这些方法中，聚类的定义使得每个聚类都特定于一组维度。这在某种程度上考虑了高维空间内的稀疏性。尽管由于数据的稀疏性，聚类可能在所有维度上都无法完美定义，但可以找到某些维度子集，其中特定的点子集可以形成高质量且有意义的聚类。当然，这些维度子集可能会随着不同的聚类而变化。此类聚类被称为投影聚类 [10]。

# 数据聚类：算法与应用

### 10.5.1 STREAM 方法

微聚类（microclustering）方法也可以扩展到高维投影聚类的情况。该算法被称为 STREAM。在 [6,7] 中，这些方法应用于高维数据流。基本思想是使用 [6] 中的增量算法来处理高维数据。由于 EM 算法要求人们学习大量的参数，当数据演变非常快时，这种方法可能不会有效。由于稀疏性，聚类可能在所有维度上都无法完美定义，但可以找到某些维度子集，其中特定的点子集可以形成高质量且有意义的聚类。通过引入一个衰减因子 $\lambda$。由于稀疏性，在所有维度上可能无法完美定义聚类，但可以找到某些维度子集，其中特定的点子集可以形成高质量且有意义的聚类。当然，这些维度子集可能会随着不同的聚类而变化。此类聚类被称为投影聚类 [10]。 (由于提供的原文文本存在部分重复和逻辑断层，此处翻译根据原文结构进行了对齐)

*(注：原文中存在大量重复段，以下为对应后续段的翻译)*

概率模型常用于聚类的另一个领域是主题建模（topic modeling）[41]的情况。在这种技术中，使用软聚类来对数据进行软聚类，其中词汇和文档以概率的方式分配到不同的划分中。由于主题建模方法使用了 EM 算法，它在实践中可能运行很慢。因此，[20] 提出了一种用于文本主题建模的方法。[20] 中的工作提出了三种常用批处理算法的在线变体：隐狄利克特分布 (LDA) [22]、狄利克特多项分布 (DCM) 混合 [29] 和 von-Mises Fisher (vMF) 混合模型 [21]。[20] 显示，这种 vMF 方法的主题变体提供了最好的结果。对这些主题建模算法的详细研究超出了本综述的范围。感兴趣的读者请参考 [20]。

## 10.5 聚类高维数据流

在许多情况下，数据流是非常高维的，因为对于挖掘过程可以使用大量的特征。高维情况对传统静态数据案例领域的聚类算法构成了特殊的挑战。这是由于高维空间中数据的稀疏性导致的。在高维空间中，所有点对都倾向于彼此几乎等距。因此，以有意义的方式定义基于距离的聚类通常是不现实的。最近有一些关于投影聚类的高维基于距离的数据技术工作。在这些方法中，聚类的定义使得每个聚类都特定于一组维度。这在某种程度上考虑了高维空间内的稀疏性。尽管由于数据的稀疏性，聚类可能在所有维度上都无法完美定义，但可以找到某些维度子集，其中特定的点子集可以形成高质量且有意义的聚类。当然，这些维度子集可能会随着不同的聚类而变化。此类聚类被称为投影聚类 [10]。

# 数据聚类：算法与应用

### 10.5.1 STREAM 方法

微聚类方法也可以扩展到高维投影聚类的情况。该算法被称为 STREAM。在 [6,7] 中，这些方法应用于高维数据流。基本思想是使用 [6] 中的增量算法来处理高维数据。

*(由于用户提供的原文文本包含大量重复的句子和不完整的片段，上述译文严格按照所提供的片段进行翻译，并确保不漏译)*

算法的过程是：当一个数据点进入时，它被放入一个自己的簇中。对于后续的数据点，我们计算它们与数据中现有簇的相似性。如果输入的数据点与现有簇足够相似，则它们被放入该簇中。否则，该输入数据点被放入一个自己的簇中。StreamClCD 算法中的一个关键操作是维护每个簇中属性值的频率计数。为了这一目的，使用了 [50] 中引入的开销计数方法。其动机是减少维护频率计数时的内存占用。当每个属性的可能的离散值数量增加时，内存需求问题变得尤为重要。这被称为大规模域场景（massive-domain scenario），将在下一节中讨论。

## 10.6.3 大规模域聚类

大规模域是指一个或多个属性的可能值数量非常大的数据域。此类域的示例如下：

- *网络应用*，许多属性（如 IP 地址）源自数百万种可能性的范围。在多维应用中，由于不同属性之间可能性的乘积，这个问题被进一步放大。
- *典型的信用卡交易*，根据交易的性质，源自数百万种不同可能性的宇宙。
- *超市交易*通常源自数百万种可能性的宇宙。在这种情况下，从空间计算效率的角度来看，确定指示不同类型分类行为的模式可能变得不可行。

底层数据的海量限制了可以用于判别性分析的计算方法。这个问题比数据流的标准聚类要困难得多。对于数据流来说，空间效率是一个特别关注的问题，因为希望将大多数数据结构留在内存中，以最大限度地提高底层数据的处理率。较小的空间需求确保了大部分数据可能留在缓存中，这可以进一步提高方法的效率。此外，可能需要在各种空间受限的架构（如移动设备、传感器硬件或单元处理器）中实现聚类算法。如果底层架构不是空间高效，这些架构对大规模域情况提出了特殊挑战。

在大规模域情况下，聚类问题从空间和时间角度来看极具挑战性。这是因为人们需要保留数据中最相关簇的判别性特征。在大规模域情况下，这可能意味着存储大量可能的属性值的频率统计。虽然这在实现上可能很困难，但大量的数据流进一步阻碍了容易确定属性值重要性。[2] 中的工作提出了一种基于草图（sketch-based）的方法，以便跟踪底层簇的中间统计。这些统计数据用于对数据到簇的分配进行近似确定。[2] 中提供了许多概率结果，表明这些近似足够准确，可以提供与无限空间聚类算法相似的结果。

数据流 $\mathcal{D}$ 包含 $d$ 维记录，记为 $\mathbf{X}_1, \dots, \mathbf{X}_N$。$\mathbf{X}_i$ 的属性表示为 $(x_i^1, \dots, x_i^d)$。假设属性值 $x_i^k$ 源有序集 $J_k = \{v_1^k, \dots, v_{M^k}^k\}$。$M^k$ 的值表示第 $k$ 个属性的域大小。$M$ 的值可以非常大，范围在百万或十亿级。从聚类应用的角度来看，这产生了一系列挑战，因为在空间受限的情况下，不再可能持有簇统计信息。

## 数据流聚类算法综

算法 CSketch(标记数据流: $\mathcal{D}$, 簇数量: $k$)

```
