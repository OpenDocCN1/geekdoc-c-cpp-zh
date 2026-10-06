

# 检测输入文件的结束

在我们的伪代码中，我们使用 `eof` 函数来判断是否已到达输入文件的末尾。该函数的通用格式如下：
eof(internalFileName)

`eof` 函数接受一个文件名作为参数，如果到达文件末尾则返回 `true`，如果未到达末尾则返回 `false`。下面的伪代码显示了一个示例：

```
// 声明一个输入文件
Declare InputFiles
// 用于存储销售金额的变量
// 从文件中读取
Declare Real sales
// 打开 sales.dat 文件。
Open salesFile "sales.dat"
// 读取文件中的所有项目
// 并显示它们。
While NOT eof(salesFile)
Read salesFile sales
Display currencyFormat(sales)
End While
// 关闭文件。
Close salesFile
```

# 删除文件

要删除文件，我们使用 `Delete` 语句。这里是通用格式：

Delete Filename

在通用格式中，*Filename* 是系统磁盘上的文件名。这是一个示例：

Delete "customers.dat"

# 重命名文件

要重命名文件，我们使用 `Rename` 语句。这里是通用格式：

Rename ExistingName, NewName

在通用格式中，*ExistingName* 是文件的现有名称（在系统磁盘上），*NewName* 是文件的新名称。这是一个示例：

Rename "temp.dat", "customers.dat"

# 定义类

通用格式：
Class ClassName
字段声明和方法定义在此处...
End Class

第一行以单词 `Class` 开头，后面跟着类名。接下来你编写类字段声明和类方法的定义。`End` 单词出现在类定义的末尾。这里是第14章所示的 `CellPhone` 示例：

```
Class CellPhone
// 字段声明
Private String manufacturer
Private String modelNumber
Private Real retailPrice

// 方法定义
Public Module setManufacturer(String manufact)
Set manufacturer = manufact
End Module

Public Module setModelNumber(String modNum)
Set modelNumber = modNum
End Module

Public Module setRetailPrice(Real real)
Set retailPrice = real
End Module

Public Function getManufacturer()
Return manufacturer
End Function

Public Function getModelNumber()
Return modelNumber
End Function

Public Function getRetailPrice()
Return retailPrice
End Function
End Class
```

# 创建类实例

要创建一个类的实例（换句话说，一个对象），你声明一个变量来引用该对象，并使用 `New` 运算符创建实例。这里有一个创建之前所示 `CellPhone` 类实例示例：

```
Declare CellPhone myPhone
Set myPhone = New CellPhone()
```

第一条语句声明了一个名为 `myPhone` 的变量。第二条语句创建了 `CellPhone` 实例，并将其内存地址分配变量 `myPhone`。

# 将十进制数转换为二进制

你可以通过绘制简单的图表并执行重复减法将十进制数转换为二进制。以下步骤显示了如何将十进制数 162 转换为二进制。

- 1. 创建一个两行的表格。顶行列出所有2的幂，直到但不大于你尝试转换的数字。（2的幂为 $2^0 = 1, 2^1 = 2, 2^2 = 4, 2^3 = 8$ 等），从右向左列出。

要将十进制 162 转换为二进制，你需要制作如下图表。（图表在 128 处停止，因为下一个 2 的幂是 256，大于你尝试转换的数字。）

| 128 | 64 | 32 | 16 | 8 | 4 | 2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

- 2. 找到图表中最大的数字（在本例中为128），在第二行下方写上 1。然后从你尝试转换的数字中减去该数。在这个问题中，结果是 34。这是你的新数字。工作区如下：

| 128 | 64 | 32 | 16 | 8 | 4 | 2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | | | | | | |

- 3. 在图表中找到不大于步骤2计算出的新数字的最大数字。在这个问题中，我们在寻找不大于34的数字。我们要找的数字是 32。在它下方写上 1。然后从你正在处理的数字中减去该数。在这个问题中，结果是 2。这是你的新数字。工作区如下：

| 128 | 64 | 32 | 16 | 8 | 4 | 2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | | 1 | | | | |

- 4. 在图表中找到不大于步骤3计算出的新数字的最大数字。在这个问题中，我们在寻找不大于2的数字。我们要找的数字是 2。在第二行下方写上 1。然后从你正在处理的数字中减去该数。在这个问题中，结果是 0。这是你的新数字。工作区如下：

| 128 | 64 | 32 | 16 | 8 | 4 | 2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | | 1 | | | | 1 |

- 5. 当你的新值为 0 时，你就完成了数字转换。回到图表，在第二行的每个空位填上 0。你的图表应该如下：

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |

第二行显示了等于 162 的二进制数：10100010

