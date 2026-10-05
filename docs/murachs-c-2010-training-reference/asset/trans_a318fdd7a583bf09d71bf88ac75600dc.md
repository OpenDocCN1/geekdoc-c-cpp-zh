

# 使用数组 Length 属性的语法

arrayName.Length

# 计算总数组平均值的代码

```sharp
decimal[] totals = [14.95m, 12.95m, 11.95m, 9.95m];
decimal sum = totals[0] + totals[1] + totals[2] + totals[3];
decimal average = sum/4;
```

# 将数字 0 到 9 放入数组的代码

```sharp
int[] numbers = new int[10];
for (int i = 0; i < numbers.Length; i++)
    numbers[i] = i;
```

# 在消息框中显示数字的代码

```sharp
string numbersString = "";
for (int i = 0; i < numbers.Length; i++)
    numbersString += numbers[i] + " ";
MessageBox.Show(numbersString, "Numbers Test");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_238_0.png)

# 使用 for 循环计算 totals数组平均值的代码

```sharp
decimal sum = 0.0m;
for (int i = 0; i < totals.Length; i++)
    sum += totals[i];
decimal average = sum/totals.Length;
```

# 在消息框中显示 totals 数组的代码

```sharp
string totalsString = "";
for (int i = 0; i < totals.Length; i++)
    totalsString += totals[i] + "\n";
MessageBox.Show("The totals are:\n" +
    totalsString + "\n" +
    "Sum: " + sum + "\n" +
    "Average: " + average, "\n" +
    "Totals Test");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_238_1.png)

图 8-3 如何处理数组

# 如何使用 foreach 循环处理数组

虽然你可以使用循环来处理数组元素，但使用 foreach 语句来编写 foreach 循环通常更容易。图 8-4 显示了如何这样做。

要编写 foreach 循环，首先编写 `foreach` 关键字，后跟一组括号。在括号内，你可以编写数组中元素的数据类型、你想要用于访问元素的名称、`in` 关键字以及数组的名称。你也可以用 `var` 关键字来代替数据类型，在这种情况下，类型将根据数组的类型推断出来。

接下来，你可以编写一个或多个语句，使用元素名称来处理该元素。如果 foreach 循环包含两个或多个语句，则必须省略围绕这些语句的大括号。

当执行 foreach 循环时，其语句会为数组中的每个元素执行一次。例如，图中的第一个示例显示了你如何使用 foreach 循环显示你在上一个图中看到的 numbers 数组中的元素。同样，第二个示例计算了 totals 数组的平均值，而第三个示例显示了 totals 数组中的元素。

如果你将这些示例与上一个图中的 `for` 循环示例进行比较，你会发现 foreach 循环不那么复杂。特别是当你使用 foreach 循环时，不需要使用计数器变量，也不需要使用索引从数组获取元素。因此，使用 foreach 循环通常比 for 循环更容易。

然而，你应该意识到，在某些时候你仍然需要使用 `for` 循环来处理数组。例如，如果你只想访问数组中的某些元素，你就需要使用 `for` 循环。如果你想使用计数器变量为数组元素分配值（如图 8-3 中的第二个示例所示），你也将需要使用 `for` 循环。

# 第 8 章 如何处理数组和集合

# foreach 循环的语法

```sharp
foreach (type elementName in arrayName)
{
    statements
}
```

# 在消息框中显示 numbers 数组的代码

```sharp
string numbersString = "";
foreach (int number in numbers)
{
    numbersString += number + " ";
}
MessageBox.Show(numbersString, "Numbers Test");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_240_0.png)

# 计算 totals数组平均值的代码

```sharp
decimal sum = 0.0m;
foreach (decimal total in totals)
    sum += total;
decimal average = sum/totals.Length;
```

# 在消息框中显示 totals 数组的代码

```sharp
string totalsString = "";
foreach (decimal total in totals)
    totalsString += total + "\n";
MessageBox.Show("The totals are:\n" + 
    totalsString + "\n" + 
    "Sum: " + sum + "\n" + 
    "Average: " + average + "\n" + 
    "Totals Test");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_240_1.png)

# 描述

- 你可以使用 foreach 循环访问数组的每个元素。图 8-4 显示了如何使用 foreach。

# 如何处理数组

到为止，本章展示了如何使用一维数组。现在，你将学习二维数组。虽然可以超过两个维度，但这种情况很少见。

# 如何创建二维数组

创建二维数组的语法是：
`type[,] arrayName = new type[rowCount,columnCount];`

创建一个 3x2 数组的语句：
`int[,] numbers = new int[3,2];`

# 如何为二维数组赋值

引用二维数组元素的语法是：
`arrayName[rowIndex, columnIndex]`

一个 4x4 数组的索引如下：

| 0,0 | 0,1 | 0,2 | 0,3 |
| 1,0 | 1,1 | 1,2 | 1,3 |
| 2,0 | 2,1 | 2,2 | 2,3 |
| 3,0 | 3,1 | 3,2 | 3,3 |

为 numbers 数组赋值的代码

```sharp
numbers[0,0] = 1;
numbers[0,1] = 2;
numbers[1,0] = 3;
numbers[1,1] = 4;
numbers[2,0] = 5;
numbers[2,1] = 6;
```

# 用一条语句创建 3x2 数组并赋值

```sharp
int[,] numbers = {{1,2}, {3,4}, {5,6}};
```

# 创建并为 3x2 字符串数组赋值的代码

```sharp
string[,] products = {"CS110", "Murach's C# 2010"}, {"JS66", "Murach's Java SE 6"}, {"A4CS", "Murach's ASP.NET with C# 2010}};
```

# 创建字符串数组的另一种方法

```sharp
var products = new string[][] {
    {"CS110", "Murach's C# 2010"},
    {"JS66", "Murach's Java SE 6"},
    {"A4CS", "Murach's ASP.NET with C# 2010"}
};
```

# 描述

- 二维数组使用索引来存储数据。你可以将这种数组想象成具有行和列的表格。
- 虽然可以超过两个维度，但这种情况很少见。

