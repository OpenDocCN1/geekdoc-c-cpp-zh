

## 复习题

8.3 以下客户订单数据（客户编号、订单编号、订购数量、单价）存储在名为 `Orders.txt` 的文本文件中。

0155, 76533, 3, 10.95
0140, 75446, 12, 8.50
0150, 75550, 1, 89.95
0145, 75648, 25, 2.50

考虑以下从上述文件读取数据的代码。

```csharp
StreamReader OrdersReader = new StreamReader("Orders.txt");
string[] fields;
while (OrdersReader.EndOfStream == false)
{
    currentLine = OrdersReader.ReadLine();
    fields = currentLine.Split(',');
}
lstDisplay.Items.Add(fields[1]);
```

`ListBox` 控件 `lstDisplay` 中显示的输出是什么？

## 8.3 将文件中的数据读取到数组

与从存储在内部内存中的数组和变量访问数据相比，从硬盘和闪存驱动器等辅助存储设备上的文件读取数据相对较慢。因此，如果程序需要多次访问存储在文件中的数据，通常更有效的做法是仅从文件读取一次数据，将其存储在一个（或多个）数组中，然后在后续使用数据时访问该数组。对于非常大的数据集，应权衡数组对内部内存的消耗与访问速度的提升。

使用数组的一个典型应用是多次查找信息，例如查询不同客户的电话号码或地址。另一个应用是计算某个字段的平均值，然后找出所有高于平均值的记录。

让我们考虑 `ReadTextFiles` 窗体的一个扩展版本，用于显示所有百分制成绩高于班级平均分的学生列表，如图 8-8 所示。

**图 8-8：** 显示高于平均分学生的 `ReadTextFiles` 窗体

![](img/143bad48262566137acc9c41f668a88f_254_0.png)

要找出高于平均分的学生，首先需要读取所有学生记录并计算班级平均分。然后，需要再次访问相同的记录，以确定哪些学生的分数高于班级平均分。

与其两次读取文件，不如只读取一次文件，计算班级平均分，并将学生姓名存储在一个一维数组中，将百分制成绩存储在另一个数组中。然后使用这些数组找出成绩高于平均分的学生。

创建这些数组时应该使用多大的数组大小？数组大小限制了数组中可存储的数据项数量。如果程序需要从记录数量不断增长的文件中读取数据，那么数组大小应尽量大，至少等于文件可能拥有的最大记录数。类似地，如果程序需要读取不同大小的文件，那么数组大小应尽可能大，至少等于最大文件的大小。为了方便查看数组，此示例将两个数组的大小限制为 10，如下面创建数组的语句所指定。

```csharp
string[] names      = new string[10];
float[] percentScores = new float[10];
```

将数据存储到数组中涉及以下过程：

- 从 `Exams.txt` 读取第一条记录，将姓名存储到 `names` 数组的第一个元素中，并将百分制成绩存储到 `percentScores` 数组的第一个元素中，如图 8-9 所示。
- 从 `Exams.txt` 读取第二条记录，将姓名存储到 `names` 数组的第二个元素中，并将百分制成绩存储到 `percentScores` 数组的第二个元素中。

对文件中的每条记录重复此过程。

**图 8-9：** `names` 数组和 `percentScores` 数组

| names {string[10]} | percentScores {float[10]} |
|----------------------|---------------------------|
| [0] "Mike Burns" | [0] 83.5 |
| [1] "Cathy Arnold" | [1] 90.5 |
| [2] "Wesley Mathews" | [2] 86 |
| [3] "Jerry Luke" | [3] 79.5 |
| [4] "Gina Rodriguez" | [4] 82.5 |
| [5] null | [5] 0 |
| [6] null | [6] 0 |
| [7] null | [7] 0 |
| [8] null | [8] 0 |
| [9] null | [9] 0 |

图 8-10 显示了读取数据、将数据存储到两个数组中并计算班级平均分的代码的第一部分。

**图 8-10：** 使用数组计算班级平均分的代码

```csharp
65 private void btnAboveAvg_Click(object sender, EventArgs e)
66 {
67     //Declare two 1-D arrays
68     string[] names = new string[10];
69     float[] percentScores = new float[10];
70     // percentScores is the array of all percent scores
71     int recordCount, index = 0;
72
73     string currentLine;
74     string[] fields;
75     float percentScore, classTotal = 0, classAvg;
76     //percentScore is the percent score for a student;
77     StreamReader examsReader = new StreamReader("Exams.txt");
78
79     while (examsReader.EndOfStream == false)
80     {
81         currentLine = examsReader.ReadLine(); // read current line
82         fields = currentLine.Split(','); // split current line
83         percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;
84
85         names[index] = fields[0]; //Store name into current element of names array
86         percentScores[index] = percentScore;  // Store percent into percentScores
87         index = index + 1;
88         classTotal = classTotal + percentScore; // Add current percent to classTotal
89     }
90     recordCount = index;
91     classAvg = classTotal / (float) recordCount;
```

让我们检查代码的关键语句。

### 第 81-83 行

```csharp
81 currentLine = examsReader.ReadLine(); // read current line
82 fields = currentLine.Split(','); // split current line
83 percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;
```

这与您之前在图 8-7 中用于计算和显示百分制成绩的代码相同。此代码读取每条记录，将记录拆分为三个字符串类型的数据项并存储在 `fields` 数组中，然后计算百分制成绩。如前所述，在第一次循环迭代后，`fields` 数组如下所示：

![](img/143bad48262566137acc9c41f668a88f_255_0.png)

### 第 85 行

`names[index] = fields[0];` //将姓名存储到 `names` 数组的当前元素中

为了访问 `names` 数组的每个元素，此语句使用变量 `index`，该变量初始化为零（第 71 行），并在循环内每次递增 1（第 87 行）。

第一次循环时，`names[index]` 指向第一个元素 `names[0]`，它被赋值为 `fields[0]` 的值，而 `fields[0]` 始终表示当前记录中的姓名。第 85 行的语句等价于：

```csharp
names[0] = fields[0];
```

因此，第一次迭代后，`names` 数组如下所示：

![](img/143bad48262566137acc9c41f668a88f_256_0.png)

第二次循环时，`index` 为 1。因此第 85 行等价于：

```csharp
names[1] = fields[0];
```

因此，第二条记录中的姓名存储在 `names` 的第二个元素中，如下所示：

![](img/143bad48262566137acc9c41f668a88f_256_1.png)

第三次、第四次和第五次循环时，`index` 分别为 2、3 和 4；因此第 85 行等价于：

```csharp
names[2] = fields[0];
names[3] = fields[0];
names[4] = fields[0];
```

在前五轮循环中读取所有记录后，数组的前五个元素中将存储姓名，如下所示：

![](img/143bad48262566137acc9c41f668a88f_256_2.png)

### 第 86 行

`percentScores[index] = percentScore;` //将百分制成绩存储到 `percentScores`

此语句与前一条语句类似，不同之处在于它将当前学生的百分制成绩存储在 `percentScores` 数组的当前元素中。由于 `index` 的值在每次循环时递增 1，第 86 行等价于：

```csharp
percentScores[0] = percentScore;
percentScores[1] = percentScore;
percentScores[2] = percentScore;
etc.
```

循环完成后，`percentScores` 数组将存储所有五个百分制成绩，如下所示：

| percentScores {float[10]} |
|---------------------------|
| [0] 83.5 |
| [1] 90.5 |
| [2] 86 |
| [3] 79.5 |
| [4] 82.5 |
| [5] 0 |
| [6] 0 |
| [7] 0 |
| [8] 0 |
| [9] 0 |

### 第 88 行

`classTotal = classTotal + percentScore;`

这一行计算所有已读取学生记录的百分制成绩的累计总和。累积百分制成绩的变量 `classTotal` 必须进行初始化（参见第 75 行）。

### 第 90-91 行

```csharp
90 recordCount = index;
91 classAvg = classTotal / (float) recordCount;
```

由于 `index` 在下一部分（图 8-10 中未显示）中会重新初始化为零，因此将其当前值（即已读取的记录数）存储在另一个变量 `recordCount` 中。

- 步骤 1-9：打开 `btnAboveAvg` 的 `Click` 事件处理程序。添加图 8-10 中第 85-91 行缺失的代码。
- 步骤 1-10：在第 89 行循环末尾设置断点，然后运行项目。
  - 单击 `ComputeAvg` 按钮，并在每次循环时观察 `names`、`percentScores` 和 `fields` 数组的值。

### 识别高于平均分的学生

为了识别百分制成绩高于班级平均分的学生，使用循环将班级平均分与 `percentScore` 数组的每个元素进行比较。如果某个元素高于班级平均分，则显示 `names` 数组中对应的元素。例如，如果 `percentScore[2]` 高于平均分，则显示 `names[2]`。

只有当两个数组被一致地加载，使得 `names` 的元素与 `percentScores` 的元素之间存在一一对应关系时，此方法才有效（例如，`percentScores[0]` 是 `names[0]` 的百分制成绩，`percent[1]` 表示 `names[1]` 的百分制成绩，依此类推）。

