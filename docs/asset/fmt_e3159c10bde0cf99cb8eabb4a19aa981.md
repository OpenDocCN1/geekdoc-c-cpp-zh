
### 7.21 写一个语句，声明一个 int 值的锯齿数组，并用下方数据表中的值初始化每行的列：

| 2 | 4 | 6 |

| 3 | 5 | 7 | 9 |

| 5 | 9 | 11 | 17 | 21 |

## List 集合 (The List Collection)

**概念：** `List` 是 .NET Framework 中的一个类，类似于数组。与数组不同，`List` 对象的大小会自动调整，以容纳存储其中的项数量。

.NET Framework 提供了一个名为 `List` 的类，可用于存储和检索项。一旦创建了 `List` 对象，你就可以将其认为是存放其他对象的容器。`List` 对象类似于数组，但比数组具有许多优势。以下是其中几个：

- 当你创建一个 `List` 对象时，你不需要知道打算存储在其中的项的数量。
- 当项被添加到 `List` 时，`List` 会自动扩展。
- 除了向 `List` 添加项外，你还可以移除项。
- 当项从 `List` 中移除时，`List` 会自动缩小。

## 创建 List (Creating a List)

这是一个如何创建一个可以持有字符串的 `List` 对象的示例：

```cs
List<string> nameList = new List<string>();
```

## 7.9 List 集合 (The List Collection)

该语句创建了一个由 `nameList` 引用的 `List` 对象：此语句创建了一个 `List` 对象，由 `jaggedArray` 引用。

## 初始化 List (Initializing a List)

你可以使用下标来访问 `List` 中的项，就像使用数组一样。例如，以下循环显示了之前声明的 `nameList` 中的项：

```cs
for (int index = 0; index < nameList.Count; index++)
{
    MessageBox.Show(nameList[index]);
}
```

## 向 List 添加项 (Adding Items to a List)

为了向 `List` 添加项，可以使用 `Add` 方法。例如，以下示例显示从文本文件读取值并添加到 `List` 中：

```cs
// 打开 Names.txt 文件。
StreamReader inputFile = File.OpenText("Names.txt");
// 创建一个持有字符串对象。
List<string> nameList = new List<string>();
// 读取文件内容。
while (!inputFile.EndOfStream)
{
    // 读取一行并添加到 List 中。
    nameList.Add(inputFile.ReadLine());
}
```

执行这些语句后，`nameList` 对象包含了从 `Names.txt` 文件读取的所有行。

你也可以使用 `foreach` 循环来遍历 `List` 中的项，就像使用数组一样。这是一个示例：

```cs
foreach (string str in nameList)
{
    MessageBox.Show(str);
}
```

## 将 List 传递给方法 (Passing a List to a Method)

有时你想编写一个接受 `List` 作为参数并对该 `List` 执行操作的方法。例如，下面的代码显示了一个名为 `DisplayList` 的方法。该方法接受一个字符串 `List` 作为参数并显示 `List` 中的每项：

```cs
private void DisplayList(List<string> sList)
{
    foreach (string str in sList)
    {
        MessageBox.Show(str);
    }
}
```

## 7.9 集合 (List Collection)

注意第 1 行，该方法有一个参数变量列表，且参数的数据类型为 `List<string>`。参数变量是 `List<string>` 对象的引用。当你调用此方法时，必须传递一个 `List<string>` 对象作为参数。

当你调用并传递一个 `List<string>` 对象作为参数时，你只需要传递引用该 List 的变量即可。下面的代码显示了如何调用 `DisplayList` 方法的示例：

```cpp
1 // 创建一个字符串列表。
2 List<string> nameList = new List<string>() { "Chris",
3 "Kathryn", "Bill" };
4
5 // 将 List 传递给 DisplayList 方法。
6 DisplayList(nameList);
```

第 2、3 行的语句创建了一个包含字符串 "Chris"、Kathryn" 和 "Bill" 的 List。第 6 行调用了 `DisplayList` 方法，将 `nameList` 对象作为参数传递。

> 注意：List 对象与数组一样，始终通过引用传递。

# 从列表中删除项

你可以使用 `RemoveAt` 方法从 List 的特定索引处删除项。下面的代码显示了一个字符串的示例：

```cpp
1 // 创建一个字符串列表。
2 List<string> nameList = new List<string>() { "Chris",
3 "Kathryn", "Bill" };
4
5 // 删除索引为 0 的项。
6 nameList.RemoveAt(0);
```

第 2、3 行的语句创建了一个包含字符串 "Chris"、Kathryn 和 "Bill" 的 List。第 6 行的语句删除了索引为 0 的字符串。在该语句执行后，List 包含字符串 "Kathryn" 和 "Bill"。

如果你知道想从 List 中删除的项的值，但不想将其作为索引来删除，那么 `Remove` 方法会在 List 中搜索该项。如果找到了该项，示例如下：

```cpp
1 // 创建一个字符串列表。
2 List<string> nameList = new List<string>() { "Chris",
3 "Kathryn", "Bill" };
4
5 // 从 List 中删除 "Bill"。
6 nameList.Remove("Bill");
```

第 2、3 行的语句创建了一个包含字符串 "Chris"、Kathryn 和 "Bill" 的 List。然后，第 6 行的语句从 List 中删除了 "Bill"。在该语句执行后，List 包含字符串 "Chris" 和 "Kathryn"。

`Remove` 方法返回一个布尔值，指示该项是否已从 List 中删除。如果在 List 中找到指定的项并将其删除，`Remove` 方法返回 `true`。如果在 List 中未找到该项，`Remove` 方法返回 `false`。

> 注意：`Remove` 方法执行顺序查找以定位指定的项。如果 List 包含大量项，其性能将会变慢。

如果你想删除 List 中的所有项，可以使用 `Clear` 方法。这是一个示例：

```cpp
nameList.Clear();
```

在该语句执行后，`nameList` 对象变为空。

# 插入项

你可以使用 `Insert` 方法在 List 的特定索引处插入项。下面的代码显示了一个示例：

```cpp
1 // 创建一个字符串列表。
2 List<string> nameList = new List<string>() { "Chris",
3 "Kathryn", "Bill" };
4
5 // 在索引 0 处插入项。
6 nameList.Insert(0, "Joanne");
```

第 2、3 行的语句创建了一个包含字符串 "Chris"、Kathryn 和 "Bill" 的 List。然后，第 6 行的语句在索引 0 处插入字符串 "Joanne"。在该语句执行后，List 包含字符串 "Joanne"、Chris、Kathryn 和 "Bill"。

> 注意：如果指定的索引小于 0 或大于 List 对象的 `Count` 属性，将发生异常。

# 在 List 中查找项

由于你使用下标符号来访问 List 中的项，因此你可以将在本章之前看到的任何数组处理算法进行修改以适用于 List。例如，你可以编写执行顺序查找、二分查找、选择排序等的代码。

在 List 中查找项的简单方法是使用 `IndexOf` 方法。`IndexOf` 方法接受一个值作为参数，并在 List 中搜索该值。如果找到了该值，该方法返回其索引。如果没有找到该值，该方法返回 -1。下面的代码显示：

```cpp
1 // 创建一个字符串列表。
2 List<string> myList = new List<string>() { "Chris",
3 "Kathryn", "Bill" };
4
5 // 查找 "Kathryn"
6 int position = myList.IndexOf("Kathryn");
7
8 // 在 List 中找到了吗？
9 if (position == -1)
10 {
11 MessageBox.Show("Kathryn was found at index " + position);
12 }
13 else
14 {
15 MessageBox.Show("Kathryn was not found");
16 }
```

# 7-4 完成测试成绩列表应用

在本教程中，你将完成一个从文件读取测试成绩到 List 的应用程序。该表单如图 7-42 所示已经创建。当你完成该应用程序时，它将从文件中读取测试成绩到 List。测试成绩将显示在 `ListBox` 控件中。计算并显示平均分以及高于和低于平均分数。

图 7-42 测试成绩列表表单

| 测试成绩列表 | 平均分： |

|---|---|

| testScoresListBox | averageLabel |

| 高平均分人数 | aboveAverageLabel |

| 低平均分人数 | belowAverageLabel |

| 获取分数按钮 | 退出按钮 |

- 第 1 步启动 Studio（或 Visual Studio）。打开 `Chap07` 文件夹下的 `Test Score List` 项目。
- 第 2 步：打开编辑器中的 `Form1` 代码。在 Program 7-5 的第 10 行处插入 `System.IO;` 指令。这是必要的，因为我们将使用 `StreamReader` 类，它是 `System.IO` 命名空间的一部分。
- 第 3 步：在编辑器打开的情况下，输入 Program 7-5 第 21-44 行的注释和 `ReadScores` 方法。`ReadScores` 方法用于接受一个 `List<int>` 作为参数并将 `TestScores.txt` 文件的内容读入。
- 第 4 步：输入 Program 7-5 第 46–54 行的注释和 `DisplayScores` 方法。`DisplayScores` 方法用于接受一个 `List<int>` 作为参数并将其内容显示在 `testListBox` 控件中。
