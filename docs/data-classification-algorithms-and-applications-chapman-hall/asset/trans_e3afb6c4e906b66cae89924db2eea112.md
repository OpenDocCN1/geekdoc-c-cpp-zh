

| 年龄 | 硬 | 无 | 软 |
|---:|---:|---:|---:|
| 8 | 1 | 1 | 0 |
| 11 | 0 | 1 | 0 |
| 13 | 0 | 1 | 0 |
| 14 | 0 | 1 | 0 |
| 16 | 1 | 0 | 0 |
| 18 | 0 | 0 | 2 |
| 23 | 1 | 1 | 0 |
| 26 | 0 | 1 | 0 |
| 32 | 0 | 1 | 0 |
| 35 | 0 | 1 | 1 |
| 36 | 0 | 0 | 1 |
| 39 | 0 | 1 | 0 |
| 44 | 0 | 0 | 1 |
| 46 | 0 | 1 | 0 |
| 47 | 0 | 1 | 0 |
| 51 | 1 | 0 | 0 |
| 52 | 0 | 1 | 0 |
| 55 | 0 | 1 | 0 |
| 63 | 0 | 1 | 0 |
| 64 | 0 | 1 | 0 |

(a) 年龄属性的 AVC 表（RainForest）

| 近/远 | 硬 | 无 | 软 |
|---|---:|---:|---:|
| 远 | 1 | 8 | 3 |
| 近 | 3 | 7 | 2 |

| 眼泪 | 硬 | 无 | 软 |
|---|---:|---:|---:|
| 正常 | 4 | 3 | 5 |
| 减少 | 0 | 12 | 0 |

| 散光 | 硬 | 无 | 软 |
|---|---:|---:|---:|
| 否 | 0 | 7 | 5 |
| 是 | 4 | 8 | 0 |

(b) 其他三个 AVC 表（RainForest 和 SPIES）

| 年龄 | 硬 | 无 | 软 |
|---|---:|---:|---:|
| 1-10 | 1 | 1 | 0 |
| 11-19 | 1 | 3 | 2 |
| 20-29 | 1 | 2 | 0 |
| 30-39 | 0 | 3 | 2 |
| 40-49 | 0 | 2 | 1 |
| 50-59 | 1 | 2 | 0 |
| 60-69 | 0 | 2 | 0 |

(c) 年龄属性的简洁 AVC 表（SPIES）

**图 4.4：** RainForest 和 SPIES 的 AVC 表。

## 4.4.2 SPIES 方法

在 [39] 中，提出了一种新的方法，称为 SPIES（用于增强可扩展性的区间统计修剪），旨在使决策树构建更节省内存和通信。算法在 *SPIES-Classifier* 过程（算法 4.2）中给出。

**算法 4.2 SPIES-Classifier**

```text
 1: function SPIES-CLASSIFIER(Level L, Dataset X)
 2:   for Node v ∈ Level L do
   { *Sampling Step* }
 3:     Sample S ← Sampling(X);
 4:     Build_Small_AVCGroup(S);
 5:     Build_Concise_AVCGroup(S);
 6:     g′ ← Find_Best_Gain(AVCGroup);
 7:     Partial_AVCGroup ← Pruning(g′, Concise_AVCGroup);

   { *Completion Step* }
 8:     Build_Small_AVCGroup(X);
 9:     Build_Concise_AVCGroup(X);
10:     Build_Partial_AVCGroup(X);
11:     g ← Find_Best_Gain(AVCGroup);

12:     if False_Pruning(g, Concise_AVCGroup)
   { *Additional Step* }
13:     Partial_AVCGroup ← Pruning(g, Concise_AVCGroup);
14:     Build_Partial_AVCGroup(X);
15:     g ← Find_Best_Gain(AVCGroup);
16:     if not satisfy_stop_condition(v)
17:       Split_Node(v);
18:   end for
19: end function
```

SPIES 方法基于 AVC 组，与 RainForest 方法类似。关键区别在于数值属性的处理方式。在 SPIES 中，节点的 AVC 组由三个子组组成：

- *Small AVC group:* 这主要由所有分类属性的 AVC 集合组成。由于分类属性的不同元素数量通常不大，这些 AVC 集合的规模很小。此外，SPIES 还为仅具有少量不同元素的数值属性添加 AVC 集合。这些集合的构建和处理方式与 RainForest 方法相同。

- *Concise AVC group:* 数据集中具有大量不同元素的数值属性的取值范围被划分为 *区间*。区间的数量以及区间的构造方式是算法的重要参数。原始 SPIES 实现使用等宽区间。简洁 AVC 组记录每个区间的类直方图（即每个类的出现频率）。

- *Partial AVC group:* 基于简洁 AVC 组，算法计算出数值属性取值范围内可能包含分割点的子集。部分 AVC 组存储已确定为分割条件候选的数值属性取值范围内的点的类直方图。

SPIES 使用两次遍历高效构建上述 AVC 组。第一次遍历是快速的 *Sampling Step*。在此，使用数据集的样本来估计小 AVC 组和简洁数值属性。基于这些，它获得最佳（最高）增益的估计值，记为 g′。然后，利用 g′，修剪掉不太可能包含分割点的区间。第二次遍历是 Completion Step。在此，使用整个数据集构建三个 AVC 子组的完整版本。部分 AVC 组将记录未被修剪区间内所有点的类直方图。

之后，可以从这些 AVC 组中获得最佳增益 g。由于修剪仅基于小和简洁 AVC 组的估计，因此可能发生错误修剪。然而，错误修剪可以在完成步骤期间使用更新后的小和简洁 AVC 组的值来检测。如果发生错误修剪，SPIES 可以对数据进行另一次遍历，以为被错误修剪的区间中的点构建部分 AVC 组。实验评估表明 SPIES 大大减少了内存需求，通常减少 85% 至 95%，并且错误修剪很少发生。

在图 4.4(c) 中，我们展示了假设使用 10 年范围的年龄属性的简洁 AVC 集合。表大小取决于所选的范围大小。将其大小与图 4.4(a) 中的 RainForest AVC 进行比较。对于离散属性和具有少量不同值的数值属性，RainForest 和 SPIES 生成相同的 small AVC 表，如图 4.4(b) 所示。

多年来已经开发出其他可扩展的决策树构建算法；代表性算法包括 BOAT [30] 和 CLOUDS [2]。BOAT 使用一种称为自助法的统计技术，将决策树构建减少到对整个数据集的尽可能少的两次遍历。此外，BOAT 可以处理数据的插入和删除。CLOUDS 是另一种使用区间来加速数值属性处理的算法 [2]。然而，CLOUDS 的方法不能保证与考虑所有可能的数值分割点所能达到的同等准确性水平（尽管在他们的实验中，差异通常很小）。此外，CLOUDS 在树的某一层划分节点时始终需要对数据集进行两次扫描。最近，SURPASS [47] 在递归划分过程中利用线性判别式。汇总统计信息（如 AVC 表）是增量获得的。与使用汇总统计信息不同，[74] 对训练数据进行采样，其置信水平由 PAC 学习理论确定。

## 4.4.3 并行决策树构建

 several studies have sought to further speed up the decision tree construction using parallel machines. 其中最早的研究之一是由 Zaki 等人 [88] 提出的，他们在磁盘驻留数据集上对 SPRINT 算法进行了共享内存并行化。在并行化 SPRINT 时，每个属性列表分配给单独的处理机。此外，Narlikar 使用细粒度线程库并行化了决策树算法 [57]，但该工作仅限于内存驻留数据集。RF-read 算法 [38] 已提出共享内存并行化。

SPIES 方法已使用中间件系统 FREERIDE（数据挖掘引擎快速实现框架）[36,37] 进行并行化 [39]，该系统支持磁盘驻留数据集上的分布式和共享内存并行化。FREERIDE 于 2000 年初开发，可被视为流行的 MapReduce/Hadoop 系统 [16] 的早期原型。它基于这样一个观察：许多流行的数据挖掘算法具有相对相似的结构。它们的共同处理结构本质上是广义归约。在算法的每个阶段，计算涉及以任意顺序读取数据实例，处理每个数据实例（类似于 MapReduce 中的 Map），并使用关联和交换运算符更新归约对象的元素（类似于 MapReduce 中的 Reduce）。

在分布式内存环境中，此类算法可以通过将数据项分配给处理器并复制归约对象来进行并行化。每个节点可以处理其拥有的<|message|>
