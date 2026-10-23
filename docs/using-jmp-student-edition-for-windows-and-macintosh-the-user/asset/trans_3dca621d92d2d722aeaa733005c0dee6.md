

## 相关性和多元技术

Multivariate 平台专门用于探索多个变量之间的关系。该平台首先显示一个标准的相关矩阵。Multivariate 平台弹出菜单提供了额外的相关选项以及查看多个变量的其他技术，例如

- 带有正态密度椭圆的散点图矩阵
- 逆相关、偏相关和成对相关
- 协方差矩阵
- 非参数关联度量
- 简单统计量（例如均值和标准差）

所有图形和当前数据表都是链接的。你可以在散点图矩阵中的任何散点图上高亮显示点，或在离群距离图上高亮显示点。这些点会在所有其他图形上高亮显示，并在数据表中被选中。

### 简介

有关 Multivariate 平台的简短介绍，请执行以下操作：

- 从示例数据文件夹中打开 Solubility.jmp。
- 选择 Analyze > Multivariate 以调出启动对话框。

![](img/a858f3b35ed4923af65c22e8829ee5a8_161_0.png)

报告出现时，你会看到相关性和散点图矩阵。

![](img/a858f3b35ed4923af65c22e8829ee5a8_162_0.png)

从这里，你可以计算多种不同的相关性，包括非参数相关性（见下文各种类别实例）。

请注意，前两个变量（1-Octanol 和 Ether）彼此相关。此外，最后四个变量也类似相关。这表明这六个变量中的变异可以用更少的维度来解释。主成分分析将证实这一点。

从平台的下拉列表中选择 Principal Components > on Correlations。

![](img/a858f3b35ed4923af65c22e8829ee5a8_162_1.png)

此处显示的主成分报告表明存在两个强变异方向，对应于特征值 4.785 和 0.945。我们可以用仅两个维度来表达这六个维度的 95% 变异。

### 启动平台并选择选项

当你选择 **Analyze > Multivariate** 时，首先会出现标准相关矩阵和散点图矩阵。此处显示的平台弹出菜单列出了额外的相关选项以及查看多个变量的其他技术。以下各节描述了 Multivariate 平台提供的表和图。

![](img/a858f3b35ed4923af65c22e8829ee5a8_163_0.png)

在以下大多数分析选项中，观测值中的缺失值会导致整个观测值被删除。例外情况是 **Pairwise Correlations**，它会排除在所考虑的任一变量上缺失的行，以及 **Simple Statistics > Univariate**，它按列计算其统计量，不考虑其他列中的缺失值。

以下许多示例使用 Solubility.jmp 示例数据表。

### Correlations Multivariate

**Correlations Multivariate** 选项给出 Correlations 表，即相关系数矩阵，汇总了每对响应（*Y*）变量之间线性关系的强度。该相关矩阵仅使用对分析中所有变量都有非缺失值的观测值。

| Variable | Ether | 1-Octanol | Carbon Tetrachloride | Benzene | Hexane | Chloroform |
|---|---:|---:|---:|---:|---:|---:|
| Ether | 1.0000 | 0.9343 | 0.5376 | 0.6489 | 0.5494 | 0.5146 |
| 1-Octanol | 0.9343 | 1.0000 | 0.6151 | 0.7197 | 0.6046 | 0.5976 |
| Carbon Tetrachloride | 0.5376 | 0.6151 | 1.0000 | 0.9573 | 0.9498 | 0.9210 |
| Benzene | 0.6489 | 0.7197 | 0.9573 | 1.0000 | 0.9091 | 0.9411 |
| Hexane | 0.5494 | 0.6046 | 0.9498 | 0.9091 | 1.0000 | 0.8719 |
| Chloroform | 0.5146 | 0.5976 | 0.9210 | 0.9411 | 0.8719 | 1.0000 |

### 逆相关和偏相关

逆相关矩阵（**Inverse Corr** 表），显示在下一幅图的顶部，提供了有用的多元信息。矩阵的对角线元素是变量与其它变量呈线性函数关系程度的函数。在逆相关中，对角线为 1/(1 − *R*²)，即该变量由所有其它变量拟合时的值。如果多元相关为零，逆对角线为 1。

### 散点图矩阵

**Figure 9.1 Example of a Scatterplot Matrix**

![](img/a858f3b35ed4923af65c22e8829ee5a8_165_0.png)

> 两个相关簇：前两个变量和接下来的四个变量。

**Scatterplot Matrix** 标题栏按钮旁边的弹出菜单可让你使用颜色和密度椭圆，并通过设置 α 水平来自定义矩阵。

![](img/a858f3b35ed4923af65c22e8829ee5a8_165_1.png)

- **Density Ellipses** 切换散点图上密度椭圆的显示，由你选择的 α 水平构建。默认情况下为 95% 椭圆。
- **Show Correlations** 在每个散点图的左上角显示相关系数。
- **Show Histograms** 在散点图矩阵的对角线上绘制直方图。这些直方图可以指定为 **Horizontal** 或 **Vertical**。此外，你还可以使用 **Show Counts** 命令切换每个条形标签的计数。

![](img/a858f3b35ed4923af65c22e8829ee5a8_166_0.png)

Ellipse α 可让你从标准 α 水平的子菜单中选择，或选择 Other 命令并具体设置密度椭圆的 α 水平。

Ellipse Color 可让你从调色板中选择以更改椭圆的颜色。

你可以通过将对角线（标签）单元格拖到对角线上的另一个位置来重新排序散点图矩阵列。例如，如果你将标记为 1-octanol 的列的单元格沿对角线向下拖动一个单元格，则列将按图 9.2 所示重新排序。

当你查看带有重新排序列的整个散点图矩阵中的模式时，你会清楚地看到变量根据其相关性聚集成组，如图 9.1 中所示的两个组所说明的那样。

**Figure 9.2 Reorder Scatterplot Matrix**

![](img/a858f3b35ed4923af65c22e8829ee5a8_166_1.png)

Drag cell diagonally

### 协方差矩阵

Covariance Matrix 命令显示分析的协方差矩阵。

### 成对相关

Pairwise Correlations 表列出了每对 Y 变量的 Pearson 积矩相关性，使用所有可用值。如果任一对存在缺失值，则计数值会有所不同。这些是 Fit Y by X 平台上 Density Ellipse 选项产生的值。

Pairwise Correlations 报告还显示显著性概率并通过条形图比较相关性，如图 9.3 所示。

**Figure 9.3 Pairwise Correlations Report**

![](img/a858f3b35ed4923af65c22e8829ee5a8_167_0.png)

### 简单统计量

Simple Statistics 子菜单允许你为每列显示简单统计量（均值、标准差等）。这些统计量可以通过两种方式计算，在数据表中有缺失值时有所不同。

Univariate Simple Statistics 是针对每列计算的，而不考虑其他列中的值。这些值与使用 Distribution 平台产生的值相匹配。

![](img/a858f3b35ed4923af65c22e8829ee5a8_167_1.png)

**Univariate Simple Statistics**

| Column | N | Mean | Std Dev | Sum | Minimum | Maximum |
|---|---:|---:|---:|---:|---:|---:|
| Ether | 72 | 1.1010 | 1.0011 | 79.2700 | -1.3000 | 2.7000 |
| 1-Octanol | 72 | 1.2665 | 0.8219 | 91.1900 | -0.7700 | 2.7000 |
| Carbon Tetrachloride | 72 | -0.0746 | 1.2700 | -5.3700 | -3.3000 | 2.7400 |
| Benzene | 72 | 0.3949 | 1.2302 | 28.4300 | -2.2600 | 3.0300 |
| Hexane | 72 | -0.7817 | 1.3964 | -56.2800 | -4.6000 | 2.1000 |
| Chloroform | 72 | 0.8065 | 1.1617 | 58.0700 | -1.9200 | 3.6700 |

注：统计量是针对每列独立计算的，不考虑其他列中的缺失值。

Multivariate Simple Statistics 是通过删除分析中任一列有缺失值的行来计算的。这些是 Multivariate 平台用于计算相关性的统计量。

**Multivariate Simple Statistics**

| Column | N | Mean | Std Dev | Sum | Minimum | Maximum |
|---|---:|---:|---:|---:|---:|---:|
| Ether | 72 | 1.1010 | 1.0011 | 79.2700 | -1.3000 | 2.7000 |
| 1-Octanol | 72 | 1.2665 | 0.8219 | 91.1900 | -0.7700 | 2.7000 |
| Carbon Tetrachloride | 72 | -0.0746 | 1.2700 | -5.3700 | -3.3000 | 2.7400 |
| Benzene | 72 | 0.3949 | 1.2302 | 28.4300 | -2.2600 | 3.0300 |
| Hexane | 72 | -0.7817 | 1.3964 | -56.2800 | -4.6000 | 2.1000 |
| Chloroform | 72 | 0.8065 | 1.1617 | 58.0700 | -1.9200 | 3.6700 |

注：已排除缺失值的行。

### 非参数相关

当你从平台弹出菜单中选择 Nonparametric Correlations 时，会显示 Nonparametric Measures of Association 表。Nonparametric 子菜单提供这三种非参数度量：

- **Spearman's Rho** 是基于数据值秩而非数据值本身计算的相关系数。
- **Kendall's Tau** 基于一致对和不一致对观测值的数量。如果 X 值较大的观测值也具有较大的 Y 值，则该对是一致的。如果 X 值较大的观测值具有较小的 Y 值，则该对是不一致的。对平局对（X 值相等或 Y 值相等的观测对）进行了校正。
- **Hoeffding's D** 是一个统计量尺度，范围从 −0.5 到 1，正值较大表示存在依赖关系。该统计量近似为对两个分类表的卡方统计量的加权和，并检测更一般的独立性偏离。

Nonparametric Measures of Association 报告还显示所有度量的显著性概率，并通过与图 9.3 类似的条形图进行比较。

参见“Computations and Statistical Details”，第 169 页，了解计算信息。

