

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_177_0.png)

图4.8 拒绝阈值（在每个实验点附近标出）对训练集的影响。仅包含那些由SFBF网络获得前L个最高概率的类别的模式。

在表4.5中，针对每个L值（L ∈ [2,10]），给出了验证集上的成功率（%S-Valid）。每个实验的拒绝阈值设置为0.95。这些实验数据表明，成功率对L没有显著依赖性。因此，选择L=2能够带来良好的泛化性能和更高的识别速度（根据我们的初步结果，比L=10时快约5倍）。

为了进一步加速NR对最近点的搜索，可以开发并行硬件，并/或尝试使用优化的数据结构，如bumptrees [22]或随机化算法 [7]。

## 4.11 结论

通用函数逼近结果是许多连接主义系统（如MLP、RBF和FLS）的关键属性。此外，选择合适的代价函数进行参数识别，使得能够高效地处理

| L | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|
| %S-Valid | 93.46 | 93.53 | 93.68 | 93.58 | 93.64 | 93.66 | 93.61 | 93.60 | 93.45 |

表4.5 混合模式识别方案：使用在线编辑的压缩数据库时的性能（见正文）。

模式识别问题。

在此框架下，可以轻松获得高效的监督非参数模糊分类器，如本章所示。基于FLS的分类器（如本文研究的FBF网络）的特殊性在于：如果除了数值训练集之外，还提供了类别的语言描述，则它可以利用这两种信息来完成模式识别任务。

此外，我们已经表明，根据可用的计算资源和目标分类性能，可以定义一系列模型，这些模型均源自FBF网络的原始形式，覆盖了涉及训练时间、性能和响应时间的大范围控制参数。

## 4.12 致谢

本工作得到了CNR、INFM和MURST的资助。我们感谢Nicola Giusti实现了竞争性和混合算法。

## 4.13 参考文献

[1] D. Alfonso, F. Masulli, and A. Sperduti. Competitive learning in a classifier based on an adaptive fuzzy system. In P.G. Anderson and K. Warwick, editors, Proceedings of the International ICSC Symposium on Industrial Intelligent Automation (IIA’96) and Soft Computing (SOCO’96), Reading, England, pages C2–C8, Millet, Alberta, Canada, 1996. ICSC.

[2] E. Barnard, F. Kanaya, and S. Miyake. Comments on ‘Bayes statistical behavior and valid generalization of pattern classifying neural networks’ (with reply). IEEE Transactions on Neural Networks, 3:1026–7, 1992.

[3] F. Casalino. Fuzzy systems for handwriting recognition. Laurea Thesis in Computer Science, University of Genoa, Genova - Italy, 1993. In Italian.

[4] F. Casalino, F. Masulli, and A. Sperduti. Rule specialization in networks of fuzzy basis functions. Intelligent Automation and Soft Computing, 4:73–82, 1998.

[5] F. Casalino, F. Masulli, A. Sperduti, and F. Vannucci. Semantic phase transition in a classifier based on an adaptive fuzzy system. In Proceedings of the Third IEEE International Conference on Fuzzy Systems, IEEE-FUZZ94, volume 2, pages 808–812, Orlando, FL, USA, 1994. IEEE.

[6] R. Caviglia. Soft-computing methods for time series forecasting. Laurea Thesis in Computer Science, University of Genoa, Genova - Italy, 1994. In Italian.

[7] K. L. Clarkson. A randomized algorithm for the closest-point queries. SIAM Journal on Computing, pages 830–847, 1988.

[8] R.O. Duda and P.E. Hart. Pattern Classification and Scene Analysis. Wiley, New York, 1973.

[9] M.D. Garris and R.A. Wilkinson. NIST Special Database3 Handwritten Segmented Characters. National Institute of Standard and Technology, Gaithersburg, MD, USA, 1992.

[10] N. Giusti, F. Masulli, and A. Sperduti. Competitive and hybrid neuro-fuzzy models for supervised classification. In Proceedings of 1997 IEEE International Conference on Neural Networks, INNC’97, pages 516–519, Houston, USA, 1997. IEEE.

[11] J. Hampshire and B. Pearlmutter. Equivalence proofs for multi-layer perceptron classifiers and the Bayesian discriminant function. In D.S. Touretzky, G. Hinton, and T. Sejnowski, editors, Connectionist Models: Proceedings of the 1990 Summer school, pages 13–19, Denver, 1990. Morgan Kaufmann, San Mateo.

[12] J.S.R. Jang. ANFIS: Adaptive-network-based fuzzy inference system. IEEE Trans. on Systems, Man, and Cybernetics, 23:655–684, 1993.

[13] C.C. Jou. Comparing learning performance of neural networks and fuzzy systems. In IEEE International Conference on Fuzzy Systems, pages 1028–1033, San Francisco, 1993. IEEE, New York, NY.

[14] F. Kanaya and S. Miyake. Bayes statistical behavior and valid generalization of pattern classifying neural networks. IEEE Transactions on Neural Networks, 2:471–475, 1991.

[15] H.M. Kim and J.M. Mendel. Fuzzy basis functions: Comparisons with other basis functions. IEEE Trans. on Fuzzy Systems, 3:158–168, 1995.

[16] C.C. Lee. Fuzzy logic in control systems: fuzzy logic controller. I. IEEE Transactions on Systems, Man, and Cybernetics, 20:404–418, 1990.

[17] Y. Lee. Handwritten digit recognition using k nearest-neighbor, radial-basis function, and backpropagation neural networks. Neural Computation, 3:440–449, 1991.

[18] F. Masulli. Bayesian classification by feedforward connectionist systems. In F. Masulli, P. G. Morasso, and A. Schenone, editors, Neural Networks in Biomedicine - Proceedings of the Advanced School of the Italian Biomedical Physics Association - Como (Italy) 1993, pages 145–162, Singapore, 1994. World Scientific. (invited).

[19] J.M. Mendel. Fuzzy logic systems for engineering: A tutorial. Proceedings of the IEEE, 83:345–377, 1995.

[20] S. Miyake and F. Kanaya. A neural network approach to a Bayesian statistical decision problem. IEEE Transactions on Neural Networks, 2:538–540, 1991.

[21] G.C. Mouzouris and J.M. Mendel. Non-singleton fuzzy logic systems. In Proc. 1994 IEEE Conf. on Fuzzy Systems, Orlando 1994, 1989. IEEE, New York.

[22] S. M. Omohundro. Bumptrees for efficient function, constraint, and classification learning. In R.P. Lippmann, J.E. Moody, and D. S. Touretzky, editors, Advances in Neural Information Processing Systems 3, pages 693–900. San Mateo, CA: Morgan Kaufmann, 1991.

[23] Theo Pavlidis. Algorithms for Graphics and Image Processing. Springer-Verlag, 1982.

[24] J. Platt. A resource-allocating network for function interpolation. Neural Computation, 3:213–225, 1991.

[25] D.W. Ruck, S.K. Rogers, M. Kabrisky, M.E. Oxley, and B.W. Suther. The multilayer perceptron as an approximation to a Bayes optimal discriminant function. IEEE Transactions on Neural Networks, 1:296–298, 1990.

[26] D.E. Rumelhart, G.E. Hinton, and R.J. Williams. Learning internal representations by error propagation. In D.E. Rumelhart and J.L. McClelland, editors, Parallel Distributed Processing, volume 1, chapter 8, pages 318–362. MIT Press, Cambridge, 1986.

[27] T.P. Vogl, J.K. Mangis, A.K. Rigler, W.T. Zink, and D.L. Alkon. Accelerating the convergence of the back-propagation method. Biological

## 5

## 多级模糊控制

Zong-Mu Yeh
Email: zongmu@cc.ntnu.edu.tw, FAX: (02)2392944

Hung-Pin Chen
Department of Industrial Education,
National Taiwan Normal University,
Taipei, Taiwan, 10610, R.O.C.

摘要................................................... 172

5.1 引言................................................... 172
多级模糊系统 • 相关研究与问题 • 多级方法

5.2 多级推理模糊系统 ...... 179
多级模糊推理引擎 • 多级模糊推理过程

5.3 模糊规则生成方法 ... 183
多级模糊推理系统的模糊规则生成 • 快速多级模糊逻辑推理

5.4 示例................... 191

5.5 结论 ....................................... 199

5.6 参考文献 ....................................... 202

