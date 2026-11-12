

![](img/fbc96b887811576a0dc93355dce68ae3_49_0.png)

图 3.4 R 中的教育变量条形图。

表 3.1 将教育变量的值重新表示为数值

| 类别值 | 数值 |
| :--- | :--- |
| illiterate | 0 |
| basic.4y | 4 |
| basic.6y | 6 |
| basic.9y | 9 |
| high.school | 12 |
| professional.course | 12* |
| university.degree | 16 |
| unknown | Missing |

* 此值基于 In-Vet，Preventing initial dropout and fostering initial inclusion，http://ivet-project.eu/wp-content/uploads/2014/06/National-Report-Portugal_Final.pdf。这两个组，professional 和 high school，将使用相同的数值 12 进行合并。这两个组中积极响应者的比例相似（111 对 10.78%），因此我们大概可以接受将它们合并。

等号右侧指定 education 变量，等号将这些值赋给左侧。当前不存在名为 education_numeric 的变量，因此将创建一个变量，并赋予 education 变量的值。

我们需要专门设置一个字典，用于将 education_numeric 变量中的分类值转换为数值。字典包含在花括号 { } 中，设置我们的字典，如下所示：

```
dict_edu = {"education_numeric": {"illiterate": 0,
"basic.4y": 4, "basic.6y": 6,
"basic.9y": 9, "high.school":12, "professional.course": 12, "university.degree":16,
"unknown": np.nan}}
```

在字典中，我们使用 **"education_numeric"** 来指定要重新编码的变量，后跟一个冒号和另一组花括号。在这第二组花括号中，我们按以下顺序指定重新编码：

变量的原始值 = 变量的新值

每个规范之间用逗号分隔。请注意，在必要时，我们使用 Python 的缺失数值 **NaN**。

最后，我们告诉 Python 使用字典来替换变量的值。

```
bank_train.replace(dict_edu, inplace=True)
```

replace() 命令将根据字典 dict_edu 中的规则替换值。

### 3.6.2 如何使用 R 重新表示分类字段值

首先，我们需要安装并加载 _plyr_ 包。

```
install.packages("plyr"); library(plyr)
```

我们需要指定 education 的哪些值对应哪些数值，遵循表 3.1 中指定的规则。

```
edu.num <- revalue(x = bank_train$education, replace =
c("illiterate" = 0, "basic.4y" = 4,
"basic.6y" = 6, "basic.9y" = 9, "high.school" = 12,
"professional.course" = 12,
"university.degree" = 16, "unknown" = NA))
```

revalue() 函数根据 **replace** 输入中给出的规则，替换 **x** 输入中给定变量的值。在 **replace** = 输入中，我们使用 **c**() 将每个重新编码片段连接在一起，使用以下结构：

变量的原始值 = 变量的新值

每个规范之间用逗号分隔。请注意，在必要时，我们使用 R 的缺失值 **NA**。我们将输出保存为 **edu.num**。

目前，**edu.num** 的值不是数值（例如，你无法使用它们制作直方图），因此我们需要将变量的水平转换为数值类型。对象 edu.num 是一个因子，我们使用以下代码将其值转换为数字：

```
bank_train$education_numeric <- as.numeric(levels(edu.num))[edu.num]
```

levels() 命令获取 edu.num 变量的因子水平，这些水平是字符串。as.numeric() 命令将它们转换为数字。这些新值应用于 edu.num 变量，结果保存为我们的新变量 education_numeric。图 3.5 显示了重新表示的教育字段 education_numeric 的直方图。

![](img/fbc96b887811576a0dc93355dce68ae3_51_0.png)

图 3.5 R 中的 education_numeric 直方图。

## 3.7 标准化数值字段

当数值字段被标准化，使得字段均值等于 0 且字段标准差等于 1 时，某些算法表现会更好，如下所示：

$z = Standardized Value = \frac{x - \bar{x}}{s} = \frac{Data value - mean}{Standard deviation}$

正 z 值可解释为数据值位于均值以上的标准差个数，而负 z 值表示数据值位于均值以下的标准差个数。一些分析师作为惯例会标准化所有数值字段。接下来，我们展示如何在 Python 和 R 中标准化数值字段。

### 3.7.1 如何使用 Python 标准化数值字段

导入所需的包。

```
from scipy import stats
```

我们将标准化 age 变量，并将其保存为新变量 age_z。

zscore 函数计算给定变量的 z 值，在此例中为 age，在代码中写作 bank_train['age']。由于 zscore() 命令是 stats 包的一部分，我们将命令写作 stats.zscore()。我们将其保存为数据集中的新变量 age_z。

### 3.7.2 如何使用 R 标准化数值字段

此代码无需安装或加载包。我们将使用的命令 scale() 包含在 R 的初始下载中。

```
bank_train$age_z <- scale(x = bank_train$age)
```

scale() 函数可以通过减去均值来中心化变量，通过除以标准差来缩放变量，或两者兼施。默认情况下，它两者都执行，以计算 z 分数。因此，在 bank_train$age 变量上使用 scale() 函数的默认设置将返回该变量的 z 分数。我们可以使用 bank_train$age_z 将 z 值保存为数据集中的新变量。

## 3.8 识别异常值

数值字段标准化后，可以使用 z 值来识别异常值，异常值是在某一维度或多个维度上具有极端值的记录。例如，考虑字段 number_of_contacts，它表示营销活动过程中与客户的联系次数。每位客户的平均联系次数为 2.6，标准差为 2.7（允许四舍五入）。因此，我们得到标准化字段如下：

number_of_contacts_z = \frac{number_of_contacts - 2.6}{2.7}

一个经验法则是，如果数据值的 z 值大于 3 或小于 -3，则该数据值为异常值。例如，一位被联系了 10 次（似乎很多）的客户将具有标准化值，

number_of_contacts_z = \frac{10-2.6}{2.7} = 2.7

因此，10 次联系虽然很多，但使用此方法不被识别为异常值，因为 2.7 < 3。

数据科学家应与客户协商，商讨如何处理任何异常值。不应自动删除异常值！也不应自动更改它们。它们的异常值可能会揭示数据的重要方面，这些方面应与客户或数据库管理员讨论。

### 3.8.1 如何使用 Python 识别异常值

在此示例中，我们将继续使用前一节中创建的 age_z 变量。我们将使用 query() 函数来查找异常值，该函数识别满足特定条件的行。

```
bank_train.query('age_z > 3 | age_z < -3')
```

我们希望所有返回记录满足的条件为 'age_z > 3 | age_z < -3'。用文字来说，此条件要求每条记录要么具有大于 3 的 age_z 值，要么具有小于 -3 的 age_z 值。"|" 由两个条件之间的字符 | 指定。

将返回所有满足指定条件的记录。在我们的示例中，有 228 条记录的 age_z 值大于 3 或小于 -3。我们可以使用这些记录创建一个仅由这些值组成的新数据集。

```
bank_train_outliers = bank_train.query('age_z > 3 |
age_z < -3')
```

通过为 query() 命令的输出命名，我们创建了一个仅包含异常值的新数据集，我们将其命名为 bank_train_outliers。

让我们按 age_z 变量对数据集 bank_train_outliers 进行排序。

```
bank_train_sort = bank_train.sort_values(['age_z'],
ascending = False)
```

.sort_values() 命令将根据指定变量对数据集中的记录进行排序。排序可以是升序或降序。在此示例中，我们希望最大的 age_z 值位于顶部，因此我们按降序排序，通过

