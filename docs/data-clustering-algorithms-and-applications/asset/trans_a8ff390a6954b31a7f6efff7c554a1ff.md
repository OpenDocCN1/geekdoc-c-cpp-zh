

## 数据聚类：算法与应用

STIRR 的缺点在于其对初始对象顺序的敏感性。它也没有确定的收敛性。权重的概念不直观，并且有多个参数需要用户指定。最终检测到的聚类是不完整的 [76]。

## 12.4.3.5 CLO

CLOPE 代表“Clustering with SLO”。它适用于对高维事务数据库进行聚类，例如市场篮子数据和 Web 服务器日志。CLOPE 被认为在事务数据库和高维数据集上快速且可扩展。CLOPE 使用增加聚类高度-宽度比的启发式方法 [74]。给定一个聚类 C，CLOPE 找到聚类中的所有项目及其各自的发生次数，即包含该项目的事务数。D(C) 是不同项目的集合，Occ(i) 是项目 i 在聚类 C 中的出现次数。CLOPE 绘制聚类 C 的直方图，X 轴按其出现次数递减排序，Y 轴为。

图 12.5 显示了两个聚类各有两个聚类的示例。对于每个聚类，统计每个不同项目的出现次数并将结果绘制为直方图。每个聚类的直方图的高度 H 和宽度 W 得到。使用聚类直方图的高度-宽度比，CLOPE 定义了聚类的全局准则函数。此示例表明，直方图的高度-宽度比越大，意味着聚类内相似性越好。

CLOPE 聚类的主要缺点是直方图对于某些数据集可能不是最优的。

## 12.4.3.6 HIERD: 层次密度聚类

![](img/b94d85a2e934001944bcc21abd9a9943_318_0.png)

**图 12.5：** 两个聚类（每个聚类有两个）的小数据集的直方图：（1）{{ab, abd}, {de, def}} 和（2）{{ab, abc}, {acd, def}}。聚类的高度-宽度用于选择最佳聚类。聚类 {de {de, def} 和 {ab, abc}} 的两个直方图质量不同。第一个聚类 {ab, abc, abd} 中 a:3, b:2, c:2, d:1 的出现次数。聚类 {ab, abc, abd} 的直方图有 4 个项目对应 8 个块，H=2.0 且 W=4（H/W=0.5）。第二个聚类 {acd, def} 的直方图有 5 个项目对应 8 个块，H=1.6 且 W=5（H/W=0.32）。第一个聚类更可取，因为更大的高度-宽度比意味着同一聚类中事务之间的重叠更多。

© 2014 by Taylor & Francis Group, LLC

## 聚类分类数据

我们有一个对象数据集 $S$（可能包含重复项），具有 $m$ 个分类属性，$X_1, \dots, X_m$。每个属性都有一个域 $D_i$，具有有限的 $d_i$ 个值。空间 $S^m$ 可以被视为一个 $m$ 维“立方体”，具有 $\prod_{i=1}^m d_i$ 个单元。单元 $\mathbf{x} = (x_1, \dots, x_m) \in S^m$ 表示由函数 $freq(\mathbf{x})$ 给出的对象集合，其中所有 $m$ 个属性都等于 $(x_1, \dots, x_m)$。我们定义 HIERDEND 超立方体 $C(\mathbf{x}_0, r) \subset S^m$，以 $\mathbf{x}_0$ 为中心，半径为 $r$，为：

```
$C(\mathbf{x}_0, r) = \{\mathbf{x} \in S^m \text{ and } dist(\mathbf{x}, \mathbf{x}_0) \leq r \text{ and } freq(\mathbf{x}) > 0\}$
```

$dist(-)$ 是一个距离，可以是 Hamming 距离。
图 12.1 说明了 3 维立方体中的两个 HIERDEND 超立方体。$freq(x) = 1$ 的单元立方体未显示，因为没有具有立方体形状的对象。通常，超立方体将等于 $S^m$ 的子空间。
子空间 $X \subset S^m$ 的密度，其中 X 可能等于超立方体 $C(\mathbf{x}_0, r) \subset S^m$，涉及对 X 的所有单元求和 $freq(x)$：

```
$density(X) = \sum_{\mathbf{c} \in X} \frac{freq(\mathbf{c})}{|\mathbf{c}|}$
```

该密度可以被视为超立方体包含 $S$ 中随机对象的可能性，其中 $|S|$ 是 $S$ 的大小。HIERDEND 找到最密集的超立方体 $C(\mathbf{x}_0, r) \subset S^m$。这是包含 $S$ 中随机对象的最大可能性的那个。
图 12.6 显示了 HIERDEND 聚类算法。$G_k$ 表示第 k 个聚类。剩余集合，$R=\{\mathbf{x} \in S^m \text{ and } \mathbf{x} \notin G_i; i=1, \dots, k\}$，是所有 $k$ 个聚类的收集对象的并集。
步骤 1 检索半径为 $r$ 的最密集超立方体 $C \subset S^m$。步骤 1 检查最密集超立方体是否代表多于一个对象（$density(C) > 1$），否则聚类包含零个或一个对象，则 $r$ 增加，以此类推。步骤 2 在级别 $r \geq1$ 处创建一个新的叶聚类。从现有叶开始，步骤 3 尝试移动到附近半径为 $r$ 的最密集超立方体。如果超立方体很密集，步骤 4 通过包含超立方体的单元来扩展聚类。这对一个聚类重复进行，直到无法再建立连接。新的对象在 $r=m$ 之前创建，大多数对象是 $freq(r) \leq1$ 且未连接的聚类被视为异常值（步骤 5）。对于许多数据集，在 $r=m$ 之前大多数对象很可能已被聚类。
最初 $r$ 默认值为 1，因为大多数数据集包含相似对象的子集。当 $r$ 增加时，子集被聚类，一个特殊过程合并相对于 $r$ 相连的聚类。尽管初始 $r=1$ 值可能导致许多聚类，但相似聚类会逐渐合并。链接表示在级别 $r \geq2$ 处创建的两个或多个聚类之间的关系。链接表示合并的聚类组。此过程构建一个或多个树结构，构建层次聚类 [50, 61]。用户指定截止级别（例如，$r=3$）以剪切树分支；链接相对于 $r$ 的截止级别，如果在级别 $r$ 存在链接，步骤 5 检查新形成的聚类是否连接到另一个聚类。步骤 6 将现有聚类链接到树中，直到 $r=m$。通过允许 $r$ 达到 $m$，构建了一个条目。在树的顶部，有一个包含数据集所有对象的单个聚类。

## 12.4.3.7 MULTIC: 多层增量聚类

MULTIC 代表“分类数据的多层增量聚类”。MULTIC 是 HIERDEND 的更快实现。MULTIC 在聚类准确性和时间效率之间取得平衡-

## 数据聚类：算法与应用

```
Input: space $S^m$.$\nOutput: a hierarchy of clusters.\nMethod:\nnr = 1. //radius of hyper-cubes\nR = $S^m$. //set of unclustered cells\nk = 0. //number of leaf cells\nk_r = 0. //number of clusters at level r\nG_k = null. //k-th cluster\nU = null. //set of hyper-cube centers
```

步骤 1：找到 $\mathbf{x}_0 \in R$ 使得 $maxdensity(C(\mathbf{x}_0, r))$。

+   如果 $density(C(\mathbf{x}_0, r)) \le \frac{1}{n}$，则：\n$r = r + 1$。$\n如果 $k_r > 1$，则：\n合并相对于 $r$ 相连的聚类\n$k_r = \#merged + \#unmerged clusters$。$\n重复步骤 1。

步骤 2：设置 $\mathbf{x}_e = \mathbf{x}_0, k = k+1, G_k = C(\mathbf{x}_e, r), R = R - C(\mathbf{x}_e, r)$ 和 $U = U \cup{\mathbf{x}_e}$。

步骤 3：找到 $\mathbf{x}^* \in C(\mathbf{x}, r)$ 使得 $\mathbf{x}^* \notin U$ 且 $maxdensity(C(\mathbf{x}^*, r))$。

+   如果 $density(C(\mathbf{x}^*, r)) > \frac{1}{n}$，则：\n更新当前聚类 $G_k: G_k = G_k \cup C(\mathbf{x}^*, r)$。$\n更新 $R: R = R - C(\mathbf{x}^*, r)$。$\n更新 $U: U = U \cup{\mathbf{x}^*}$。$\n重置新的中心：$\mathbf{x}_e = \mathbf{x}^*$。$\n转到步骤 3。\n否则，移动到下一步。

+   步骤 5：设置 $k_r = k_r + 1.$\n如果 $k_r > 1$，则执行行 (3)-(4)。\n如果 $r < m$ 且 $density(R) > 1$，转到步骤 1。

步骤 6：当 $r < m$ 时，执行行 (1)-(4)。

图 12.6：HIERD 算法。

关注聚类质量以及方法的速度和对大型数据集的可扩展性。MULTIC 由对具有少量多层结构分类数据集的聚类动机而来。实例，在网络中，一个聚类（或模块）可能有一个由少数紧密连接的对象（节点）组成的中心，周围是稀疏连接的外围 [27, 13, 8, 9, 11]。在数据上，MULTIC 优于创建平面聚类的其他算法。MULTIC 产生分层（或嵌套）聚类，这与传统层次聚类在几个方面不同。MULTIC 不需要指定的参数，并且产生的聚类对于生物信息学中寻找蛋白质模块和复合体以及可视化很有用 [7, 11, 13, 62, 68]。

© 2014 by Taylor & Francis Group, LLC

