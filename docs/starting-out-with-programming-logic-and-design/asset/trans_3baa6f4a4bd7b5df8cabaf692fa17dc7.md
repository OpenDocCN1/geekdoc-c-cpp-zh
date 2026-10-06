

# 给数组元素赋值

你通过下标访问数组中的单个元素。例如，假设上文描述的 `numbers` 是一个整型数组，以下伪代码为它的五个元素中的每一个赋值了值。

```
Set numbers[0] = 20
Set numbers[1] = 30
Set numbers[2] = 40
Set numbers[3] = 50
Set numbers[4] = 60
```

这段伪代码将值 20 赋值给元素 0，将值 30 赋值给元素 1，依此类推。图 8-2 显示了这些语句执行后数组的内容。

![](img/c939132f78787c7f339c6977b3fc8c85_310_0.png)

> 注意：表达式 `numbers[0]` 的读法是 "numbers sub zero"。

# 输入和输出数组内容

你可以像处理普通变量一样从键盘读取值并将其存储在数组元素中。你也可以输出数组元素的内容。程序 8-1 中的伪代码显示了一个用于存储和显示用户输入值的数组。

```
// 创建员工数量的常量。
Integer SIZE = 3

// 声明一个数组来存储每个员工
// 工作的小时。
Declare Integer hours[SIZE]

// 获取员工 1 的工作时长。
Display "Enter the hours worked by employee 1."
Input hours[0]

// 获取员工 2 的工作时长。
Display "Enter the hours worked by employee 2."
Input hours[1]
```

# 8.1 数组基础 287

```
// 获取员工 3 的工作时长。
Display "Enter the hours worked by employee 3."
Input hours[2]

// 显示输入的值。
Display "The hours you entered:"
Display hours[0]
Display hours[1]
Display hours[2]
```

程序输出（输入部分加粗显示）
Enter the hours worked by employee 1.
[40]
Enter the hours worked by employee 2.
[20]
Enter the hours worked by employee 3.
[15]
The hours you entered:
40
20
15

让我们仔细观察这个程序。第 2 行声明了一个命名常量 `SIZE`，并初始化为值 3。然后，第 6 行声明了一个名为 `hours` 的整型变量。`SIZE` 常量被用数组大小声明符，因此 `hours` 数组将有 3 个元素。第 10、14 和 18 行的 `Input`语句从键盘读取并将这些值存储在数组元素中。然后，第 22 到 24 行的 `Display`语句输出存储在每个数组元素中的值。

在程序的运行时，用户输入了值 40、20 和 15，这些值被存储在 `hours` 数组中。图 8-3 显示了存储这些值后数组的内容。

# 图 8-3 hours 数组的内容

| 40 | 20 | 15 |
| hours[0] | hours[1] | hours[2] |

# 使用循环遍历数组

所有的编程语言都允许将一个数字存储在变量中，然后将其作为下标。这使得可以使用循环遍历整个数组，对每个元素执行相同的操作。例如，查看程序 8-2 中的伪代码。

# 程序 8-2

```
1 // 声明一个包含 10 个元素的整型数组。
2 Declare Integer series[10]
3
4 // 声明一个用于循环的变量。
5 Declare Integer index
6
7 // 将每个数组元素设置为 100。
8 For index = 0 To 9
9 Set series[index] = 100
10 End For
```

在第 2 行声明了一个名为 `series` 的整型数组，在第 5 行声明了一个名为 `index` 的整型变量。（注：原文此后存在大量重复段落，已根据指令要求不重复输出重复内容）。

