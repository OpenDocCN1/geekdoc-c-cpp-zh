

## A.2.2 推荐包

在撰写本文时，共有 15 个推荐包，如 R FAQ 第 5.1.2 节所示。这些包包含在任何标准的 R 安装中，它们扩展了基础包的功能，包含了更具专业性（但仍然通用）的统计方法和计算工具。在书中，你将使用此列表中的 MASS 和 boot。

```
Kernsm  MASS  Matrix  class  cluster
codetools  foreign  lattice  mgcv  nme
rpart    spatial  survival
```

这些推荐包不会自动加载。如果你想访问这些包中的函数或数据集，请通过调用 `library` 手动加载它们。例如，要访问 MASS 的部分数据集，请在提示符处执行以下命令：

```R
library("MASS")
```

某些包在加载时会提供简短的欢迎信息，R 总是会通知你发生了任何掩蔽（masking）（见第 12.3.1 节）。当你关闭 R 会话时，该包也会关闭；如果你打开另一个 R 实例并想再次使用它，你需要重新加载它。如果你决定在某个会话中不再需要某个包并想卸载它（例如避免任何潜在的掩蔽问题），可以使用以下方法：

```R
detach("package:MASS", unload=TRUE)
```

你可以在书中第 9.1 节和第 12.3.1 节找到有关包加载和卸载的主题和技术细节。

## A.2.3 贡献包

在这些内置和推荐包之外，通过 CRAN 提供了大量的用户贡献包（user-contrib packages），服务于统计、数学、计算和图形领域的各种目的和应用。如果你导航到本地的 CRAN 镜像站点，页面左侧的 Packages 链接（见图 A-2）将带你进入一个包含更多链接的页面，这些链接提供了 CRAN 上可用包的最新列表。你还会发现非常有用的 CRAN Task Views（任务视图）页面，它是一个针对特定主题的文章集合，提供了相关包的概述，如图 A-3 所示。这是熟悉 R 中可以进行的各种专业分析类型的极佳方法。

### CRAN Task View

- CRAN
- Bayesian Inferencer（贝叶斯推断）
- CheckNotes
- ClassMethods（类方法）
- ClusterAnalysis（聚类分析）
- Clustering（聚类）
- Distributions（分布）
- Environment（环境）
- Experiments（实验）
- Factor（因子）
- Forecasting（预测）
- Geometry（几何）
- HighPerformance（高性能）
- MachineLearning（机器学习）
- Methods（方法）
- Networks（网络）
- NLP（自然语言处理）
- Optimization（优化）
- Statistics（统计）
- Bayesian（贝叶斯）
- Chemometrics and Composite Design（化学计量与复合设计）
- Clustering, Design, Monitoring, and Analysis（聚类、设计、监控与分析）
- Cluster Analysis & Fuzzy Mixture Models（聚类分析与模糊混合模型）
- Differential Equations（微分方程）
- Probability Distribution（概率分布）
- Environmental and Spatial Data（环境与空间数据）
- Design of Experiments (DoE) & Analysis of Experimental Data（实验设计与实验数据分析）
- Generative Models（生成模型）
- Graphics（图形）
- Dynamics & Graphs & Visualization（动力学、图与可视化）
- HighPerformance Computing & Parallel Computing with R（R 的高性能计算与并行计算）
- Machine Learning and Deep Learning（机器学习与深度学习）
- Model Analysis（模型分析）
- Networks（网络）
- Natural Language Processing（自然语言处理）
- Optimization（优化）
- Operations Research（运筹学）
- Pharmacokinetics（药代动力学）
- Psychometric Methods（心理测量方法）
- About R（关于 R）
- The R Project（R 项目）
- R Sources（R 源码）
- Shiny
- Packages（包）
- Documentation（文档）
- Help（帮助）
- Contributed（贡献的）

要访问这些视图，需要通过 `install.packages("name")` 或 `update.packages()`（更新已安装且为新的许多包中的第一个）安装相应的包，例如 `update.packages("economics")`。

图 A-3：CRAN Task Views 网页。每篇文章都讨论了重要的 CRAN

在书中，你将使用一些贡献包。某些用于访问数据集或对象，另一些用于其独特的功能或说明统计方法。它们列在此处：

| car | faraway | GGally | ggplot2 | ggvis |
| gridExtra | ks | misc3d | mvnorm | rgl |
| scatterplot | shape | spatstat | tseries | | | |

当你访问任何贡献包时，你需要连接互联网来下载和安装它。包的大小通常小于几兆字节。一旦安装了包，你就可以通过调用 `library` 加载它以访问上述列出的相关功能，在书的相关部分，需要时会提示你这样做。

你现在已经知道了几种为 R 执行下载和安装包的方法，以 `ks` 包（Duong, 2007）为例。

贡献的 R 包在正确性、速度、效率和用户友好方面通常具有良好的质量。虽然在提交的包发布到 CRAN 之前必须通过一些基础的兼容性检查，但通过这些检查并不意味着该包的整体质量和可用性。你只有通过使用该包、研究其文档并寻找任何相关的出版物才能判断这一点。

安装 R 和贡献包 741

## 在 CRAN 上查找包

CRAN 上的每个 R 包都有其自己的标准网页，提供了可下载文件的直接链接和关于该包的重要信息。在 CRAN 的某一个列表中找到包名并点击它，或者在 Google 上快速搜索，在我们的案例中 *ks r cran*。图 A-4 显示了 ks 网页的顶部。

| ks: Kernel Smoothing（核平滑） |
| :--- |
| 用于单变量和多变量数据的平滑。 |
| 版本: 1.9.5 |
| 依赖: R (>= 1.4.0), KernSmooth (>= 2.22), misc3d (>= 0.4), mvtnorm, rgl (>= 0.66)) |
| 导入: grDevices, graphics, misscool, stats, utils |
| 建议: MASS |
| 发布:2015-10-07 |
| 作者: Tarm Duong, duam.duong@gmail.com |
| 许可证: GPL-2 | GPL-3 |
| URL: http://www.mvstat.net/tduang |
| 需要编译: yes |
| 材料: Multivariate |
| CRAN 检查: 无结果 |

图 A-4：CRAN 网页上 ks 的描述性信息

除了版本号、维护者姓名和联系方式等基本信息外，你还会看到 `Depends` 字段。这对于安装非常重要；如果你感兴趣的 R 包依赖于其他贡献包（并非所有），你还需要安装那些包才能让你的包成功安装。

查看图 A-4，你可以看到你的 R 版本需要晚于 1.4，`ks` 需要 `KernSmooth`（已安装——它是 A.2.2 节中提到的推荐包之一），它还需要 `misc3d`、`mvtnorm` 和 `rgl`。幸运的是，如果你直接从 R 中安装 R 包，依赖项也会自动安装。

## 在提示符处安装包

下载和安装贡献的 R 包的最快方法是直接从 R 提示符使用 `install.packages` 命令。从全新的安装的 R 开始，我在我的 iMac 上看到以下内容：

```R
install.packages("ks")
--- 请为本次会话选择一个 CRAN 镜像 ---
正在安装依赖项 'misc3d', 'mvtnorm', 'rgl'

--snip--
```

你可能首先会被要求选择一个 CRAN 镜像。列表弹出并默认仅仅包含安全的 HTTPS 服务器；选择 HTTP 将切换到不安全的服务器。我选择了 HTTP，找到了新西兰镜像并点击 OK，如图 A-5 所示。一旦你执行了该操作，选定的镜像将保持为你选择的设置，直到你重置它；见第 A.4.1 节。

![](img/b2cfc85cbb129f60fe59a2bae074fe4_776_0.png)

A-5：下载贡献包时选择 CRAN 镜像站点的弹出窗口。左：可选的 HTTP 服务器。右：本地 HTTP 镜像。

点击 OK 后，R 会列出将下载的依赖项，并为每个包显示下载通知（在截取的输出中）。有额外的说明：

- 你只需要需要时才安装包，这将节省硬盘空间，以便按 usual 调用 `library` 加载。
- 你可能会被提示为安装的包创建一个本地文件夹。这样做是为了确保 R 在通过 `library` 请求包时从哪里获取。同意此意味着你拥有了一个用户特定的包库，这通常是一个好主意。
- `install.packages` 在这里有很多可选参数；在提示符处调用 `install.packages` 提供的帮助文件。例如，如果你想在控制台中指定一个 CRAN 镜像，请将相关的 URL 作为字符串传递给 `repos` 参数，或者如果你想防止依赖项安装，使用 `dependencies` 参数。

