
其中 φ: R^N → R^{d_h} 是映射到维度为 d_h 的高维特征空间；b_l 为偏置项；且 l = 1, ..., maxk − 1。然而，对于大规模网络，我们可以利用底层特征映射的显式表达式且 d_h = N。由于 KSC 公式对任意正定核函数均有效，我们使用归一化线性核函数以避免任何核参数。投影 e_i^{(l)} 表示由 sign(e_i^{(l)}) 给出的 maxk − 1 个二元聚类指示符的潜在变量，可通过编码/解码方案与最终组组合。对应于该原始公式的对偶问题为

D^{-1} M_D α^{(l)} = λ_l α^{(l)} (9.5)

其中 M_D = I_{N_r} − (1/N_r 1_{N_r} 1_{N_r}^T D^{-1}) / (1_{N_r}^T D^{-1} 1_{N_r})。α^{(l)} 为对偶变量，且核函数 K: R^N × R^N → R 扮演相似度函数的作用。

## 9.2.3.2 模型选择

KSC-net 为用户提供选择两种模型选择技术之一的选项，即 BAF 准则 [1] 或自调优程序 [3]。

### 算法 1：BAF 模型选择准则

数据：给定码本 Cβ、maxk 和 P = {e_valid1, ..., e_valid_Nv}。

结果：最大 BAF 值和最优 k。

- 1. 对每个 k ∈ {2, ..., maxk} 执行
- 2. 使用码本 Cβ 计算训练节点的聚类成员。
- 3. 得到聚类 Δ = {C1, ..., Ck} 并计算每个 C_j 的聚类均值 u_j。
- 4. 对于每个验证节点 valid_d，得到 max_j cos(θ_{j,valid_d})，其中 cos(θ_{j,valid_d}) = (e_valid_d^T u_j) / (||e_valid_d|| ||u_j||)，j = 1, ..., k。
- 5. 维护字典 MaxSim(valid_i) = max_j cos(θ_{j,valid_i})，j = 1, ..., k。
- 6. 为验证节点得到聚类 Δ_valid = {C_valid1, ..., C_validk}。
- 7. 定义 BAF 为 BAF(k) = Σ_{i=1}^k Σ_{valid_i ∈ C_i} 1/k * MaxSim(valid_i) / |C_i|。
- 8. 结束
- 9. 保存最大 BAF 值以及对应的 k。

## 9.2.3.3 外样本扩展

理想情况下，当社区不重叠时，我们将得到 k 个良好分离的社区，且归一化拉普拉斯矩阵具有 k 个分段常数特征向量。这是因为最大特征值 1 的重数为 k，如文献 23 所示。

在 KSC 的情况下，由于中心化矩阵 M_D，特征向量具有零均值，且二值化特征向量的最优阈值是自确定的（等于 0）。因此我们需要 k − 1 个特征向量。然而，在真实网络中，社区表现出重叠且不具有分段常数特征向量。

### 算法 2：自动识别 k 个社区的算法

数据：P = {e_valid1, e_valid2, ..., e_valid_k}。

结果：给定大规模网络中的聚类数 k。

- 1. 使用投影向量 e_valid ∈ P 及其 CosDist() 构造 S。
- 2. 设置 t ∈ {0.1, 0.2, ..., 1}。
- 3. 对每个 t ∈ t 执行
- 4. 将 S 保存到临时变量 R 中，即 R := S 且 SizeC_t = []。
- 5. 当 S 不是空矩阵时循环
- 6. 找到余弦距离 < t 的节点数最多的 e_valid。
- 7. 确定这些节点的数量并将其追加到 SizeC_t。
- 8. 删除对应这些节点索引的行和列。
- 9. 结束
- 10. 如文献 3 中所述，从 SizeC_t 计算熵和期望平衡度。
- 11. 使用熵和平衡度计算 F 测度 F(t)。
- 12. 结束
- 13. 将 F 测度最大时的阈值作为 max t 得到。
- 14. 将 k 估计为向量 SizeC_max t 中项的个数。

解码方案包括将验证/测试阶段得到的聚类指示符与码本 C_B 进行比较，并基于汉明距离选择最近的码本。该方案对应于误差校正输出码 ECOC 解码程序 [24]，并在外样本扩展中也使用。

外样本扩展基于分数变量，该变量对应于将映射后的外样本节点投影到训练阶段找到的特征向量上。通过对出样本节点的分数变量进行二值化，可以得到聚类指示符

sign(e_test^{(l)}) = sign( Ω_test α^{(l)} + b_l 1_{N_test} ) (9.6)

其中 l = 1, ..., k − 1；Ω_test 是使用测试节点计算的 N_test × N_tr 核矩阵，其元素为 Ω_test,ij = K(x_i, x_j)；r = 1, ..., N_test；且 i = 1, ..., N_tr。这种对外样本节点的自然扩展是 KSC 的主要优势。这样，聚类模型可以在无监督学习过程中进行训练、验证和测试。对于测试集，我们使用整个网络。如果网络无法放入内存，我们将其划分为块以并行计算每个测试块的聚类成员。

![图 9.4](img/1643181e79c76dc765d55a7355afb4a4_202_0.png)

图 9.4 使用自调优准则为合成网络选择最优 k。

network. 调整兰德指数 ARI [25] 的值为 0.999，这意味着 KSC 方法提供的社区成员与原始真实情况一样好。如果我们在算法 3 的演示脚本中将 mod_sel = 'Self'，则执行自调优模型选择。它使用熵和平衡聚类的概念来识别网络中的最优聚类数 k。图 9.4 展示了使用自调优模型选择程序从验证集的特征投影生成的块对角亲和矩阵 S。从图 9.4 可以观察到亲和矩阵 S 中有七个块。为了计算这些块的数量，自调优程序将熵和平衡的概念一起用作 F 测度。图 9.4 显示 F 测度在阈值 t = 0.2 时最大，其值为 2.709。对应于该阈值值识别出的聚类数 k 为 7，这与真实社区的数量相等。

### 算法 3：使用 BAF 准则的合成网络演示脚本

```text
Data:
netname = 'network'; // Name of the file and extension should be '.txt'
baseinfo = 1; // Ground truth exists
cominfo = 'community'; // Name of ground truth file and extension should be '.txt'
weighted = 0; // Whether a network is weighted or unweighted
frac_network = 15; // Percentage of network to be used as training and
maxk = 10; // maxk is maximum value of k to be used in eigen-decomposition, use
// maxk = 10 for k <= 10 else use maxk = 100
mod_sel = 'BAF'; // Method for model selection (options are 'BAF' or 'Self')
output = KSCnet(netname,baseinfo,cominfo,weighted,frac_network,maxk,mod_sel);
```

```text
Result
output = 1; // When community detection operation completes
netname_numclu_mod_sel.csv; // Number of clusters detected
netname_outputlabel.csv; // Cluster labels assigned to the nodes
netname_ARI.csv; // Valid only when ground truth is known, provides information
// about ARI and number of communities covered
```

## 9.3.2 KSC 子函数

我们简要描述在 KSCnet() 函数中调用的一些子函数。首先，大规模网络以边列表形式提供，可能带或不带真实信息；我们将边列表转换为稀疏邻接矩阵 A。frac_network 提供有关网络总节点数中有百分之多少用于训练和验证集的信息。我们设置条件以检查 N_tr 或 N_valid 不能超过最大值为 5000。然后我们使用 “system” 命令运行 FURS 选择技术，如脚本语言 Python 中所实现。Python 先决条件在 “ReadMe.txt” 中提供。图 9.5 演示了使用 FURS 选择技术选择训练和验证集时获得的输出。

从图 9.5 可以观察到，语句 “First Step of the Sampling Process Completed” 出现了两次（一次用于训练，一次用于验证）。

- **KSCmod.** KSCmod 函数接收一个布尔状态变量作为输入，以确定是训练阶段还是测试阶段。如果为 0，则我们提供训练和验证集作为输入；否则，输入为训练和测试集。它还接收 maxk 和特征值分解算法作为输入（选项为 “eig” 或 “eigs”）。它使用 Python 代码计算核矩阵，然后求解特征值分解问题以获得模型。输出为模型及其参数、训练/验证/测试集特征投影以及码本 C_B。对于验证集，我们还获得对应于 maxk 的社区归属，但对于测试集，我们获得对应于最优 k 的聚类成员。
- **KSCcodebook.** KSCcodebook 接收特征投影和特征向量作为输入。它取这些特征投影的符号，计算前 k 个最频繁的代码词并将其输出为码本。它还使用 KSCmembership 函数估计训练节点的聚类成员。
- **KSCmembership.** KSCmembership 接收训练/验证/测试集的特征投影和码本作为输入。它取这些特征投影的符号并计算码本与符号 e 之间的汉明距离。它将相应节点分配给与其汉明距离最小的聚类。

在 BAF 模型选择准则的情况下，我们利用 KSCcodebook 和 KSCmembership 功能来估计最优社区数 k 的

```text
>> descscript
First Step of the Sampling Process Completed
Degree Matrix Empty for the 1 time
Degree Matrix Empty for the 2 time
0.960400104523 seconds
Elapsed time is 1.072581 seconds.
First Step of the Sampling Process Completed
Degree Matrix Empty for the 1 time
Degree Matrix Empty for the 2 time
0.637403992517 seconds
Elapsed time is 0.743813 seconds.
```

图 9.5 选择训练和验证集的 FURS 输出。
