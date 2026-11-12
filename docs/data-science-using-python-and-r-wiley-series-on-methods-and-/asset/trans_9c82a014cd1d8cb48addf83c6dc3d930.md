

我们还可以从包中导入特定部分，而无需导入整个包。例如，在第 6 章中，我们将使用 sklearn.tree 包中的 DecisionTreeClassifier() 和 export_graphviz 命令。为此，我们将使用以下代码：

```
from sklearn.tree import DecisionTreeClassifier, export_graphviz
```

请注意，语法与我们之前导入包的方式有所不同。我们不再使用 import sklearn.tree，而是以 from sklearn.tree 开头。使用 from 告诉 Python 在哪里查找我们想要的命令。在 from sklearn.tree 之后，我们使用 import 指定要导入的内容。如果我们只导入 DecisionTreeClassifier 命令，则在该命令名称后结束该行。但是，由于我们要导入两个命令，我们添加一个逗号并继续使用第二个命令名称 export_graphviz。执行此行将导入这两个命令。

## 2.2.4 将数据导入 Python

现在我们将讨论如何将数据集导入 Python。在本文中，我们将使用 read_csv 命令，采用以下结构：

```
your_name_for_the_data_set = pd.read_csv(*the_path_to_the_file*)
```

read_csv 命令来自 pandas 包。按照第 2.2.3 节中的代码，我们将 pandas 包导入为 pd。导入 pandas 包后，我们可以通过输入 pd 来访问 read_csv 命令。要使用 read_csv() 命令，请输入 pd，然后加一个句点，接着是命令 read_csv。

代码的下一部分是数据文件的路径，包含在双引号中。对于许多 Windows 用户，路径将以 C:/ 开头并以文件名结尾。例如，在第 4 章中，您需要导入 bank_marketing_training 数据集。导入数据集的代码如下所示。

```
bank_train = pd.read_csv("C:/ ... /bank_marketing_training")
```

程序员将使用自己的文件路径替换上述路径中的 "C:/..." 部分。导入数据文件的示例如下所示。

```
bank_train = pd.read_csv("C:/Users/Data Science/Data/bank_marketing_training")
```

第 4 章的 Python 指南告诉读者将 bank_marketing_training 数据集读入为 bank_train。这不仅指定了要导入的数据集，还指定了调用数据集的名称。要遵循该指令，您应将数据集的名称指定为 bank_train，如上述代码所示。请记住您将数据集保存为什么名称，并尽量保持名称相对较短。您保存数据的名称将是您在其余代码中每次想要使用该数据时都要输入的名称。

## 2.2.5 在 Python 中保存输出

某些命令生成可在其他代码行中使用的输出。要在后续代码中使用输出，您需要将输出保存为命名对象。要保存输出，请遵循以下结构：

```
your_name_for_the_output = the_command_that_generated_the_output
```

您可能会注意到上述结构与我们用来导入 bank_marketing_training 数据集的结构相似。您可能正确推断出，我们使用的命令 read_csv() 生成了 bank_marketing_training 数据集的“输出”，并且我们将该输出命名为 bank。导入数据集使用与在特定名称下保存输出相同的编码语法。现在让我们使用列联表来说明运行命令但不保存输出与运行命令并保存输出之间的区别。

在第 4 章中，您需要创建一个列联表并保存它，以便使用该表制作条形图。创建列联表的代码只有一行，如下所示，并在图 2.3 中显示。

```
pd.crosstab(bank_train['previous_outcome'], bank_train['response'])
```

如果不保存 crosstab() 命令生成的输出，则生成的列联表将在 Spyder 中显示，如图 2.3 所示。在图中，“In”表示我们运行的代码，“Out”表示生成的输出。

如果我们只想制作一个表，而不在代码的其他地方使用它，那么这就足够了。但是，我们想使用这个表来制作条形图。因此，我们必须保存它。要保存它，我们在生成输出的命令左侧添加一个保存项目的名称和一个等号。代码如下所示，并在图 2.4 中显示。

```
In [9]: pd.crosstab(bank_train['previous_outcome'], bank_train['response'])
Out[9]:
response        yes
previous_outcome  no   yes
failure         2390  385
nonexistent     21176 2834
success         328   569
```

图 2.3 在 Python 中不保存输出的情况下创建列联表。

```
In [10]: crosstab_01 = pd.crosstab(bank_train['previous_outcome'], bank_train['response'])
```

```
In [11]:
```

![](img/fbc96b887811576a0dc93355dce68ae3_27_0.png)

```
In [11]: crosstab_01
Out[11]:
response        no   yes
previous_outcome
failure         2390  385
nonexistent     21176 2034
success         328   569
```

![](img/fbc96b887811576a0dc93355dce68ae3_27_1.png)

```
crosstab_01 = pd.crosstab(bank_train['previous_outcome'], bank_train['response'])
```

名称可以是任何内容，前提是它以字母（而不是数字或符号）开头，并且不包含句点或下划线以外的其他特殊字符。在图 2.4 中，我们将表命名为 crosstab_01。

请注意，图 2.4 中没有输出。“In”语句从“In [10]”跳到“In [11]”，中间没有指定“Out [10]”。Python 跳过“Out”语句，因为 crosstab() 命令生成的输出已保存为名称 crosstab_01。

要查看输出，请单独运行我们给输出的名称，在此例中为 crosstab_01。结果如图 2.5 所示。

## 2.2.6 在 Python 中访问记录和变量

在您的数据科学探险中，您可能想要检查特定记录。例如，我们如何访问 bank_train 数据集中的记录？我们使用所有 pandas 数据框都具有的 loc 属性，并说明您想查看数据框的哪一部分。

Python 从记录零开始引用其记录，因此如果我们想查看第一条记录，我们请求记录 0。同样，要查看第二条记录，请求记录 1，依此类推。例如，要查看 bank_train 的第一条记录，请使用以下代码：

```
bank_train.loc[0]
```

如上使用 loc 属性查看第一条记录将返回该记录的所有变量值。图 2.6 显示 bank_train 数据集中第一条记录的前四个变量值。

```
In [30]: bank_train.loc[0]
Out[30]:
age             56
job        housemaid
marital       married
education      basic.4y
```

图 2.6 Python 显示 bank_train 数据集中第一条记录的变量值（仅显示前四个变量）。

如果我们想访问许多记录怎么办？我们将使用 .loc 属性并列出我们想查看的记录。如果您想要第一、第三和第四行，请使用以下代码：

```
bank_train.loc[[0, 2, 3]]
```

另一方面，如果您想要前 10 行（包含第 10 行），则应使用以下代码：

```
bank_train[0:10]
```

虽然我们按数字引用行，但我们的列有名称。这意味着，如果我们想指定要查看哪个变量，我们需要提供其名称。

```
bank_train['age']
```

使用一组括号并将变量名放在单引号中将返回整个变量。代码和前四个 age 值如图 2.7 所示。

如果我们想查看多个变量怎么办？我们将使用 .loc 属性并列出我们想查看的变量。如果我们想查看 age 和 job 变量，我们将每个变量名放在单引号中，放在双括号内，并用逗号分隔。

```
bank_train[['age', 'job']]
```

此命令的输出如图 2.8 所示。

## 2.2.7 在 Python 中设置图形

在离开 Python 编码部分之前，我们还需要解决一件事：如何在 Python 中获取和调整图形输出。

默认情况下，Spyder 在右下角窗口的 IPython 控制台中显示所有图形。图 2.9 显示了一个示例，使用直方图。这些没有编辑选项的小型显示对于简单图形可能是可以接受的。但是，我们将制作复杂图形，这将需要进一步编辑和更大的显示。为了使我们能够详细查看和操作图形，我们需要更改 Spyder 的图形设置。

