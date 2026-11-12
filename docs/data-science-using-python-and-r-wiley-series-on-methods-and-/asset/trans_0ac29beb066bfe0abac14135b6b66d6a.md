

## 4.1 EDA 与 HT

客户或分析师通常持有希望数据验证的先验假设。此类假设的一个示例是：与固定电话用户相比，手机用户的正面响应率是否更高？由此产生的假设检验（HT）可以使用经典统计方法或数据科学的交叉验证方法（第 5 章）来执行。

另一方面，客户或分析师可能对数据可能揭示的内容没有任何显著的先验概念。在这种情况下，他们可能更倾向于使用探索性数据分析（EDA）或图形数据分析。EDA 允许用户：

- 使用图形探索预测变量与目标变量之间的关系。
- 使用图形和表格推导将提高预测价值的新变量。
- 合理使用分箱，以提高预测价值。

在本章中，我们将继续探索第 3 章中的 bank_marketing_training 数据集。我们首先使用图形来研究目标响应与分类预测变量之间的关系。

## 4.2 带响应叠加的条形图

我们可以使用带响应叠加的条形图来探索分类预测变量与目标变量之间的关系。图 4.1 显示了带目标响应叠加的 previous_outcome 条形图。previous_outcome 指的是与同一客户之前营销活动的结果，大多数客户没有此类之前的经历。

显然，大多数客户与该变量没有任何之前的营销经历（变量值 nonexistent）。一般而言，（未归一化的）条形图

![](img/fbc96b887811576a0dc93355dce68ae3_59_0.png)

### 图 4.1 来自 R 的带响应叠加的 previous_outcome 条形图。

![](img/fbc96b887811576a0dc93355dce68ae3_59_1.png)

### 图 4.2 来自 R 的带响应叠加的 previous_outcome 归一化条形图。

对于显示分类变量值的分布很有用。但是，不清楚哪个类别的响应者比例更大。Nonexistent 拥有最多的响应者，但也拥有最多的非响应者。为了澄清此类情况，我们可以获得一个归一化条形图，它使每个条形的长度相等，从而更容易比较响应比例。图 4.2 表示 previous_outcome 的此类归一化条形图，

带响应叠加。从图 4.2 可以清楚地看出，正面响应比例最高的群组是 success，即那些对公司之前活动做出正面响应的客户。有趣的是，上次做出负面响应（failure）的客户，此次的成功率也略高于没有之前联系的客户。

此练习展示了使用条形图时的两项最佳实践。

## 最佳实践：条形图

- 当带叠加的条形图对响应比例不清楚时，用归一化条形图加以补充。
- 但是，切勿在未提供其未归一化版本的情况下提供归一化条形图，因为归一化版本未指示原始分布（每个类别中的记录数量）。

## 4.2.1 使用 Python 构建带叠加的条形图

加载所需的包，并将 bank_marketing_training 数据集读取为 bank_train。

```
import pandas as pd
bank_train = pd.read_csv("C:/.../bank_marketing_training")
```

创建条形图的第一步是创建预测变量和目标变量值的列联表。我们使用 crosstab() 命令创建表格。

```
crosstab_01 = pd.crosstab(bank_train['previous_outcome'], bank_train['response'])
```

此代码稍后将详细检查。目前，我们将表格保存为 crosstab_01。

现在，我们可以根据表格创建条形图。

```
crosstab_01.plot(kind='bar', stacked = True)
```

要创建条形图，请将 .plot() 附加到 crosstab_01 对象的末尾。plot() 命令接受各种可选输入值。我们指定 kind = 'bar' 来绘制条形图，并指定 stacked = True 来指定堆叠条形图。

要创建归一化版本，我们需要更改表格，使每个单元格中的值是预测变量 previous_outcome 每个值中 "no" 和 "yes" 响应值的比例，如下所示：

```
crosstab_norm = crosstab_01.div(crosstab_01.sum(1), axis = 0)
```

![](img/fbc96b887811576a0dc93355dce68ae3_61_0.png)

### 图 4.3 来自 Python 的带响应叠加的 previous_outcome 归一化条形图。

div() 命令将在每个指定轴内，用另一个对象除以表格的值。在我们的示例中，我们希望用表格第 1 行单元格之和除以第 1 行的单元格，以此类推，适用于第 2 行和第 3 行。为了实现这一点，我们首先将要除以的值设置为 crosstab_01.sum(1)，即表格中每一行的和。然后我们设置 axis = 0 以指定我们希望用这些值除以表格的行。结果是一个表格，其单元格是该行中落在该列的数据比例。我们将生成的表格保存为 crosstab_norm。

保存表格后，使用上述堆叠条形图代码对其进行可视化。

```
crosstab_norm.plot(kind='bar', stacked = True)
```

生成的图表如图 4.3 所示。

## 4.2.2 使用 R 构建带叠加的条形图

使用 bank_train 读取 bank_marketing_training 数据集。我们将使用 ggplot2 包来创建图表。您需要使用 install.packages() 安装一次该包，然后在每次编写新代码时使用 library() 打开它。

```
install.packages("ggplot2"); library(ggplot2)
```

ggplot 代码使用加号（+）将不同的命令链接在一起，如以下示例所示。请注意，加号必须紧跟在前面的命令之后，中间没有换行，但后面可以跟换行。

要创建 *先前结果* 变量的条形图，我们使用 `ggplot()` 和 `geom_bar()` 命令。

```
ggplot(bank_train, aes(previous_outcome)) + geom_bar() +
coord_flip()
```

`ggplot()` 命令开始绘制图表。`bank_train` 输入指定正在使用的数据集，感兴趣的变量列在 `aes()` 下（“aes”代表“美学”）。第二段代码是 `geom_bar()`，它指定应制作条形图。代码知道使用哪个变量是因为前面的 `ggplot()` 命令。可选的第三段代码是 `coord_flip()`，它将使条形水平运行。

要创建带 *响应* 叠加的条形图，我们添加 fill 输入。

```
ggplot(bank_train, aes(previous_outcome)) + geom_bar(aes(fill = response)) + coord_flip()
```

请注意，唯一的变化是在 `geom_bar()` 内部添加 `aes(fill = response)`。结果是图 4.1 所示的图表。

要归一化条形图，请在 `geom_bar()` 内部添加 `position = "fill"`，如下所示。

```
ggplot(bank_train, aes(previous_outcome)) + geom_bar(aes(fill = response),
position = "fill") + coord_flip()
```

输入 `position = "fill"` 添加到 `geom_bar()` 命令内部，但在 `aes()` 外部。结果是图 4.2 所示的图表。

## 4.3 列联表

为了帮助量化分类预测变量与目标之间的关系，我们可以构建一个 *列联表*，它是两个变量的交叉表，并包含每个变量值组合（即每种情况）的一个单元格。图 4.4 包含 *先前结果* 与 *响应* 的列联表。请注意，通常的做法是让目标变量表示行，预测变量表示列。对于 EDA，包含列百分比也很有帮助。图 4.5 包含带列百分比的表格。大多数客户没有之前的营销活动（*不存在*），因此请注意，其中 21,176 个响应了 *否* 而 2034 个响应了 *是*。总体而言，请注意，*是* 响应的比例仅为 *失败* 的 13.9% 和 *不存在* 的 8.8%，但当客户之前的营销活动 *成功* 时，则高达 64%。

列联表的最佳实践如下。

