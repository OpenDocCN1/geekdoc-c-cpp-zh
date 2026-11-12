

要创建索引，我们首先需要找到数据集中的记录数和列数。

```
bank_train.shape
```

在数据集名称后使用.shape将给出数据集中的行数和列数。输出中的第一个数字是记录数，26,874。第二个是变量数。

一旦我们知道了记录数，我们就创建一个新变量，为每条记录分配一个唯一的整数。

```
bank_train['index'] = pd.Series(range(0,26874))
```

嵌套命令Series()和range()创建一串数字，其下限为零，上限为记录数。由于Series()命令包含在pandas包中，并且我们将pandas包重命名为pd，因此在Series()命令前加上pd和一个句点。结果是代码pd.Series()。请注意，range()命令的下限为零而不是一，因为Python从零开始计数位置。我们将这串数字作为数据集中的新变量index保存，方法是使用bank_train['index']将pd.Series(range())的输出分配给bank_train数据集的index变量。

要查看带有新变量的数据集，我们可以查看数据集的开头部分。

```
bank_train.head
```

在数据集名称后使用.head将生成包含数据集中每个变量的前30条和后30条记录的输出。

### 3.4.2 如何使用R添加索引字段

使用RStudio中的Import Dataset按钮将数据集导入为bank_train名称。要创建索引字段，我们首先需要知道数据集中有多少条记录。

```
n <- dim(bank_train)[1]
```

dim()命令给出将其名称用作输入值的数据集的记录数和变量数；在此例中为bank_train数据集。在dim(bank_train)末尾添加[1]将导致仅输出第一个数字，即记录数。我们将输出保存为小写字母“n”，这是样本量的常用表示法。如果单独执行n，输出将是数字26,874，即数据集中的记录数。

一旦我们有了记录数，我们就创建一个新变量，为每条记录分配一个唯一的整数，以指定其在数据集中的顺序。

```
bank_train$Index <- c(1:n)
```

函数c()将其输入值合并为单个对象。在我们的例子中，输入是1:n，代表“从1到n的整数（包含两端）”。命令c(1:n)将给出从1到bank数据集记录数的一串数字。我们将这串数字作为数据集中的新变量Index保存，方法是将c(1:n)保存为bank_train$Index。

要查看带有新索引变量的数据集，请运行head()命令，以bank_train数据集作为其唯一输入。

```
head(bank_train)
```

生成的输出是所有变量（包括Index变量）的前六条记录。

## 3.5 更改误导性字段值

字段days_since_previous是自上次市场活动联系客户以来的天数计数。该字段明显是数值型，因此我们可以查看图3.1中R提供的days_since_previous直方图。请注意，大多数数据值接近1000，少数值接近零。事实证明，数据库管理员使用代码999表示以前未被联系过的客户。因此，我们需要将字段值999更改为缺失值，在Python和R中操作如下。

![](img/fbc96b887811576a0dc93355dce68ae3_45_0.png)

图3.1 R中days_since_previous的直方图，大多数值接近1000。

4参见附录。数据汇总与可视化。

## 3.5.1 如何使用Python更改误导性字段值

如果您未按前一节Python部分所述打开`pandas`包或读入数据集，请立即执行此操作。本节我们还需要导入`numpy`包。

```
import numpy as np
```

我们需要识别所有`days_since_previous`值为999的记录，并将其替换为Python中表示缺失值的代码`NaN`。完成替换后，我们将在`days_since_previous`变量名下保存该变量，从而有效覆盖先前变量的值。

```
bank_train['days_since_previous'] = bank_train['days_since_previous'].replace({999: np.NaN})
```

代码`bank_train['days_since_previous']`访问变量`days_since_previous`。命令`replace({999: np.NaN})`查找`days_since_previous`变量中的每个999实例，并将其替换为值`NaN`。要将新编辑的变量保存到其原始名称下，我们通过重用变量名`bank_train['days_since_previous']`将右侧设置为等于左侧的原始`days_since_previous`变量。

要创建变量的直方图，请使用`hist()`命令。

```
bank_train['days_since_previous'].plot(kind = 'hist', title = 'Histogram of Days Since Previous')
```

在变量名后使用`.plot()`将绘制变量的图表。我们使用`kind = 'hist'`指定应制作直方图。`title`输入（包含在单引号中）创建直方图的标题。输出如图3.2所示。在第4章中，我们将查看更复杂的直方图。

## 3.5.2 如何使用R更改误导性字段值

如果您未按前一节R部分所述读入数据集，请立即执行此操作。

我们需要识别`days_since_previous`变量中每个999的实例，并将其替换为R中表示缺失值的代码值`NA`。

![](img/fbc96b887811576a0dc93355dce68ae3_47_0.png)

图3.2 Python中days_since_previous的直方图，缺失值已正确编码。

```
bank_train$days_since_previous <- ifelse(test = bank_train$days_since_previous == 999,
yes = NA, no = bank_train$days_since_previous)
```

ifelse()命令检查test =下指定的条件，如果测试条件为真，则将days_since_previous变量赋值为yes =后给出的值；如果测试条件为假，则将days_since_previous变量赋值为no =后给出的值。

在我们的例子中，对每条记录进行检查，看其是否在days_since_previous变量中包含值999。如果是，则返回值NA。如果不是，则返回days_since_previous变量中的原始值。要将返回值字符串保存为变量days_since_previous，请使用bank_train$days_since_previous将输出保存为变量。

要创建变量的直方图，请使用hist()命令。

```
hist(bank_train$days_since_previous, xlab = "days_since_previous",
main = "Histogram of days_since_previous - Missing values replaced by NA")
```

hist()命令有一个必需输入，即感兴趣的变量。我们使用bank_train$days_since_previous作为感兴趣的变量。可选输入值main和xlab分别指定直方图的标题和X轴标签。请注意，标签必须包含在引号中。

图3.3显示了排除缺失值后的days_since_previous直方图。

![](img/fbc96b887811576a0dc93355dce68ae3_48_0.png)

图3.3 R中days_since_previous的直方图，缺失值已排除。

## 3.6 将分类数据重新表示为数值

图3.4显示了education字段的条形图。请注意，该字段是分类型的，意味着字段值之间没有顺序。换句话说，如果我们保持字段原样，那么我们的数据科学算法将不知道university_degree表示的教育程度高于basic.4yr。为了向算法提供此信息，我们将数据值转换为数值，其中一个值明显大于另一个值。执行此操作时需要谨慎，以便保持各类别之间的相对差异。

表3.1展示了我们计划如何完成此转换。temporary course的值1/2来源于脚注中所示的出版物，作为通常高中学习课程的替代方案。当然，未知值也需要重新表示为缺失值。

### 3.6.1 如何使用Python重新表示分类字段值

我们将复制education变量，并将其命名为education_numeric，以准备将其分类值替换为数值。

```
bank_train['education_numeric'] = bank_train['education']
```

