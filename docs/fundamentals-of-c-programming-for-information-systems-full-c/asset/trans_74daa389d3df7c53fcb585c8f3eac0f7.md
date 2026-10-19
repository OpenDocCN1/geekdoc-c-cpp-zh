

# 复习题

**8.8** 以下表单在前面讨论过，用户可以通过在每次输入一组数据后点击保存按钮，将多组数据保存到文本文件中。

![](img/143bad48262566137acc9c41f668a88f_273_0.png)

下面显示的代码将文本框中的姓名和两个分数写入文件 Exams.txt。

```
StreamWriter examsWriter;
private void WriteToTextFiles_Load(object sender, EventArgs e)
{
    examsWriter = new StreamWriter("Exams.txt", true);
}
private void btnSave_Click(object sender, EventArgs e)
{
    string name, score1, score2;
    name = txtName.Text;
    score1 = txtScore1.Text;
    score2 = txtScore2.Text;
    examsWriter.WriteLine(name + ", " + score1 + ", " + score2);
}
private void WriteToTextFiles_FormClosing(object sender, FormClosingEventArgs e)
{
    examsWriter.Close();
}
```

名为 examsWriter 的 streamWriter 在类级别声明，在窗体的 Load 事件中创建，在按钮的 Click 事件中多次使用，并在 FormClosing 事件中关闭。如果将声明语句（`StreamWriter examsWriter;`）移动到窗体的 Load 事件处理程序的开头，如下所示，会有什么效果？

// StreamWriter examsWriter;
private void WriteToTextFiles_Load(object sender, EventArgs e)
{
    StreamWriter examsWriter;
    examsWriter = new StreamWriter("Exams.txt", true);
}

请注意，recordCount 是一个值类型变量。因此，必须通过引用传递，以便 ComputePercent 可以更改其值。

ComputePercent 方法的完整代码如图所示 8-28。该方法读取每个学生的姓名和两个考试分数，计算百分比分数，将姓名存储在由参数 names 引用的数组中，并将百分比分数存储在由 percentScores 引用的数组中。

## 图 8-28：ComputePercent 方法

```
private void ComputePercent(string[] names, float[] percentScores, ref int recordCount )
{
    int index = 0;
    string currentLine;
    string[] fields;
    float percentScore;
    StreamReader examReader = new StreamReader("Exams.txt");

    while (examReader.EndOfStream == false)
    {
        currentLine = examReader.ReadLine();
        fields = currentLine.Split(',');
        percentScore = 100*(float.Parse(fields[1]) + float.Parse(fields[2]))/200;

        names[index] = fields[0]; //Store name into names array
        percentScores[index] = percentScore; // Store percent into percentScores
        index = index + 1;
    }
    recordCount = index;
}
```

再次说明，如前所述，两个数组的引用变量按值传递，因为此方法无需更改对数组的引用。通过引用传递引用变量允许方法访问相应的数组并更改数组的值。

调用 ComputePercent 的 btnDisplayPercent 的 Click 事件处理程序如图所示 8-29。

## 图 8-29：调用 ComputePercent 的 DisplayPercent 按钮事件处理程序

```
private void btnDisplayPercent_Click(object sender, EventArgs e)
{
    string[] names = new string[10];      //Declare names array
    float[] percentScores = new float[10]; // Declare percentScores array
    int recordCount = 0;

    ComputePercent(names, percentScores, ref recordCount); // Invoke ComputePercent

    lstDisplay.Items.Clear();
    string fmtStr = "{0,-15}{1,8:N1}";
    lstDisplay.Items.Add(string.Format(fmtStr, "Name", "Percent"));
    // Get names and percent scores from arrays and display them
    for (int index=0; index < recordCount; index++)
        lstDisplay.Items.Add(string.Format(fmtStr, names[index], percentScores[index]));
}
```

第 47 行调用 ComputePercent 方法，该方法更新两个数组。

第 54 行访问数组以在 ListBox 中显示它们。

btnDisplayAboveAvg 的 Click 事件处理程序也调用 ComputePercent，如图所示 8-30。该事件处理程序使用数组中的数据计算平均值并显示高于平均值的学生姓名。

## 图 8-30：调用 ComputePercent 的 DisplayAboveAvg 按钮事件处理程序

```
private void btnDisplayAboveAvg_Click(object sender, EventArgs e)
{
    string[] names = new string[10];
    float[] percentScores = new float[10];
    int index, recordCount = 0;

    ComputePercent(names, percentScores, ref recordCount);

    // Compute class average:
    float classTotal = 0, classAvg;
    foreach (float percentScore in percentScores)
        classTotal += percentScore;
    classAvg = classTotal / recordCount;

    lstDisplay.Items.Clear();
    string fmtStr = "{0,-15}{1,8:N1}{2,12:N1}";
    lstDisplay.Items.Add(string.Format(fmtStr, "Name", "Percent", "class Avg"));
    // Display above average:
    for (index = 0; index < recordCount; index++)
    {
        if (percentScores[index] > classAvg)
            lstDisplay.Items.Add(string.Format(fmtStr, names[index], percentScores[index], classAvg));
    }
}
```

调用 ComputePercent 后（第 63 行），此方法在第 67 行访问数组以累积总计，并在第 78 行显示姓名和百分比。

## 第 5 步-1：打开如图所示 8-26 的 PassingArrays 表单。

- 填写图 8-28 第 20 行 ComputePercent 的缺失参数。
- 添加第 34 行和第 35 行的代码以将姓名和百分比存储到数组中。
- 取消注释第 38 行。
- 添加语句以在 btnDisplayPercent 的 Click 事件过程（第 47 行，图 8-29）中调用 ComputePercent。
- 添加语句以调用 DisplayAboveAvg（第 60 行，图 8-30）。

## 第 5 步-2：运行表单并测试代码。

# 8.8 二维 2-D 数组

一维 1-D 数组存储一组数据。 二维 2-D 数组可以存储多组相同类型的数据。 例如，六种不同产品每年的每个季度的销售量可以存储在具有 6 行和 4 列的 2-D 数组中，其中每个单元格代表数组的一个元素。 每行代表不同的产品，每列代表不同的季度，如图所示 8-31。

## 图 8-31：一个 2-D 数组

列（季度）
索引 0 (qtr 1) 1(qtr 2) 2(qtr 3) 3(qtr 4)
行（产品） 0
1
2
3
4
5

## 创建 2-D 数组

创建 2-D 数组的语法是

```
type[,] arrayName = new type[rowCount, columnCount]
```

其中 rowCount 是行数，columnCount 是列数。 请注意，表示 2-D 数组的变量的声明需要在方括号对内使用逗号。

以下语句创建一个名为 sales 的 int 类型数组，具有 6 行和 4 列：

```
int[,] sales = new int[6, 4];
```

## 使用初始值创建 2-D 数组

您可以使用数组初始化器通过在花括号内指定每组值来创建具有非零初始值的 2-D 数组，如下所示。

```
int[,] sales = { {16, 32, 23, 40}, {144, 182, 169, 205}, {54, 49, 72, 63} }
```

前面的语句创建了以下名为 sales 的 2-D 数组，具有 3 行和 4 列。

列
0 1 2 3
行 0 16 32 23 40
1 144 182 169 205
2 54 49 72 63

## 引用 2-D 数组中的元素

2-D 数组中的每个元素都由行索引和列索引引用。 这里有一些例子：

sales[0, 0]—行 0 列 0 的元素，值为 16
sales[0, 1]—行 0 列 1 的元素，值为 32
sales[0, 2]—行 0 列 2 的元素，值为 23
...
sales[1, 0]—行 1 列 0 的元素，值为 144
sales[1, 1]—行 1 列 1 的元素，值为 182
sales[1, 2]—行 1 列 2 的元素，值为 169

## 示例：使用 2-D 数组进行销售数据

此示例使用以下数据，该数据由产品编号和一组产品的季度销售组成：

1033, 16, 32, 23, 40
1009, 144, 182, 169, 205
1014, 54, 49, 72, 63
1005, 38, 62, 55, 77
1001, 7, 9, 8, 15
1025, 98, 110, 105, 130

处理这些数据的应用程序使用一个表单，允许用户指定任何产品编号并显示该产品的总销售额，如图所示 8-32。

图 8-32：TwoDimArrays 表单

![](img/143bad48262566137acc9c41f668a88f_284_0.png)

在此应用程序中，您需要存储两种类型的数据。 尽管产品编号仅由数字组成，但它本质上是文本数据，因为您不会对其进行任何数值计算。 销售数据 however 是整数。 数组必须是单一类型。

一个选项是创建一个 string 类型 1D 数组来存储产品编号，并创建另一个 int 类型 2-D 数组来存储销售。

