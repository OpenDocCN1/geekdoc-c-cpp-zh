

- [70] X. Wu, K. Yu, H. Wang, and W. Ding. Online streaming feature selection. In Proceedings of the 27th International Conference on Machine Learning, pages 1159–1166, 2010.
- [71] Z. Xu, R. Jin, J. Ye, M. Lyu, and I. King. Discriminative semi-supervised feature selection via manifold regularization. In IJCAI'09: Proceedings of the 21st International Joint Conference on Artificial Intelligence, 2009.
- [72] S. Yang, L. Yuan, Y. Lai, X. Shen, P. Wonka, and J. Ye. Feature grouping and selection over an undirected graph. In Proceedings of the 18th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 922–930. ACM, 2012.
- [73] J. Ye and J. Liu. Sparse methods for biomedical data. ACM SIGKDD Explorations Newsletter, 14(1):4–15, 2012.
- [74] L. Yu and H. Liu. Feature selection for high-dimensional data: A fast correlation-based filter solution. In International Conference on Machine Learning, 20:856, 2003.
- [75] M. Yuan and Y. Lin. Model selection and estimation in regression with grouped variables. Journal of the Royal Statistical Society: Series B (Statistical Methodology), 68(1):49–67, 2006.
- [76] P. Zhao and B. Yu. On model selection consistency of Lasso. Journal of Machine Learning Research, 7:2541–2563, 2006.
- [77] Z. Zhao and H. Liu. Semi-supervised feature selection via spectral analysis. In Proceedings of SIAM International Conference on Data Mining, 2007.
- [78] D. Zhou, J. Huang, and B. Schölkopf. Learning from labeled and unlabeled data on a directed graph. In International Conference on Machine Learning, pages 1036–1043. ACM, 2005.
- [79] J. Zhou, J. Liu, V. Narayan, and J. Ye. Modeling disease progression via fused sparse group Lasso. In Proceedings of the 18th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 1095–1103. ACM, 2012.
- [80] H. Zou. The adaptive lasso and its oracle properties. Journal of the American Statistical Association, 101(476):1418–1429, 2006.
- [81] H. Zou and T. Hastie. Regularization and variable selection via the elastic net. Journal of the Royal Statistical Society: Series B (Statistical Methodology), 67(2):301–320, 2005.

## 3.1 引言

在机器学习中，分类被视为监督学习方法的一种实例，即从带标签的训练数据中推断出一个函数。训练数据由一组训练样本组成，每个样本是一个由输入对象（通常是向量）**x** = ⟨x₁, x₂, …, x_d⟩ 和期望输出值（通常是类别标签）y ∈ {C₁, C₂, …, C_K} 构成的配对。给定这样一组训练数据，分类算法的任务是分析训练数据并生成一个推断函数，该函数可用于通过为每个新样本分配正确的类别标签来分类新的（迄今为止未见过的）样本。一个例子是将给定的电子邮件归入“垃圾邮件”或“非垃圾邮件”类别。

分类的一个常见子类是*概率分类*，在本章中我们将重点介绍一些概率分类方法。概率分类算法使用统计推断为给定样本找到最佳类别。除了像其他分类算法一样简单地分配最佳类别外，概率分类算法还会输出该样本属于每个可能类别的相应概率。通常会选择概率最高的类别作为最佳类别。一般来说，概率分类算法相比非概率分类器具有几个优势。首先，它可以输出与其所选类别标签相关联的置信度值（即概率），因此如果其对选择任何特定输出的置信度过低，它可以放弃分类。其次，概率分类器可以更有效地整合到更大的机器学习任务中，从而部分或完全避免错误传播问题。

在概率框架内，概率分类的关键点在于估计后验类别概率 *p*(C_k|x)。获得后验概率后，我们使用决策理论 [5] 为每个新输入 **x** 确定类别归属。基本上，我们有两种方法可以估计后验概率。

第一种情况，我们专注于分别确定每个类别 C_k 的类别条件概率 *p*(x|C_k)，并单独推断先验类别 *p*(C_k)。然后利用贝叶斯定理，我们可以获得后验类别概率 *p*(C_k|x)。等价地，我们可以直接对联合分布 *p*(x, C_k) 建模，然后进行归一化以获得后验概率。由于类别条件概率定义了生成我们所测量特征的统计过程，这些显式或隐式地对输入和输出分布进行建模的方法被称为*生成模型*。如果观测数据确实是从生成模型中采样得到的，那么拟合生成模型的参数以最大化数据似然是一种常用方法。在本章中，我们将介绍两种常见的概率生成模型用于分类的示例：朴素贝叶斯分类器和隐马尔可夫模型。

另一类模型是通过学习一个判别函数 *f*(x) = *p*(C_k|x) 来直接建模后验概率 *p*(C_k|x)，该函数将输入 **x** 直接映射到类别标签 C_k。这种方法通常被称为*判别模型*，因为所有努力都集中在定义整体判别函数，同时考虑类别条件概率。例如，在二类问题中，*f*(x) = *p*(C_k|x) 可能是 0 到 1 之间的连续值，使得 *f* < 0.5 表示类别 C₁，而 *f* > 0.5 表示类别 C₂。在本章中，我们将介绍几种概率判别模型，包括逻辑回归（一种广义线性模型 [23]）和条件随机场。

在本章中，我们介绍几种用于概率分类的基本模型和算法，包括以下内容：

- **朴素贝叶斯分类器。** 朴素贝叶斯分类器是一种简单的概率分类器，它基于应用贝叶斯定理并带有强（朴素）独立性假设。朴素贝叶斯分类器的一个典型应用是文档分类。
- **逻辑回归。** 逻辑回归是一种基于一个或多个观测变量来预测分类因变量结果的方法。描述可能结果的概率使用逻辑函数建模为观测变量的函数。
- **隐马尔可夫模型。** 隐马尔可夫模型（HMM）是动态贝叶斯网络的一种简单情形，其中隐藏状态形成一条链，并且每个状态只有某些可能的值可以被观测到。HMM 的一个目标是根据观测值及其依赖关系推断隐藏状态。HMM 的一个非常重要的应用是自然语言处理中的词性标注。
- **条件随机场。** 条件随机场（CRF）是马尔可夫随机场的一种特殊情况，但每个节点的状态都以某些观测值为条件。CRF 可以被视为一种判别式分类器，因为它们不对观测值的分布进行建模。信息抽取中的命名实体识别是 CRF 的应用之一。

本章组织如下。在第 3.2 节中，我们简要回顾贝叶斯定理，并介绍朴素贝叶斯分类器，这是一种成功的生成式概率分类方法。在第 3.3 节中，我们描述一种流行的判别式概率分类方法——逻辑回归。随后，我们在第 3.4 节开始讨论用于分类的概率图模型，介绍两种流行的概率分类模型，即隐马尔可夫模型和条件随机场。最后，我们在第 3.5 节给出总结。

## 3.2 朴素贝叶斯分类

朴素贝叶斯分类器基于贝叶斯定理，特别适用于输入维度较高的情况。尽管朴素贝叶斯分类器很简单，但它通常可以达到与一些复杂分类方法（如决策树和选定的神经网络分类器）相当的性能。朴素贝叶斯分类器在应用于大型数据集时也表现出高准确性和高速度。在本节中，我们将简要回顾贝叶斯定理，然后概述朴素贝叶斯分类器及其在机器学习中的应用，特别是文档分类。

### 3.2.1 贝叶斯定理与预备知识

一个广泛使用的分类框架由概率论中的一个简单定理 [5, 11] 提供，即贝叶斯定理或贝叶斯法则。在介绍贝叶斯定理之前，让我们先以如下形式回顾概率论的两个基本规则：

$$p(X) = \sum_Y p(X,Y) \tag{3.1}$$

$$p(X,Y) = p(Y\mid X)p(X). \tag{3.2}$$

