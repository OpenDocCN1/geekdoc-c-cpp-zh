

![](img/fbc96b887811576a0dc93355dce68ae3_234_0.png)

图 A.7 左偏数据的箱线图。

- 四分位距（IQR）是衡量变异程度的指标，对异常值的存在不敏感。\(IQR = Q3 - Q1\)。
- 在用于检测异常值的IQR方法中，数据值\(x\)如果满足以下任一条件，则为异常值：
  - \(x \le Q1 - 1.5(IQR)\)，或
  - \(x \ge Q3 + 1.5(IQR)\)。
- 数据集的五数概要包括最小值、\(Q1\)、中位数、\(Q3\)和最大值。
- 箱线图是基于五数概要的图形，用于识别对称性和偏态。假设对于某个特定数据集（非来自表A.1），我们有\(Min = 15, Q1 = 29, Median = 36, Q3 = 42\)，且\(Max = 47\)。则箱线图如图A.7所示。
  - 箱体覆盖从Q1到Q3的数据“中间一半”。
  - 左须线延伸至非异常值的最小值。
  - 右须线延伸至非异常值的最大值。
  - 当左须线比右须线长时，分布呈左偏，反之亦然。
  - 当两须线长度大致相等时，分布呈对称。图A.7中的分布显示出左偏的证据。

## 第4部分：双变量关系的汇总与可视化

- 双变量关系是两个变量之间的关系。
- 两个分类变量之间的关系使用列联表进行汇总，列联表是对两个变量的交叉汇总，并包含每个变量值组合（即每种情况）的一个单元格。表A.5是变量mortgage和risk的列联表。总计列包含risk的边缘分布，即仅针对该变量的频数分布。同样，总计行代表mortgage的边缘分布。

- 从列联表中可以学到很多。坏风险的基准比例为2/10 = 20%。然而，没有抵押的申请人的坏风险比例为1/3 = 33%，高于基准；有抵押的申请人的坏风险比例仅为1/7 = 1%，低于基准风险。因此，申请人是否有抵押对于预测风险很有用。

- 聚类柱状图是列联表的图形表示。图A.8显示了按mortgage聚类的risk的聚类柱状图。请注意，两组之间的差异一目了然。

- 要汇总定量变量与分类变量之间的关系，我们为分类变量的每个水平计算定量变量的汇总统计量。例如，Minitab提供了收入的以下汇总统计量，分别针对坏风险记录和好风险记录。所有汇总指标在好风险下均更大。差异显著吗？我们需要进行假设检验来找出答案（第4章）。

### 表A.5 Mortgage与Risk的列联表

| 风险 | 是 | 否 | 总计 |
| :--- | :--- | :--- | :--- |
| 好 | 6 | 2 | 8 |
| 坏 | 1 | 1 | 2 |
| 总计 | 7 | 3 | 10 |

![](img/fbc96b887811576a0dc93355dce68ae3_235_0.png)

图A.8 按mortgage聚类的risk聚类柱状图。

![](img/fbc96b887811576a0dc93355dce68ae3_236_0.png)

图A.9 收入与风险的个体值图。

### 描述统计量：收入

| 变量 | 风险 | 均值 | 标准差 | 最小值 | 中位数 | 最大值 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 收入 | 坏 | 28,050 | 5728 | 24,000 | 28,050 | 32,100 |
| 收入 | 好 | 33,663 | 7402 | 25,000 | 32,600 | 48,000 |

- 要可视化定量变量与分类变量之间的关系，我们可以使用**个体值图**，它本质上是一组垂直点图，分类变量中的每个类别对应一个。图A.9显示了收入与风险的个体值图，表明好风险的收入往往更大。

- **散点图**用于可视化两个定量变量x和y之间的关系。每个(x, y)点在笛卡尔平面上作图，x轴在水平方向，y轴在垂直方向。图A.10显示了八个散点图，展示了变量之间的一些可能关系类型，以及**相关系数r**的值。

- **相关系数r**量化了两个定量变量之间线性关系的强度和方向。相关系数定义为

```
r = \frac{\sum (x - \bar{x})(y - \bar{y})}{(n-1)s_x s_y}
```

完美正线性关系，r = 1

强正线性关系，r = 0.9

中等正线性关系，r = 0.5

完美负线性关系，r = -1

强负线性关系，r = -0.9

中等负线性关系，r = -0.5

无明显线性关系，r = 0

存在非线性关系但无线性关系，r = 0

图A.10 x和y之间的一些可能关系。

其中\(s_x\)和\(s_y\)分别表示x变量和y变量的标准差。\(-1 \le r \le 1\)。

- 在数据挖掘中，当记录数量很大（超过1000条）时，即使r值很小（如–0.1 ≤ r ≤ 0.1）也可能具有统计显著性。

- 如果r为正且显著，我们说x和y正相关。x的增加与y的增加相关联。

- 如果r为负且显著，我们说x和y负相关。x的增加与y的减少相关联。

## 索引

a priori algorithm, 47, 70, 199
accounting auditing purposes, 142
add_constant() command, 154
addmargins() command, 53, 123–4, 125
adult_ch6_test data set, 81
adult_ch6_training data set, 81, 82
aes() command, 58
Alcohol_flag, 115, 116, 117, 122, 124
All Negative Model, 77, 101, 109
All Positive Model, 77, 109
Anaconda software package, 9
apriori() command, 208, 210
A-priori probabilities, 125
arules package, 204, 205
as.factor() command, 148
as.numeric() command, 36
association, 5.7
association rules, 30
confidence difference criterion, 208–9
confidence of, 201
confidence quotient criterion, 209–10
confirming our metrics, 207–8
lift, 201–2
mining, 200, 202–6
support for, 200–201
valediction, 210
attributes, 215
backpropagation algorithm, 134
bank_additional data set, 71
bank_additional_full.txt data set, 29
bank_marketing_test data set, 29, 31
bank_marketing_training data set, 22–3, 29, 47, 49, 50
bank_train data set, 24, 25
bar chart, 218

bar() commands, 55, 57
bar graphs
best practices, 49
with response overlay, 47–51
from Python of age_binned, 61, 62, 63
from R of age_binned, 59, 60
from R of previous outcome, 47, 48
using Python, 49–50
using R, 50–51
in R of education variable, 36, 37
baseline model performance, 4, 78
for Binary Classification, 77
k-ary classification, 77
for regression, 162–3
for estimation models, 163
final regression model, 163
Bayes theorem
marginal probability, 114
noninformative prior, 114
posterior probability, 114
predictor variable values, 113
prior probability, 114
best subsets regression, 161
using R, 162
between-cluster variation, 142
Biggest Category Model, 77
binning
based on predictive value
using Python, 59–62
using R, 62–3
best practices, 59
BIRCH clustering, 142
bivariate relationship, 225
boxplot, 225
branches, 81

C5.0 algorithm
decision trees
using Python, 89–90
using R, 89, 90–91
R, evaluation measures of, 102, 103
CART see classification and regression tree (CART) model
cases or subjects, 215
categorical() command, 84
categorical data as numeric, reexpression of using Python, 36–8
using R, 38–9
categorical variables see also qualitative variables
bar chart, 218
frequency (or count), 217, 218
(relative) frequency distribution, 217, 218
pie chart, 218
c() command, 24, 103
census, 217
class conditional independence, 114
classification, 5, 6–7
classification and regression tree (CART) model, 11
married node, 82–3
non-married marital status node, 83
root node split, 82, 83–4
using Python, 84–6
using R, 86–8
clothing_data_driven_test data set, 101
clothing_data_driven_training data set, 103
clothing_sales_test data sets, 152, 154, 156, 161, 189, 190, 191
clothing_sales_training data sets, 152, 154, 156, 161, 189, 190, 191
clothing_store_PCA_test data sets, 175
clothing_store_PCA_training data sets, 175
clustered bar chart, 226
clustering, 5, 7, 30
accounting auditing purposes, 142
BIRCH, 142
gene expression, 142
hierarchical, 142
K-means, 142–4
Kohonen networks, 142
target marketing, 141
validation, 144–5
colnames() command, 86
colnames() values, 204

columns of interest section, 25
column_stack() command, 56, 159
combination function, 131–3
components, 175
concat() command, 74
conditional independence, 118
conditional probabilities, 125
confidence difference criterion, 208–9
using R, 208–9
confidence of the rule, 209
confidence quotient criterion using R, 209–10
contingency tables, 225, 226
best practices, 52
for evaluating model 1, 101
for evaluating model 2, 106
for evaluating model 3, 108
of sex and death, 136
using Python, 13–14, 52–3, 123
using R, 23–4, 53
corr variable, 216
corr() command, 181
correlation coefficient, 227, 229
correlation matrix from Python, 180
credit card, 154, 157
cross(tab) command, 13, 14, 49, 61
cross-validation process, 3, 70
cumulative (relative) frequency distribution, 219
curvilinear behavior, 133
cut() command, 62
data, 216
data balancing, 3
data debugging, 70
data.frame() command, 85, 145, 160
data mining process, 142
data modeling, preparation balancing training data set, 73–6
baseline model performance, 77–8
data partitioning, 69–72
Setup Phase, 69
validating your partition, 72
data partitioning, 69–72
data preparation adding an index field using Python, 31–2
using R, 32–3
bank marketing data set, 29

