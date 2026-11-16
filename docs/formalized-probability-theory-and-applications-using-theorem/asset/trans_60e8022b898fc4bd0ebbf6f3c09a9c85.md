

### 图 6. 一个简单的管道

![](img/0e284aa46fa831bc38a68343fef110e3_215_0.png)

按其故障率（\(\lambda\)）分为 3 类，即 30 个段（\(\lambda = 0.0025\)）、20 个段（\(\lambda = 0.0023\)）和 10 个段（\(\lambda = 0.015\)）。所提出的管道可靠性分析方法允许我们正式验证涉及任意数量段和任意故障率的通用表达式。在本节中，我们正式验证了图 5 所示简单管道的可靠性，该管道有 N 个段，具有任意指数分布的故障时间（Zhang & Shao, 2008）。

我们通过在 HOL 中形式化指数随机变量，对图 6 所示管道进行正式可靠性分析。

### 定义 12.18

```
|- ∀ p X l. exp_dist p X l = ∀ x. (CDF p X x = if 0 ≤ x then 1
- exp (-1 * x) else 0)
```

谓词 exp_dist 确保随机变量 X 在概率空间 p 中具有故障率 l 的指数随机变量的累积分布函数（CDF）。我们根据此定义对一组指数分布随机变量列表进行分类，如下所示：

### 定义 12.19

```
|- ∀ p L. list_exp [ ] L = T ∧
∀ p h t L. list_exp p (h::t) L =
exp_dist p (HD L) h ∧ list_exp p t (TL L)
```

list_exp 函数接受一个故障率列表、一个随机变量列表 L 和一个概率空间 p。它保证列表 L 中的所有元素在概率空间 p 中都服从指数分布，对应的故障率由另一个列表给出。为此，它使用了列表函数 HD 和 TL，分别返回列表的头部和尾部。

接下来，我们将图 5 所示的管道建模为串行 RBD，如下所示：

### 定义 12.20

```
|- ∀ p L . pipeline p L = rel_series p L
```

现在，我们可以使用定义 12.19 来保证函数 pipeline 的随机变量列表参数仅包含指数随机变量，从而验证管道可靠性的以下简化表达式。

### 定理 12.15

```
⊢ ∀ p L x C. prob_space p ∧ (events p = POW (p_space p)) ∧
0 ≤ x ∧ x ≤ 2 ∧ LENGTH (rel_event_list p L x) ∧ mutual_indep p
(rel_event_list p L x) ∧
list_exp p C L ∧ (LENGTH C = LENGTH L) ⇒
(pipeline p (rel_event_list p L x) = exp (-list_sum C * x))
```

前五个假设与定理 12.9 中使用的相同。第六个假设 list_exp p C L 确保随机变量列表 L 包含所有指数随机变量，其对应的故障率由列表 C 给出。下一个假设保证两个列表 L 和 C 的长度相同。而定理 12.5 的结论表示给定管道模型所需的可靠性关系。这里函数 list_sum 递归地添加其列表参数的元素，并用于添加所有指数分布随机变量的故障率，这些故障率反过来用于建模管道串行 RBD 的各个段。定理 12.15 的证明基于定理 12.9 和指数函数 exp 的某些性质。与涉及概率论指导的定理 12.9 验证推理相比，该推理非常直接（约 100 行 HOL 代码）。这一事实说明了我们核心形式化在进行管道可靠性分析方面的有用性。

此经正式验证结果的显著特点包括其通用性，即所有变量都是普遍量化的，因此可以特例化以获得给定管道在任何给定参数下的可靠性；以及其正确性得到保证，因为验证过程中涉及可靠的定理证明器，这确保了结果有效性所需的所有假设都伴随定理。另一个值得提及的点是，管道各段的单独故障率可以以列表形式（即 C）轻松提供给上述定理。上述提到的优势并非任何其他基于计算机的石油和天然气管道可靠性分析方法所共有，从而清楚地表明了所提方法的有用性。

## 12.6 结论

由于工程系统在安全关键型应用中的广泛使用，可靠性分析的准确性已成为当务之急，错误的可靠性估计可能导致包括无辜生命损失在内的灾难性后果。在本章中，我们提出了常用 RBD 配置（即串行、并行、并串行和串并行）的高阶逻辑形式化，以便在定理证明器中促进安全关键型系统的正式可靠性分析。为了说明所提方法的有效性，我们还分析了一个十九节点的网络和一个简单的石油和天然气管道结构，发现我们分析的通用性和可靠性是其显著特点。在本章所提出结果的基础上，其他常用 RBD（如 K-out-of-N）和韦伯分布随机变量的形式化工作正在进行中。除这些基础性发展外，我们还计划开展一些涉及机械系统（如管道和汽车）以及云计算中虚拟数据可依赖性分析的广泛案例研究。

## 参考文献

Abbasi, N. (2012). 基于高阶逻辑定理证明的可靠性分析。(博士论文)。Concordia University, Montreal, Canada.

Abbasi, N., Hasan, O., & Tahar, S. (2010). 使用连续随机变量的形式寿命可靠性分析。载于《逻辑、语言、信息与计算研讨会论文集》(LNCS)，(第 6188 卷，第 84–97 页)。Springer。doi:10.1007/978-3-642-13824-9_8

Abbasi, N., Hasan, O., & Tahar, S. (2010). 使用定理证明的可靠性分析。IEEE Transactions on Computers, 59(5), 579–592. doi:10.1109/TC.2009.165

Abbasi, N., Hasan, O., & Tahar, S. (2014). 使用定理证明的寿命可靠性分析方法。Journal of Computer and System Sciences, 80(2), 323–345. doi:10.1016/j.jcss.2013.05.002

Abd-Allah, A. (1997). 将可靠性框图扩展到软件架构 (技术报告 USC-CSE-97-501)。南加州大学计算机科学系。

Ahmad, W., Hasan, O., Tahar, S., & Hamdi, M.S. (2014). 迈向石油和天然气管道的形式可靠性分析。载于《智能计算机数学会议论文集》(LNAI)，(第 8543 卷，第 30–44 页)。Springer。

ASENT RBD 分析工具。(2015)。2015 年 2 月 7 日检索自 https://www.raytheoneagle.com/asent/rbd.htm

Billinton, R., & Allan, R. N. (1992). 工程系统可靠性评估。Springer。doi:10.1007/978-1-4899-0685-4

Hasan, O., Tahar, S., & Abbasi, N. (2010). 使用定理证明的可靠性分析。IEEE Transactions on Computers, 59(5), 579–592. doi:10.1109/TC.2009.165

Huffman, D. L., & Antelme, F. (2009). 具有优雅降级的太阳能发电系统可用性分析。载于《可靠性与可维护性研讨会论文集》(第 348–352 页)。IEEE。doi:10.1109/RAMS.2009.4914701

Kolowrocki, K. (2009). 具有劣化组件的多状态系统可靠性与风险分析。Electronic Journal of International Group on Reliability, 2(1), 86–104.

Lin, C., Teng, H., Yang, C., Weng, H-L., Chung, M-C., & Chung, C-C. (2010). 使用可靠性框图的网状网络可靠性分析。载于《工业信息学 (INDIN)》(第 975–979 页)。IEEE。

ReliaSoft。(2015)。2015 年 2 月 7 日检索自 http://www.reliasoft.com/

Robidoux, R., Xu, R. H., Xing, L., & Zhou, M. (2010). 使用彩色 Petri 网的动态可靠性框图自动建模。IEEE Transactions on Systems, Man, and Cybernetics. Part A, Systems and Humans, 40(2), 337–351. doi:10.1109/TSMCA.2009.2034837

Sahinoglu, M. (2007). 可信计算：分析与定量工程评估。John Wiley & Sons。doi:10.1002/9780470127872

Sahinoglu, M., & Ramamoorthy, C. V. (2005). 用于在简单和复杂嵌入式系统中编码、解码和计算可靠性的 RBD 压缩、解压缩和混合技术工具。IEEE Transactions on Instrumentation and Measurement, 54(5), 1789–1799. doi:10.1109/TIM.2005.855103

Sahinoglu, M., & Rice, B. (2010). 网络可靠性评估。Computational Statistics, 2(2), 189–211. doi:10.1002/wics.81

Soszynska, J. (2010). 可变运行条件下港口石油管道运输系统的可靠性与风险评估。International Journal of Pressure Vessels and Piping, 87(2–3), 81–87. doi:10.1016/j.ijpvp.2010.01.002

Zhang, Z., & Shao, B. (2008). 不同管段在不同时期的可靠性评估。载于《服务运营与物流及信息学》(第 1779–1782 页)。IEEE。

## 关键术语和定义

**可靠性：** 可靠性定义为系统或组件在某个时间间隔内执行其所需任务的概率。

**可靠性框图：** 可靠性框图 (RBDs) 是由块和连接线组成的图形结构。块通常代表系统组件，这些组件的连接由连接线描述。如果存在从输入到输出的至少一条正常功能组件路径，则系统被认为是功能正常的，否则它失效。

**生存性：** 生存性是给定系统在给定时间后存活的概率。

