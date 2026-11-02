

选作模型与复杂度之间的折衷；也就是说，一个复杂的模型可以定义更精细的模式，但会牺牲计算复杂度。采用一种稳健且高效的主成分分析（PCA）来提取视频中的稀疏前景。为了避免每次迭代中昂贵的奇异向量分解运算，利用短时间内背景几乎不变的特点，将秩1约束用于PCA。然后采用狄利克雷过程混合模型对从PCA提取的稀疏分量进行建模。与文本文档的生成模型类似，在事件袋模型中，每个特征向量被视为运动模式的一个样本。多项分布和高斯混合的组合定义了运动的位置和数量。开发了一种衰减的马尔可夫链蒙特卡洛（MCMC）增量推理方法，用于在线设定中的固定成本更新。只要过去的任意点以非零概率被选中，后验就可以保证收敛到真实值。传统的衰减函数如指数衰减只依赖于时间，而对于场景理解问题，概率分布还依赖于聚类空间中的数据，即过去观测与当前观测之间的距离。为了提高对大规模设置的可扩展性，通过测量聚类之间的距离来表示每个聚类中样本之间的距离。该框架在一个长达140小时的视频上进行了测试，该视频的规模相当大，并证明了它能够提供与现有场景理解算法相当的模式发现性能。这项工作增强了我们有效且高效地从无界视频流中发现未知模式的能力，为多媒体数据的大规模主题建模提供了一个非常有前景的框架。

## 19.6 结论与未来方向

互联网和社交媒体平台如Facebook、Twitter和YouTube已经如此普及，以至于每分钟都会产生数以百万计甚至数十亿计的新媒体数据，如照片和视频。用户被如此多的信息淹没，消化海量信息变得相当困难且耗时。来自信息检索领域的概率主题模型通过发现隐藏的主题结构来有效组织大规模多媒体数据，这是非常可取的。另一方面，传统的主题模型如PLSI和LDA由于计算复杂度过高，难以扩展到TB或PB级别的海量数据集，这也是许多传统机器学习和数据挖掘算法所面临的难题。随着云计算的出现，主题模型预计将越来越适用于多媒体数据。谷歌的MapReduce和雅虎的Hadoop是大规模数据处理的显著例子。这些技术已证明对大数据分析任务非常有效。

虽然主题模型在文本文档上的成功已经得到了很好的验证，但最近很多工作致力于将其应用于大规模多媒体分析，其中多媒体数据可以是文本、图像、音频和视频等形式。从19.3节到19.5节可以明显看出，主题建模是一种非常有用的、强大的技术，可以在非常大的规模上解决多媒体云计算问题（Barnard et al. 2003; Blei and Jordan 2003; Duygulu et al. 2002; Li and Perona 2005; Sivic et al. 2006; Wang et al. 2009）。例如，普通高斯混合模型和Corr-LDA之间的比较研究表明，在图像自动标注和基于文本的图像检索任务中，Corr-LDA显著更好。已经提出了各种分布式和并行计算框架，如PLDA和并行支持向量机（PSVM）（Chang et al. 2007）来解决多媒体计算的可扩展性问题。DISC图是大规模数据分析的另一个流行设计（Bryant 2007）。流行的大数据处理框架MapReduce在多媒体云计算应用中也取得了成功，例如网络规模的计算机视觉（White et al. 2010）。大规模数据高维性的另一个主要问题是过拟合。提出了一种新的语义概念模型（Yan et al. 2009）来解决过拟合问题，结果证明了该方法的效果。

在未来的工作中，随着数据规模的不断增长，可扩展性将成为一个更突出的问题。基于Web的多媒体数据挖掘（White et al. 2010）展示了在MapReduce框架中实现计算机视觉算法（如训练、聚类和背景减除）的能力。基于云的计算仍将是大规模多媒体分析的一个非常活跃的研究领域。此外，对于基于云的大规模多媒体计算，非常希望在用户界面上可视化高维数据并易于解释。当前的方法主要显示带有词频的主题（Blei 2012），这是有限的，因为隐藏的主题结构也连接着不同的文档。多媒体数据和底层主题之间的关系更加复杂。可视化这些复杂关系将极大地帮助人们消费多媒体内容。此外，主题模型通常以离线方式训练，即整个批次的数据被一次用于构建模型。这个过程不适合在线设置，因为数据流随时间不断到达。通过在线学习（Barbara and Domeniconi 2008），当新数据到达时，我们不需要重建整个主题模型，只需基于新数据增量更新参数。因此，在线学习可以为多媒体分析提供更高效的解决方案，因为某些多媒体内容本质上是流式的。此外，特征选择和特征工程对多媒体分析和检索至关重要。随着深度学习的最新进展（Hinton et al. 2006; Hinton and Salakhutdinov 2006），学习多媒体数据的紧凑表示和特征将成为一个重要的研究课题。

## 参考文献

- Ahmed, A., Low, Y., and Smola, A. Scalable Distributed Inference of Dynamic User Interests for Behavioral Targeting. ACM SIGKDD Conference on Knowledge Discovery from Data, 2011.
- Barbara, D., and Domeniconi, C. On-line LDA: Adaptive Topic Models for Mining Text Streams with Applications to Topic Detection and Tracking. IEEE International Conference on Data Mining, 2008.
- Barnard, K., Duygulu, P., Forsyth, D., De Freitas, N., Blei, D., and Jordan, M. Matching Words and Pictures. Journal of Machine Learning Research, 3, 1107–1135, 2003.
- Blei, D. Probabilistic Topic Models. Communications of the ACM, 55(4), 77–84, 2012.
- Blei, D., and Jordan, M. Modeling Annotated Data. ACM SIGIR Conference on Research and Development in Information Retrieval, 127–134, 2003.
- Newman, D., Asuncion, A., Smyth, P., and Welling, M. Distributed Inference for Latent Dirichlet Allocation. Neural Information Processing Systems, 1081–1088, 2007.
- Papadimitriou, C.H., Raghavan, P., Tamaki, H., and Vempala, S. Latent Semantic Indexing: A Probabilistic Analysis. ACM SIGACT-SIGMOD-SIGART Symposium on Principles of Database Systems, 159–168, 1998.
- Powell, R., and Li, J. Piccolo: Building Fast, Distributed Programs with Partitioned Tables. USENIX Conference on Operating Systems Design and Implementation, 2010.
- Rana, S., and Venkatesh, S. Large-Scale Statistical Modeling of Motion Patterns: A Bayesian Nonparametric Approach. Indian Conference on Computer Vision, Graphics and Image Processing, 2012.
- Rosen-Zvi, M., Griffiths, T., Steyvers, M., and Smith, P. The Author-Topic Model for Authors and Documents. Uncertainty in Artificial Intelligence, 2004.
- Sivic, J., Russell, B., Zisserman, A., Freeman, W., and Efros, A. Unsupervised Discovery of Visual Object Class Hierarchies. IEEE Conference on Computer Vision and Pattern Recognition, 2008.
- Smola, A., and Narayanamurthy, S. An Architecture for Parallel Topic Model. Very Large Database (VLDB), 3(1), 703–710, 2010.
- Teh, Y., Jordan, M., Beal, M., and Blei, D. Hierarchical Dirichlet Processes. Journal of American Statistical Association, 101(476), 1566–1581, 2006.
- Wallach, H. Topic Modeling: Beyond Bag of Words. International Conference on Machine Learning, 2006.
- Wang, Q., Xu, J., Li, H., and Craswell, N. Regularized Latent Semantic Indexing. ACM SIGIR Conference on Research and Development in Information Retrieval, 2011.
- Wang, Y., Bai, H., Stanton, M., Chen, M., and Chang, E.Y. PLDA: Parallel Latent Dirichlet Allocation for Large-Scale Applications. Conference on Algorithmic Aspects in Information and Management, 301–314, 2009.
- White, B., Yeh, T., Lin, J., and Davis, L. Web-Scale Computer Vision using MapReduce for Multimedia Data Mining. ACM KDD Conference Multimedia Data Mining Workshop, 2010.
- Xiang, E., Yan, R., and Hauptmann, A. Mining Associated Text and Images with Dual-Wing Harmoniums. Uncertainty in Artificial Intelligence, 2005.
- Yan, R., Fleury, M., and Smith, J., Large-Scale Multimedia Semantic Concept Modeling Using Robust Subspace Bagging and MapReduce. ACM Workshop on Large-Scale Multimedia Retrieval and Mining, 2009.
- Zhai, K., Graber, J., Asadi, N., and Alkoujua, M. Mr.LDA: A Flexible Large Scale Topic Modeling Package Using Variational Inference in MapReduce. ACM Conference World Wide Web, 2012.
- Zhu, W., Luo, C., Wang, J., and Li, S. Multimedia Cloud Computing. IEEE Signal Processing Magazine, 28(3), 59–69, 2011.

