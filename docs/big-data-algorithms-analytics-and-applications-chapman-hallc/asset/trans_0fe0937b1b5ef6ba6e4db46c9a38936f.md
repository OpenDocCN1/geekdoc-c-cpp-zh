
调整聚类数

```
/usr/lib64/python2.6/site-packages/scipy/maxentropy/__init__.py:19: DeprecationWarning:
The scipy.maxentropy module is deprecated in scipy 0.10, and scheduled to be
removed in 0.11.

If you are using some of the functionality in this module and are of the
opinion that it should be kept or moved somewhere - or you are even interested
to maintain/improve this whole module - please ask on the scipy-dev mailing
list.

The logsumexp function has already been moved to scipy.misc.
DeprecationWarning)
Elapsed time is 17.60555 seconds.
/usr/lib64/python2.6/site-packages/scipy/maxentropy/__init__.py:19: DeprecationWarning:
The scipy.maxentropy module is deprecated in scipy 0.10, and scheduled to be
removed in 0.11.

If you are using some of the functionality in this module and are of the
opinion that it should be kept or moved somewhere - or you are even interested
to maintain/improve this whole module - please ask on the scipy-dev mailing
list.

The logsumexp function has already been moved to scipy.misc.
DeprecationWarning)
Elapsed time is 17.672895 seconds.
```

图 9.6 在识别 k 时获得的输出片段。

大规模网络。然而，“Self”模型选择技术独立于这些函数工作，并使用熵和平衡的概念来计算由验证集特征投影生成的亲和矩阵 S 在通过真实信息重新排序后块对角线的数量。图 9.6 表示我们在尝试识别大规模网络中社区的最优数量 k 时获得的片段。

在图 9.6 中，我们观察到“DeprecationWarning”，我们忽略它，因为它与我们未使用的“scipy”库中的某些功能有关。我们还观察到我们在两个地方获得了“Elapsed time…”。一次是在构建训练模型之后，第二次是在我们使用验证集执行模型选择之后出现。图 9.7 表示获得测试集社区归属所需的时间。由于整个网络中只有 5000 个节点，并且由于内存限制我们将测试集分为 5000 个节点的块，因此我们在图 9.7 中观察到“I am in block 1”。图 9.8 展示了合成网络的基于社区的结构。当我们使用 BAF 选择标准或“Self”选择技术时，我们得到的结果相同。

```
I am in block 1
/usr/lib64/python2.6/site-packages/scipy/maxentropy/__init__.py:19: DeprecationWarning:
The scipy.maxentropy module is deprecated in scipy 0.10, and scheduled to be
removed in 0.11.

If you are using some of the functionality in this module and are of the
opinion that it should be kept or moved somewhere - or you are even interested
to maintain/improve this whole module - please ask on the scipy-dev mailing
list.

The logsumexp function has already been moved to scipy.misc.
DeprecationWarning)
Elapsed time is 110.644138 seconds.
```

图 9.7 在估计测试聚类成员资格时获得的输出片段。

![](img/1643181e79c76dc765d55a7355afb4a4_205_0.png)

图 9.8 KSC 方法学为合成网络检测到的社区。

### 9.3.3 KSC 在真实网络上的演示

我们提供一个演示脚本来展示 KSC 方法学在真实的大规模 YouTube 网络上的应用，该网络有 1,134,890 个节点和 2,987,624 条边。该网络高度稀疏。这是一个社交网络，用户之间可以建立友谊并创建其他用户可以加入的群组。我们在下面提供演示脚本。

图 9.9 显示了 BAF 模型选择标准在 YouTube 社交网络上的有效性。从图 9.9 中，我们观察到在

![](img/1643181e79c76dc765d55a7355afb4a4_205_1.png)

图 9.9 通过 BAF 标准为 YouTube 网络选择最优 k。

BAF 与 k 曲线上存在多个局部峰值。然而，我们选择 BAF 值最大的峰值。这发生在 k = 4 时，BAF 值为 0.8995。由于我们可以为终端用户提供整个网络的聚类成员资格，终端用户可以使用各种内部质量标准来估计 resulting 社区的质量。

如果我们在算法 4 的演示脚本中将 mod_sel = 'Self'，那么我们将使用无参数模型选择技术。由于事先不知道真实社区，我们尝试使用算法 2 中提到的贪婪选择技术来估计块对角结构以确定 SizeCi 向量。图 9.10 显示 F-measure 在 t = 0.1 时最大，其值为 0.224。对应于该阈值值的识别出的社区数量 k 为 36（图 9.11）。

![](img/1643181e79c76dc765d55a7355afb4a4_206_0.png)

图 9.10 通过自调优标准为 YouTube 网络选择最优 k。

![](img/1643181e79c76dc765d55a7355afb4a4_206_1.png)

图 9.11 分别由“BAF”和“Self”模型选择技术检测到的 YouTube 网络社区结构，使用参考文献 26 中提供的软件可视化。（引自 Lancichinetti, A. et al., Plos One, 6(e18961), 2011.）

### 算法 4：使用 BAF 标准对 YouTube 网络的演示脚本

数据：

```
netname = 'youtube_mod';    //Name of the file and extension should be '.txt'
baseinfo = 0;    //Ground truth does not exists
cominfo = [];    //No ground truth file so empty set as input
weighted = 0;    //Whether a network is weighted or unweighted
frac_network = 10;    //Percentage of network to be used as training and
                      //validation set
maxk = 100;    //maxk is maximum value of k to be used in eigen-decomposition,
               //use maxk = 10 for k < 10 else use maxk = 100
mod_sel = 'BAF';    //Method for model selection (options are 'BAF' or 'Self')
output = KSCnet(netname,baseinfo,cominfo,weighted,frac_network,maxk,mod_sel);
```

结果：

```
output = 1;    //When community detection operation completes
netname_numclu_mod_sel.csv;    //Number of clusters detected
netname_outputlabel.csv;    //Cluster labels assigned to the nodes
```

## 9.4 结论

在本章中，我们对用于大数据网络社区检测的方法论进行了实践性阐述。该技术基于谱聚类的概念构建，并被称为 KSC。核心概念是在一个小的代表性子图上构建模型，该子图捕捉了大规模网络固有的社区结构。子图是通过 FURS [2] 选择技术获得的。然后，在该子图上构建了 KSC 模型。模型参数通过以下两种技术之一获得：（1）BAF 标准或（2）自调优技术。KSC 模型具有强大的样本外扩展特性。该特性用于大数据网络中以前未见节点的社区归属。我们还解释并演示了 KSC-net 软件的使用，该软件使用 KSC 方法学作为底层核心概念。

## 致谢

EU：导致这些结果的研究已获得欧洲研究理事会在欧盟第七框架计划（FP7/2007-2013）/ ERC AdG A-DATADRIVE-B（290923）下的资助。本章仅反映作者的观点；联盟不对所含信息的任何用途承担责任。Research Council KUL：GOA/10/09 MaNet，CoE PFV/10/002（OPTEC），BIL12/11T；博士/博士后资助。Flemish government—FWO：projects G.0377.12（structured systems），G.088114N（tensor-based data similarity）；PhD/postdoc grants。IWT：project SBO POM（100031）；PhD/postdoc grants。iMinds Medical Information Technologies：SBO 2014。Belgian Federal Science Policy Office：IUAP P7/19（DYSCO，dynamical systems，control and optimization，2012–2017）。

- 24. J. Baylis; Error Correcting Codes: A Mathematical Introduction. Boca Raton, FL: CRC Press, 1988.
- 25. R. Rabbany, M. Takaffoli, J. Fagnan, O.R. Zaiane and R.J.G.B. Campello; Relative validity criteria for community mining algorithms. In International Conference on Advances in Social Networks Analysis and Mining (ASONAM), pp. 258-265, 2012.
- 26. A. Lancichinetti, F. Radicchi, J.J. Ramasco and S. Fortunato; Finding statistically significant communities in networks. PLoS One, 6:e18961, 2011.

